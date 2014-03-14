<h2>4. Report Data</h2>  
The application retrieves vehicle report data using the following methods.  
  
* All methods in this section are formed off the base URI `/v1/[serial]/data`, using the GET HTTP method  
* The success code is 200 (OK)  
* Response data is formatted as JSON  
* Response data is returned in reverse chronological order (most recent data first)  
* In the case that a CarmaLink is not found for a given serial number, an error response will be returned  
  
**"All Activity" Report**  
URL: `/all_activity`  
Response Body: `All Activity Report`  

**"Engine Overspeed" Report**  
URL: `/engine_overspeed`  
Response Body: `List<Engine Overspeed Report>`  

**"Hard Acceleration" Report**  
URL: `/hard_accel`  
Response Body: `List<Hard Acceleration Report>`  
  
**"Hard Braking" Report**  
URL: `/hard_braking`  
Response Body: `List<Hard Braking Report>`  
  
**"Hard Cornering" Report**  
URL: `/hard_cornering`  
Response Body: `List<Hard Cornering Report>`  
  
**"Idling" Report**  
URL: `/idling`  
Response Body: `List<Idling Report>` 

**"Overspeeding" Report**  
URL: `/overspeeding`   
Response Body: `List<Overspeeding Report>`  

**"Parking" Report**  
URL: `/parking`   
Response Body: `List<Parking Report>`  
  
**"Parking Brake Drag" Report**  
URL: `/parking_brake`   
Response Body: `List<Parking Brake Drag Report>`  

**"Seatbelt Not In Use" Report**  
URL: `/seatbelt`   
Response Body: `List<Seatbelt Not Used Report>`  
  
**"Trip Summary" Report**  
URL: `/trip_report`   
Response Body: `List<Trip Summary Report>`  
  
**"Vehicle Health" Report**  
URL: `/vehicle_health`   
Response Body: `List<Vehicle Health Report>`  
  
**"Status" Report**  
URL: `/status`   
Response Body: `List<Status Report>`  
  
**"New Deployment" Report**  
URL: `/new_deployment`   
Response Body: `List<New Deployment>`  
  
### Filtering  
In addition to the required authentication query parameters, these methods accept four optional query parameters as explained below. These parameters can be used to specify the range of data queried, with the exception of all_activity, which ignores ’limit’ and ’offset’ parameters.  
  
`since=<timestamp_millis>` limit before which no older data should be returned (default is 0)  
  
`before=<timestamp_millis>` limit after which no newer data should be returned - useful for paging (default is current time)  
  
`offset=<integer>` numeric offset from which to start returning data (default is 0, max is 100)  
  
`limit=<integer>` limit to the number of results to return (default is 50, max is 250)   
    
[Next Section: Using the "All Activity" Report](https://github.com/CarmaSys/CarmaLinkAPI-unstable/blob/1.6/usingTheAllActivityReport.md)
