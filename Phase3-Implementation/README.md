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
