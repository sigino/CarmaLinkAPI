<h2>Engine configuration</h2>  
The transponder has the ability to provide fuel consumption information in vehicles that support OBD-II (light-duty) or SAE J1939 (heavy-duty). Sometimes this data is directly available from the vehicle, but many times it must be estimated based on various sensor values. To assist in making the transponder's fuel consumption calculations as accurate as possible it helps to provide it the vehicle's fuel type and engine displacement using the API's engine configuration resource.  

> :information_source:  
>  
> All engine configuration request URIs are relative to /config/engine  

<h3>Creating a new engine configuration</h3>  
To create a new engine configuration for a given serial number, you must send a new PUT request containing the **Engine Configuration Update** object in JSON format, which will have the following fields:  

Field | JSON Name | Value type
------|-----------|-----------
Fuel type | fuel | String; "FUEL_GASOLINE" or "FUEL_DIESEL"  
Engine displacement | displacement | Float; volume of the engine in liters  

If the operation is successful, the HTTP response will have a status code of 204.  

<h3>Reading an engine configuration</h3>  
Like report configurations, there is a corresponding **Engine Configuration View** object, which contains the same fields as the Engine Configuration Update object, but also includes a "status" field that has one of the 4 string values from the section describing Report Configuration View objects.  

<h3>Usage example</h3>  
If we have installed our transponder in a Ford Mustang with a 5.0 liter engine, we would create the following engine configuration:  

HTTP request  
```javascript
PUT https://api.carmalink.com:8282/v1/159821/config/engine
{
  "fuel" : "FUEL_GASOLINE",
  "displacement" : 5.0
}
```  

To read back this configuration:  
HTTP request
```javascript
GET https://api.carmalink.com:8282/v1/159821/config/engine
```  

HTTP response
```javascript
{
  "fuel" : "FUEL_GASOLINE",
  "displacement" : 5.0,
  "status" : "PENDING_ACTIVATION"
}
```  

[:fast_forward: Next Section: Configuring multiple transponders](/configuringMult.md)
