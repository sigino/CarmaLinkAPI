<h2>2. Configuration</h2>  
A new CarmaLink is a bit of a blank slate: by default it only has one hard-coded report that it will generate when it is installed (the 'New Deployment' report). It's up to the API user to create a configuration for each type of event CarmaLink should be reporting on and/or activating its buzzer for.  

Once CarmaLink receives a configuration from the server it is stored in non-volatile memory so that this information is not lost between reset or power cycles.  

<h3>Defining a report configuration</h3>
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

