<h2>Querying Single Vs. Multiple CarmaLinks</h2>  
All endpoints need to specify which CarmaLinks to query by their serial number. In some cases the application may need to query multiple (or all) CarmaLinks under an API account. To achieve this you can specify multiple serial numbers or ranges in the following format:  
  
    /v1/[serial][.|-][serial]  
  
To append CarmaLinks to query use the dot operator ("."). To specify consecutive ranges use the hyphen operator ("-").   
  
**Query Operators**  
Use "." to query two or more non-consecutive CarmaLinks, in this case serial numbers 123, 432 and 152 ex. /v1/123.432.152/data/status  
Use "-" to query a range of CarmaLinks, in this case 123 through 555 (inclusive of end numbers) ex. /v1/123-555/data/status  
Use "all" to query all CarmaLinks associated with your API account ex. /v1/all/data/status  

**! Important**  
Be careful with ranges. If you specify an invalid range or a range which includes a non-valid serial number, the range will be thrown out of the query.  
  
### Multiple CarmaLink Query Data Object  
When querying more than one CarmaLink you will usually receive a 200 response from the server along with a special JSON data object.  
  
**Multiple Query JSON Object**  
```javascript
{  
    "data" : {  
      "serial1" : [ result objects ] ,  
      "serial2" : [ result objects ]   
    },  
    "errors" : {  
       "serial3" : { "error" : "Error Message", "code" : HTTP Error Code },  
       "serial4" : { "error" : "Error Message", "code" : HTTP Error Code }  
    }  
}
```
  
**When issuing PUT commands**   
If you issue a multiple query using a PUT command and the API is sent an invalid Update Configuration, it will immediately return a 400 without any response body, and abort any attempts to PUT on specified CarmaLinks.  
  
**Multiple Query Example**  
```javascript
/**  
* sample request: /v1/47.200.100/data/status  
**/  
{  
  "data": {  
    "47": [  
      {  
        "configId": 23,  
        "serial": 47,  
        "eventStart": 1347987050641,  
        "reportTimestamp": 1347987077227,  
        "duration": 26586,  
        "location": {  
          "longitude": -73.8226421,  
          "latitude": 42.6260305,  
          "accuracy": 15.06,  
          "heading": 352.87958  
        },  
        "vehicleVoltage": 11.851867,  
        "gsmSignalStrength": -85  
      },  
      {  
        "configId": 23,  
        "serial": 47,  
        "eventStart": 1347987050641,  
        "reportTimestamp": 1347987057159,  
        "duration": 6518,  
        "location": {  
          "longitude": -73.8226421,  
          "latitude": 42.6260305,  
          "accuracy": 15.06,  
          "heading": 352.87958  
        },  
        "vehicleVoltage": 12.138812,  
        "gsmSignalStrength": -89  
      }  
    ],  
    "200": [  
      {  
        "configId": 109,  
        "serial": 200,  
        "eventStart": 1348751837332,  
        "reportTimestamp": 1348752273692,  
        "duration": 436360,  
        "location": {  
          "longitude": -73.82306129999999,  
          "latitude": 42.626288699999996,  
          "accuracy": 2.7610002,  
          "heading": 244.21552  
        },  
        "vehicleVoltage": 12.927912,  
        "gsmSignalStrength": -83  
      }   
    ]  
  },  
  "errors": {  
    "100": {  
      "error": "CarmaLink not found.",  
      "code": 404  
    }  
  }  
}
```
[Next Section: Report Configuration](https://github.com/CarmaSys/CarmaLinkAPI/blob/1.5/reportConfiguration.md)
