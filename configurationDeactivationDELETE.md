<h2>Configuration Deactivation - DELETE</h2>  
Users may deactivate configurations they no longer want to have running using the HTTP DELETE method on the respective resource. Contrary to the standard implications of this method, it does not actually delete any data on the server. If you want to disable the buzzer for the configuration, see Buzzer Configuration. Once the CarmaLink has acknowledged the configuration deactivation request, it will no longer send data reports of that type and the buzzer will likewise no longer respond to events related to the deactivated configuration.  

**"Engine Overspeed" Report**  
URL: `/engine_overspeed`  

**"Hard Acceleration" Report**  
URL: `/hard_accel`  

**"Hard Braking" Report**  
URL: `/hard_braking`  

**"Hard Cornering" Report**  
URL: `/hard_cornering`  

**"Status" Report**  
URL: `/status`  

**"Idling" Report**  
URL: `/idling`  

**"Overspeeding" Report**  
URL: `/overspeeding`  

**"Parking" Report**  
URL: `/parking`  

**"Parking Brake Drag" Report**  
URL: `/parking_brake`  

**"Seatbelt Not In Use" Report**  
URL: `/seatbelt`  

**"Trip Report" Report**  
URL: `/trip_report`  

**"Vehicle Health" Report**  
URL: `/vehicle_health`  

  
### Deactivate Response  
Successful deactivation requests will return an HTTP status code 204. If a resource is already deactivated, an HTTP 404 response will be returned instead.  
  
After performing a successful deactivation request on a resource, GET requests to that resource will also return HTTP 404. However, clients may still retrieve a given configuration record by specifying a configuration id as a query parameter, which will return the record with all its properties as described above.  

[Next Section: Report Data](https://github.com/CarmaSys/CarmaLinkAPI/blob/1.6/reportData.md)
