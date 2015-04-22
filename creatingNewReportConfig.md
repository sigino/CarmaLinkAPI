<h2>Creating a new report configuration</h2>
A report configuration is created by using the PUT method on the report's configuration URI. The body of the request should contain a Report Configuration Update object in JSON format with the appropriate values for each field.  

Not all reports support all fields and some have restrictions regarding the requested values. Any field that is optional and has no default value will default to 'null'.  

:information_source: > All report configuration URIs are relative to /report_config  
> The success code is 204 (No Content)

**"Engine Overspeed" Report**  
URL: `/engine_overspeed`  
Allowance: optional, defaults to 0  
Threshold: required, units of RPM, must be > 0  
Location: optional, defaults to false  
Buzzer: optional  
Optional Parameters: optional  
Optional Conditions: not supported  

**"Hard Acceleration" Report**  
URL: `/hard_accel`  
Allowance: optional, defaults to 0  
Threshold: required, units of meters/sec^2, must be > 0  
Location: optional, defaults to false  
Buzzer: optional  
Optional Parameters: optional  
Optional Conditions: not supported  

**"Hard Braking" Report**  
URL: `/hard_braking`  
Allowance: optional, defaults to 0  
Threshold: required, units of meters/sec^2, must be < 0  
Location: optional, defaults to false  
Buzzer: optional  
Optional Parameters: optional  
Optional Conditions: not supported  

**"Hard Cornering" Report**  
URL: `/hard_cornering`  
Allowance: optional, defaults to 0  
Threshold: required, units of meters/sec^2, must be > 0  
Location: optional, defaults to false  
Buzzer: optional  
Optional Parameters: optional  
Optional Conditions: not supported  

**"Hard Cornering" Report**  
URL: `/hard_cornering`  
Allowance: optional, defaults to 0  
Threshold: required, units of meters/sec^2, must be > 0  
Location: optional, defaults to false  
Buzzer: optional  
Optional Parameters: optional  
Optional Conditions: not supported  

**"Status" Report**  
URL: `/status`  
Allowance: optional, defaults to 0  
Threshold: required, identifies send interval in msec, must be ≥ 5000  
Location: optional, defaults to false  
Buzzer: ignored  
Optional Parameters: optional  
Optional Conditions: not supported  

**"Idling" Report**  
URL: `/idling`  
Allowance: required, ≥ 5000  
Threshold: ignored  
Location: optional, defaults to false  
Buzzer: optional  
Optional Parameters: optional  
Optional Conditions: not supported  

**"Overspeeding" Report**  
URL: `/overspeeding`  
Allowance: optional, defaults to 0  
Threshold: required, units of km/hr, must be ≥ 50  
Location: optional, defaults to false  
Buzzer: optional  
Optional Parameters: optional  
Optional Conditions: not supported  

**"Parking" Report**  
URL: `/parking`  
Allowance: = 0  
Threshold: required, identifies send interval in msec, must be ≥ 1800000  
Location: optional, defaults to false  
Buzzer: ignored  
Optional Parameters: optional  
Optional Conditions: not supported  

**"Seatbelt Unbuckled" Report**  
URL: `/seatbelt`  
Allowance: optional, defaults to 0  
Threshold: Identifies minimum vehicle speed, must be > 0  
Location: optional, defaults to false  
Buzzer: optional  
Optional Parameters: optional  
Optional Conditions: not supported  

**"Transported" Report**  
URL: `/transported`  
Allowance: optional, defaults to 0  
Threshold: required, identifies send interval in msec, must be ≥ 30000  
Location: optional, defaults to false  
Buzzer: ignored  
Optional Parameters: optional  
Optional Conditions: not supported  

**"Trip Summary" Report**  
URL: `/trip_report`  
Allowance: optional, defaults to 0  
Threshold: ignored  
Location: optional, defaults to false  
Buzzer: ignored  
Optional Parameters: optional  
Optional Conditions: not supported  

**"Vehicle Health" Report**  
URL: `/vehicle_health`  
Allowance: = 0  
Threshold: ignored  
Location: optional, defaults to false  
Buzzer: ignored  
Optional Parameters: optional  
Optional Conditions: optional  


--
<h3>Usage Example</h3>  
In this example, we configure CarmaLink serial number 159821's 'overspeeding' threshold to 129kph (~80mph), with a 5 second allowance, and we'd like the generated report to include location, an odometer reading, and the vehicle's battery voltage.  Also, the buzzer should sound an alert at high volume to let the driver know they are going too fast.  

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

