## Report types  
This section includes descriptions of each type of report.  

--
### Engine Overspeed  
The Engine Overspeed event starts when a vehicle's engine speed (RPM) has gone over the configured threshold, and ends when it falls under the threshold.  

A report is generated at event start and event end. Beyond the standard report parameters, the following fields are included in this type of report when available:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|-------------
Maximum engine speed	| maxEngineSpeed | Float | RPM | Identifies the maximum RPM over the course of the event. This is really only useful when inProgress is 'false' (Overspeeding just ended).    

--
### Hard Acceleration  
The Hard Acceleration event starts when a vehicle's forward acceleration (positive) is greater than the configured threshold, and ends when it falls under the threshold.  

A report is generated at event end. Beyond the standard report parameters, the following fields are included in this type of report when available:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Maximum acceleration | maxAcceleration | Float | meters/sec^2 | Identifies the maximum forward acceleration over the course of the event.  

--
### Hard Braking  
A Hard Braking event starts when a vehicle's forward deceleration (negative) is less than the configured threshold, and ends when it rises above the threshold.  

A report is generated at event end. Beyond the standard report parameters, the following fields are included in this type of report when available:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Minimum acceleration | minAcceleration | Float | meters/sec^2 | Identifies the minimum (negative) acceleration over the course of the event.

--
### Hard Cornering  
The Hard Cornering event occurs when a vehicle's lateral acceleration is over the configured threshold.  

A report is generated at event end. Beyond the standard report parameters, the following fields are included in this type of report when available:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Direction | direction | String | "LEFT" or "RIGHT" | Identifies which direction the vehicle was turning during the event.
Maximum acceleration | maxAcceleration | Float | meters/sec^2 | Identifies the maximum (positive) acceleration over the course of the event.  

--
### Idling  
The Idling event starts when the vehicle's engine is running (RPM > 0) and the speed is 0. The Idling event ends when the engine switches off, or if the speed is greater than 0.  

A report is generated at the end of the Idling event. Beyond the standard report parameters, the following fields are included in this type of report when available:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|-----
Fuel consumed | fuelConsumed | Float | liters | Identifies the amount of fuel used during the idle event.  
--

### Overspeeding  
The Overspeeding event starts when a vehicle's speed has exceeded the configured threshold, and ends when it falls below this threshold.  

A report is generated at the end of the Overspeeding event. Beyond the standard report parameters, the following fields are included in this type of report when available:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Maximum speed |	maxSpeed	| Float | km/hr	| Identifies the maximum vehicle speed over the course of the event.  
--

### Parking  
The Parking event starts when the vehicle switches off, and ends when the vehicle switches on. This can serve as a useful 'ping' to identify battery voltage and that the transponder is still plugged in when parked for long periods.  

A report is generated at event start, periodically at the configured 'threshold' interval, and at event end. Beyond the standard report parameters, the following fields are included in this type of report when available:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Average battery voltage |	averageBatteryVoltage	| Float	| volts	| Identifies the average battery voltage since the engine switched off.
--

### PTO  
The PTO event starts when the PTO is switched on, and ends when the PTO is switched off. A report is generated on event start and on event end. There are no additional standard parameters in this report.  
  
--

### Seatbelt Unbuckled  
The Seatbelt Unbuckled event starts when the driver's seatbelt is not fastened AND the vehicle speed exceeds a configured threshold, and ends when the seatbelt is fastened OR the speed falls below the threshold.  

A report is generated at event end.  Beyond the standard report parameters, the following fields are included in this type of report when available:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Maximum speed	| maxSpeed	| Float	| km/hr	| Identifies the maximum vehicle speed over the course of the event.
--

### Status  
The Status event starts when the vehicle's combustion engine switches on (RPM > 0) or the vehicle begins moving under its own power (for hybrid or electric vehicles), and ends when combustion engine is off and the vehicle is not moving under its own power. This is the opposite of the Parking report, and at any given moment one of these events, either Status or Parking, will be true.  

A report is generated at event start, periodically at the configured 'threshold' interval, and when the event ends.  Beyond the standard report parameters, the following fields are included in this type of report when available:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Distance | distance	| Float |	km	| Identifies how far the vehicle has traveled since the engine switched on.  
Fuel consumed | fuelConsumed | Float | liters | Identifies how many liters of fuel the vehicle has consumed since the engine switched on.  
--

### Stopped  
The Stopped event starts when the vehicle speed falls to 0, and ends when the vehicle speed rises above 0. With an appropriate allowance (typically 90-120 seconds), this report can be helpful to identify each location a vehicle stopped and for how long, even if the 'trip' is not considered over.  
  
A report is generated on event start and on event end. There are no additional standard parameters in this report.  
  
--

### Transported  
The Transported event starts when the vehicle begins moving while it is off, and ends when it stops moving or the vehicle switches on. This is useful to capture theft or tow events.  

A report is generated on event start, periodically at the configured 'threshold' interval, and on event end. There are no additional standard parameters in this report.  

--

### Trip Summary  
The Trip Summary event is the same as the Status event, but its reports contains some additional information.  

A report is generated on event start and event end. Beyond the standard report parameters, the following fields are included in this type of report when available:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Average battery voltage | averageBatteryVoltage | Float	| volts |	Identifies the average battery voltage since the engine switched on.
Distance	| distance | Float |	km |	Identifies how far the vehicle has traveled since the engine switched on.
Fuel consumed |	fuelConsumed	| Float	| liters |	Identifies how many liters of fuel the vehicle has consumed since the engine switched on.  
--

### Vehicle Health  
The Vehicle Health report tracks problems with the engine, emissions system, tire pressure, and/or battery. Due to the unique way this report is processed, the duration value has no meaning.  

A report is generated whenever the vehicle diagnostic trouble codes (DTCs) change, or the state of any of the optional conditions change state. Beyond the standard report parameters, the following fields are included in this type of report when available:  

Field | JSON name | Value type | Units | Description
------|-----------|------------|-------|------------
Diagnostic trouble codes | dtcs | List of strings | -	| **For light-duty vehicles**, these are the SAE J1979 (OBD-II) trouble codes. **For heavy-duty vehicles**, these are the SAE J1939 FMI/SPN codes.  

--
[:fast_forward: Next Section: **Non-configurable reports**](/nonConfigurable.md)
