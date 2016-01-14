## Non-configurable reports  
Presently there is only one non-configurable report: the New Deployment report.  

### New Deployment  
The New Deployment report identifies when the transponder was installed, when it was last removed, and some information about the vehicle it is connected to.  

**Dispatch**  
This report is created when the transponder is installed in a vehicle, and updated when that vehicle is first switched on.  

**Structure**  
A New Deployment report has a much different structure than configurable reports:  

Field | JSON name | Value type | Description 
------|-----------|------------|-------------
Serial number | `"serial"` | Long; required | Transponder serial number
Installation time | `"installationTime"` | Long; required | POSIX time in milliseconds when the transponder was plugged in
Removal time | `"removalTime"` | Long; optional | POSIX time in milliseconds when the transponder was last unplugged (within 3 minutes)
Deployment time | `"deploymentTime"` | Long; optional | POSIX time in milliseconds when the transponder started running its reports (typically when the vehicle first starts)
Vehicle Identification Number | `"vin"` | String; optional | 17-digit string identifying the vehicle the transponder is plugged into  

The New Deployment report is the only report that can get updated: that is, you will typically receive the serial number, installation time and removal time shortly after you plug the transponder in. When you start the vehicle this report will then update to include the deployment time and VIN (if available).  

--
[:fast_forward: Next Section: **Retrieving report data**](/retrievingReportData.md)
