### CodeIgniter 4.0.3

**Endpoint**
```php
public function index() {
  $data = $this->request->getJSON();
```

**Source code** ([/codeigniter4/CodeIgniter4/system/HTTP/IncomingRequest.php](https://github.com/codeigniter4/CodeIgniter4/blob/6da204ce23f239b3c8f54530f8f0994bd27d80dd/system/HTTP/IncomingRequest.php#L361-L363))
```php
public function getJSON(bool $assoc = false, int $depth = 512, int $options = 0) {
  return json_decode($this->body, $assoc, $depth, $options);
```

**JSON Content-Type**  
Doesn't have built-in Content-Type checking functionality, attacker can use `application/x-www-form-urlencoded` Content-Type with JSON body.