# 3. Report generation  
Once the transponder has received the report configurations you've created, it will be able to detect when these events occur. At any given moment each of these events can be thought of as a condition that evaluates to either 'true' or 'false'. Depending on the type of event, reports will be generated during one or more of the following circumstances:  
* When the event transitions from 'false' to 'true': this is called the **event start**  
* Periodically while the event is true  
* When the event transitions from 'true' to 'false': this is called the **event end**  

The process of creating a report consists of capturing some information about the event state, the current time, and then packing the current value of any configurable or non-configurable parameters that belong in that type of report. Once generated, the report is stored in the non-volatile memory of the transponder's file system until this data can be transmitted. The transponder will attempt to send report data to the server once every few minutes, though it could be much longer if it is in an area with poor cellular service.

--
[:fast_forward: Next Section: **4. Report data**](/4reportData.md)
