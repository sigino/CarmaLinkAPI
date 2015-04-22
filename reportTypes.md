## Report types  
This section includes descriptions of each type of report.  

--
### Engine Overspeed  
The Engine Overspeed report is used to identify when a vehicle's engine has gone over the configured threshold.  

<b>Dispatch</b>  
This report is sent both at the start and end of the event.  

<b>Parameters</b>  
Beyond the standard report parameters, the following fields are always included in this type of report:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|-------------
In progress	| inProgress | Boolean | true or false | Identifies if the event is just starting (true) or just ending (false) as of the reportTimestamp.
Maximum engine speed | maxEngineSpeed | Float | RPM | Identifies the maximum RPM over the course of the event. This is really only useful when inProgress is 'false' (Overspeeding just ended).  
--
 
### Hard Acceleration  
The Hard Acceleration report identifies when a vehicle's forward acceleration (positive) is greater than the configured threshold.  

<b>Dispatch</b>  
This report is sent at the end of the Hard Acceleration event.  

<b>Parameters</b>  
Beyond the standard report parameters, the following fields are always included in this type of report:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Maximum acceleration | maxAcceleration | Float | meters/sec^2 | Identifies the maximum forward acceleration over the course of the event.  
--

### Hard Braking  
The Hard Braking report identifies when a vehicle's forward deceleration (negative) is less than the configured threshold.  

<b>Dispatch</b>  
This report is sent at the end of the Hard Braking event.  

<b>Parameters</b>  
Beyond the standard report parameters, the following fields are always included in this type of report:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Minimum acceleration | minAcceleration | Float | meters/sec^2 | Identifies the minimum (negative) acceleration over the course of the event.
--

### Hard Cornering  
The Hard Cornering report identifies when a vehicle's lateral acceleration is over the configured threshold.  

<b>Dispatch</b>  
This report is sent at the end of the Hard Cornering event.  

<b>Parameters</b>  
Beyond the standard report parameters, the following fields are always included in this type of report:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Direction | direction | String | "LEFT" or "RIGHT" | Identifies which direction the vehicle was turning during the event.
Maximum acceleration | maxAcceleration | Float | meters/sec^2 | Identifies the maximum (positive) acceleration over the course of the event.  
--

### Idling  
The Idling report identifies time and fuel used idling the engine.  

<b>Dispatch</b>  
This report is sent at the end of the idling event.  

<b>Parameters</b>  
Beyond the standard report parameters, the following fields are always included in this type of report:  

Field | JSON name | Value type | Units 
------|-----------|------------|-------
Fuel consumed | fuelConsumed | Float | liters  
--

### Overspeeding
