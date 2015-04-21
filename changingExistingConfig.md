<h2>Changing an existing report configuration</h2>  
To change an existing report configuration you follow the same procedure as creating a new report configuration with the exception that **you only need to include the fields you would like to change**. Any field not included in the Report Configuration Update object will retain its existing value.  

For a given report up to one configuration is active at a time. This means that when you change the configuration the API automatically deactivates the existing configuration, and then creates a new configuration with your changes (with a new configuration ID).  


Usage Example  
Let's say we want to lower our Overspeeding report's allowance from 5 seconds to 1 second.  

HTTP request
```javascript
PUT https://api.carmalink.com:8282/v1/159821/report_config/overspeeding
{
  "allowance" : 1000
}
```
On the subsequent GET, we would see something like the following response body:

HTTP response body
```javascript
{
  "configId" : 397748,
  "status" : "PENDING_ACTIVATION",
  "threshold" : 160.0,
  "allowance" : 1000,
  "location" : true,
  "buzzer" : "HIGH",
  "optionalParams" : [ "BATTERY_VOLTAGE", "ODOMETER" ]
}
```

Note that the configuration ID is new.  
