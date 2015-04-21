<h2>Reading a report configuration</h2>
To read a report configuration, you simply send an HTTP request using the GET method on the report's configuration URI. No body is required, and if one is included, it is ignored.  
The HTTP response will have a status code of 200.  
The format of this Report Configuration View object has the same basic fields as Report Configuration Update, but includes two new fields: configuration ID and status.  

