### CherryPy 18.6.0

**Endpoint**
```py
@cherrypy.expose
def index(self, *args, **kwargs):
  data = cherrypy.request.params

@cherrypy.expose
@cherrypy.tools.json_in()
def index(self, *args, **kwargs):
  data = cherrypy.request.json
```

**Source code**  
[/cherrypy/cherrypy/cherrypy/_cpreqbody.py](https://github.com/cherrypy/cherrypy/blob/05ee11a96940817e471cce3675ac1fb1810f11e8/cherrypy/_cpreqbody.py#L392-L395)
```py
processors = {'application/x-www-form-urlencoded': process_urlencoded,
              'multipart/form-data': process_multipart_form_data,
              'multipart': process_multipart,
```
[/cherrypy/cherrypy/cherrypy/lib/jsontools.py](https://github.com/cherrypy/cherrypy/blob/05ee11a96940817e471cce3675ac1fb1810f11e8/cherrypy/lib/jsontools.py#L16)
```py
def json_in(content_type=[ntou('application/json'), ntou('text/javascript')],
```

**Content-Type**
```
application/x-www-form-urlencoded
multipart/form-data
multipart
```

**Multipart Content-Type**
| Check             | Value            |
|-------------------|------------------|
| Mime-Type         | case-sensitive   |
| Multiple boundary | last position    |
| Boundary key      | case-insensitive |

**HTTP Request**
```http
POST / HTTP/1.1
Host: localhost
Content-Type: multipart; boundary=yyy; BoUndary=xxx
Content-Length: 67

--xxx
Content-Disposition: form-data; name="test"

test
--xxx--
```

**JSON Content-Type**
```
application/json
text/javascript
```

**HTTP Request**
```http
POST / HTTP/1.1
Host: localhost
Content-Type: text/javascript
Content-Length: 13

{"test":true}
```