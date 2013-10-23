<h2>Introduction</h2>
For further customer support, log onto the customer support portal at support.carmasys.com  
  
<b>Overview</b>  
CarmaLink is a vehicle telematics device (VTD) whose purpose is to provide information useful for end-user profitability improvement based decision making.

The VTD, once installed, communicates with our servers using wireless Internet technology. Carma's servers manage operation of the VTD, including: monitoring health and status, enabling data communication in both directions, and performing firmware upgrades. Overall, the customer is given application-level control of the VTD by means of the CarmaLink.API (API), as described herein. "Application-level" means the configuration of the VTD used to gather and report information based on customer's needs.  

The CarmaLink.API is a publicly available RESTful web interface. All VTD configuration requests are issued to this public API, where they are stored and then sent down to the VTD for execution. The VTD then sends data back for retrieval and reporting purposes where it is stored and made accessible via the CarmaLink.API. Customers may then make API calls to retrieve this report data.  

Data is gathered from the vehicle's electronic control units via the OBD-II port, as well as the GPS module. In the API, all data is organized as a collection of reports, with each configurable at the VTD level for different behaviors (e.g., hard braking, overspeeding, or trip summary).  

A report is triggered by events; e.g., an overspeeding report is activated when the vehicle is moving faster than configured threshold. Once triggered, a report is considered active in the VTD until an end condition is met, which is generally the loss of the initial triggering condition. At this point, a report is generated with specific relevant data and sent to the server for retrieval via the API. In the case of the overspeeding example, useful information such as start time and duration as well as maximum vehicle speed experienced during this interval are reported.     

<a href="https://github.com/CarmaSys/CarmaLinkAPI/blob/1.5/terminology.md">Next section: Terminology</a>

