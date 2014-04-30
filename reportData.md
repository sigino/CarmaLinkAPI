# Getting CarmaLink Report Data  
Now that we know how to make configurations to a CarmaLink, let's grab some data. The API endpoint trip_report gives us the CarmaLink's trip reports:  
**Input**  
```javascript  
curl -i -X GET https://api.carmalink.com:8282/v1/150/data/trip_report/  
```  
**Output**  
```javascript  
HTTP/1.1 200 OK  
Date: Tue, 04 Sep 2012 18:53:01 GMT  
Content-Type: application/json  
Content-Length: 9038  
[  
 {  
 "configId": 155,  
 "serial": 150,  
 "eventStart": 1346781139660,  
 "reportTimestamp": 1346781732737,  
 "duration": 593077,  
 "location": null,  
 "fuelConsumed": 8.349162,  
 "distance": 4.3463326,  
 "voltage": 13.989481,  
 "maxOverspeed": null,  
 "inProgress": false  
 },  
 {  
 "configId": 155,  
 "serial": 150,  
 "eventStart": 1346781139660,  
 "reportTimestamp": 1346781139660,  
 "duration": 0,  
 "location": null,  
 "fuelConsumed": 0,  
 "distance": 0,  
 "voltage": 14.0398245,  
 "maxOverspeed": null,  
 "inProgress": true  
 },  
 {  
 "configId": 155,  
 "serial": 150,  
 "eventStart": 1346779708362,  
 "reportTimestamp": 1346780257804,  
 "duration": 549442,  
 "location": null,  
 "fuelConsumed": 5.29524,  
 "distance": 4.1501393,  
 "voltage": 14.341754,  
 "maxOverspeed": null,  
 "inProgress": false  
 },  
 {  
 "configId": 155,  
 "serial": 150,  
 "eventStart": 1346779708362,  
 "reportTimestamp": 1346779708362,  
 "duration": 0,  
 "location": null,  
 "fuelConsumed": 0,  
 "distance": 0,  
 "voltage": 13.137997,  
 "maxOverspeed": null,  
 "inProgress": true  
 },  
 {  
 "configId": 155,  
 "serial": 150,  
 "eventStart": 1346644321946,  
 "reportTimestamp": 1346644496410,  
 "duration": 174464,  
 "location": null,  
 "fuelConsumed": 9.13256,  
 "distance": 1.4420023,  
 "voltage": 14.328916,  
 "maxOverspeed": null,  
 "inProgress": false  
 },  
 {  
 "configId": 155,  
 "serial": 150,  
 "eventStart": 1346644321946,  
 "reportTimestamp": 1346644321946,  
 "duration": 0,  
 "location": null,  
 "fuelConsumed": 0,  
 "distance": 0,  
 "voltage": 11.9492235,  
 "maxOverspeed": null,  
 "inProgress": true  
 },  
 {  
 "configId": 155,  
 "serial": 150,  
 "eventStart": 1346619777769,  
 "reportTimestamp": 1346619985697,  
 "duration": 207928,  
 "location": null,  
 "fuelConsumed": 4.124356,  
 "distance": 1.4323553,  
 "voltage": 14.303386,  
 "maxOverspeed": null,  
 "inProgress": false  
 },  
 {  
 "configId": 155,  
 "serial": 150,  
 "eventStart": 1346619777769,  
 "reportTimestamp": 1346619777769,  
 "duration": 0,  
 "location": null,  
 "fuelConsumed": 0,  
 "distance": 0,  
 "voltage": 12.092696,  
 "maxOverspeed": null,  
 "inProgress": true  
 },  
 {  
 "configId": 155,  
 "serial": 150,  
 "eventStart": 1346547788951,  
 "reportTimestamp": 1346547992553,  
 "duration": 203602,  
 "location": null,  
 "fuelConsumed": 6.9067497,  
 "distance": 1.4427567,  
 "voltage": 14.169531,  
 "maxOverspeed": null,  
 "inProgress": false  
 },  
 {  
 "configId": 155,  
 "serial": 150,  
 "eventStart": 1346547788951,  
 "reportTimestamp": 1346547788951,  
 "duration": 0,  
 "location": null,  
 "fuelConsumed": 0,  
 "distance": 0,  
 "voltage": 11.908231,  
 "maxOverspeed": null,  
 "inProgress": true  
 },  
 {  
 "configId": 155,  
 "serial": 150,  
 "eventStart": 1346519186374,  
 "reportTimestamp": 1346519359017,  
 "duration": 172643,  
 "location": null,  
 "fuelConsumed": 4.1658096,  
 "distance": 1.0618714,  
 "voltage": 13.958849,  
 "maxOverspeed": null,  
 "inProgress": false  
 },  
 {  
 "configId": 155,  
 "serial": 150,  
 "eventStart": 1346519186374,  
 "reportTimestamp": 1346519186374,  
 "duration": 0,  
 "location": null,  
 "fuelConsumed": 0,  
 "distance": 0,  
 "voltage": 11.867238,  
 "maxOverspeed": null,  
 "inProgress": true  
 }  
]  
```  
**WHOA WHOA WHOA!** That's a lot of information. Let's try that again with a parameter limit set to one, this only returns one result (in reverse chronological order):  
**Input**  
```javascript  
curl -i -X GET https://api.carmalink.com:8282/v1/150/data/trip_report?limit=1  
```  
**Output**  
```javascript  
HTTP/1.1 200 OK  
Date: Tue, 04 Sep 2012 19:39:28 GMT  
Content-Type: application/json  
Content-Length: 285  
[ {  
 "configId" : 155,  
 "serial" : 150,  
 "eventStart" : 1346781139660,  
 "reportTimestamp" : 1346781732737,  
 "duration" : 593077,  
 "location" : null,  
 "fuelConsumed" : 8.349162,  
 "distance" : 4.3463326,  
 "voltage" : 13.989481,  
 "maxOverspeed" : null,  
 "inProgress" : false  
} ]  
```

