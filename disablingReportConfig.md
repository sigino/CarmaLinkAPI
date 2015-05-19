<h2>Disabling a report configuration</h2>  
Any report you don't want the transponder to run anymore can be deactivated using the DELETE method on the respective report configuration URI. No body should be included, but the header should have Content-Type: application/json. Successful deactivation requests will return an HTTP status code 204. This status code is also returned if a resource is already deactivated, or a configuration was never created for this report.  

Contrary to the standard implications of this method, it does not actually delete any data on the server. Instead, on a read-back of the report's configuration, you will see the status change to 'PENDING_DEACTIVATION', and then 'DEACTIVATED' when the transponder receives the request. Deactivating a report will also automatically disable the buzzer for that report.  

Deactivating a report will also automatically disable the buzzer for that report. If you just want to disable the buzzer for the configuration, see Buzzer Configuration.  

To re-enable a report, simply use the PUT method on the report's configuration URI with a Content-Type: application/json and an empty JSON object in the request body. If this report supports a buzzer configuration, it is recommended that you also include the previous valid buzzer volume.  

[:fast_forward: Next Section: Changing an existing report configuration](/changingExistingConfig.md)
