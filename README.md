# Weekend Warrior
Code 301 Final Project

## Created by: Christopher Hamersly, Paul Rest, Stephen Baldock, and Daisy Johnson

## Overall problem domain and how this project solves those problems:
The user has a limited amount of time and wants to get the most out their weekend. This app gives you options to fill up the time you have available, whether it be a lot or a little making you a true weekend warrior. This website will be a one-stop-shop to give all the information you need like trail guides, playlists that match your adventure and restaurant recommendations etc.

## summary of project: A web-app to help you figure out the best way to spend your weekend outside.

## Version
1.0 - Server Setup
1.1 - Three CORE API deployment
1.2 - CRUD capability
1.3 - Additional API deployment
1.4 - Full CRUD capability

## Architecture
Backend utilizes superagent for API calls to googlebooks API and postgres to query a SQL database. Frontend is served with EJS components.

## WireFrame

![Weekend Warrior Wireframe](diagrams/Weekend_Warrior_Wireframe.png)

## Domain Model

![Domain Model](diagrams/domain_model.png)



## Libraries Used:
 - Express
 - EJS
 - dotenv
 - superagent
 - pg
 
 ## API Endpoints
**Location IQ API**
https://us1.locationiq.com/v1/search.php
**Climbing Routes API by lat & lon**
https://www.mountainproject.com/data/get-routes-for-lat-lon?lat=40.03&lon=-105.25&maxDistance=10&minDiff=5.6&maxDiff=5.10&key=200790534-05370a505ab38e493dbb8b4c24c7dadd
**Hiking Routes API by lat & lon**
https://www.hikingproject.com/data/get-trails?lat=40.0274&lon=-105.2519&maxDistance=10&key=200790534-badad5b9f2f1c28cff7c1bd0f669131e
**Trail Running API by lat & lon**
https://www.trailrunproject.com/data/get-trails?lat=40.0274&lon=-105.2519&maxDistance=10&key=200790534-badad5b9f2f1c28cff7c1bd0f669131e
**Mountain Biking API by lat & lon**
https://www.mtbproject.com/data/get-trails 
**Camping API by lat & lon**
https://developer.nps.gov/api/v1/parks
**Breweries by lat & lon**
https://api.openbrewerydb.org/breweries'
**Local Music by lat & lon**
http://musicovery.com/api/V6/artist.php?fct=getfromlocation 

## Example API Response - Location IQ
  {
    place_id: '235549103',
    licence: 'https://locationiq.com/attribution',
    osm_type: 'relation',
    osm_id: '237385',
    boundingbox: [ '47.4810022', '47.7341357', '-122.459696', '-122.224433' ],
    lat: '47.6038321',
    lon: '-122.3300624',
    display_name: 'Seattle, King County, Washington, USA',
    class: 'place',
    type: 'city',
    importance: 0.78297917356438,
    icon: 'https://locationiq.org/static/images/mapicons/poi_place_city.p.20.png'
  }
## Example API Response - Hiking
   {
      id: 7031994,
      name: 'Shore Loop Road',
      type: 'Trail',
      summary: 'A beautiful city park that offers views of downtown Seattle and Mt. Rainier.',
      difficulty: 'green',
      stars: 4.4,
      starVotes: 11,
      location: 'Mercer Island, Washington',
      url: 'https://www.hikingproject.com/trail/7031994/shore-loop-road',
      imgSqSmall: 'https://cdn2.apstatic.com/photos/hike/7032902_sqsmall_1554996783.jpg',
      imgSmall: 'https://cdn2.apstatic.com/photos/hike/7032902_small_1554996783.jpg',
      imgSmallMed: 'https://cdn2.apstatic.com/photos/hike/7032902_smallMed_1554996783.jpg',
      imgMedium: 'https://cdn2.apstatic.com/photos/hike/7032902_medium_1554996783.jpg',
      length: 2.5,
      ascent: 133,
      descent: -134,
      high: 91,
      low: 22,
      longitude: -122.2572,
      latitude: 47.5513,
      conditionStatus: 'All Clear',
      conditionDetails: 'Dry',
      conditionDate: '2020-06-16 21:21:35'
    },
    
