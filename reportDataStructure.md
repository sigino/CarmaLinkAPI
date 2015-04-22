## Report data structure  
All configurable reports produce Report Data objects in JSON format that contain the following standard fields:  

Field | JSON Name | Value type | Notes
------|-----------|------------|-------
Serial Number | serial | Integer | Identifies the transponder's serial number.  
Configuration ID | configId | Integer | References the specific configuration that caused this report to be generated.  
Event start timestamp	| eventStart | Integer | Specifies the POSIX time in milliseconds when the report's trigger condition first became true (after any allowance).  
Report timestamp | reportTimestamp | Integer | Specifies the POSIX time in milliseconds when the report was generated.  
Duration | duration | Integer | The Report timestamp minus the event start timestamp.  

All of this information will always be in all reports, with the exception of the non-configurable New Deployment report.  

In it's most basic form, a report will simply tell you when the trigger condition (as defined by the configuration) became true, and for how long. Depending on your configuration, the Report Data object may also include the Location object and/or the Optional Parameters object.  

### Location Object  
The Location object provides a kinematic snapshot of your vehicle in time and space. It provides the following fields:  

Field | JSON Name | Value type | Notes  
------|-----------|------------|-------
Longitude | longitude | Double | Degrees  
Latitude | latitude | Double | Degrees  
Accuracy | accuracy | Float | Meters, in reference to the longitude/latitude  
Heading |	heading	| Float |	Degrees, where 0° is north, 90° is east, 180° is south, and 270° is west
Speed | speed	| Float | km/hour  
Timestamp | gpsTimestamp | Integer | Specifies the POSIX time in milliseconds when location data was captured: this will likely be older than the report timestamp!  

If you set 'location' in your report configuration to 'true', then the transponder will try to include location information in your report. This information will be null (missing) in all reports until the transponder acquires a GPS lock.  

**GPS Timestamp**  
One special quality of the location object is that it includes its own timestamp. The transponder will update its location information as quickly as possible, and under favorable operating conditions that means that the 'gpsTimestamp' should be approximately equal to the 'reportTimestamp'. However, sometimes GPS lock can be lost, for example, when you enter a structure (tunnel, parking garage, etc). In this case, the transponder will always provide the **last known** location in the report data object: the freshness of this data will be indicated by the difference in time between the reportTimestamp and gpsTimestamp. Therefore, when examining report data it is important to see how recent the location information is with respect to the report timestamp.  

### Optional Parameters Data Object  
The Optional Parameters Data object includes any parameters specified in the report's configuration, and could include:  
Field | JSON Name | Value type | Units | Notes  
------|-----------|------------|-------|--------  
Battery voltage | batteryVoltage | Float | Volts | Typically accurate to within 50mV.    
Emission monitors | emissionMonitors | Integer | - | This is the bit-encoded value returned by an OBD-II (SAE J1979) Mode 1, PID 1 request that indicates which emission monitors are supported and which are incomplete.  
Fuel level | fuelLevel | Float | % | Reported as a decimal (0.5 = 50%)  
Fuel rate | fuelRate | Float | liters/hour | Engine configuration should be set to ensure this value is as accurate as possible.
Distance to service | distanceToService | Integer | km | When available, it is accurate to the nearest ten kilometers.   
Duration to service | durationToService | Integer | Milliseconds | When available, it is accurate to the nearest day (86400000 ms).
Odometer | odometer | Float | km | Accuracy is typically +/- 10km when available.  
Is low battery voltage | isLowBatteryVoltage | Boolean | true or false | Indicates that the battery voltage is low enough where starting the engine might soon become difficult.  
Is low tire pressure | isLowTirePressure | Boolean | true or false | This will correspond to a 'low tire pressure' warning light being illuminated on the dash.  

As indicated in the report configuration section, values for these parameters will only be included in the Optional Parameters Data object if the deployment (vehicle) supports them. Many of these parameters are not 'standard' OBD-II data, and so it is possible that for your make/model of vehicle, this data will not be available. If this is the case, these fields will simply not be included in the Optional Parameters object.  

Unlike the Location object, all values in the Optional Parameters Data object are collected within a second or two of the reportTimestamp time.

### Other report data  
In addition to this standard and optional data included in a Report Data object, some reports include additional data fields as standard. These fields will be mentioned in each report's respective section.  
