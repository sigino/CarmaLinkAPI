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
##### Python 2.X and Python 3.X Example  
```python  
# Utilizes Requests, an Apache2 Licensed HTTP library for python
# http://docs.python-requests.org

# to install for python 3:
# $ pip3 install requests
# $ pip3 install requests_oauthlib

# to instal for python 2.X:
# $ pip install requests
# $ pip install requests_oauthlib

# if you are using a version of python earlier than python 2.7.9,
# or receive an InsecurePlatformWarning, you will require the following :

# $ pip install pyopenssl ndg-httpsclient pyasn1
#import urllib3.contrib.pyopenssl
#urllib3.contrib.pyopenssl.inject_into_urllib3()

# End of python < v2.7.9 only

import requests
from requests_oauthlib import OAuth1

  #url information...
HOST = 'api.carmalink.com'
PORT = 8282
SERIAL_NUMBER = 204
RESOURCE_PATH = '/v1/%i/report_config/trip_report' %(SERIAL_NUMBER)
PROTOCOL = 'https://'

  #oauth tokens
CONSUMER_KEY = 'JiYmll7CX3AXDgasnnIDeg'
CONSUMER_SECRET = 'mWPBRK5kG2Tkthuf5zRV1jYWOEwnjI6xs3QVRqOOg'
  #We do not require these, as it is a 0 legged approach
USER_OAUTH_TOKEN = None
USER_OAUTH_TOKEN_SECRET = None

  #form url
url = "%s%s%s%s" %(PROTOCOL, HOST, (":%i" % PORT if not(PORT is None) else ""), RESOURCE_PATH)

  #generate auth token for requests
oauth_auth = OAuth1(CONSUMER_KEY, CONSUMER_SECRET)

result = requests.get(url, auth = oauth_auth)

print result.status_code
print result.text
object = result.json()  
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
