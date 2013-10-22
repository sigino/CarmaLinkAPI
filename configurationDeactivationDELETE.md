<h2>Configuration Deactivation - DELETE</h2>  
Users may deactivate configurations they no longer want to have running using the HTTP DELETE method on the respective resource. Contrary to the standard implications of this method, it does not actually delete any data on the server. If you want to disable the buzzer for the configuration, see Buzzer Configuration.  Once the CarmaLink has acknowledged the configuration deactivation request, it will no longer send data reports of that type and the buzzer will likewise no longer respond to events related to the deactivated configuration.  
  
**Hard Acceleration Report**  
URL: `/hard_accel`  
Description: Deactivate hard acceleration report  
  
**Hard Braking Report**  
URL: `/hard_braking`  
Description: Deactivate hard braking report  
  
**Hard Cornering Report**  
URL: `/hard_cornering`  
Description: Deactivate hard cornering report  
  
**Status Report**  
URL: `/status`  
Description: Deactivate status report  
  
**Idling Report**  
URL: `/idling`  
Description: Deactivate idling report  
  
**Overspeeding Report**  
URL: `/overspeeding`  
Description: Deactivate overspeeding report  
  
**Parking Brake Drag Report**  
URL: `/parking_brake`  
Description: Deactivate parking brake drag report  
  
**Seatbelt Not In Use Report**  
URL: `/seatbelt`  
Description: Deactivate seatbelt not in use report    
  
**Trip Report**  
URL: `/trip_report`  
Description: Deactivate trip report  
  
**Vehicle Health Report**  
URL: `/vehicle_health`  
Description: Deactivate vehicle health report  
  
  
### Deactivate Response  
Successful deactivation requests will return an HTTP status code 204. If a resource is already deactivated, an HTTP 404 response will be returned instead.  
  
After performing a successful deactivation request on a resource, GET requests to that resource will also return HTTP 404. However, clients may still retrieve a given configuration record by specifying a configuration id as a query parameter, which will return the record with all its properties as described above.  

[Next Section: Report Data](https://github.com/CarmaSys/CarmaLinkAPI/blob/1.4/ReportData.md)