## Database Relationship Diagram
SQL Tables - MVP
* **Hiking**
 * Key | Image | Trail Name | Summary | Latitude | Longitude | Distance | Total Elevation | Max Height | Difficulty Rating | Condition Status | Reviews 
* **Camping**
 * Key | Image | Campground Name | Latitude | Longitude | Description | Firewood | Restrooms | Reservations | Fees | Potable Water | Accessibility
* **Rock Climbing**
 * Key | Image | Name | Latitude | Longitude | Type | Pitches | Stars 
* **Location ID**
 * Key | Search_Query | Formatted_Query | Latitude | Longitude
 
 ## Database Schemas
 CREATE TABLE locations (
  "id" SERIAL PRIMARY KEY,
  "search_query" VARCHAR(255),
  "display_name" VARCHAR(255),
  "lat" DECIMAL(12, 9),
  "lon" DECIMAL(12, 9)
);


DROP TABLE IF EXISTS trails;

CREATE TABLE trails (
  "id" SERIAL PRIMARY KEY,
  "api_id" VARCHAR(255),
  "name" VARCHAR(255),
  "summary" VARCHAR(10000),
  "img_medium" VARCHAR(1000),
  "latitude" VARCHAR(255),
  "longitude" VARCHAR(255),
  "length" VARCHAR(255),
  "ascent" VARCHAR(255),
  "high" VARCHAR(255),
  "difficulty" VARCHAR(255),
  "conditionstatus" VARCHAR(255),
  "stars" VARCHAR(255),
  "notes" VARCHAR(10000)
);


DROP TABLE IF EXISTS camping; 

CREATE TABLE camping (
  "id" SERIAL PRIMARY KEY,
  "api_id" VARCHAR(255),
  "image" VARCHAR(255),
  "name" VARCHAR(255),
  "latitude" DECIMAL(12, 9),
  "longitude" DECIMAL(12, 9),
  "description" VARCHAR(10000),
  "entrance_fees" VARCHAR(10000),
  "activities" VARCHAR(10000),
  "notes" VARCHAR(10000)
);


DROP TABLE IF EXISTS climbing;

CREATE TABLE climbing (
  "id" SERIAL PRIMARY KEY,
  "api_id" VARCHAR(255),
  "location" VARCHAR(255),
  "name" VARCHAR(255),
  "type" VARCHAR(255),
  "pitches" VARCHAR(255),
  "stars" VARCHAR(255),
  "latitude" DECIMAL(12, 9),
  "longitude" DECIMAL(12, 9),
  "img_medium" VARCHAR(255),
  "notes" VARCHAR(10000)
);


DROP TABLE IF EXISTS mtn_biking;

CREATE TABLE mtn_biking (
  "id" SERIAL PRIMARY KEY,
  "api_id" VARCHAR(255), 
  "location" VARCHAR(255),
  "name" VARCHAR(255),
  "type" VARCHAR(255),
  "difficulty" VARCHAR(255),
  "stars" VARCHAR(255),
  "latitude" DECIMAL(12, 9),
  "longitude" DECIMAL(12, 9),
  "img_medium" VARCHAR(255),
  "summary" VARCHAR(10000),
  "length" VARCHAR(255),
  "notes" VARCHAR(10000)
);


DROP TABLE IF EXISTS breweries;

CREATE TABLE breweries (
  "id" SERIAL PRIMARY KEY,
  "api_id" VARCHAR(255),
  "name" VARCHAR(255),
  "latitude" DECIMAL(12, 9),
  "longitude" DECIMAL(12, 9),
  "type" VARCHAR(255),
  "website" VARCHAR(255),
  "notes" VARCHAR(10000)
);


![Entity Relationship Diagram](diagrams/entity_relationship.png)






