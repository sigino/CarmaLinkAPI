<h2>Terminology</h2>  
<b>Allowance</b>  
The allowance specifies a duration before an event is considered to have occurred.  For example, if a report dictates an allowance of 1000ms, the report condition must remain true for greater than that time, otherwise the event will not be reported.  This also means that the event start time in the report is offset by the value of the allowance.  So for an allowance of 1000ms, the real start time is n-1000ms.  
  
<b>API</b>  
Application Programming Interface  
  
<b>CEL</b>  
Check Engine Light  
  
<b>configId</b>  
Unique ID number assigned to a specific configuration on a single CarmaLink.  Note: configId is not a global variable, it can be unique to each CarmaLink even if the configuration is the same across multiple CarmaLinks.  
  