As you can see, a trip report returns some useful information. Another option is if we wanted to get all trip reports for CarmaLink 150 since Sept. 4th, 2012 at 2:37pm EST (note this is the 3rd item's "reportTimestamp" in our large list that was first returned). In this case we'll use the parameter since set to UNIX epoch time (1346780257804) :  
**Input**  
```javascript  
curl -i -X GET https://api.carmalink.com:8282/v1/150/data/trip_report?since=1346780257804  
```

**Output**  
```javascript  
HTTP/1.1 200 OK  
Date: Tue, 04 Sep 2012 20:26:59 GMT  
Content-Type: application/json  
Content-Length: 552  
[  
 {  
 "configId": 155,  
 "serial": 150,  
 "eventStart": 1346781139660,  
 "reportTimestamp": 1346781732737,  
 "duration": 593077,  
 "location": null,  
 "fuelConsumed": 8.349162,  
 "distance": 4.3463326,  
 "voltage": 13.989481,  
 "maxOverspeed": null,  
 "inProgress": false  
 },  
 {  
 "configId": 155,  
 "serial": 150,  
 "eventStart": 1346781139660,  
 "reportTimestamp": 1346781139660,  
 "duration": 0,  
 "location": null,  
 "fuelConsumed": 0,  
 "distance": 0,  
 "voltage": 14.0398245,  
 "maxOverspeed": null,  
 "inProgress": true  
 }  
]  
```
✓ When using the "before" and "since" parameters with report API endpoints make sure to use EPOCH time with milliseconds.    

### Report Data API Parameters  
| Parameter Name     | Type           | Description                                                     | Default Value        | Max   |
| ------------------ |----------------|-----------------------------------------------------------------|----------------------|-------|
| limit              | int            | Number of results to return in report list |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |
