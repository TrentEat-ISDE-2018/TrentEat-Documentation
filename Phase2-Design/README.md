# TrentEat
### Gabriele Scarton - gabriele.scarton@studenti.unitn.it

# Phase 2 - Design
![alt text](https://raw.githubusercontent.com/TrentEat-ISDE-2018/TrentEat-Documentation/master/Phase2-Design/ISDE_start_point.png)

This service design is base on this assumptions:
- An easy way for users to share their position (or the position they want to stay) is the use of Telegram sharing position feature. Using a Telegram Bot makes easy to map a user need (identified by a bot command) to a service API.
- The agritur info are available in a CSV format on dati.trentino.it, but they can be filtered and stored in a internal database for easy accessing.
- The dataset have all the addresses but not the GPS location. For having that info, useful to calculate distances, a address-to-coordinates service is linked to the service.
- For a one-day trip, it's useful to filter the data by the local weather
