<h2>Summary of Reports</h2>  
The following list summarizes reports provided by the API. Taken together, they describe the complete application/operational definition of the CarmaLink available to the customer. See the following sections of this document for detailed information on how to set up (configure) each report and how to retrieve the report data.  

The **URL** field for a report gives the unique part of the API resource name that is used to reference the configuration of the report, and also that report's output data.  
  
When the **Allowance** field for a report is checked, it means that the report can be configured with a time allowance to filter out events of too-short duration. Otherwise, no allowance is supported or allowed for the report configuration.  
  
When the **Threshold** field for a report is checked, it means that the report must be configured with a valid value that is used in evaluating the report's start condition. Otherwise, no threshold is supported or allowed for the report configuration.  
  
When the **Location** field for a report is checked, it means that the report must be configured with a true/false flag that determines whether or not GPS-provided location data is included in this report's data.  

When the **Buzzer** field for a report is checked, it means that an additional configuration option exists that, when enabled, causes the CarmaLink to generate audible warning sounds in the vehicle while the report is activated.  

**Hard Acceleration**  
URL: `/hard_accel`  
Allowance: Yes  
Threshold: Yes  
Location: Yes  
Buzzer: Three rising notes  
Options: No  
Trigger (Activation Condition): Vehicle acceleration exceeds specified threshold  
Notes: Sent at the end of the event (once hard acceleration has ended); threshold must be a positive number.  
  
**Hard Braking**  
URL: `/hard_brake`  
Allowance: Yes  
Threshold: Yes  
Location: Yes  
Buzzer: Three falling notes  
Options: No  
Trigger (Activation Condition): Vehicle deceleration exceeds specified threshold  
Notes: Sent at the end of the event (once hard acceleration has ended); "deceleration" is really just negative acceleration, and so the threshold must be a negative number. For example if the threshold is -2.0 m/s2, then if the CarmaLink detects a vehicle acceleration of -2.5 m/s2, the report will be triggered.  
  
**Hard Cornering**  
URL: `/hard_cornering`  
Allowance: Yes  
Threshold: Yes  
Location: Yes  
Buzzer: Hi/low two note (0 sec gap)  
Options: No  
Trigger (Activation Condition): Vehicle lateral acceleration exceeds specified threshold  
Notes: Sent at the end of the event; threshold must be a positive number.  
  
**Idling**  
URL: `/idling`  
Allowance: Yes  
Threshold: No  
Location: Yes  
Buzzer: Freefall down notes (5 sec gap)  
Options: No  
Trigger (Activation Condition): Vehicle engine is on, but the speed is zero  
Notes: Sent at the end of the event.  
  
**New Deployment**  
URL: `/new_deployment`  
Allowance: No  
Threshold: No  
Location: No  
Buzzer: No  
Options: No  
Trigger (Activation Condition): CarmaLink is either plugged into a vehicle or first communicates with a vehicle's ECU (typically when the engine is turned on; usually the VIN is not available prior to this)  
Notes: CarmaLink functionality is sometimes limited by the capabilities of the vehicle's ECU. Whenever a CarmaLink is plugged into a vehicle it must assess the ECU's capabilities as provided via OBD-II.  
  
**Overspeeding**  
URL: `/overspeeding`  
Allowance: Yes  
Threshold: Yes  
Location: Yes  
Buzzer: High/low two note (5 sec gap)  
Options: No  
Trigger (Activation Condition): Vehicle speed exceeds specified threshold  
Notes: Sent at the end of the event; threshold must be a positive number.  
  
**Parking Brake Drag**  
URL: `/parking_brake`  
Allowance: Yes  
Threshold: Yes  
Location: Yes  
Buzzer: High/low two note (3 sec gap)  
Options: No  
Trigger (Activation Condition): Vehicle speed exceeds specified threshold while parking brake is engaged  
Notes: Sent at the end of event.  
  
**Seatbelt Not In Use**  
URL: `/seatbelt`  
Allowance: Yes  
Threshold: Yes  
Location: Yes  
Buzzer: Hi/low two note (3 sec gap)  
Options: No  
Trigger (Activation Condition): Vehicle speed exceeds specified threshold while seatbelt is unbuckled  
Notes: Sent at the end of event.  
  
**Status**  
URL: `/status`  
Allowance: No  
Threshold: Yes  
Location: Yes  
Buzzer: No  
Options: No  
Trigger (Activation Condition): Occurs on a periodic basis while the vehicle is on; reports status data  
Notes: A snapshot of certain vehicle and CarmaLink data; the reporting period is specified by the customer using the Threshold.  
  
**Trip Summary**  
URL: `/trip_report`  
Allowance: No  
Threshold: No  
Location: Yes  
Buzzer: No  
Options: OptionalParameters: ODOMETER, DURATION_TO_SERVICE, DISTANCE_TO_SERVICE  
Trigger (Activation Condition): Trip begins when vehicle engine state changes from off to on, and ends when engine state returns to off  
Notes: Sent at both the beginning and end of the trip. The end-of-trip report will include total distance traveled, fuel consumed, average battery voltage and the final odometer reading in Km (if supported).  
  
**Vehicle Health**  
URL: `/vehicle_health`  
Allowance: No  
Threshold: No  
Location: Yes  
Buzzer: No  
Options: OptionalConditions: TIRE_PRESSURE_CHANGE
OptionalParameters: ODOMETER, DURATION_TO_SERVICE, DISTANCE_TO_SERVICE  
Trigger (Activation Condition): Sends the DTCs when the check engine light is illuminated or if any of the optional conditions are triggered. Returns check engine light status and tire pressure status (if available).  
Notes: Sent at the beginning and end of the event.  
  
[Next Section: Authentication & Permissions](https://github.com/CarmaSys/CarmaLinkAPI/blob/1.4/Authentication_and_Permissions.md)
