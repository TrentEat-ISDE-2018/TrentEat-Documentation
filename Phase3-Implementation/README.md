# TrentEat
### Gabriele Scarton - gabriele.scarton@studenti.unitn.it

# Phase 3 - Implementation
In this section will be described how the design is translated to code and what was needed to be changed to make the idea doable.

### Geocoding Service
The geocoding service is an adapter of Google Maps API: https://developers.google.com/maps/documentation/geocoding/intro
It takes a string request, it obtains a response using API, parse this response and returns a simplified JSON with only needed data, latitude and longitude. For parsing the JSON ignoring the unwanted information (i.e. without mapping it in a java class), a configuration is added to the Jackson ObjectMapper:
```java
ObjectMapper mapper = new ObjectMapper()
	.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);
```
The student Google account is not suitable for a GMaps API key, so it has been retrieved with a normal Google account. Since the request are limited, the endpoint is protected with an API key.
```
GET http://datalayer.herokuapp.com/geocoding/{API KEY}/{location: trento}
```
```json
{
    "location": "trento",
    "lat": 46.0747793,
    "lon": 11.1217486
}
```
### Weather Service
The weather service is an adapter of OpenWeatherMaps API: https://openweathermap.org/
It takes a request of latitude and longitude, it obtains a response using API, parse this response and returns a simplified JSON with only needed data, the string representation of the actual weather and temperature, plus the place ID (if it's needed a response checking). Since the request are limited, the endpoint is protected with an API key.
```
GET http://datalayer.herokuapp.com/weather/{API KEY}/{lat: 46.0747793}/{lon: 11.1217486}
```
```json
{
    "id": "800",
    "main": " Clear",
    "description": " clear sky",
    "temp": 19.99000000000001,
    "temp_min": 14,
    "temp_max": 26
}
```
### Data Service
The data service consists of a Heroku Postgres DB and a REST service for CRUD operations. From the original dataset, in the db are saved only Agriturs that offered eating service and the data are filtered. Also, using the Geocoding service, the fields latitude and longitude were added. Since some places weren't recognized by Google Maps, then some addresses were slightly modified. All GET request are free, the other requests that modify the db are restricted by a key. 
```
GET https://datalayer.herokuapp.com/agritur/{complete name of agritur, such SOCIETA' AGRICOLA MASO DELLO SPECK}
```
```
GET https://datalayer.herokuapp.com/agritur/all
```
```
PUT/DELETE https://datalayer.herokuapp.com/agritur/{complete name}?key={key}
```
```
POST https://datalayer.herokuapp.com/agritur?key={key}
```
```json
{
    "phone": "340 1524315",
    "email": null,
    "website": null,
    "altitude": null,
    "address": "Loc. Pozze di Sopra, n. 2, Daiano",
    "lat": 46.3056346,
    "lon": 11.4362104,
    "name": "SOCIETA' AGRICOLA MASO DELLO SPECK",
    "num_for_eat": 60,
    "num_for_sleep": 0
}
```

### Business Logics Service
The business logic service manages all the previous service in order to provide a SOAP API for clients.
Methods list:
```java
	//get data and weather of an agritur
	public Agritur getDetailedAgritur(String name);
	//get agriturs near a GPS location
	public List<Agritur> getNearAgritur(double distance, double lat, double lon);
	//get agriturs that have <query> into their names
	public List<Agritur> getAgriturByQuery(String query);
	//let a user vote an agritur
	public void userMarkAgritur(String userId, String agritur, double mark);
	//the user decides to view an agritur info page
	public void userViewAgritur(String userId, String agritur);
	//the user asks for recommendation
	public List<Agritur> recommendAgritur(String userId);
```
