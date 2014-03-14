<h2>Units</h2>  
All data from the API is in SI units by default. In certain cases as described in this document, a query field can be included in a web request to specify alternate (International) units.  

**Acceleration**  
m/s<sup>2</sup> - Meters per (second squared)  
  
**Date & Time**  
ms - Unix epoch time (also called POSIX time), defined as the number of seconds that have elapsed since midnight Coordinated Universal Time (UTC), January 1, 1970 (not counting leap seconds - as such, it is not an absolutely linear representation of time nor a true representation of UTC).  

**Distance**  
km - Kilometers  

**Distance to service**  
km - This is the estimated distance until the next scheduled service, as indicated by the ECU. The precision is to the nearest ten kilometers.  

**Duration**  
ms - Milliseconds  

**Duration to service**  
ms - This is the amount of time remaining until the next scheduled service as indicated by the ECU. The precision is to the nearest day (86400000 ms).  

**Engine Speed**  
rpm - Revolutions per minute  

**Fuel consumed**  
l - Litres  
  
**Level**  
% - Percentage of the whole amount remaining  

**Location**  
°,° - Degrees (+North or -South), degrees(+East or -West) in decimal format  

**Location Accuracy**  
m - Radius (meters)  

**Location Heading**  
° - Degrees in decimal format  

**Network Signal Strength**
dBm - Strength of the mobile network signal (RSSI)  

**Odometer**  
km - This represents the total distance driven as indicated by the vehicle's ECU. The precision is to the nearest 10 km.  

**Speed**  
km/hr kph - Kilometers per hour (magnitude)  

**Temperature**  
°C - Degrees in Celsius   

**Voltage**  
V - Volts, measured between the OBD-II power and ground pins   

[Next Section: Summary of Reports](https://github.com/CarmaSys/CarmaLinkAPI/blob/1.6/summaryOfReports.md)
