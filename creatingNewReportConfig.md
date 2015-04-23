<h2>Creating a new report configuration</h2>
A report configuration is created by using the PUT method on the report's configuration URI. The body of the request should contain a Report Configuration Update object in JSON format with the appropriate values for each field.  

Not all reports support all fields and some have restrictions regarding the requested values. Any field that is optional and has no default value will default to 'null'.  

> :information_source:   
>
> All report configuration URIs are relative to /report_config  
> The success code is 204 (No Content)  

<sub>Report</sub> | <sub>URI</sub> | <sub>Allowance</sub> | <sub>Threshold</sub> | <sub>Location</sub> | <sub>Buzzer</sub> | <sub>Optional Parameters</sub> | <sub>Optional Conditions</sub>
-------|-----|-----------|-----------|----------|--------|---------------------|---------------------
<sub>Engine Overspeed</sub> | <sub>`/engine_overspeed`</sub> | <sub>optional, defaults to 0</sub> | <sub>required, units of RPM, must be > 0</sub> | <sub>optional, defaults to false</sub> | <sub>optional</sub> | <sub>optional</sub> | <sub>not supported</sub>  
Hard Acceleration</sub> | <sub>`/hard_accel`</sub> | <sub>optional, defaults to 0</sub> | <sub>required, units of meters/sec^2, must be > 0</sub> | <sub>optional, defaults to false</sub> | <sub>optional</sub> | <sub>optional</sub> | <sub>not supported</sub>   
<sub>Hard Braking</sub> | <sub>`/hard_braking`</sub> | <sub>optional, defaults to 0</sub> | <sub>required, units of meters/sec^2, must be < 0</sub> | <sub>optional, defaults to false</sub> | <sub>optional</sub> | <sub>optional</sub> | <sub>not supported</sub>  
<sub>Hard Cornering</sub> | <sub>`/hard_cornering`</sub> | <sub>optional, defaults to 0</sub> | <sub>required, units of meters/sec^2, must be > 0</sub> | <sub>optional, defaults to false</sub> | <sub>optional</sub> | <sub>optional</sub> | <sub>not supported</sub>  
Status | <sub>`/status` | <sub>optional, defaults to 0 | <sub>required, identifies send interval in msec, must be ≥ 5000 | <sub>optional, defaults to false | <sub>ignored | <sub>optional | <sub>not supported  
Idling | `/idling` | required, ≥ 5000 | ignored | optional, defaults to false | optional | optional | not supported  
Overspeeding | `/overspeeding` | optional, defaults to 0 | required, units of km/hr, must be ≥ 50 | optional, defaults to false | optional | optional | not supported  
Parking | `/parking` | = 0 | required, identifies send interval in msec, must be ≥ 1800000 | optional, defaults to false | ignored | optional | not supported  
Seatbelt Unbuckled | `/seatbelt` | optional, defaults to 0 | Identifies minimum vehicle speed, must be > 0 | optional, defaults to false | optional | optional | not supported  
Transported | `/transported` | optional, defaults to 0 | required, identifies send interval in msec, must be ≥ 30000 | optional, defaults to false | ignored | optional | not supported  
Trip Summary | `/trip_report` | optional, defaults to 0 | ignored | optional, defaults to false | ignored | optional | optional | not supported  
Vehicle Health | `/vehicle_health` | = 0 | ignored | optional, defaults to false | ignored | optional | optional  


--
<h3>Usage Example</h3>  
In this example, we configure the transponder's serial number 159821's 'Overspeeding' threshold to 129kph (~80mph), with a 5 second allowance, and we'd like the generated report to include location, an odometer reading, and the vehicle's battery voltage.  Also, the buzzer should sound an alert at high volume to let the driver know they are going too fast.  

```javascript
PUT https://api.carmalink.com:8282/v1/159821/report_config/overspeeding  
{  
  "threshold" : 160.0,  
  "allowance" : 5000,  
  "location" : true,  
  "buzzer" : "HIGH",  
  "optionalParams" : [ "BATTERY_VOLTAGE", "ODOMETER" ]  
}  
```

[:fast_forward: Next Section: Reading a report configuration](/readingReportConfig.md)
