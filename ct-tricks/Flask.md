### Flask 1.1.2

**Endpoint**
```py
@app.route('/', methods=['POST'])
def test():
  if request.is_json:
    data = request.get_json()
```

**Source code**  
[/pallets/werkzeug/src/werkzeug/wrappers/json.py](https://github.com/pallets/werkzeug/blob/88457c5ffde7f494fa029c05cb576274cf2b20e7/src/werkzeug/wrappers/json.py#L56-L65)
```py
def is_json(self):
  ...
  mt = self.mimetype
  return (mt == "application/json"
            or mt.startswith("application/") and mt.endswith("+json"))
```
[/pallets/werkzeug/src/werkzeug/http.py](https://github.com/pallets/werkzeug/blob/88457c5ffde7f494fa029c05cb576274cf2b20e7/src/werkzeug/http.py#L98)
```py
_option_header_start_mime_type = re.compile(r",\s*([^;,\s]+)([;,]\s*.+)?")
...
def parse_options_header(value: Optional[str], multiple: bool = False) -> Any:
  ...
  match = _option_header_start_mime_type.match(value)
  ...
  rest = match.group(2)
  ...
  optmatch = _option_header_piece_re.match(rest)
  ...
  option, count, encoding, language, option_value = optmatch.groups()
  ...
  option = unquote_header_value(option)
    if option_value is not None:
      option_value = unquote_header_value(option_value, option == "filename")
```

**JSON Content-Type**
```
application/json
application/XXX+json
application/json,XXX
application/json XXX
```

**HTTP Request**
```http
POST / HTTP/1.1
Host: localhost
Content-Type: application/XXX+json
Content-Length: 13

{"test":true}
```

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
| Boundary key      | case-sensitive   |

**HTTP Request**  
Quotes in key are supported, can be used to hide attack payload from WAF.
```http
POST / HTTP/1.1
Host: localhost
Content-Type: multipart/form-data; boundary=yyy; "boundary"=xxx
Content-Length: 69

--xxx
Content-Disposition: form-data; name="test"

test
--xxx--
```