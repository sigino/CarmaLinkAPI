## 4. Authentication & permissions  

### Authentication  
OAuth is the method used for parties to verify each other's identity. The OAuth 1.0a specification can be found at [RFC 5849](http://tools.ietf.org/html/rfc5849).  

### Permissions  
API users are assigned an apiKey and secretKey pair, allowing access to their range of the transponder uniquely assigned serial numbers. Note: a transponder is owned by one user that is accessible with one api/secret key pair, and an API request made referencing a serial number not belonging to the user results in an error code being returned.

### OAuth 1.0a  
We suggest obtaining a good OAuth 1.0a library for the development environment you plan to use. The official OAuth site [maintains a repository of libraries for various languages](http://oauth.googlecode.com/svn/) along with a general listing of [external open source initiatives](http://oauth.net/code/). You will need to make sure that the library you choose supports OAuth 1.0a and the GET/PUT/DELETE HTTP verbs as well as sending and receiving JSON-encoded content.  

The API does not use two or three legged authentication, so there is no need for any kind of access or request tokens from the server. You will simply need to properly sign the request by including the "Authorization:" HTTP 1.1 header. Here is a sample of what that header should look like when sent:  

##### HTTP 1.1 Header  
```javascript  
Authorization: OAuth oauth_consumer_key="JiYm4l74tXddzz4snnIDeg",oauth_nonce="976cd77d0b33b524417f9f44884b7f00",oauth_signature_method="HMAC-SHA1",oauth_timestamp="1348260490",oauth_version="1.0",oauth_signature="XG%2FBcoKd0S2eNUNeJCCof%2BI8bxI%3D"  
```
--  
##### Ruby Example  
```ruby  
#!/usr/bin/env ruby -rubygems
# gem install oauth
 
require 'oauth'
require 'json'
 
consumer = OAuth::Consumer.new("JiYmll7CX3AXDgasnnIDeg","mWPBRK5kG2Tkthuf5zRV1jYWOEwnjI6xs3QVRqOOg")
response = consumer.request(:get,'https://api.carmalink.com:8282/v1/204/data/trip_report')
 
print response.body  
```
--
##### Python Example  
```python  
# Utilizes Leah Culver's OAuth library
# http://oauth.googlecode.com/svn/code/python/
# to install: $ easy_install oauth
 
import httplib
import oauth.oauth as oauth
 
CONSUMER_KEY = 'JiYmll7CX3AXDgasnnIDeg'
CONSUMER_SECRET = 'mWPBRK5kG2Tkthuf5zRV1jYWOEwnjI6xs3QVRqOOg'
HOST = 'api.carmalink.com'
PORT = 8282
PROTOCOL = 'https://'
RESOURCE_PATH = '/v1/204/data/trip_report'
NULL_TOKEN = None
RESOURCE_URL = PROTOCOL + HOST + ':' + str(PORT) + RESOURCE_PATH
 
# example client using httplib with headers
class SimpleOAuthClient(oauth.OAuthClient):
    def __init__(self, server, port=httplib.HTTP_PORT):
        self.server = server
        self.port = port
        self.connection = httplib.HTTPSConnection("%s:%d" % (self.server, self.port))
    def access_resource(self, oauth_request):
        print 'OAuth Header : %s' % str(oauth_request.to_header())
        self.connection.request('GET',RESOURCE_PATH,headers=oauth_request.to_header())
        response = self.connection.getresponse()
        return response.read()
 
 
client = SimpleOAuthClient(HOST, PORT)
consumer = oauth.OAuthConsumer(CONSUMER_KEY, CONSUMER_SECRET)
signature_method_hmac_sha1 = oauth.OAuthSignatureMethod_HMAC_SHA1()
oauth_request = oauth.OAuthRequest.from_consumer_and_token(consumer, token=NULL_TOKEN, http_method='GET', http_url=RESOURCE_URL)
oauth_request.sign_request(signature_method_hmac_sha1, consumer, NULL_TOKEN)
result = client.access_resource(oauth_request)
 
print 'response: %s' % str(result)  
```
--
##### PHP Example  
```php
<?php
define('CONSUMER_KEY','JiYmll7CX3AXDgasnnIDeg');
define('CONSUMER_SECRET','mWPBRK5kG2Tkthuf5zRV1jYWOEwnjI6xs3QVRqOOg');
define('HOST','api.carmalink.com');
define('PROTOCOL','https://');
define('PORT',8282);
define('RESOURCE_PATH','/v1/204/data/trip_report');
 
$oauth = new OAuth(CONSUMER_KEY,CONSUMER_SECRET);
$oauth->fetch(PROTOCOL.HOST.':'.PORT.RESOURCE_PATH,null,OAUTH_HTTP_METHOD_GET)
$response = $oauth->getLastResponse();
print_r($response);
```  

[:fast_forward: Next Section: 5. Revision History](/5revisionHistory.md)
