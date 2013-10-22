Report configurations are created or updated by issuing a series of PUT commands to the API.  
  
*All of these PUT methods accept the content type application/json  
*The success code is 204 (No Content)    
*If a rejected field is added to a request, the request will fail with error code 400  
  
**Hard Acceleration Report**  
URL: `/hard_accel`  
Allowance: allowed  
Threshold: > 0  
Location: true/false  
Buzzer: high/medium/off  
OptionalConditions: N/A  
OptionalParams: N/A  
Description: Reports hard acceleration above a given threshold, in Gs  
  
**Hard Braking Report**  
URL: `/hard_braking`  
Allowance: allowed  
Threshold: < 0  
Location: true/false  
Buzzer: high/medium/off  
OptionalConditions: N/A  
OptionalParams: N/A  
Description: Reports hard braking below a given (negative) threshold, in Gs  
  
**Hard Cornering Report**  
URL: `/hard_cornering`  
Allowance: allowed  
Threshold: > 0  
Location: true/false  
Buzzer: high/medium/off  
OptionalConditions: N/A  
OptionalParams: N/A  
Description: Reports hard cornering above a given threshold. The maximum acceleration recorded is returned as well as a direction, RIGHT or LEFT  
  
**Status Report**  
URL: `/status`  
Allowance: rejected  
Threshold: ≥ 5000  
Location: true/false  
Buzzer: rejected  
OptionalConditions: N/A  
OptionalParams: N/A  
Description: Reports Status periodically while the vehicle is on  
  
**Idling Report**  
URL: `/idling`  
Allowance: ≥ 5000  
Threshold: rejected  
Location: true/false  
Buzzer: high/medium/off  
OptionalConditions: N/A  
OptionalParams: N/A  
Description: Reports idling events past a given time allowance  
  
**Overspeeding Report**  
URL: `/overspeeding`  
Allowance: allowed  
Threshold: > 0  
Location: true/false  
Buzzer: high/medium/off  
OptionalConditions: N/A  
OptionalParams: N/A  
Description: Reports overspeeding - The query string ’units=mph’ can be used to specify the threshold as MPH   
 
**Parking Brake Drag Report**  
URL: `/parking_brake`  
Allowance: allowed  
Threshold: > 0  
Location: true/false  
Buzzer: high/medium/off  
OptionalConditions: N/A  
OptionalParams: N/A  
Description: Reports overspeeding - Reports occurrences of driving while the parking brake is engaged.  
  
**Seatbelt Not In Use Report**  
URL: `/seatbelt`  
Allowance: allowed  
Threshold: > 0  
Location: true/false  
Buzzer: high/medium/off  
OptionalConditions: N/A  
OptionalParams: N/A  
Description: Reports occurrences of driving without wearing a seatbelt.    
  
**Trip Report**  
URL: `/trip_report`  
Allowance: rejected  
Threshold: rejected  
Location: true/false  
Buzzer: rejected  
OptionalConditions: N/A  
OptionalParams: ODOMETER,  
DURATION_TO_SERVICE,  
DISTANCE_TO_SERVICE  
Description: Sent at the beginning and end of a trip. Location at the beginning of a trip may not be accurate.  
  
**Vehicle Health Report**  
URL: `/vehicle_health`  
Allowance: rejected  
Threshold: rejected  
Location: true/false  
Buzzer: rejected  
OptionalConditions: TIRE_PRESSURE_CHANGE  
OptionalParams: ODOMETER,  
DURATION_TO_SERVICE,  
DISTANCE_TO_SERVICE  
Description: Sent when there is a change in state of the MIL or any of the optional conditions.  
  
### Configuration Data Content - The Configuration Update Structure  
The allowance, threshold, and location flag for a report configuration PUT command are delivered in the JSON-encoded content of the message. This data type is named Configuration Update and is defined as follows.  
  
**! Not all configuration update fields are used by all PUT commands. Unused fields have a value of null.**  
  
**Allowance**  
JSON Name: allowance  
Value: number of milliseconds, > 0  
Description: The allowance specifies a duration before an event is considered to have occurred.  For example, if a report dictates an allowance of 1000ms, the report condition must remain true for greater than that time, otherwise the event will not be reported.  This also means that the event start time in the report is offset by the value of the allowance.  So for an allowance of 1000ms, the real start time is n-1000ms.  
  
