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
The Overspeeding report captures instances when a vehicle's speed has exceeded a configured threshold.  

<b>Dispatch</b>  
This report is sent when the vehicle speed has fallen below the configured threshold.  

<b>Parameters</b>  
Beyond the standard report parameters, the following fields are always included in this type of report:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Maximum speed |	maxSpeed	| Float | km/hr	| Identifies the maximum vehicle speed over the course of the event.  
--

### Parking  
The Parking report is sent while the vehicle is off. This can serve as a useful 'ping' to identify battery voltage and that the device is still plugged in when parked for long periods.  

<b>Dispatch</b>  
This report is sent periodically while the vehicle's engine is off at an interval defined by this report's 'threshold', and once when the engine transitions from 'off' to 'on'.  

<b>Parameters</b>  
Beyond the standard report parameters, the following fields are always included in this type of report:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Average battery voltage |	averageBatteryVoltage	| Float	| volts	| Identifies the average battery voltage since the engine switched off.
In progress	| inProgress	| Boolean	| true or false	| Identifies if the engine is still off (true) or just switched from off to on (false) as of the reportTimestamp.  
--

### Seatbelt Unbuckled  
The Seatbelt Unbuckled report identifies when the driver's seatbelt is not fastened and the vehicle speed exceeds a configured threshold.  

<b>Dispatch</b>  
This report is sent when the event is over: either the seatbelt is fastened, or the vehicle speed falls below the configured threshold.  

<b>Parameters</b>  
Beyond the standard report parameters, the following fields are always included in this type of report:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Maximum speed	| maxSpeed	| Float	| km/hr	| Identifies the maximum vehicle speed over the course of the event.
--

### Status  
The Status report is sent while the engine is running.  

<b>Dispatch</b>  
This report is sent when the vehicle's engine transitions from 'off' to 'on', and periodically while the engine is running, at an interval defined by this report's 'threshold'.  

<b>Parameters</b>  
Beyond the standard report parameters, the following fields are always included in this type of report:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Cellular signal strength | gsmSignalStrength	| Float |	dBm	| Received signal strength indication (RSSI) for the local cellular network.  
--

### Transported  
The Transported report captures vehicle movement when the engine is not running. For example, if the vehicle is stolen or being towed.  

<b>Dispatch</b>  
Reports are generated when the vehicle first begins moving, periodically at the configured interval, and finally once when the vehicle stops moving.  

<b>Parameters</b>  
Beyond the standard report parameters, the following fields are always included in this type of report:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
In progress |	inProgress | Boolean | true or false | Identifies if the vehicle is still moving (true) or just stopped moving (false) as of the reportTimestamp.
--

### Trip Summary  
The Trip Summary report provides data calculated during the duration of a trip.  

<b>Dispatch</b>  
Reports are generated when the trip starts (engine switches from 'off' to 'on') and when the trip stops (engine switches from 'on' to 'off').  

<b>Parameters</b>  
Beyond the standard report parameters, the following fields are always included in this type of report:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Average battery voltage | averageBatteryVoltage | Float	| volts |	Identifies the average battery voltage since the engine switched on.
Distance	| distance |	Float |	km |	Identifies how far the vehicle has traveled since the engine switched on.
Fuel consumed |	fuelConsumed	| Float	| liters |	Identifies how many liters of fuel the vehicle has consumed since the engine switched on.
In progress |	inProgress |	Boolean |	true or false |	Identifies if the engine is still running as of the reportTimestamp.  
--

### Vehicle Health  
The Vehicle Health report tracks problems with the engine, emissions system, tire pressure, and/or battery. Due to the unique way this report is processed, the duration value has no meaning.  

<b>Dispatch</b>  
Reports are generated whenever the number of diagnostic trouble codes (DTCs) changes, or the state of any of the optional conditions change.  

<b>Parameters</b>  
Beyond the standard report parameters, the following fields are always included in this type of report:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Diagnostic trouble codes | dtcs | List of strings | -	| **For light-duty vehicles**, these are the SAE J1979 (OBD-II) trouble codes. **For heavy-duty vehicles**, these are the SAE J1939 FMI/SPN codes.
