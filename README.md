
<html>
<head>
<body class="mceContentBody wiki-content fullsize">
<p> </p>
<h1>CarmaLink.API v1.4</h1>
<p>
<h1>1. Introduction</h1>
<table class="wysiwyg-macro" data-macro-body-type="RICH_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2luZm99&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-name="info">
<h2 class="p1">Summary of changes since v1.1</h2>
<ul>
<div>
<h2 class="p1">Overview</h2>
<p class="p1">CarmaLink is a vehicle telematics device (VTD) whose purpose is to provide information useful for end-user profitability improvement based decision making.</p>
<p class="p1">The VTD, once installed, communicates with our servers using wireless Internet technology. Carma's servers manage operation of the VTD, including: monitoring health and status, enabling data communication in both directions, and performing firmware upgrades. Overall, the customer is given application-level control of the VTD by means of the CarmaLink.API (API), as described herein. "Application-level" means the configuration of the VTD used to gather and report information based on customer's needs.</p>
<p class="p1">The CarmaLink.API is a publicly available RESTful web interface. All VTD configuration requests are issued to this public API, where they are stored and then sent down to the VTD for execution. The VTD then sends data back for retrieval and reporting purposes where it is stored and made accessible via the CarmaLink.API. Customers may then make API calls to retrieve this report data.</p>
<p class="p1">
<p class="p1">A report is triggered by events; e.g., an overspeeding report is activated when the vehicle is moving faster than configured threshold. Once triggered, a report is considered active in the VTD until an end condition is met, which is generally the loss of the initial triggering condition. At this point, a report is generated with specific relevant data and sent to the server for retrieval via the API. In the case of the overspeeding example, useful information such as start time and duration as well as maximum vehicle speed experienced during this interval are reported. </p>
<h2>Terminology</h2>
<p>The following table defines certain terms. </p>
<table class="confluenceTable">
<h2>Units</h2>
<p class="p1">All data from the API is in SI units by default. In certain cases as described in this document, a query field can be included in a web request to specify alternate (International) units.</p>
<table class="confluenceTable">
<h2>Summary of Reports</h2>
<p class="p1">The following table summarizes reports provided by the API. Taken together, they describe the complete application/operational definition of the CarmaLink available to the customer. See the following sections of this document for detailed information on how to set up (configure) each report and how to retrieve the report data.</p>
<div class="section">
<p style="text-align: center;"> </p>
<table class="confluenceTable">
<h1>2. Authentication & Permissions</h1>
<h3>Authentication</h3>
<p>
<h3>Permissions</h3>
<p>API users are assigned apiKey and secretKey pair, allowing access to their range of CarmaLink uniquely assigned serial numbers. Note: a CarmaLink is owned by one user that is accessible with one api/secret key pair, and an API request made referencing a serial number not belonging to the user results in an error code being returned. </p>
<h3>OAuth 1.0a</h3>
<p>
<p>Since the CarmaLink.API only uses two-legged authentication, there is no need for any kind of access or request tokens from the server. You will simply need to properly sign the request by including the "Authorization:" HTTP 1.1 header. Here is a sample of what that header should look like when sent:</p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6dGl0bGU9SFRUUCAxLjEgSGVhZGVyfGxhbmd1YWdlPWJhc2h9&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="language=bash|title=HTTP 1.1 Header" data-macro-name="code">
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6dGl0bGU9UnVieSBFeGFtcGxlfHRoZW1lPU1pZG5pZ2h0fGxhYmVsPUNvZGVTYW1wbGVzfGxpbmVudW1iZXJzPXRydWV8bGFuZ3VhZ2U9cnVieXxjb2xsYXBzZT10cnVlfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="collapse=true|label=CodeSamples|language=ruby|linenumbers=true|theme=Midnight|title=Ruby Example" data-macro-name="code">
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6dGl0bGU9UHl0aG9uIEV4YW1wbGV8dGhlbWU9RW1hY3N8bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1weXRob258Y29sbGFwc2U9dHJ1ZX0&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="collapse=true|language=python|linenumbers=true|theme=Emacs|title=Python Example" data-macro-name="code">
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6dGl0bGU9UEhQIEV4YW1wbGV8dGhlbWU9RW1hY3N8bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1waHB8Y29sbGFwc2U9dHJ1ZX0&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="collapse=true|language=php|linenumbers=true|theme=Emacs|title=PHP Example" data-macro-name="code">
<h2>Querying Single Vs. Mutliple CarmaLinks</h2>
<p>All endpoints need to specify which CarmaLinks to query by their serial number. In some cases the application may need to query multiple (or all) CarmaLinks under an API account. To achieve this you can specify multiple serial numbers or ranges in the following format:</p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGFuZ3VhZ2U9YmFzaH0&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="language=bash" data-macro-name="code">
<p>To append CarmaLinks to query use the dot operator ("."). To specify consecutive ranges use the hyphen operator ("-"). </p>
<table class="wysiwyg-macro" data-macro-body-type="RICH_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2luZm86dGl0bGU9UXVlcnkgT3BlcmF0b3JzfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="title=Query Operators" data-macro-name="info">
<table class="wysiwyg-macro" data-macro-body-type="RICH_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e25vdGU6dGl0bGU9SW1wb3J0YW50fQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="title=Important" data-macro-name="note">
<h3>Multiple CarmaLink Query Data Object</h3>
<p>When querying more than one CarmaLink you will usually receive a 200 response from the server along with a special JSON data object. </p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6dGl0bGU9TXVsdGlwbGUgUXVlcnkgSlNPTiBPYmplY3R8dGhlbWU9RW1hY3N8bGFuZ3VhZ2U9amF2YXNjcmlwdH0&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="language=javascript|theme=Emacs|title=Multiple Query JSON Object" data-macro-name="code">
<table class="wysiwyg-macro" data-macro-body-type="RICH_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e25vdGU6dGl0bGU9V2hlbiBpc3N1aW5nIFBVVCBjb21tYW5kcyB9&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="title=When issuing PUT commands " data-macro-name="note">
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6dGl0bGU9TXVsdGlwbGUgUXVlcnkgRXhhbXBsZXx0aGVtZT1FbWFjc3xsYW5ndWFnZT1qYXZhc2NyaXB0fGNvbGxhcHNlPXRydWV9&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="collapse=true|language=javascript|theme=Emacs|title=Multiple Query Example" data-macro-name="code">
<h1>3. Report Configuration</h1>
<p>
<p> An application manages these configurations by using the following methods.</p>
<h3>General Configuration</h3>
<p>In order for certain values reported by CarmaLink to be accurate, the correct engine fuel type and displacement must be configured. Clients can do so using the general configuration resource. The general configuration resource is a simple resource located directly under the carmalink resource in the API hierarchy:</p>
<table class="confluenceTable">
<p>Clients can configure the resource by sending a json object with the following structure:</p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6dGl0bGU9R2VuZXJhbCBDb25maWd1cmF0aW9uIFVwZGF0ZSBPYmplY3R8bGFuZ3VhZ2U9amF2YXNjcmlwdH0&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="language=javascript|title=General Configuration Update Object" data-macro-name="code">
<table class="wysiwyg-macro" data-macro-body-type="RICH_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e25vdGV9&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-name="note">
<table class="wysiwyg-macro" data-macro-body-type="RICH_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e3RpcH0&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-name="tip">
<p> </p>
<p>Valid values for "fuel" are "FUEL_GASOLINE" and "FUEL_DIESEL", and the "displacement" member is in litres.</p>
<p>When a GET request is made to the general_config resource, a similar javascript object is returned, but including an additional field for the configuration status of the object with respect to the CarmaLink:</p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6dGl0bGU9R2VuZXJhbCBDb25maWd1cmF0aW9uIFZpZXcgT2JqZWN0fGxhbmd1YWdlPWphdmFzY3JpcHR9&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="language=javascript|title=General Configuration View Object" data-macro-name="code">
<p>If no general configuration has been set for a CarmaLink, the general configuration view will have all null values.</p>
<div class="section">
<h2>Configuration Data Create/Update Commands - PUT</h2>
<p>
<table class="wysiwyg-macro" data-macro-body-type="RICH_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2luZm99&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-name="info">
<h4>Definition</h4>
<table class="confluenceTable">
<h3>Configuration Data Content - The Configuration Update Structure</h3>
<p>
<table class="wysiwyg-macro" data-macro-body-type="RICH_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e25vdGV9&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-name="note">
<h4>Definition</h4>
<table class="confluenceTable">
<h3>Usage Example</h3>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1qYXZhc2NyaXB0fQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="language=javascript|linenumbers=true" data-macro-name="code">
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1qYXZhc2NyaXB0fGZpcnN0bGluZT0wfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="firstline=0|language=javascript|linenumbers=true" data-macro-name="code">
<h3>Configuration Status Structure (From Command to Activation)</h3>
<p>When the API is used to send a new report configuration for a CarmaLink to the server, that configuration cannot immediately take effect on the CarmaLink. There is a period of time during which the existing configuration on the CarmaLink continues to be in effect, until the next time the CarmaLink connects to the server and receives the new configuration. This happens, at minimum, at the rate specified by the (current configuration of the) Status report, though in general the CarmaLink connects to the server anytime there is new report data ready to be uploaded. A given report configuration thus has four possible statuses:</p>
<ul>
<p>Each report configuration has its own configuration status. As will be shown in the next section, once a PUT command has been used to send a report configuration, a corresponding GET command can be used to check its status.</p>
<h4>Definition</h4>
<table class="confluenceTable">
<h4>Code Example</h4>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1qYXZhc2NyaXB0fGZpcnN0bGluZT0wfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="firstline=0|language=javascript|linenumbers=true" data-macro-name="code">
<h3>configId (Keeping Track of Report Configurations)</h3>
<p class="column">The server assigns a unique ID number, called the Configuration ID, to each new report configuration it receives through the API. As will be shown in the next section, the GET commands used to check configuration statuses include this ID in the data returned. Since most customer applications will benefit from having this ID number; it is recommended practice that once a PUT command is sent with a new report configuration, it should be followed with a matching GET command to retrieve the ID assigned to the configuration. </p>
<p class="column">Perhaps even more importantly, when report data generated by the CarmaLink is retrieved from the server using the API, this data includes the Configuration ID of the configuration that was in effect when the report was generated. This matters, for example, if the customer decides to change the threshold for the overspeeding report. The next time an overspeeding report is received, how does the customer know which threshold setting was in effect for this report? The Configuration ID in the report data is the key.</p>
<h2>Configuration Data Read Commands - GET</h2>
<p>
<table class="wysiwyg-macro" data-macro-body-type="RICH_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2luZm99&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-name="info">
<h4 class="column">Definition</h4>
<table class="confluenceTable">
<div class="section">
<div class="section">
<h3>Filtering</h3>
<div class="column">
<div class="column">
<h3>Report Structures</h3>
<h4>All Activity Report</h4>
<p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1qYXZhc2NyaXB0fGZpcnN0bGluZT0wfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="firstline=0|language=javascript|linenumbers=true" data-macro-name="code">
<h4>
<p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1qYXZhc2NyaXB0fGZpcnN0bGluZT0wfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="firstline=0|language=javascript|linenumbers=true" data-macro-name="code">
<h4>Hard Braking Report</h4>
<p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1qYXZhc2NyaXB0fGZpcnN0bGluZT0wfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="firstline=0|language=javascript|linenumbers=true" data-macro-name="code">
<h4>Hard Cornering Report</h4>
<p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1qYXZhc2NyaXB0fGZpcnN0bGluZT0wfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="firstline=0|language=javascript|linenumbers=true" data-macro-name="code">
<h4>
<p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1qYXZhc2NyaXB0fGZpcnN0bGluZT0wfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="firstline=0|language=javascript|linenumbers=true" data-macro-name="code">
<h4>Overspeeding Report</h4>
<p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1qYXZhc2NyaXB0fGZpcnN0bGluZT0wfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="firstline=0|language=javascript|linenumbers=true" data-macro-name="code">
<h4>Parking Brake Drag Report</h4>
<p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1qYXZhc2NyaXB0fGZpcnN0bGluZT0wfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="firstline=0|language=javascript|linenumbers=true" data-macro-name="code">
<h4>Seatbelt Not Used Report</h4>
<p>An object representing a seatbelt not in use report.</p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1qYXZhc2NyaXB0fGZpcnN0bGluZT0wfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="firstline=0|language=javascript|linenumbers=true" data-macro-name="code">
<h4>
<p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1qYXZhc2NyaXB0fGZpcnN0bGluZT0wfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="firstline=0|language=javascript|linenumbers=true" data-macro-name="code">
<h4>Vehicle Health Report</h4>
<p>An object representing a vehicle health report.</p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1qYXZhc2NyaXB0fGZpcnN0bGluZT0wfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="firstline=0|language=javascript|linenumbers=true" data-macro-name="code">
<p>
<p>
<p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6dGhlbWU9Q29uZmx1ZW5jZXxsaW5lbnVtYmVycz10cnVlfGxhbmd1YWdlPWphdmFzY3JpcHR8Zmlyc3RsaW5lPTB9&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="firstline=0|language=javascript|linenumbers=true|theme=Confluence" data-macro-name="code">
<h4>Location Object</h4>
<p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1qYXZhc2NyaXB0fGZpcnN0bGluZT0wfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="firstline=0|language=javascript|linenumbers=true" data-macro-name="code">
<h4>New Deployment Report</h4>
<p>
<h5>
<p>
<ol>
<li>
<li>Vehicle is turned on</li>
<li>CarmaLink connects to the ECU and retrieves the VIN (New Deployment)</li>
</ol>
<p>
<table class="wysiwyg-macro" data-macro-body-type="RICH_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e25vdGV9&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-name="note">
<p>
<table class="wysiwyg-macro" data-macro-body-type="PLAIN_TEXT" style="background-image: url(/plugins/servlet/confluence/placeholder/macro-heading?definition=e2NvZGU6bGluZW51bWJlcnM9dHJ1ZXxsYW5ndWFnZT1qYXZhc2NyaXB0fGZpcnN0bGluZT0wfQ&locale=en_GB&version=2); background-repeat: no-repeat;" data-macro-parameters="firstline=0|language=javascript|linenumbers=true" data-macro-name="code">
<div class="layoutArea">
<div class="layoutArea">
<p>SAE J1979</p>
<p>SAE J2012</p>
<p> </p>
</body>
</html>