**Threshold**  
JSON Name: threshold  
Value: specific to each report configuration  
Description: Specifies a value that is the trigger for the report to begin. In overspeeding, for example, the threshold is the speed that vehicle must exceed for the report to occur.  
  
**Location**  
JSON Name: location  
Value: true or false  
Description: Specifies whether location information should be included in the generated report.  
  
**Buzzer**  
JSON Name: buzzer  
Value: "OFF","MEDIUM" or "HIGH"  
Description: Specifies the volume of the CarmaLink's buzzer when the event is triggered. Can be turned off with "OFF."  
  
**Optional Params**  
JSON Name: optionalParams  
Value: additional properties to return and specific to each report configuration  
Description: This field can contain a list of strings to optionally add extra parameters to a report. The parameters allowed are specific to each report.  
  
**Optional Conditions**  
JSON Name: optionalConditions  
Value: additional conditions to trigger a report  
Description: This field can contain a list of strings to include optional report trigger conditions. The conditions allowed are specific to each report.  
  
  
### Usage Example  
    PUT https://api.carmalink.com:8282/v1/[serial]/report_config/overspeeding/  
  
```javascript
{  
  "threshold" : 160,  
  "allowance" : 5000,  
  "location" : true,  
  "buzzer" : "HIGH",  
  "optionalParams" : ["ODOMETER", "DURATION_TO_SERVICE"],  
  "optionalConditions" : ["TIRE_PRESSURE_CHANGE"]  
 }
```
    
### Configuration Status Structure (From Command to Activation)  
When the API is used to send a new report configuration for a CarmaLink to the server, that configuration cannot immediately take effect on the CarmaLink. There is a period of time during which the existing configuration on the CarmaLink continues to be in effect, until the next time the CarmaLink connects to the server and receives the new configuration. This happens, at minimum, at the rate specified by the (current configuration of the) Status report, though in general the CarmaLink connects to the server anytime there is new report data ready to be uploaded. A given report configuration thus has four possible statuses:  
* Pending Activation: configuration has been received by the server via API call, but has not yet been sent down to the CarmaLink
* Activated: configuration has been sent down to the CarmaLink and is now being used  
* Pending Deactivation: the configuration is the one being used by the CarmaLink, but a newer one has been   received by the server, and this one will be deactivated the next time the CarmaLink checks in with the server.  
* Deactivated: configuration is no longer being used by the CarmaLink; it has been replaced by a more recent one.  
Each report configuration has its own configuration status. As will be shown in the next section, once a PUT command has been used to send a report configuration, a corresponding GET command can be used to check its status.  
  
Configuration Status: **ACTIVATED**  
Description: The CarmaLink is up to date with the latest configuration  
  
Configuration Status: **PENDING_ACTIVATION**  
Description: The CarmaLink hasn't updated to the latest configuration, but the API has the information  
  
Configuration Status: **DEACTIVATED**  
Description: The CarmaLink is up to date with the latest configuration  
  
Configuration Status: **PENDING_DEACTIVATION**  
Description: The CarmaLink hasn't updated to the latest configuration, but the API has the information  
  
### Code Example  
    enum { PENDING_ACTIVATION, ACTIVATED, PENDING_DEACTIVATION, DEACTIVATED }   
  
### configId (Keeping Track of Report Configurations)  
The server assigns a unique ID number, called the Configuration ID, to each new report configuration it receives through the API. As will be shown in the next section, the GET commands used to check configuration statuses include this ID in the data returned. Since most customer applications will benefit from having this ID number; it is recommended practice that once a PUT command is sent with a new report configuration, it should be followed with a matching GET command to retrieve the ID assigned to the configuration.   
  
Perhaps even more importantly, when report data generated by the CarmaLink is retrieved from the server using the API, this data includes the Configuration ID of the configuration that was in effect when the report was generated. This matters, for example, if the customer decides to change the threshold for the overspeeding report. The next time an overspeeding report is received, how does the customer know which threshold setting was in effect for this report? The Configuration ID in the report data is the key.  
  
[Next Section: Configuration Data Read Commands - GET](https://github.com/CarmaSys/CarmaLinkAPI/wiki/Configuration-Data-Read-Commands---GET)
