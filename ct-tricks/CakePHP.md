### CakePHP 4.0.9

**Endpoint**
```php
$data = $this->request->input('json_decode');
```

**Source code** ([/cakephp/cakephp/src/Http/ServerRequest.php](https://github.com/cakephp/cakephp/blob/b5c17f7a8aa20a0334b7689a90b1fd9383783bed/src/Http/ServerRequest.php#L1279-L1291))
```php
public function input(?callable $callback = null, ...$args)
{
  $this->stream->rewind();
  $input = $this->stream->getContents();
  if ($callback) {
    array_unshift($args, $input);
    return call_user_func_array($callback, $args);
```

**JSON Content-Type**  
Doesn't have built-in Content-Type checking functionality, attacker can use `application/x-www-form-urlencoded` Content-Type with JSON body.

**Multipart Content-Type**  
Same as [PHP](ct-tricks/PHP.md)