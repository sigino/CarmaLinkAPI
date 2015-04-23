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
<sub>Hard Acceleration</sub> | <sub>`/hard_accel`</sub> | <sub>optional, defaults to 0</sub> | <sub>required, units of meters/sec^2, must be > 0</sub> | <sub>optional, defaults to false</sub> | <sub>optional</sub> | <sub>optional</sub> | <sub>not supported</sub>   
<sub>Hard Braking</sub> | <sub>`/hard_braking`</sub> | <sub>optional, defaults to 0</sub> | <sub>required, units of meters/sec^2, must be < 0</sub> | <sub>optional, defaults to false</sub> | <sub>optional</sub> | <sub>optional</sub> | <sub>not supported</sub>  
<sub>Hard Cornering</sub> | <sub>`/hard_cornering`</sub> | <sub>optional, defaults to 0</sub> | <sub>required, units of meters/sec^2, must be > 0</sub> | <sub>optional, defaults to false</sub> | <sub>optional</sub> | <sub>optional</sub> | <sub>not supported</sub>  
<sub>Status</sub> | <sub>`/status`</sub> | <sub>optional, defaults to 0</sub> | <sub>required, identifies send interval in msec, must be ≥ 5000</sub> | <sub>optional, defaults to false</sub> | <sub>ignored</sub> | <sub>optional</sub> | <sub>not supported</sub>  
<sub>Idling</sub> | <sub>`/idling`</sub> | <sub>required, ≥ 5000</sub> | <sub>ignored</sub> | <sub>optional, defaults to false</sub> | <sub>optional</sub> | <sub>optional</sub> | <sub>not supported</sub>  
<sub>Overspeeding</sub> | <sub>`/overspeeding`</sub> | <sub>optional, defaults to 0</sub> | <sub>required, units of km/hr, must be ≥ 50</sub> | <sub>optional, defaults to false</sub> | <sub>optional</sub> | <sub>optional</sub> | <sub>not supported</sub>  
<sub>Parking</sub> | <sub>`/parking`</sub> | <sub>= 0</sub> | <sub>required, identifies send interval in msec, must be ≥ 1800000</sub> | <sub>optional, defaults to false</sub> | <sub>ignored</sub> | <sub>optional</sub> | <sub>not supported</sub>  
<sub>Seatbelt Unbuckled</sub> | <sub>`/seatbelt`</sub> | <sub>optional, defaults to 0</sub> | <sub>Identifies minimum vehicle speed, must be > 0</sub> | <sub>optional, defaults to false</sub> | <sub>optional</sub> | <sub>optional</sub> | <sub>not supported</sub>  
<sub>Transported</sub> | `/transported` | <sub>optional, defaults to 0</sub> | <sub>required, identifies send interval in msec, must be ≥ 30000</sub> | <sub>optional, defaults to false</sub> | <sub>ignored</sub> | <sub>optional</sub> | <sub>not supported</sub>  
<sub>Trip Summary</sub> | `/trip_report` | <sub>optional, defaults to 0</sub> | <sub>ignored</sub> | <sub>optional, defaults to false</sub> | <sub>ignored</sub> | <sub>optional</sub> | <sub>optional</sub> | <sub>not supported</sub>  
<sub>Vehicle Health</sub> | `/vehicle_health` | <sub>= 0</sub> | <sub>ignored</sub> | <sub>optional, defaults to false</sub> | <sub>ignored</sub> | <sub>optional</sub> | <sub>optional</sub>  


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
