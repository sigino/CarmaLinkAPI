<h2>1. Introduction</h2>  
For further customer support, email us at <a href="mailto:support@carmasys.com?Subject=API%20v1.6">
support@carmasys.com</a>  

<b>Overview</b>  
CarmaLink is a vehicle telematics device whose purpose is to provide useful information to fleet managers and drivers. A built-in cellular module allows CarmaLink to wirelessly connect to Carma's servers in order to: collect a new configuration, send data, or receive a firmware upgrade. Overall, the developer is given application-level control of their CarmaLinks by means of the CarmaLink.API (API), as described herein.  
  
The CarmaLink.API is a publicly available RESTful web interface. All configuration requests are issued to this API, where they are stored and then sent down to CarmaLink for execution. These configuration requests identify which reports CarmaLink will run and whether the onboard buzzer should be activated under any conditions to provide audible feedback to the driver. Once received, CarmaLink collects the data required by the configuration and generates reports as necessary. Data is gathered from various sources, including: a GPS module, a three-axis accelerometer, and the vehicle's electronic control units (ECUs). The generated reports are then periodically sent to servers where they are stored and made accessible through the API. An application may then make API calls to retrieve this report data.  

In this document you will learn how to use the API to properly configure your CarmaLinks and acquire the data they generate.  
