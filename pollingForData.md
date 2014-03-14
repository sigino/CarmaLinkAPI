<h2>Polling For Data</h2>  
If your application needs to periodically poll for report data it's suggested that you set up a status report to contact the server at least once during the polling interval. Each time you receive a successful status report from CarmaLink you can assume that all data up until that point has been sent to the server and you may query for it as you wish. If however, the CarmaLink happens to lose its wireless signal and it can't send any report data, you will note that you do not get a status report back (or any reports for that matter). Your application should take note of the last successful _reportTimestamp_ the CarmaLink reported. You may continue to poll and when CarmaLink regains connectivity, it will push all the delinquent reports to the server. At this point your application can "catch up" to any data missed during this period by querying for any data with the "since" query parameter using the CarmaLink's last successful status _reportTimestamp_ as the value.  
  
### Dealing With Queued Data Due To Poor Wireless Signal  
CarmaLink can only transmit while connected to a GSM wireless network. Some common trouble spots include underground car parks and tunnels.  
  
While CarmaLink has poor signal strength, reports are still recorded and queued and will be sent once signal strength has improved. To ensure your application receives all the queued data, it must use the timestamp from the last report received as seen in the example below.  
  
    https://api.carmalink.com:8282/v1/all/data/all_activity?since=[last polling timestamp]
  
### Detecting CarmaLink Connectivity  
If your application wants to know the connection status of a CarmaLink, it is recommended to configure a status report. Because status reports are temporal, not event driven, it will fire on a periodic basis which allows for a simple connectivity check. If the set period has been exceeded without receiving a status report it can be assumed that CarmaLink has poor signal strength and cannot transmit.  
  
### Report Data Structures  
All report data objects, with the exception of the 'New Deployment' report, *always* contain the following elements:  
  
**serial**  
the serial number of the reporting CarmaLink  
  
**configId**  
the report configuration identifier from which this report was generated  
  
**eventStart**  
the event start timestamp  
  
**reportTimestamp**  
the timestamp of the report  
  
**duration**  
(reportTimestamp - eventStart)  

! Other than these required fields, all other fields or objects inside a report are ONLY present if the information is available and accurate.  For example, the device will not include the 'fuelConsumed' field in the 'Trip Summary' report if this data is unavailable. Similarly, the 'location' object data will not be present in any report until a GPS lock has been established.  
  
-----  
  
Some report data includes a special "location" object if the CarmaLink has been configured to use it:  
  
**longitude**  
Longitude in degrees  
  
**latitude**  
Latitude in degrees  
  
**accuracy**  
Radius in meters  
  
**heading**  
The direction in degrees  
  
**speed**  
Speed of vehicle in Km/Hr  
  
Location data will not be available until CarmaLink has established a positive satellite lock. The vehicle's surrounding environment such as underground car parks, tunnels, dense urban environments and terrain can impact the satellite lock. Placement and orientation of CarmaLink is an important factor in the ability to obtain a location; follow the installation instructions in the User Guide for the best location lock.  
  
-----  

### Report Structures  
**All Activity Report**  
Each ellipsized array contains a list of report objects of the appropriate type. All the other report types are included except for New Deployment Report.  
```javascript
{  
 "statusReports":[...],  
 "accelerationReports":[...],  
 "hardBrakingReports":[...],  
 "hardCorneringReports":[...],  
 "idlingReports":[...],  
 "overspeedingReports":[...],  
 "summaryReports":[...],  
 "parkingBrakeDragReports":[...],  
 "seatbeltReports":[...],  
 "vehicleHealthReports":[...]  
}  
```

**Engine Overspeed Report**  
An object representing an engine overspeed report. This report is generated both at the start ("inProgress" : true) and at the end ("inProgress" : false) of the event. The "maxEngineSpeed" field is given in RPM.  
```javascript
{  
 "serial" : 49,  
 "configId" : 5192,  
 "eventStart" : 1371679278585,  
 "reportTimestamp" : 1371679279105,  
 "duration" : 520,  
 "maxEngineSpeed" : 6841.1,  
 "inProgress" : false  
}  
```

**Hard Acceleration Report**  
An object representing a hard acceleration report.  
```javascript
{  
 "serial" : 49,  
 "configId" : 4883,  
 "eventStart" : 1371679278585,  
 "reportTimestamp" : 1371679278962,  
 "duration" : 377,  
 "maxAcceleration" : 3.45  
}  
```
  
**Hard Braking Report**  
An object representing a hard braking report.  
```javascript
{  
 "serial" : 49,  
 "configId" : 9939,  
 "eventStart" : 1385764856768,  
 "reportTimestamp" : 1385764862490,  
 "duration" : 5722,  
 "minAcceleration" : -4.53  
}  
```
  
**Hard Cornering Report**  
An object representing a hard cornering report.  
```javascript
{  
 "serial" : 49,  
 "configId" : 4932,  
 "eventStart" : 1380474999953,  
 "reportTimestamp" : 1380475001459,  
 "duration" : 1506,  
 "maxAcceleration" : 1.53,  
 "direction" : "RIGHT"  
}  
```
  
