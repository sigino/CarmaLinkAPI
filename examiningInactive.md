<h2>Examining inactive report configurations</h2>  
Only the `'current'` configuration is returned when performing a GET on the standard report configuration URI. If you'd like to check out the values inside an inactive configuration, you include the 'id' query string with the appropriate configuration ID.    

Usage Example
Lets say we have a bunch of Overspeeding reports that reference the old configuration ID (397746), but we forgot what the characteristics of that configuration were! Simply use the ID query string to find out:  

HTTP request  
```javascript
GET https://api.carmalink.com:8282/v1/159821/report_config/overspeeding?id=397746
```

HTTP response body  
```javascript
{
  "configId" : 397746,
  "status" : "DEACTIVATED",
  "threshold" : 160.0,
  "allowance" : 5000,
  "location" : true,
  "buzzer" : "HIGH",
  "optionalParams" : [ "BATTERY_VOLTAGE", "ODOMETER" ]
}
```  

[:fast_forward: Next Section: Buzzer configuration](/buzzerConfig.md)
