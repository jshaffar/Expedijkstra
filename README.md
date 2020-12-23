# ✈️ Expedijkstra ✈️
 By Jeremy Shaffar, Siriam Mantheem, Muhammed Safwat Jamil. 
 <br />
 Final Project for CS225 at UIUC

## Presentation Video
Here is the link to our final presentation video:
https://uofi.box.com/s/iqgz9p3chj5m6lsovrh73raqiz5vm15x

## Purpose
We wanted to graph flights, and determine the optimal path. In addition we wanted to traverse the graph to see all the paths, and vizualize how to get to all of the airports from one airport.

## Usage
### Notes 
* Airports are referenced by there IATA code. See https://www.iata.org/en/publications/directories/code-search/?airport.search=JFK to search for specific airports.
* Flags have to be seperated i.e -d -v -b and not -bdv. Although it doesn't matter order of the flags, -b and -d flags cannot be used together, and -vl and -ve flags cannot be used with -d either, as they are specific animation customizations.
* Airports must be full capital i.e JFK not Jfk
 ### Basics
 * no flags = Continually input two airports to get optimal route in command line. Ends when q or Q is pressed.
 * -d = djikstras Can view shortest route in command line
 * -b = bfs Can check bfs traversal at traversal_order.txt.
 * -v = vizualize Can view line in Maps folder depending on which one used. 
 
 ### DFS vizualization
 * -d and -v. Viewable at Maps/dijikstras.png. Route starts at red and ends at green, with blue airports as intermediate.
 ### BFS vizualizations customizations (must use -b and some form of -v)
 
 * -ve or -v or -ve NUM: vizulize bfs with edge every second. Takes long time depending on num inputed.
  If no num or invalid num, it defaults to 4 which should be fairly quick. Will be viewable  in file Maps/bfs_by_edges.gif.
 * -vl : vizualization of bfs with a new layer every frame, with the inputed number of edges. Will be viewable in Maps/bfs_by_layer.gif. This should be much quicker than -ve, with only a couple frames in the animation. 
 
 ### Example Usage 
 * ./air -b JFK; Does bfs traversal begininng at JFK. Can check bfs traversal at traversal_order.txt.
 * ./air -d JFK SFO - Does Dijkstras from JFK to SFO. Printed out optimal route in command line.
 * ./air -b -ve JFK 40; Performs and vizualizes bfs from JFK. Vizualization adds a frame every edge, so very slow. Will add 40 frames. Can view in Maps/vizualize_by_edges.gif. A preloaded one located in the example folder, and also is below, is there if you want to see it without building one.
 * ./air -b -vl JFK; Performs and vizualizes bfs from JFK by layer (every bfs is done with that layer of depth).
 * ./air -d -v JFK SFO; Does Dijkstras from JFK to SFO and vizualizes it. Starts at red and ends at green with all intermediate airports in blue. Viewable map at Maps/dijikstras.png.
 * ./air; Allows user to input to airports in loop to continueally find best route with Dijikstras.
## Results
All results are in Examples folder.

#### Dijikstras algorithm text proof from Chacalluta Airport in Chile, to Jersey Airport in Jersey, Channel Islands.
Chacalluta Airport, Arica -> El Alto International Airport, La Paz -> Viru Viru International Airport, Santa Cruz -> Adolfo Suárez Madrid–Barajas Airport, Madrid -> Nantes Atlantique Airport, Nantes -> Southampton Airport, Southampton -> Jersey Airport, Jersey

#### Djikistras Vizualization from Kristianstad Airport (KID) in Scania, Sweden to  Uberlandia Airport (UDI) in Uberlândia, Brazil
https://github.com/jshaffar/Expedijkstra/blob/master/Examples/ari_jer_dij_example.txt
![alt text](https://github.com/jshaffar/Expedijkstra/blob/master/Examples/kid_udi_dijikstra.png)
#### BFS animation by layer from Herat Airport (HEA) in Herat, Afganistan
![alt text](https://github.com/jshaffar/Expedijkstra/blob/master/Examples/herat_bfs_by_layer.gif)
#### BFS animation by edge from Macarther Airport (ISP) in Islip, New York for the first 400 edges of traversal.
![alt text](https://github.com/jshaffar/Expedijkstra/blob/master/Examples/isp_bfs_by_edge_400.gif)
 <br />
Actual order of bfs traversal from Minot International Airport (MOT) in Minot, North Dakota, can be found at https://github.com/jshaffar/Expedijkstra/blob/master/Examples/mot_bfs_order.txt

## Data Format
For this project, the data was taken from https://openflights.org/data.html, and is the flight and route as of June 2014. The raw files can be found in the data folder of the repository. The data is in a .dat file and is separated by commas. There is an airports.dat that contains airport data with the following fields in order. The fields are strings unless stated otherwise(Like latitude, longitude, altitude):

```
Airport ID    Unique OpenFlights identifier for this airport.
Name 	      Name of airport. May or may not contain the City name.
City 	      Main city served by airport. May be spelled differently from Name.
Country       Country or territory where airport is located. See Countries to cross-reference to ISO 3166-1 codes.
IATA 	      3-letter IATA code. Null if not assigned/unknown.
ICAO 	      4-letter ICAO code. Null if not assigned.
Latitude      Decimal degrees, usually to six significant digits. Negative is South, positive is North.
Longitude     Decimal degrees, usually to six significant digits. Negative is West, positive is East.
Altitude      In feet.
Timezone      Hours offset from UTC. Fractional hours are expressed as decimals, eg. India is 5.5.
DST 	      Daylight savings time. One of E (Europe), A (US/Canada), S (South America), O (Australia), Z (New Zealand), N (None) or U (Unknown).
Tz            database time zone 	Timezone in "tz" (Olson) format, eg. "America/Los_Angeles".
Type 	      Type of the airport. Value "airport" for air terminals, "station" for train stations, "port" for ferry terminals and "unknown" if not known. In airports.csv, only type=airport is included.
Source 	      Source of this data. "OurAirports" for data sourced from OurAirports, "Legacy" for old data not matched to OurAirports (mostly DAFIF), "User" for unverified user contributions. In airports.csv, only source=OurAirports is included. 
```
There is a routes.dat file that contains routes which are the edges in our graph. The data fields for routes.dat are as follows in order:

 ```
Airline                 2-letter (IATA) or 3-letter (ICAO) code of the airline.
Airline ID              Unique OpenFlights identifier for airline (see Airline).
Source airport          3-letter (IATA) or 4-letter (ICAO) code of the source airport.
Source airport ID       Unique OpenFlights identifier for source airport (see Airport)
Destination airport     3-letter (IATA) or 4-letter (ICAO) code of the destination airport.
Destination airport ID  Unique OpenFlights identifier for destination airport (see Airport)
Codeshare               "Y" if this flight is a codeshare (that is, not operated by Airline, but another carrier), empty otherwise.
Stops 	                Number of stops on this flight ("0" for direct)
Equipment               3-letter codes for plane type(s) generally used on this flight, separated by spaces
 ```
 Our code only uses the 3-letter (IATA) code for the airports from the routes file.