**Idling Report**  
An object representing an idling report.  
```javascript
{  
 "serial" : 49,  
 "configId" : 8483,  
 "eventStart" : 1388959222356,  
 "reportTimestamp" : 1388959293432,  
 "duration" : 71076,  
 "fuelConsumed" : 1.23  
}  
```

**Overspeeding Report**  
An object representing an overspeeding report.  
```javascript
{  
 "serial" : 49,  
 "configId" : 884,  
 "eventStart" : 1364906765951,  
 "reportTimestamp" : 1364906778002,  
 "duration" : 12051,  
 "maxSpeed" : 120.54  
}  
```
  
**Parking Report**  
An object representing a 'Parking' report. When the "inProgress" field is set to true, the vehicle is still parked.  When this field is false, the parked state has concluded, and the vehicle has started traveling.  
```javascript
{  
 "serial" : 49,  
 "configId" : 884,  
 "eventStart" : 1364906765951,  
 "reportTimestamp" : 1364910365951,  
 "duration" : 3600000,  
 "averageBatteryVoltage" : 12.52,  
 "inProgress" : false  
}  
```

**Parking Brake Drag Report**  
An object representing a parking brake drag report.  
```javascript
{  
 "serial" : 49,  
 "configId" : 854,  
 "eventStart" : 1364906575296,  
 "reportTimestamp" : 1364906680933,  
 "duration" : 105637,  
 "distance" : 5.6,  
 "maxSpeed" : 32.54  
}  
```
  
**Seatbelt Not Used Report**  
An object representing a seatbelt not in use report.  
```javascript
{  
 "serial" : 49,  
 "configId" : 908,  
 "eventStart" : 1392158187270,  
 "reportTimestamp" : 1392158214037,  
 "duration" : 26767,  
 "maxSpeed" : 47.87  
}  
```
    
**Trip Summary Report**  
An object representing a trip summary report.  
```javascript
{  
 "serial" : 49,  
 "configId" : 884,  
 "eventStart" : 1391612028990,  
 "reportTimestamp" : 1391612386612,  
 "duration" : 357622,  
 "fuelConsumed" : 32.46,  
 "distance" : 45.66,  
 "averageBatteryVoltage" : 14.3,  
 "inProgress": false  
}  
```
  
**Vehicle Health Report**  
An object representing a vehicle health report.  
```javascript
{  
 "serial" : 49,  
 "configId" : 8836,  
 "eventStart" : 1391718245781,  
 "reportTimestamp" : 1391718246782,  
 "duration" : 1001,  
 "dtcs" : [ "P0374" ]  
}  
```
  
**Status Report**  
An object representing a Status report.  
```javascript
{  
 "serial" : 49,  
 "configId" : 2345,  
 "eventStart" : 1392214039016,  
 "reportTimestamp" : 1392215206357,  
 "duration" : 1167341,  
 "gsmSignalStrength" : -75.0  
}  
```
  
**Location Object**  
An object representing a location. This sub-object is included in any reports that support enabling the location flag.  
```javascript
"location" : {  
 "longitude" : -73.8231057,  
 "latitude" : 42.6263101,  
 "accuracy" : 5.164,  
 "heading" : 236.34811,  
 "speed" : 25.2  
}  
```
  
**Optional Parameters Object**  
An object representing the optional parameter data for the given report.  This sub-object will only appear in a report that has been configured to include optional parameters: only the parameters listed in the configuration will be present in this sub-object.  
```javascript
"optionalParams" : {  
 "odometer" : 96921.01,  
 "durationToService" : 60,  
 "distanceToService" : 157,  
 "emissionMonitors" : 517376,  
 "fuelLevel" : 54.3,  
 "isLowBatteryVoltage" : false,  
 "isLowTirePressure" : true,  
 "batteryVoltage" : 13.8  
}  
```
  
-----  
  
### New Deployment Report  
An object representing a new deployment. Note, this object is updated by two separate events on the CarmaLink. The first event is when the CarmaLink is initially installed into a vehicle’s OBDII port. A "New Installation" event is sent to the server and this deployment record is created with the ’installationTime’ and ’removalTime’ fields set. The second event is when the vehicle is started for the first time following a new installation. A "New Deployment" event is then sent to the server with the ’deploymentTime’ and ’vin’ (if available) fields set.  
  
**Deployment Timeline**  
  ![timeline image](img/API_deployTimeline400.png)(width=250, height=145)  
1. CarmaLink is plugged into the vehicle (New Installation)   
2. Vehicle is turned on  
3. CarmaLink connects to the ECU and retrieves the VIN (New Deployment)  
  
**Not all vehicles support VIN through OBD-II. Vehicles that don't support VIN will return an empty string "" for the VIN.**  

```javascript
{  
 "serial" : 49,  
 "installationTime" : 1344707279452,  
 "removalTime" : 1344701632346,  
 "deploymentTime" : 1344707286452,  
 "vin" : "1FTPX14534FA30554"  
}  
```
  
[Next Section: 5. Referenced Documents & Standards](https://github.com/CarmaSys/CarmaLinkAPI/blob/1.6/referencedDocumentsAndStandards.md)
