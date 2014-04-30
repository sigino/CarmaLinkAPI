# Deleting Configurations  
All CarmaLink configurations can be deleted via a DELETE request to the API. For example, you have configured an overspeeding event to occur on a CarmaLink at 75mph, but now you want to delete it from the CarmaLink.  

**Input**  
```javascript  
curl -i -X DELETE https://api.carmalink.com:8282/v1/150/report_config/overspeeding/  
```

**Output**  
```javascript  
HTTP/1.1 204 No Content  
Date: Wed, 05 Sep 2012 15:06:02 GMT  
```  

*Success!*
