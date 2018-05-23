# SmartJP
A Model-Driven Solution to Support Smart Mobility Planning


# Installation Instructions - SmartJP
The SmartJP can be installed starting from the SmartJP.zip file. Once you have extracted this zip file, you should have the folders and files listed below. <b>Note:</b> the GTFS ZIP files must not be extracted.

* SmartJP.jar, the Open Trip Planner (OTP) - based application, in a single runnable JAR file. This has been compiled from a modified version of the OTP (http://www.opentripplanner.org/) source code. The modifications are related to the implemented "updaters" needed to support the management of the multiple mobility views realized in the approach: 1)Mobility Challenges; 2)Mobility Resources; 3)Mobility Remarks.

/graphs
  /current
    Graph.obj
    map.osm
    router-config.json
    trento-gtfs.zip
    
 * router-config.son: a configuration file for OTP specifying the "real-time OTP Graph updaters" types and their urls. It is read when the OTP server is started.
 
 * Graph.obj, map.osm, trento-gtfs.zip: it specifies every locations in the Trento (Italy) region and how to travel between them. It has been compiled using Open Street Map (https://www.openstreetmap.org/) data (map.osm file) for the street and path network and GTFS (trento-gtfs-zip file) data for transit scheduling.
 
 ## Starting up SmartJP
 To start the SmartJP, from the main directory, run the following command:
 
 <i>java -Xmx2G -jar SmartJp.jar  --router current --graphs graphs --server</b>
 
 * --router specifies the name of the router we want to use.
 * --graphs specifies the graph directory
 * --server indicates that we want to launch the journey planner in server mode
 
 It should only take less then a minute to loas the graph and start the Grizzly server. If all has worked you should see the message: <i> Grizzly server running </i>. You must leave the command/prompt/terminal window open. If you close it, the server will stop running. You can stop the server without closing the window by entering <i> Ctrl-C</i>.
 
 You can now access the web interface using the URL: <i>http://localhost:8080</i> (use Firefox of Chrome and not Internet Explorer).
 
 You can now zoom into the Trento area and request a route by setting and origin and a destination directly on the map. You can speficy travel dates, times and modes using "Trip Options" window (See Figure below). You can also change the background map from the layer stack icon at the top right.
 
 <p align="center">
  <img src="https://github.com/das-fbk/SmartJP/blob/master/GUI.png" width="650"/>
</p>

 


## Contributors

This study has been designed, developed, and reported by the following investigators:

* <b> Antonio Bucchiarone </b> - Fondazione Bruno Kessler (FBK), Trento - Italy

* <b> Antonio Cicchetti </b> - Malardalen University, Vasteras - Sweden





