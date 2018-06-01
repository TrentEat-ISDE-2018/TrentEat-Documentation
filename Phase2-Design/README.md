# TrentEat
### Gabriele Scarton - gabriele.scarton@studenti.unitn.it

# Phase 2 - Design
![alt text](https://raw.githubusercontent.com/TrentEat-ISDE-2018/TrentEat-Documentation/master/Phase2-Design/ISDE_project.png)

This service design is based on this assumptions:
- An easy way for users to share their position (or the position they want to stay) is the use of Telegram sharing position feature. Using a Telegram Bot makes easy to map a user need (identified by a bot command) to a service API.
- The agritur info are available in a CSV format on dati.trentino.it, but they can be filtered and stored in a internal database for easy accessing.
- The dataset have all the addresses but not the GPS location. For having that info, useful to calculate distances, a address-to-coordinates service must be linked to the service.
- For a one-day trip, it's useful to filter the data by the local weather

## Heroku design
![alt text](https://raw.githubusercontent.com/TrentEat-ISDE-2018/TrentEat-Documentation/master/Phase2-Design/ISDE_Heroku_management.png)
Since Heroku offers only 5 free slot and 2 are already occupied by assignments, the project is splitted in 3 parts:
- the Telegram bot, which manages the user interface and user data
- the business process, which manage all other services and provide information for the users
- the other services (the API calls and the agritur data) all wrapped in a single application. I choose to aggregate these services because they aren't directly connected, they all comunicate with the business process service, and only one of them use a instance of a database, then the aggregation doesn't modify the logic of the project

