<h2>Terminology</h2>  
**Allowance**  
The allowance specifies a duration before an event is considered to have occurred.  For example, if a report dictates an allowance of 1000ms, the report condition must remain true for greater than that time, otherwise the event will not be reported.  This also means that the event start time in the report is offset by the value of the allowance.  So for an allowance of 1000ms, the real start time is n-1000ms.  
  
**API**  
Application Programming Interface  
  
**CEL**  
Check Engine Light  
  
**configId**  
Unique ID number assigned to a specific configuration on a single CarmaLink.  Note: configId is not a global variable, it can be unique to each CarmaLink even if the configuration is the same across multiple CarmaLinks.  

**DTC(s)**  
Diagnostic Trouble Codes as defined by SAE J2012.  

**ECU**  
The primary Engine Control Unit that CarmaLink communicates with.  

**GPS**  
Global Positioning System  

**HMAC**  
Hash-based Message Authentication Code  

**JSON**  
JavaScript Object Notation  

**MIL**  
Malfunction Indicator Lamp, see CEL.  

**Must**  
Read as requirement.  

**OBD-II**  
On-Board Diagnostics as defined by SAE J1979  

**Optional Parameter**  
This field can contain a list of strings to optionally add extra parameters to a report. The parameters allowed are specific to each report.  

**Optional Condition**  
This field can contain a list of strings to specify optional conditions on which to trigger a report. The conditions allowed are specified to each report.  

**Nonce**  
An arbitrary number used only once in a cryptographic communication.  

**Parameter**  
Value recorded such as speed, acceleration or engine fault.  

**Report**  
Representation of higher-level vehicle data characteristics made available. On the CarmaLink, an active report is one whose triggering conditions (threshold and/or allowance) have been met, and is thus collecting data relevant to the report.  

**Report Configuration**  
Collection parameters coupled with thresholds, allowances, and driver feedback (buzzer) that defines the operational behavior of a report. On the CarmaLink, an active report configuration is one that is presently loaded and enabled: its threshold condition is being checked.  

**Serial**  
This refers to the serial number of the CarmaLink.  

**SHA1**  
The most commonly adopted Secure Hash Algorithm: a cryptographic hash function designed by the United States National Security Agency and published by the United States NIST as a U.S. Federal Information Processing Standard.  

**Should**  
Read as suggestion.  

**Threshold**  
Specifies a value that is the trigger for the report to begin. In overspeeding, for example, the threshold is the speed that vehicle must exceed for the report to occur.  

**VIN**  
Vehicle Identification Number  
  
<a href="https://github.com/CarmaSys/CarmaLinkAPI/blob/1.4/units.md">Next Section: Units</a>

