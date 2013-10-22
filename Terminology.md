<h2>Terminology</h2>  
<b>Allowance</b>  
The allowance specifies a duration before an event is considered to have occurred.  For example, if a report dictates an allowance of 1000ms, the report condition must remain true for greater than that time, otherwise the event will not be reported.  This also means that the event start time in the report is offset by the value of the allowance.  So for an allowance of 1000ms, the real start time is n-1000ms.  
  
<b>API</b>  
Application Programming Interface  
  
<b>CEL</b>  
Check Engine Light  
  
<b>configId</b>  
Unique ID number assigned to a specific configuration on a single CarmaLink.  Note: configId is not a global variable, it can be unique to each CarmaLink even if the configuration is the same across multiple CarmaLinks.  
  
<b>DTC(s)</b>  
Diagnostic Trouble Codes as defined by SAE J2012.  
  
<b>ECU</b>  
The primary Engine Control Unit that CarmaLink communicates with.  
  
<b>GPS</b>  
Global Positioning System  
  
<b>HMAC</b>  
Hash-based Message Authentication Code  
  
<b>JSON</b>  
JavaScript Object Notation  
  
<b>MIL</b>  
Malfunction Indicator Lamp, see CEL.  
  
<b>Must</b>  
Read as requirement.    
  
<b>OBD-II</b>  
On-Board Diagnostics as defined by SAE J1979  
  
<b>Optional Parameter</b>  
This field can contain a list of strings to optionally add extra parameters to a report.  
  
<b>Optional Condition</b>  
This field can contain a list of strings to specify optional conditions on which to trigger a report. The conditions allowed are specified to each report.  
  
<b>Nonce</b>  
An arbitrary number used only once in a cryptographic communication.  
  
<b>Parameter</b>  
Value recorded such as speed, acceleration or engine fault.  
  
<b>Report</b>  
Representation of higher-level vehicle data characteristics made available. On the CarmaLink, an active report is one whose triggering conditions (threshold and/or allowance) have been met, and is thus collecting data relevant to the report.  
  
<b>Report Configuration</b>  
Collection parameters coupled with thresholds, allowances, and driver feedback (buzzer) that defines the operational behavior of a report. On the CarmaLink, an active report configuration is one that is presently loaded and enabled: its threshold condition is being checked.  
  
<b>Serial</b>  
This refers to the serial number of the CarmaLink.  
  
<b>SHA1</b>  
The most commonly adopted Secure Hash Algorithm: a cryptographic hash function designed by the United States National Security Agency and published by the United States NIST as a U.S. Federal Information Processing Standard.  

<b>Should</b>  
Read as suggestion.  
  
<b>Threshold</b>  
Specifies a value that is the trigger for the report to begin. In overspeeding, for example, the threshold is the speed that vehicle must exceed for the report to occur.  
  
<b>VIN</b>  
Vehicle Identification Number  

