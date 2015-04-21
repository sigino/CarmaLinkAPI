<h2>Creating a new report configuration</h2>
A report configuration is created by using the PUT method on the report's configuration URI. The body of the request should contain a Report Configuration Update object in JSON format with the appropriate values for each field.  
Not all reports support all fields and some have restrictions regarding the requested values. Any field that is optional and has no default value will default to 'null'.  

<em>All report configuration URIs are relative to /report_config  
The success code is 204 (No Content)  </em>

