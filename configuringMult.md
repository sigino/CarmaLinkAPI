## Configuring multiple transponders  
Our examples thus far have been focused on configuring one transponder per HTTP request. If you have a number of transponders with different configurations, this is the best way to manage them. However, many times you may want to assign the same configuration to many (or all) transponders on your API account. The API provides a means of accomplishing this through a modified request URI and response format.  

### Changes to the request  
A set of transponders can be configured in a single HTTP request by adding the serial number of each to the <serial> part of the URI using special operators:  

* Use a dot operation (".") to append another serial number  
* Use the hyphen operator ("-") to specify a consecutive range of serial numbers  
* OR use "all" to specify all serial numbers assigned to your API account  

> :warning: Important  
>  
> Be careful with ranges. If you specify an invalid range or a range which includes a non-valid serial number, the range will be thrown out of the query.  

The rest of the request looks the same as if you were addressing a single transponder.  

Behind the scenes, the API actually makes individual requests for each serial number listed and then collates the results into a single object that is returned in the HTTP response body.  
  
<h3>Changes to the response</h3>
The response from the server will include a **Multiple Query Response** object in JSON format that contains the following fields:  

Field | JSON name | Value | Description
------|-----------|-------|-------------
Data | data | List of objects | This field contains response information for each successful request.
Error | error | List of objects | This field contains the status code and error description for each failed request.  

For each serial number in the request URI there will be a correspondingly named object that exists either in the Data (on success) or Error (on failure) objects.  

<b>On success</b>
For PUT and DELETE requests that are successful, each serial number will have an object that contains a "success" field with a value of "true", and a "code" field with an integer value of 204.  

For GET requests that are successful, each serial number will have its own Report Configuration View object.  

<b>On failure</b>
For any failed request, each serial number will have an object that contains an "error" field with a string describing the error, and a "code" field with an integer value of the HTTP status code.  

### Usage example  
The following example configures serial numbers 8, 18, 19, 20, and 25 with the same Overspeeding configuration we have previously used.  
 
--
##### HTTP request
```javascript
PUT https://api.carmalink.com:8282/v1/8.18-20.25/report_config/overspeeding
{
  "threshold" : 160.0,
  "allowance" : 5000,
  "location" : true,
  "buzzer" : "HIGH",
  "optionalParams" : [ "BATTERY_VOLTAGE", "ODOMETER" ]
}
```  
--
##### HTTP response  
```javascript
{
  "data" : {
    "8" : {
      "success" : true,
      "code" : 204
    },
    "18" : {
      "success" : true,
      "code" : 204
    },
    "19" : {
      "success" : true,
      "code" : 204
    },
    "20" : {
      "success" : true,
      "code" : 204
    },
    "25" : {
      "success" : true,
      "code" : 204
    }
 },
  "errors" : {}
}
```  
--  
Reading back this same configuration:  
##### HTTP request  
```javescript
GET https://api.carmalink.com:8282/v1/8.18-20.25/report_config/overspeeding  
```  
--  
##### HTTP response  
```javascript
{
  "data" : {
    "8": {
      "configId" : 96185,
      "status" : "PENDING_ACTIVATION",
      "threshold" : 160.0,
      "allowance" : 5000,
      "location" : true,
      "buzzer" : "HIGH",
      "optionalParams" : [ "BATTERY_VOLTAGE", "ODOMETER" ]
    },
    "18": {
      "configId" : 85547,
      "status" : "PENDING_ACTIVATION",
      "threshold" : 160.0,
      "allowance" : 5000,
      "location" : true,
      "buzzer" : "HIGH",
      "optionalParams" : [ "BATTERY_VOLTAGE", "ODOMETER" ]
    },
    "19": {
      "configId" : 20147,
      "status" : "PENDING_ACTIVATION",
      "threshold" : 160.0,
      "allowance" : 5000,
      "location" : true,
      "buzzer" : "HIGH",
      "optionalParams" : [ "BATTERY_VOLTAGE", "ODOMETER" ]
    },
    "20": {
      "configId" : 31088,
      "status" : "PENDING_ACTIVATION",
      "threshold" : 160.0,
      "allowance" : 5000,
      "location" : true,
      "buzzer" : "HIGH",
      "optionalParams" : [ "BATTERY_VOLTAGE", "ODOMETER" ]
    },
    "25": {
      "configId" : 16943,
      "status" : "PENDING_ACTIVATION",
      "threshold" : 160.0,
      "allowance" : 5000,
      "location" : true,
      "buzzer" : "HIGH",
      "optionalParams" : [ "BATTERY_VOLTAGE", "ODOMETER" ]
    }
 },
  "errors" : {}
}
```  
--  

[:fast_forward: Next Section: 3. Report data](/3reportData.md)
