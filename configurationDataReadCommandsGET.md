<h2>Configuration Data Read Commands - GET</h2>  
Report configurations are retrieved by issuing a series of GET commands to the API.  
  
* All GET methods accept an additional, optional query parameter, `id={configId}` specifying a specific config id to return. When not provided, the CarmaLink's most recent report configuration is returned  
* All of the GET methods accept the content type application/json  
* The success code is 200 (OK)  
  
**Hard Acceleration Report**  
URL: `/hard_accel`  
Description: Get configuration of current (or previous) hard acceleration report  
  
**Hard Braking Report**  
URL: `/hard_braking`  
Description: Get configuration of current (or previous) hard braking report  
  
**Hard Cornering Report**  
URL: `/hard_cornering`  
Description: Get configuration of current (or previous) hard cornering report  
  
**Status Report**  
URL: `/status`  
Description: Get configuration of current (or previous) status report  
  
**Idling Report**  
URL: `/idling`  
Description: Get configuration of current (or previous) idling report  
  
**Overspeeding Report**  
URL: `/overspeeding`  
Description: Get configuration of current (or previous) overspeeding report  
  
**Parking Brake Drag Report**  
URL: `/parking_brake`  
Description: Get configuration of current (or previous) parking brake drag report  
  
**Seatbelt Not In Use Report**  
URL: `/seatbelt`  
Description: Get configuration of current (or previous) seatbelt not in use report  
  
**Trip Report**  
URL: `/trip_report`  
Description: Get configuration of current (or previous) trip report  
  
**Vehicle Health Report**  
URL: `/vehicle_health`  
Description: Get configuration of current (or previous) vehicle health report  
  
  
### Read Result Data - The Configuration View Structure  
Data returned to the API in response to a report configuration GET is JSON-encoded and in a format called the Configuration View. It includes:  
* The Configuration ID is an identification number for the configuration value with respect to its associated serial number.  Config ID is not a global variable.  
* The Configuration Status of this configuration  
* The content that was provided in the the Configuration Update data sent with this configuration's SET command.  
  
**Usage Example**  
```text
GET https://api.carmalink.com:8282/v1/[serial]/report_config/overspeeding/
```
   
_Response:_  
```javascript
{  
  "configId" : 53  
  "status" : "ACTIVATED",  
  "threshold" : 160,  
  "allowance" : 5000,  
  "buzzer" : "HIGH",  
  "location" : true  
}
```
  
[Next Section: Configuration Deactivation - DELETE](https://github.com/CarmaSys/CarmaLinkAPI/wiki/Configuration-Deactivation-DELETE)  
