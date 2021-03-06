# Data Representation and Querying Project 2015
### Author: Ross Byrne
A third year Data Representation and Querying Project 2015. A project to design a simple API for a dataset.

## Introduction
This project provides the design and documentation for the dataset "Parks in Galway City" which is available at [data.gov.ie](http://data.gov.ie).

The **Parks in Galway City** Dataset contains information about all of the public parks that can be found in Galway City. This could be a particularly useful dataset to hook into if creating an information application based on Galway City. Whether this API is used solely for the parks in Galway or as part of a larger application accessing this information, including the location data, could be an integral part of an application. 

## About The Parks In Galway City Dataset
The dataset comes in the form of a .CSV file which I have converted  into JSON, making it easier to work with. The dataset currently, at the time of writing, has 29 entries. Each entry has 14 columns with the following headings:

Heading | Description  
---------|-----------
"OBJECTID" | An ID given to each park. 
"NUMBER" | A number given to each park.
"NAME" | Name of the park.
"LOCATION" | Location of park eg. "Newcastle, Galway".
"AREAOFCITY" | The area of the city the park is located eg. "City- West".
"OPENINGHRs" | Opening hours of the park.
"FACILITIES" | Facilities in the park eg. Tennis Courts, Dressing Rooms, etc.
"DESCR" | A description of the park eg. "Local Neighbourhood Park".
"Lat" | The latitude coordinate of the park.
"Long" | The longitude coordinate of the park.
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
The following is the first entry of the dataset in JSON format. This will give you an understanding of how the data is laid out using the above headings.

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
You can receive a list of all the parks in Galway, using the HTTP POST method, at the following URL:

*http://galwayparksapi.com/parks/all*

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

### Accessing Lists of Parks Using Filters
You can request a list of parks based on a filter, such as, all parks with a tennis court etc using the HTTP GET method.
The following is a URL example of the format you would use to achieve this.

*http://galwayparksapi.com/parks/?[filter]=[parameter]*

Now, replace [filter] with a field from the dataset, which could be any of the fields including: objectid, number, name, location. etc.

Then replace [parameter] with the results you are looking for. An example would look like this.

**Example One**

*http://galwayparksapi.com/parks/?location=Newcastle+Galway/*

This would return an array of all the parks that have that location, in JSON format.
If there isn't any park with that location, an empty array is returned.

**Example Two**

Another example could look like the following:

*http://galwayparksapi.com/parks/?facilities=pitch*

This would return an array of any park that has any type of pitch listed in its facilities section.

#### Multiple Filters
To search for parks in a more complex fashion, by using more then one filter, is just as easy as using one filter.

*http://galwayparksapi.com/parks/?[filter]=[parameter]&[filter]=[parameter]*

Just like with a single filter and parameter, replacing [filter] with the field you are seaching for, such as facilities or openinghrs, and replacing [parameter] with the values you are looking for such as tennis court, you get a list of all the parks that satisfy that condition. As you can see with multiple filters, you can repeat the proccess of [filter]=[parameter] by separating them with a **'&'** symbol.

**Example**

*http://galwayparksapi.com/parks/?facilities=tennis+court&areaofcity=city+west*

This is using two filters and will return an array of parks that have a tennis court and are in city west.

This method can be used with many different filters but remember, the more filters you use, the more narrow your search will be. This can result in getting back very few results or none at all.

#### Getting A List of Parks Closest To Current Location

Lets say you want to get the users location data and search for the park closest to them. You could easily do this, using the users longitude and latitude, with a POST method, using the following URL:

*http://galwayparksapi.com/parks/closest-long-lat/*

This will return an array of all the parks, starting with the park that is closest to the longitude and latitude coordinates provided.

You might also want to limit the number of results returned by the POST method. This can be done using the following URL:

*http://galwayparksapi.com/parks/closest-long-lat/[number]*

Replace [number] with the number of parks you want to be given back eg. the 5 closest parks. This will return the specified number of results, starting with the park that is closest to the specified longitude and latitude.

Limiting the number of results returned back would look like this:

*http://galwayparksapi.com/parks/closest-long-lat/6*

This returns the 6 closest parks to the longitude and latitude used in the POST method.

## Conclusion

Due to the nature of the dataset, mainly because it is a dataset of parks, users may not add or remove entries. It would not make sense, simply because an average user is not going to be building parks or tearing down existing ones.
