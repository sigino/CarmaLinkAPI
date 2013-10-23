<h2>Polling for Data</h2>  
If your application needs to periodically poll for report data it's suggested that you set up a status report to contact the server at least once during the polling interval. Each time you receive a successful status report from CarmaLink you can assume that all data up until that point has been sent to the server and you may query for it as you wish. If however, the CarmaLink happens to lose its wireless signal and it can't send any report data, you will note that you do not get a status report back (or any reports for that matter). Your application should take note of the last successful reportTimestamp the CarmaLink reported. You may continue to poll and when CarmaLink regains connectivity, it will push all the delinquint reports to the server. At this point your application can "catch up" to any data missed during this period by querying for any data with the "since" query parameter using the CarmaLink's last succesful status reportTimestamp as the value.  
  
### Dealing With Queued Data Due To Poor Wireless Signal  
CarmaLink can only transmit while connected to a GSM wireless network. Some common trouble spots include underground car parks and tunnels.  
  
While CarmaLink has poor signal strength, reports are still recorded and queued and will be sent once signal strength has improved. To ensure your application receives all the queued data, it must use the timestamp from the last report received as seen in the example below.  
  
    https://api.carmalink.com:8282/v1/all/data/all_activity?since=[last polling timestamp]
  
**Detecting CarmaLink Connectivity**  
If your application wants to know the connection status of a CarmaLink, it is recommended to configure a status report. Because status reports are temporal, not event driven, it will fire on a periodic basis which allows for a simple connectivity check. If the set period has been exceeded without receiving a status report it can be assumed that CarmaLink has poor signal strength and cannot transmit.  
  
**Report Data Structures**  
All report data objects contain the following elements:  
  
**serial**  
the serial number of the reporting CarmaLink  
  
**configId**  
the report configuration id from which this report was generated  
  
**eventStart**  
the event start timestamp  
  
**duration**  
the duration  
  
**reportTimestamp**  
the timestamp of the report  
  
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
 "faultReports":[...],  
 "accelerationReports":[...],  
 "hardBreakingReports":[...],  
 "idlingReports":[...],  
 "overspeedingReports":[...],  
 "summaryReports":[...]  
}
```
  
**Hard Acceleration Report**  
An object representing a hard acceleration report.  
```javascript
{  
 "serial":49,  
 "configId": 4883,  
 "eventStart":1341256638660,  
 "duration":13242,  
 "maxAcceleration":3.45,  
 "reportTimestamp":1357738287406  
}
```
  
**Hard Braking Report**  
An object representing a hard braking report.  
```javascript
{  
 "serial":49,  
 "configId": 9939,  
 "eventStart":1341256638660,  
 "duration":13242,  
 "minAcceleration":-4.53,  
 "reportTimestamp":1357738287406  
}
```
  
**Hard Cornering Report**  
An object representing a hard cornering report.  
```javascript
{  
 "serial":49,  
 "configId": 4932,  
 "eventStart":1341256638660,  
 "duration":1342,  
 "maxAcceleration":1.53,  
 "direction": "RIGHT"  
 }
```
  
**Idling Report**  
An object representing an idling report.  
```javascript
{  
 "serial":49,  
 "configId": 8483,  
 "eventStart":1341256638660,  
 "duration":13242,  
 "fuelConsumed":1.23,  
 "reportTimestamp":1357738287406  
}
```
  
**Overspeeding Report**  
An object representing an overspeeding report.  
```javascript
{  
 "serial":49,  
 "configId": 884,  
 "eventStart":1341256638660,  
 "duration":13242,  
 "maxSpeed":120.54,  
 "reportTimestamp":1357738287406  
}
```
  
**Parking Brake Drag Report**  
An object representing a parking brake drag report.  
```javascript
{  
 "serial":49,  
 "configId": 854,  
 "eventStart":1341256638660,  
 "duration":2132423,  
 "distance": 5.6,  
 "maxSpeed":32.54,  
 "reportTimestamp":1357738287406  
}
```
  
**Seatbelt Not Used Report**  
An object representing a seatbelt not in use report.  
```javascript
{  
 "serial":49,  
 "configId": 908,  
 "eventStart":1341256634660,  
 "duration":945423,  
 "distance": 23.65,  
 "maxSpeed": 47.87,  
 "reportTimestamp":1357738287406  
}
```
    
**Trip Summary Report**  
An object representing a trip summary report. (add context for inProgress)  
```javascript
{  
 "serial":49,  
 "configId": 884,  
 "eventStart":1341256638660,  
 "duration":13242,  
 "fuelConsumed":32.46,  
 "distance": 45.66,  
 "voltage": 14.3,  
 "odometer": 62838.37,  
 "durationToService" : 40,  
 "distanceToService" : 403,  
 "inProgress": false,  
 "reportTimestamp":1357738287406  
}
```
  
**Vehicle Health Report**  
An object representing a vehicle health report.  
```javascript
{  
 "serial":49,  
 "configId": 8836,  
 "eventStart": 13412566398487,  
 "reportTimestamp":1357738287406,  
 "duration": 0,  
 "dtcs": ["P8374"],  
 "tirePressureLow": true  
 }
```
  
**Status Report**  
An object representing a Status report.  
```javascript
{  
 "serial":49,  
 "configId": 2345,  
 "eventStart": 1341256638660,  
 "duration": 83928,  
 "vehicleVoltage":12.994524,  
 "gsmSignalStrength":-75.0,  
 "reportTimestamp":1357738287406  
}
```
  
**Location Object**  
An object representing a location. This sub-object is included in any reports that support enabling the location flag.  
```javascript
{  
 "longitude": -73.8231057,  
 "latitude": 42.6263101,  
 "accuracy": 5.164,  
 "heading": 236.34811,  
 "speed": 25  
}
```
  
-----  
  
### New Deployment Report  
An object representing a new deployment. Note, this object is updated by two separate events on the CarmaLink. The first event is when the CarmaLink is initially installed into a vehicle’s OBDII port. A "New Installation" event is sent to the server and this deployment record is created with the ’installationTime’ and ’removalTime’ fields set. The second event is when the vehicle is started for the first time following a new installation. A "New Deployment" event is then sent to the server with the ’deploymentTime’ and ’vin’ (if available) fields set (among others which aren’t represented here).  
  
**Deployment Timeline**  
1. CarmaLink is plugged into the vehicle (New Installation)   
2. Vehicle is turned on  
3. CarmaLink connects to the ECU and retrieves the VIN (New Deployment)  
  ![timeline image](img/API_deployTimeline.png)
  **! Not all vehicles support VIN through OBD-II. Vehicles that don't support VIN will return an empty string "" for the VIN.**  
  
```javascript
{  
 "serial":49,  
 "installationTime": 1344707279452,  
 "removalTime":1344701632346,  
 "deploymentTime":1344707286452,  
 "vin":"1FTPX14534FA30554"  
}
```
  
[Next Section: Referenced Documents & Standards](https://github.com/CarmaSys/CarmaLinkAPI/blob/1.4/referencedDocumentsAndStandards.md)
