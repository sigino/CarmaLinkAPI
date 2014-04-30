# Configuring a CarmaLink  
Once you have obtained an API key, you are ready to start making calls to the API. In order to start receiving relevant data from the CarmaLink, you need to configure the CarmaLink to inform it which events you will want it to track. First, let's check our CarmaLink's status configuration, for the sake of the following examples, we'll say that our CarmaLink has a serial number of "150":  
**Input**
'curl -i -X GET https://api.carmalink.com:8282/v1/150/report_config/status/'  

**Output**  
`HTTP/1.1 404 Not Found  
Date: Tue, 04 Sep 2012 18:19:00 GMT`  

**Uh oh!** It looks as though something is wrong. In fact the issue is either:  

    There is no CarmaLink with serial number 150 or  
    The CarmaLink hasn't yet been configured for this.  

In this case, since we know serial number 150 exists, the 404 error means the CarmaLink has not yet been configured for this specific report type. In this case, we must configure the CarmaLink status for CarmaLink 150. With this configuration we need to tell the API how frequently the CarmaLink should report back any data to the server.  

✓ An API call to set a configuration that returns a HTTP 404 indicates the configuration hasn't yet been set or you have an invalid serial number.  

Whenever you need to set or update an configuration you must issue a HTTP PUT with the request body being of content-type 'application/json.' The contents request body should be a standard configuration update JSON object that looks like this:  

**Sample Configuration Update Object**  
```javascript  
{    
    "threshold" : float,    
    "allowance" : int,  
    "location"    : bool,  
    "params"  : null  
}  
````  
You only need to send properties relevant to the configuration. In this case we're updating a device status, so we'll use 60,000ms (report back every minute). Our call will look like this:  
**Input**  
`curl -i -H "Content-Type:application/json" -X PUT --data "{\"threshold\": 60000}" https://api.carmalink.com:8282/v1/150/report_config/status/`  

**Output**  
HTTP/1.1 204 No Content  
Date: Tue, 04 Sep 2012 18:25:06 GMT  

API calls that return 204 are considered successful. We have successfully configured CarmaLink 150 to report status every minute. Now let's try our first call we made that resulted in an error again:  
**Input**  
`curl -i -X GET https://api.carmalink.com:8282/v1/150/report_config/status/`  

**Output**  
```javascript  
HTTP/1.1 200 OK  
Date: Tue, 04 Sep 2012 18:31:36 GMT  
Content-Type: application/json  
Content-Length: 109  
{  
 "status" : "PENDING_ACTIVATION",  
 "configId" : 176,  
 "locationEnabled" : false,  
 "frequency" : 60000  
}  
```  

As you can see, we now get back a 200 and some relevant JSON data. Note that the "status" is "PENDING_ACTIVATION," this means that the CarmaLink has not yet been contacted with the new configuration from the server.   
