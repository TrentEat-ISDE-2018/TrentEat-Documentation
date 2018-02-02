# TrentEat
### Gabriele Scarton - gabriele.scarton@studenti.unitn.it

# Phase 1 - Requirements
On the brainstorming session, the idea was to help people finding the best spot for climbing, walking and discovering the beautiful Trentino mountains.
Searching for public data, it hasn't found anything suitable for storing in a database without a proper web scraping.
Instead, looking into dati.trentino.it, it was found a nice database with over 400+ agritur (http://dati.trentino.it/dataset/agriturismi-del-trentino).
So, the main idea chenaged to "finding mountian spots" to "finding best place to discover typical place to stay and eat".

### Use case scenario
A person visiting Trentino by car want to find a local place to stay and eat in order to discover Trentino. Using search engines and travelling sites, the results are the most rated and visited places. The small places are difficult to find: since they are visited by few people with few reviews on travelling sites and probably no waebsite to display on a search result. TrentEat can offer a list of place based only on the place location. 

### Requiremets
The user must send the position and the service must return a list of Agritur, based on what they offered: typical food or place to stay the night
An internal rating system can be useful to rate all the places in the db: since at the beginning they are displayed only by their position, every place, big or small, has the same chance to be evaluated.

