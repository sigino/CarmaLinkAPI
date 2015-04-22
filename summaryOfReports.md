<h2>Summary of Reports</h2>  
The following table provides a description of what types of vehicle operation the transponder can be configured to detect.  

Report Name | Trigger (Activation Condition)
------------|--------
Engine Overspeed | Engine speed (RPM) exceeds specified threshold.
Hard Acceleration | Vehicle acceleration exceeds specified threshold.  
Hard Braking | Vehicle deceleration exceeds specified threshold.  
Hard Cornering | Vehicle lateral acceleration exceeds specified threshold.  
Idling | Vehicle engine is on, but the speed is zero.  
New Deployment | CarmaLink is plugged into a vehicle. This report is always active, and not configurable.  
Overspeeding | Vehicle speed exceeds specified threshold.  
Parking | Occurs on a periodic basis while the vehicle is off.  
Seatbelt Unbuckled | Vehicle speed exceeds specified threshold while driver's seatbelt is unbuckled.  
Status | Occurs on a periodic basis while the vehicle is on.  
Transported | Occurs on a periodic basis while the vehicle is both off and moving.  
Trip Summary | Trip begins when vehicle engine state changes from off to on, and ends when engine state returns to off.  
Vehicle Health | Sent when the DTC string changes values or if any of the optional conditions are triggered.  

--
:information_source:   
All URIs mentioned in this document are relative to `https://api.carmalink.com:8282/v1/<serial>`, where `<serial>` specifies the transponder serial number(s) of interest.  

All data exchanged in the API is formatted in JSON: any HTTP request or response containing a body should have the Content-Type: application/json header.  

All requests require an Authorization header with a valid signature in order to be processed. Skip ahead to chapter 4 for more information.
