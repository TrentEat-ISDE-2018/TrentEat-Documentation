# TrentEat
### Gabriele Scarton - gabriele.scarton@studenti.unitn.it
(see subfolder for a more detailed documentation)

### Requirements
Given a client, an user searching for agriturs in Trentino send request to TrentEat. The service must return a list of Agritur, based or on position or by ratings given by user, with some realtime data to help user choosing an agritur.

### Design
In order to fulfill the requirements, the service must save the list of agritur, implement a geocoding service, implement a weather service, implement a user-friendly client and implement a business logic service which link all these services. Since there are only 3 heroku application available, this is the design idea:
![alt text](https://raw.githubusercontent.com/TrentEat-ISDE-2018/TrentEat-Documentation/master/Phase2-Design/ISDE_Heroku_management.png)

### Implementation
The geocoding service is an REST adapter of Google Maps API: https://developers.google.com/maps/documentation/geocoding/intro

The weather service is an REST adapter of OpenWeatherMaps API: https://openweathermap.org/

The data service consists of a Heroku Postgres DB and a REST service for CRUD operations.

The business logic service manages all the previous service in order to provide a SOAP API for clients.

Also, the business service adapts a recommendation service from Recombee: https://docs.recombee.com/api.html

For a detailed list of API call, see the Implementation folder.

For a user-friendly client, a Telegram bot was implemented, available here: https://t.me/TrentEatBot
