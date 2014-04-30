# Introduction  
This is a supplement document for CarmaLink.API  
  
### Vocabulary  
*Should* - suggestion  
*Must* - requirement  
  
### Requirements  
The CarmaLink API is a RESTful API utilizing HTTP. In order to use it you will need access to a module/library which supports HTTP (such as urllib2 for Python or libcurl with PHP) or a command-line program like cURL. All requests to the API must be signed using OAuth 1.0a's two-legged approach. Instead of "rolling your own" library, we suggest you use any library that supports OAuth 1.0a and RESTful HTTP verbs: "GET, PUT & DELETE." For futher information, check the main API Documentation under OAuth.  
All responses are sent with a valid HTTP response code along with optional JSON-encoded data. It is strongly recommended you use a library to support JSON parsing/serialization.   
  
### Terminology  
*Trip*  
An event which begins when a vehicle's engine turns on and ends when the cycle completes with the engine turning off.  
  
*Idle*  
Occurs when vehicle's engine is on, but has not moved in a period which exceeds the CarmaLink's idle threshold.  
  
*Overspeeding*  
An event which occurs when a vehicle's speed exceeds that set by the CarmaLink's overspeeding threshold.  

*Buzzer*  
A buzzer located on the CarmaLink that sounds when a specific event occurs.  

*Hard Acceleration*  
An event which occurs when a vehicle accelerates quickly in excess of the CarmaLink's threshold.  

*Hard Braking*  
An event which occurs when a vehicle brakes quickly in excess of the CarmaLink's threshold.  

*Engine Fault*  
An event which indicates the vehicle's engine has reported some sort of error to the CarmaLink.  

### Assumptions  
This guide assumes you have obtained a CarmaLink with a valid serial number for testing purposes and have plugged it into a vehicle.  

### Obtaining Access  
In order to use the CarmaLink API you must obtain the appropriate keys from a Carma API sales team member. Authentication is handled by OAuth 1.0a, who's spec is located [here](http://oauth.net/core/1.0a/).  
  
### cURL Examples  
It is important to note that all of the for all of the following command line cURL examples below to work it is assumed you will also be sending along the valid OAuth authorization header, for simplicity we are omitting these lengthy arguments to cURL. For example, here is the first configuration example complete with authorization:  
  
*cURL Example With OAuth Headers*  
```
curl -i -X GET https://api.carmalink.com:8282/v1/150/report_config/status -H "Authorization: OAuth oauth_consumer_key=\"JiYm4l74tXddzz4snnIDeg\",oauth_nonce=\"976cd77d0b33b524417f9f44884b7f00\",oauth_signature_method=\"HMAC-SHA1\",oauth_timestamp=\"1348260490\",oauth_version=\"1.0\",oauth_signature=\"XG%2FBcoKd0S2eNUNeJCCof%2BI8bxI%3D\""
```   

