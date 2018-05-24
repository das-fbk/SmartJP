# SmartJP
A Model-Driven Solution to Support Smart Mobility Planning


# Installation Instructions
The SmartJP can be installed starting from the SmartJP.zip file. Once you have extracted this zip file, you should have the folders and files listed below. <b>Note:</b> the GTFS ZIP files must not be extracted.

* SmartJP.jar, the Open Trip Planner (OTP) - based application, in a single runnable JAR file. This has been compiled from a modified version of the OTP (http://www.opentripplanner.org/) source code. The modifications are related to the implemented "updaters" needed to support the management of the multiple mobility views realized in the approach: 1)Mobility Challenges; 2)Mobility Resources; 3)Mobility Remarks.

- /graphs
   - /current
     - Graph.obj
     - map.osm
     - router-config.json
     - trento-gtfs.zip
    
 * router-config.json: a configuration file for OTP specifying the "real-time OTP Graph updaters" types and their urls. It is read when the OTP server is started.
 
 * Graph.obj, map.osm, trento-gtfs.zip: it specifies every locations in the Trento (Italy) region and how to travel between them. It has been compiled using Open Street Map (https://www.openstreetmap.org/) data (map.osm file) for the street and path network and GTFS (trento-gtfs-zip file) data for transit scheduling.
 
 ## Starting up SmartJP
 To start the SmartJP, from the main directory, run the following command:
 
 <i>java -Xmx2G -jar SmartJp.jar  --router current --graphs graphs --server</i>
 
 * --router specifies the name of the router we want to use.
 * --graphs specifies the graph directory
 * --server indicates that we want to launch the journey planner in server mode
 
 It should only take less then a minute to loas the graph and start the Grizzly server. If all has worked you should see the message: <i> Grizzly server running </i>. You must leave the command/prompt/terminal window open. If you close it, the server will stop running. You can stop the server without closing the window by entering <i> Ctrl-C</i>.
 
 You can now access the web interface using the URL: <i>http://localhost:8080</i> (use Firefox of Chrome and not Internet Explorer).
 
 You can now zoom into the Trento area and request a route by setting and origin and a destination directly on the map. You can speficy travel dates, times and modes using "Trip Options" window (See Figure below). You can also change the background map from the layer stack icon at the top right.
 
 <p align="center">
  <img src="https://github.com/das-fbk/SmartJP/blob/master/GUI.png" width="100%"/>
</p>

 
## Mobility Remarks Example
To see how, thanks to the Model-Driven support, the SmartJP is able to consider <i>Mobility Remarks</i>, we can start explaining the following JSON file generated by the <i>Model-Driven Mobility Configurator</i>.
```
{
	"blocks": [
		{	
		"wayId": 25340095,
		"startNodeId": 276104484,
		"endNodeId": 276104881
		},
		{	
		"wayId": 25340095,
		"startNodeId": 173096043,
		"endNodeId": 173096047
		},
		{	
		"wayId": 25340095,
		"startNodeId": 272398985,
		"endNodeId": 271743214
		}
	]				
}
```
This JSON has been generated by the Model-Driven Mobility Configurator and describes that a specific <i>Road Segment</i> (i.e., in Via Dei Pomari) must be BLOCKED. This file is taken into account by the SmartJP during each planning task and will avoid the specific road segment. In the figure below, we can see the resulting journey planning when the user selects the "Drive Only" travel mode.

<p align="center">
  <img src="https://github.com/das-fbk/SmartJP/blob/master/MobilityRemarks-BlockedSegments.png" width="100%"/>
</p>


## Mobility Resource Example
To see how, thanks to the Model-Driven support, the SmartJP is able to consider <i>Mobility Resources</i>, we can start explaining the following JSON file generated by the <i>Model-Driven Mobility Configurator</i>.

```
{
 "routes":[
		{	
		"routeId": "1__400",
		"startDate": "20180520",
		"endDate": "20180523"
		}
	]
}
```

This JSON has been generated by the Model-Driven Mobility Configurator and describes that a specific <i>Bus Route</i> (i.e., line 400) must be SUSPENDED in a specific date range (From May, 20 2018 to May 23, 2018). This file is taken into account by the SmartJP during each planning task and will avoid the specific bus (Bus n. 5) in the specific period from any of its planning results.

### Example 1: Bus n.5 SUSPENDED (In the date range)
<p align="center">
  <img src="https://github.com/das-fbk/SmartJP/blob/master/MobilityResources-InRange.png" width="100%"/>
</p>

### Example 2: Bus n.5 NOT SUSPENDED (Out of the date range)
<p align="center">
  <img src="https://github.com/das-fbk/SmartJP/blob/master/MobilityResources-OutRange.png" width="100%"/>
</p>

# The Mobility Modelling Layer
The modelling approach adopted in our solution is based on the separation of concerns principle; in particular, it provides three different views, called mobility challenges, mobility resources, and mobility remarks. It is worth noting the 1:1 correspondence between the modelling layer concepts and the code layer. Indeed the modelling layer abstracts the code layer, allowing the domain experts to deal with the complexity of smart mobility management.

## Mobility Challenges View
The model depicted in the following picture includes the definition of means of trasportation and their relationships when considered for planning. Moreover, it is possible to specify specific characteristics of available routes, as well as travel preferences in terms of planning parameters.

<p align="center">
  <img src="https://github.com/das-fbk/SmartJP/blob/master/MobilityChallengesModel.png" width="100%"/>
</p>

Notably, the example specifies that whenever the selected means of transportation are <i>Bus</i> or <i>Transit</i>, it has to be established how much the user is willing to walk. In this particular case, if the user prefers a <i>leastwalking</i> route, a parameter about the maximum walking distance acceptable for a travel plan has to be set. In turn, the value for such a parameter, that is <i>maxWalkingDistance</i>, is set to 500m by default as per city administration policies. These values might be modified by user's preferences, green policies, and so forth.

## Contributors

This study has been designed, developed, and reported by the following investigators:

* <b> Antonio Bucchiarone </b> - Fondazione Bruno Kessler (FBK), Trento - Italy

* <b> Antonio Cicchetti </b> - Mälardalen University, Västerås - Sweden





