# Data Representation and Querying Project 2015
### Author: Ross Byrne
A third year Data Representation and Querying Project 2015. A project to design a simple API for a dataset.

## Introduction
This project provides the design and documentation for the dataset "Parks in Galway City" which is available at [data.gov.ie](http://data.gov.ie).

The **Parks in Galway City** Dataset contains information about all of the public parks that can be found in Galway City. This could be a particularly useful dataset to hook into if creating an information application based on Galway City. Whether this API is used solely for the parks in Galway or as part of a larger application, accessing this information, including the location data, could be an integral part of an application. 

## About The Parks In Galway City Dataset
The dataset comes in the form of a .CSV file which I have converted  into JSON, making it easier to work with.
The dataset has 14 columns with the following headings:

Heading | Discription  
---------|-----------
"OBJECTID" | An id given to each park. 
"NUMBER" | A number given to each park.
"NAME" | Name of the park.
"LOCATION" | Location of park eg. "Newcastle, Galway".
"AREAOFCITY" | The area of the city the park is located eg. "City- West".
"OPENINGHRs" | Opening hours of the park.
"FACILITIES" | Facilities in the park eg. Tennis Courts, Dressing Rooms, etc.
"DESCR" | A description of the park eg. "Local Neighbourhood Park".
"Lat" | the latitude coordinate of the park.
"Long" | the longitude coordinate of the park.
"EastITM" | Irish Transverse Mercator (ITM) East value. *
"NorthITM" | Irish Transverse Mercator (ITM) North vaule.
"EastIG" | East Irish Grid Reference number. **
"NorthIG" | North Irish Grid Reference number.

### * 
> From Wikipedia - [Irish Transverse Mercator](https://en.wikipedia.org/wiki/Irish_Transverse_Mercator).

> _"**Irish Transverse Mercator (ITM)** is the geographic coordinate system for Ireland."_

### **
> From Wikipedia - [Irish grid reference system](https://en.wikipedia.org/wiki/Irish_grid_reference_system).

> _"The **Irish grid reference system** is a system of geographic grid references commonly used in Ireland (both Northern Ireland and the Republic of Ireland)."_

## Example Entry
The following is the first entry of the dataset in JSON formate. This will give you an understanding of how the data is layed out using the above headings.

```json
{
    "OBJECTID":1,
    "NUMBER":1,
    "NAME":"Corrib Park",
    "LOCATION":"Newcastle, Galway",
    "AREAOFCITY":"City- West",
    "OPENINGHRs":"No restricted opening hours",
    "FACILITIES":"Passive Recreational Walkways, 3G Artificial Surface Pitch, Multi- Use Games Area(MUGA), Planting areas with flowers, sh",
    "DESCR":"Local Neighbourhood Park",
    "Lat":53.279,
    "Long":-9.075,
    "EastITM":528328.238,
    "NorthITM":725961.154,
    "EastIG":128361.999,
    "NorthIG":225932.124
  }
  ```

## Accessing The Dataset
#### Receiving A List of All Parks
You can recive a list of all the parks in Galway, using the HTTP GET method, at the following URL:

*"http://galwayparksapi.com/parks/all"*

In this case, using "all" after ".../parks/" will return an array of all the parks, in JSON format.

**Example:**
```json
[
  {
    "OBJECTID":1,
    "NUMBER":1,
    "NAME":"Corrib Park",
    "LOCATION":"Newcastle, Galway",
    "AREAOFCITY":"City- West",
    "OPENINGHRs":"No restricted opening hours",
    "FACILITIES":"Passive Recreational Walkways, 3G Artificial Surface Pitch, Multi- Use Games Area(MUGA), Planting areas with flowers, sh",
    "DESCR":"Local Neighbourhood Park",
    "Lat":53.279,
    "Long":-9.075,
    "EastITM":528328.238,
    "NorthITM":725961.154,
    "EastIG":128361.999,
    "NorthIG":225932.124
  },
  { ... },
  { ... }
]
```
