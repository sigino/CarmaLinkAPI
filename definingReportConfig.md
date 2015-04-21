<h2>Defining a report configuration</h2>  
For each report of interest, the API user must send configuration information to the appropriate URI. This <b>Report Configuration Update object</b> in JSON format characterizes the vehicle activity that should be detected, and will have some or all of the following fields:  

**Threshold**  
JSON Name: threshold  
Value: Float; units specific to each report type  
Description: Specifies a value that is the trigger for the report to begin.  

**Allowance**  
JSON Name: allowance  
Value: Integer; number of milliseconds  
Description: Specifies a time duration over which the report's event trigger (value exceeding threshold) must remain set before the report is actually triggered. The allowance acts as a filtering mechanism, so that events that are too brief to be considered relevant are ignored.  

**Location**  
JSON Name: location  
Value: Boolean; true or false  
Description: Specifies whether location information should be included in the generated report.  

**Buzzer**  
JSON Name: buzzer  
Value: String; "OFF","MEDIUM" or "HIGH"  
Description: Specifies the volume of the CarmaLink's buzzer when the event is triggered. If never assigned for the report, the buzzer defaults to "OFF".  

**Optional Parameters**  
JSON Name: optionalParams  
Value: List of strings; see Optional Parameters section  
Description: This field can contain a list of strings to optionally add parameters to a report.  

**Optional Conditions**  
JSON Name: optionalConditions  
Value: List of strings; see Optional Conditions section  
Description: This field can contain a list of strings that specify optional report trigger conditions. Only certain reports are allowed to be configured with optional conditions.  



--
<h2>Optional Parameters</h2>  
The Optional Parameters field identifies 'extra' information that should be present in reports generated from this configuration. Current optional parameters include:  

optionalParam value | Notes
--------------------|-------
BATTERY_VOLTAGE | The vehicle battery voltage as captured by CarmaLink's A/D convertor.  
EMISSION_MONITORS | Returns emission monitor support and status information.  
FUEL_LEVEL | Available on some vehicles.  
FUEL_RATE | Available on most vehicles.
DISTANCE_TO_SERVICE | This is the estimated distance until the next scheduled service as indicated by the instrument cluster. Only available on select vehicles that support this parameter.  
DURATION_TO_SERVICE | This is the amount of time remaining until the next scheduled service as indicated by the instrument cluster. Only available on select vehicles that support this parameter.  
ODOMETER | From the instrument cluster; only available on select vehicles that support this parameter.  
IS_LOW_BATTERY_VOLTAGE | Available on all vehicles.  
IS_LOW_TIRE_PRESSURE | From the instrument cluster; only available on select vehicles that support this parameter.  

<h2>Optional Conditions</h2>  
The Optional Conditions field identifies 'extra' conditions that can cause a report to be generated. Specifically, a report is created anytime a given condition changes values. Presently, only the 'Vehicle Health' report is allowed to use of these optional conditions.  

optionalCondition value:  
EMISSION_MONITORS  
IS_LOW_BATTERY_VOLTAGE  
IS_LOW_TIRE_PRESSURE  
