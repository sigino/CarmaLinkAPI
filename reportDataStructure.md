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


