### Symfony 5.1.2

**Endpoint**
```php
public function test(Request $request) {
  if($request->getContentType() === 'json') {
    $data = json_decode($request->getContent(), true);
```

**Source code** ([/symfony/symfony/src/Symfony/Component/HttpFoundation/Request.php](https://github.com/symfony/symfony/blob/27d84dbe57ce65203b26232b87e6660fdba2f30e/src/Symfony/Component/HttpFoundation/Request.php#L1316-L1332))
```php
public function getContentType() {
  return $this->getFormat($this->headers->get('CONTENT_TYPE'));
}

public function getFormat(?string $mimeType){
  $canonicalMimeType = null;
  if (false !== $pos = strpos($mimeType, ';')) {
    $canonicalMimeType = trim(substr($mimeType, 0, $pos));
  }
  ...
  foreach (static::$formats as $format => $mimeTypes) {
    if (\in_array($mimeType, (array) $mimeTypes)) {
      return $format;
    }
    if (null !== $canonicalMimeType && \in_array($canonicalMimeType, (array) $mimeTypes)) {
      return $format;
```

**JSON Content-Type**
```
application/json
application/x-json
```

**XML Content-Type**
```
text/xml
application/xml
application/x-xml
```

**HTTP Request**  
```http
POST /json HTTP/1.1
Host: localhost
Content-Type: application/x-json
Content-Length: 13

{"test":true}
```

**Multipart Content-Type**  
Same as [PHP](/ct-tricks/PHP.md)