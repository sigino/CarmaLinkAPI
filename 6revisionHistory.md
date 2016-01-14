## 6. Revision History  

### Summary of changes since v1.1 
* Changed /device_status to /status in URLs.  
* Removed /devices/ from all URLs as it's unnecessary.  
* Updated document for consistency, all urls in examples pointing towards https://api.carmalink.com:8282  
* Removed the apiKey from URL as it's not up to date with OAuth 1.0a method we currently use (https://api.carmalink.com:8282/v1/devices/apiKey/deviceNum)  
* Added description of location sub-object which is returned in some report views  

### Summary of changes since v1.2  
* Updated default and max limits for records returned by data queries.  
* Added support for buzzer on idling.  
* Added support for odometer reading in trip reports & terminology.  
* Added support for time and distance to next service in trip reports & terminology.  
* Changed "v[version]" to "v1" for consistency.  
* Changed "params" field in configuration object to "optionalParams"  

### Summary of changes since v1.3  
* Added Parking Brake report for BMW, Mini, Ford, Mazda, Volvo, Jaguar, Land Rover and vehicles  
* Added Seatbelt report for BMW, Mini, Ford, Mazda, Jaguar, Land Rover and vehicles  
* Added Vehicle Health report that includes MIL and TPMS (for BMW, Mini, Ford, Mazda, Jaguar, Land Rover and vehicles)  
* Added Hard Cornering report  
* Expanded odometer support for Mazda, Volvo, Jaguar, Land Rover and vehicles  
* Expanded duration/distance to service support for Mini vehicles  
* Deprecated Engine Fault report  

### Summary of changes since [v1.4](https://github.com/CarmaSys/CarmaLinkAPI/tree/1.4") 
* Expanded support for optional parameters to all reports except New Deployment  
* Added description of new "optionalParams" object  
* Removed odometer, duration to service, and distance to service as possible fields in trip report: these are now in the "optionalParams" object  
* Added support for fuel level as an optional parameter  
* Added support for emission monitor status as an optional parameter  
* Added support for emission monitor status as an optional condition on the Vehicle Health Report  

### Summary of changes since v1.5  
* Added support for 'Is Low Battery Voltage' as an optional parameter  
* Added support for 'Is Low Battery Voltage' as an optional condition on the 'Vehicle Health' report  
* Added support for 'Is Low Tire Pressure' as an optional parameter  
* Added support for 'Is Low Tire Pressure' as an optional condition on the 'Vehicle Health' report  
* Added support for 'Battery Voltage' as an optional parameter  
* Removed "tirePressureLow" field in Vehicle Health report: to include this data, add 'Is Low Tire Pressure' as an optional parameter when configuring the Vehicle Health report  
* Removed "vehicleVoltage" field in the Status report: to include this data, add 'Battery Voltage' as an optional parameter when configuring the Status report  
* Changed "voltage" field in Trip Report to "averageBatteryVoltage" to eliminate confusion regarding this parameter  
* Added 'Engine Overspeed' report  
* Added 'Parking' report  

### Summary of changes since v1.6  
* Added support for 'FuelRate' as an optional parameter  
* Added 'Transported' report  
* Added 'gpsTimestamp' to the location object  
* Deprecated 'All Activity' and 'Parking Brake' reports  
* Changed engine configuration URI  

### Summary of changes since v1.7  
* Added "inProgress" and "cellSignalStrength" as standard parameters in all configurable reports; replaces "gsmSignalStrength" in the Status report  
* Added "distance" and "fuelConsumed" to the Status report  
* Parking reports are now sent on event start  
* Add "Report generation" section to clarify how/when reports are created  
 

[:fast_forward: Next Section: 7. Referenced documents & standards](/7referencedDocStand.md)
