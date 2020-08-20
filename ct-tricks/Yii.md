### Yii 2.0.35

**Endpoint**
```php
$config = ['components' => ['request' => ['parsers' => ['application/json' => 'yii\web\JsonParser'

public function actionIndex() {
    $data = Yii::$app->getRequest();
```

**Source code** ([/yiisoft/yii2/framework/web/Request.php](https://github.com/yiisoft/yii2/blob/175a20100496b46952f0226385880d17d0ed5cbb/framework/web/Request.php#L551-L573))
```php
public function getBodyParams() {
  ...
  $rawContentType = $this->getContentType();
  if (($pos = strpos($rawContentType, ';')) !== false) {
    $contentType = substr($rawContentType, 0, $pos);
  ...
  if (isset($this->parsers[$contentType])) {
    $parser = Yii::createObject($this->parsers[$contentType]);
    ...
    $this->_bodyParams = $parser->parse($this->getRawBody(), $rawContentType);
  ...
  } elseif ($this->getMethod() === 'POST') {
    $this->_bodyParams = $_POST;
```

**JSON Content-Type**
```
application/json;XXX
```

**CSRF**  
Without additional checks, an attacker can change `application/json` requests to `application/x-www-form-urlencoded` body encoding

**Multipart Content-Type**  
Same as [PHP](/ct-tricks/PHP.md)