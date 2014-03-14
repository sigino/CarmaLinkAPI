<h2>Summary of Reports</h2>  
The following table summarizes reports provided by the API. Taken together, they describe the complete application/operational definition of the CarmaLink available to the customer. See the following sections of this document for detailed information on how to set up (configure) each report and how to retrieve the report data.  

The **URL** field for a report gives the unique part of the API resource name that is used to reference the configuration of the report, and also that report's output data.  
  
When the **Allowance** field for a report is checked (✓), it means that the report can be configured with a time allowance to filter out events of too-short duration. Otherwise, no allowance is supported or allowed for the report configuration.  
  
When the **Threshold** field for a report is checked (✓), it means that the report must be configured with a valid value that is used in evaluating the report's start condition. Otherwise, no threshold is supported or allowed for the report configuration.  
  
When the **Location** field for a report is checked (✓), it means that the report must be configured with a true/false flag that determines whether or not GPS-provided location data is included in this report's data.  

When the **Buzzer** field for a report is checked (✓), it means that an additional configuration option exists that, when enabled, causes the CarmaLink to generate audible warning sounds in the vehicle while the report is activated.  

When the **Optional Parameters** field for a report is checked (✓), it means that the report can be configured with a set of strings that determines which additional parameters are included in this report's data.  

**"Engine Overspeed" Report**  
URL: `/engine_overspeed`  
Allowance: ✓  
Threshold: ✓  
Location: ✓  
Optional Parameters: ✓  
Buzzer: High/low two note (5 sec gap)  
Trigger (Activation Condition): Engine speed exceeds specified threshold  
Notes: Sent at the beginning and end of the event.  

**"Hard Acceleration" Report**  
URL: `/hard_accel`  
Allowance: ✓  
Threshold: ✓  
Location: ✓  
Optional Parameters: ✓  
Buzzer: Three rising notes  
Trigger (Activation Condition): Vehicle acceleration exceeds specified threshold  
Notes: Sent at the end of the event (once hard acceleration has ended); threshold must be a positive number.  
  
**"Hard Braking" Report**  
URL: `/hard_braking`  
Allowance: ✓  
Threshold: ✓  
Location: ✓  
Optional Parameters: ✓  
Buzzer: Three falling notes  
Trigger (Activation Condition): Vehicle deceleration exceeds specified threshold  
Notes: Sent at the end of the event (once hard acceleration has ended); "deceleration" is really just negative acceleration, and so the threshold must be a negative number. For example if the threshold is -2.0 m/s<sup>2</sup>, then if the CarmaLink detects a vehicle acceleration of -2.5 m/s<sup>2</sup>, the report will be triggered.  
  
**"Hard Cornering" Report**  
URL: `/hard_cornering`  
Allowance: ✓  
Threshold: ✓  
Location: ✓  
Optional Parameters: ✓  
Buzzer: Hi/low two note (0 sec gap)  
Trigger (Activation Condition): Vehicle lateral acceleration exceeds specified threshold  
Notes: Sent at the end of the event; threshold must be a positive number.  
  
**"Idling" Report**  
URL: `/idling`  
Allowance: ✓  
Threshold: ∅  
Location: ✓  
Optional Parameters: ✓  
Buzzer: Freefall down notes (5 sec gap)  
Trigger (Activation Condition): Vehicle engine is on, but the speed is zero  
Notes: Sent at the end of the event.  

**"New Deployment" Report**  
URL: `/new_deployment`  
Allowance: ∅  
Threshold: ∅  
Location: ∅  
Optional Parameters: ∅  
Buzzer: ∅  
Trigger (Activation Condition): CarmaLink is either plugged into a vehicle or first communicates with a vehicle's ECU (typically when the engine is turned on; usually the VIN is not available prior to this)  
Notes: CarmaLink functionality is sometimes limited by the capabilities of the vehicle's ECU. Whenever a CarmaLink is plugged into a vehicle it must assess the ECU's capabilities as provided via OBD-II.  
  
**"Overspeeding" Report**  
URL: `/overspeeding`  
Allowance: ✓  
Threshold: ✓  
Location: ✓  
Optional Parameters: ✓  
Buzzer: High/low two note (5 sec gap)  
Trigger (Activation Condition): Vehicle speed exceeds specified threshold  
Notes: Sent at the end of the event; threshold must be a positive number.  

**"Parking" Report**  
URL: `/parking`  
Allowance: ∅  
Threshold: ✓  
Location: ✓  
Optional Parameters: ✓  
Buzzer: ∅  
Trigger (Activation Condition): Vehicle is off  
Notes: Periodically sent while the vehicle is parked, and once when the vehicle transitions from off to on. The reporting period is specified by the customer using the Threshold. The minimum allowed reporting interval is 6 hours (21600000ms).  
  
**"Parking Brake Drag" Report**  
URL: `/parking_brake`  
Allowance: ✓  
Threshold: ✓  
Location: ✓  
Optional Parameters: ✓  
Buzzer: Hi/low two note (3 sec gap)  
Trigger (Activation Condition): Vehicle speed exceeds specified threshold while parking brake is engaged  
Notes: Sent at the end of the event.  
  
**"Seatbelt Not In Use" Report**  
URL: `/seatbelt`  
Allowance: ✓  
Threshold: ✓  
Location: ✓  
Optional Parameters: ✓  
Buzzer: Hi/low two note (3 sec gap)  
Trigger (Activation Condition): Vehicle speed exceeds specified threshold while seatbelt is unbuckled  
Notes: Sent at the end of event.  
  
**"Status" Report**  
URL: `/status`  
Allowance: ∅  
Threshold: ✓  
Location: ✓  
Optional Parameters: ✓  
Buzzer: ∅  
Trigger (Activation Condition): Occurs on a periodic basis while the vehicle is on; reports status data  
Notes: A snapshot of certain vehicle and CarmaLink data; the reporting period is specified by the customer using the Threshold. The minimum allowed reporting interval is 5 seconds (5000ms).  
  
**"Trip Summary" Report**  
URL: `/trip_report`  
Allowance: ∅  
Threshold: ∅  
Location: ✓  
Optional Parameters: ✓  
Buzzer: ∅  
Trigger (Activation Condition): Trip begins when vehicle engine state changes from off to on, and ends when engine state returns to off  
Notes: Sent at both the beginning and end of the trip. The end-of-trip report will include total distance traveled, fuel consumed, and average battery voltage.  
  
**"Vehicle Health" Report**  
URL: `/vehicle_health`  
Allowance: ∅  
Threshold: ∅  
Location: ✓  
Optional Parameters: ✓  
Buzzer: ∅  
Trigger (Activation Condition): Sent when the DTC string changes values or if any of the optional conditions are triggered  
Notes: The duration for this report is not meaningful.  

<h3>Optional Parameters</h3>  
These parameters can be added to any report and will return additional information.  

EMISSION_MONITORS  
FUEL_LEVEL  
ODOMETER  
DURATION_TO_SERVICE  
DISTANCE_TO_SERVICE  
IS_LOW_TIRE_PRESSURE  
IS_LOW_BATTERY_VOLTAGE  
BATTERY_VOLTAGE
   
[Next Section: Authentication & Permissions](https://github.com/CarmaSys/CarmaLinkAPI-unstable/blob/1.6/authenticationAndPermissions.md)
