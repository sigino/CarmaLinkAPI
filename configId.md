# Why Would I Need "configId?"  
When reporting data back, the API usually references some kind of configuration. For instance, say a CarmaLink has a overspeeding configuration of 70mph. The vehicle exceeds the threshold when the driver speeds up to 74mph on a highway. An overspeeding event is logged. Later on, the CarmaLink gets a new overspeeding configuration using 75mph as the threshold. This is why reports include a configId - so you can reference a particular configuration's threshold at the point the event was originally triggered. You can receive other information about a configuration by querying it via the API as for example:  

**Input**  
```javascript  
curl -i -X GET https://api.carmalink.com:8282/v1/150/report_config/overspeeding?id=95  
```
**Output**  
```javascript  
HTTP/1.1 200 OK  
Date: Wed, 05 Sep 2012 19:15:19 GMT  
Content-Type: application/json  
Content-Length: 130  
{  
  "threshold" : 135.0,  
  "allowance" : 0,  
  "location" : false,  
  "params" : null,  
  "status" : "ACTIVATED",  
  "configId" : 95  
}  
```
[Next Section: Deleting Configurations](deletingConfigurations.md)
