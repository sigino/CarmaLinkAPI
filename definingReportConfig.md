<h2>Defining a report configuration</h2>  
For each type of event of interest, the API user must send configuration information to the appropriate URI. This *Report Configuration Update object* in JSON format characterizes the vehicle activity (aka 'the event') that should be detected, and will have some or all of the following fields:  

> :information_source:  
>  
> *For all JSON objects discussed in this document, the 'Value type' is in reference to the native data-type the server uses to store this information.*

Field | JSON Name | Value type | Description 
------|-----------|------------|------------
Threshold | threshold | Float; units specific to each report type | Specifies a value that is the trigger for the report to begin.
Allowance | allowance | Integer; number of milliseconds | Specifies a time duration over which the report's event trigger (value exceeding threshold) must remain set before the report is actually triggered. The allowance acts as a filtering mechanism, so that events that are too brief to be considered relevant are ignored.
Location | location | Boolean; true or false | Specifies whether location information should be included in the generated report.
Buzzer | buzzer | String; "OFF","MEDIUM" or "HIGH" | Specifies the volume of the transponder's buzzer when the event is triggered. If never assigned for the report, the buzzer defaults to "OFF".
Optional Parameters | optionalParams | List of strings; see Optional Parameters section | This field can contain a list of strings to optionally add parameters to a report.
Optional Conditions | optionalConditions | List of strings; see Optional Conditions section | This field can contain a list of strings that specify optional report trigger conditions. Only certain reports are allowed to be configured with optional conditions.  



--
<h2>Optional Parameters</h2>  
The Optional Parameters field identifies 'extra' information that should be present in reports generated from this configuration. Current optional parameters include:  

optionalParam value | Notes
--------------------|-------
BATTERY_VOLTAGE | The vehicle battery voltage as captured by the transponder's A/D convertor.  
EMISSION_MONITORS | Returns emission monitor support and status information.  
FUEL_LEVEL | Available on some vehicles.  
FUEL_RATE | Available on most vehicles.
DISTANCE_TO_SERVICE | This is the estimated distance until the next scheduled service as indicated by the instrument cluster. Only available on select vehicles that support this parameter.  
DURATION_TO_SERVICE | This is the amount of time remaining until the next scheduled service as indicated by the instrument cluster. Only available on select vehicles that support this parameter.  
ODOMETER | From the instrument cluster; only available on select vehicles that support this parameter.  
IS_LOW_BATTERY_VOLTAGE | Available on all vehicles.  
IS_LOW_TIRE_PRESSURE | From the instrument cluster; only available on select vehicles that support this parameter.  

<h2>Optional Conditions</h2>  
The Optional Conditions field identifies `'extra'` conditions that can cause a report to be generated. Specifically, a report is created anytime a given condition changes values. Presently, only the `'Vehicle Health'` report is allowed to use of these optional conditions.  

<h3>optionalCondition value:</h3>  
EMISSION_MONITORS  
IS_LOW_BATTERY_VOLTAGE  
IS_LOW_TIRE_PRESSURE  

[:fast_forward: Next Section: Creating a new report configuration](/creatingNewReportConfig.md)
