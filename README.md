## About Komz
#### Our Mission – “Getting Butts in Saddles”

Komz is a free cycling-specfic mobile application featuring a down to ride (DTR) feed, events calendar, chat channels and a contact organizer.

Website:[https://komz.bike](https://komz.bike/)

Download: [iOS](https://itunes.apple.com/us/app/komz/id1358822361?mt=8) - [Android](https://play.google.com/store/apps/details?id=bike.komz.komzapp)

# Why Komz Event Schema?
The problem is that cycling events are posted in various places online (e.g. websites, facebook, slack, meetup, etc.)

The goal of this repo is the serve as a standard data format for all cycling events. (e.g. Mountain, Race, Road, XC, etc.)

Komz will be serving both as an events API aggregator (getEvents) as well as an API consumer (addEvent). Details of accessing these APIs will be posted in the future, but will be using this event data schema for both getting events and setting events.

If you have any questions or are interested please [Reach Out](https://support.komz.bike/hc/en-us/requests/new)

Last Updated: 11/1/2018



## Komz Event Schema (JSON)
** WORK IN PROGRESS**

Details of the normalized event data

### JSON Property Types
| Type        | Description  |
| ------------- | -----|
| string      | a string (of arbitrary length)|
| number      | a number including floating point numbers|
| integer      |  an integer|
| array      |  an array|
| boolean      |   a boolean value (1/0, true/false)|
| object      | (alias json) an JSON-encoded object|
| date      | a date. This MUST be in ISO6801 format YYYY-MM-DD or, if not, a format field must be provided describing the structure|
| time      | HH:MM AM/PM|
| datetime      | a date-time. This MUST be in ISO 8601 format of YYYY-MM-DDThh:mm:ssZ in UTC time or, if not, a format field must be provided|


### JSON Properties
| Name        | Type           | Description  | Required  |
| ------------- | -------------| -----| -----|
| name     | string      |  Name of event | * |
| startDate | datetime      |  When the event will begin |  * |
| endDate | datetime      |  When the event will stop |  * |
| skin | Object      |  Digital Assets for styling |   |
| skin.avatar | string      |  URL of image |  |
| skin.background | string      |  URL of image |  |
| source | Object      |  Details of original event data |   |
| source.url | string      |  URL of Event |  |
| location | object      |  Location Details |  * |
| location.fullAddress | string      |  Full address of Event |  * |
| location.label | string      |  Location of event (optional) |  * |
| location.latitude | number      | Latitude of event location |  * |
| location.longitude | number      | Longitude of event location |  * |
| type | string      | Acceptable types (all lowercase one word): race, road, mountain, mixed, xc, other ) |  * |
| skill | array      | Any of the following letters: a,b,c,d,e,s - Note S is for Social (No Drops) |  * |
| shortDescription | string      | Short description of event (140 Character Limit) |   |
| description | string      | full description of event  |  * |
| isRecurring| boolean | does this event repeat |
| repeatValue| integer | ability to set reoccuring events e.g. 1 week - event repeats every week at same startDate. Limit value to 4 (e.g. once every 4 weeks which is not the same as 1 month)|
| repeatUnit| string | All lowercase strings: "week", "month" |
| distance| number | Distance of ride, default is miles (imperial) or kilometers (metric) |
| unit | string | Measurement Unit - All lowercase strings: "imperial" or "metric" |
| urls | object      | Key/Value pair of additional resources. Single descriptive word and a URL link|   |


Sample Response for an Event

```
{
  "events": [
    {
      "name": "Iceman Cometh Challenge",
      "startDate": "2018-11-03T12:00:00.000Z",
      "endDate": "2018-11-03T19:30:00.000Z",
      "skin":{
        "avatar": "https://dk1xgl0d43mu1.cloudfront.net/user_files/iceman/site_assets/000/017/254/medium.png?1473434784",
        "background":"https://i.imgur.com/KwU0IAT.png"
      },
      "source": {
        "url":"https://www.iceman.com/"
      },
      "location": {
        "fullAddress": "605 North Birch Street Kalkaska, MI 49646",
        "label": "Kalkaska Civic Center",
        "latitude": 44.7391119,
        "longitude": -85.1850988
      },
      "type": "race",
      "skill":["a","b","c","d","e"],
      "shortDescription": "Boasting over 5000 participants, Iceman Cometh is America's largest single-day mountain bike race!",
      "description": "The Iceman Cometh Challenge is a point to point mountain bike race held traditionally on the first Saturday of November. The race starts in downtown Kalkaska, Michigan and finishes thirty miles later at Timber Ridge RV & Recreation Resort on the eastern edge of Traverse City, Michigan. \n\n\n\nThe course consists primarily of dirt roads, two-tracks (the majority of the course), abandoned railroad beds and the world famous Vasa Nordic ski trail. It crosses only one paved road (Williamsburg Rd at mile 17) as it winds through the breathtaking terrain of the Pere Marquette State Forest in Northern Lower Michigan.\n \n\n\nIn 2016, 5393 athletes participated! The Bell’s Iceman events attracts competitive cyclists from Mexico, Canada and 38 states. Ages range from 1.5 years to 80 years of age. Their ability levels vary from first time racers to Olympians.",
      "urls": [
        {
          "website": "https://www.iceman.com/events/1990982-2018-bell-s-iceman-cometh-challenge"          
        },{
      "route": "https://dk1xgl0d43mu1.cloudfront.net/user_files/iceman/site_assets/000/003/468/original.pdf?1407938633"          
        },{
          "registration": "https://www.iceman.com/events/1990982-2018-bell-s-iceman-cometh-challenge/event_registrations/new"    
        }]
    }]
  }
```

Sample response for a recurring event

```
{
"events":[{
      "name": "Rochester Hills - Iceman Weekly A/B + C Training Ride",
      "startDate": "2018-10-31T22:00:00.000Z",
      "endDate": "2018-11-01T00:00:00.000Z",
      "skin":{
        "avatar": "",
        "background":"https://kingdom.komz.bike/uploads/38f29e6b85c33f5903107a5edab4be10"
      },
      "location": {
        "fullAddress": "2265 Crooks Rd, Rochester Hills, MI 48309",
        "label": "Clubhouse BFD",
        "latitude": 42.67,
        "longitude": -83.22
      },
      "type": "mountain",
      "skill":["a","b","c"],
      "description": "JTree and Я2R are hosting the annual weekly! Check KOMZ for weekly updates. \n\nIceman Wednesday Weekly A/B Ride. \n\nJ. Ross is also leading out a C ride as well starting the 19th\n\nStart Time:  6:00pm\nStart Location:  Clubhouse BFD https://goo.gl/maps/JQ48kgaDGN32 plenty of nearby parking if the lot is full\nRoute:  https://www.strava.com/routes/15367616 download it!\nWhat to bring:  MTB, front/rear lights, proper necessities and enough hydration for 2 hours.\n\nPost Ride Food/Beers at Clubhouse BFD!\n\nThis is a fast/fun group ride to simulate wheel-to-wheel combat just like the actual race only we won’t be cross-eyed the entire time.  However, there will be “Accelerated Speed” sections.  According to the route above, it calculates ride time about 2:17 but we completed a similar ride in previous years as low as 1:50 so bring your legs!  Average speed with stops is about 17mph but normal cruising speed is 18-20mph.  (For reference - Most riders have a 34 or 36 tooth chainring.)  The “Don’t be a Dick” rule is in effect. This is a friendly but fast ride.\n\n“Accelerated Speed” sections with rolling regroups:\nMt Vernon - 28 to Inwood https://www.strava.com/segments/7418951\nDequindre Hill - Predmore to Inwood https://www.strava.com/segments/1731833\nHIxon Climb https://www.strava.com/segments/6940589\nSheldon School Sprint https://www.strava.com/segments/15446817 STOP at Mead Rd just before returning to pavement(East/West traffic is blind and does not have a stop sign)",
    "isRecurring", true,
    "repeatValue": 1,
    "repeatUnit":"week",
    "urls": [
        {
          "route": "https://www.strava.com/routes/15367616"          
        }]
    }]
}
