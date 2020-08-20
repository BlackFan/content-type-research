### Express body-parser 1.19.0

**Endpoint**
```js
var bodyParser = require('body-parser')
var app = express()
app.use(bodyParser.json())

app.use(function (req, res) {
  data = req.body
```

**Source code** ([/jshttp/type-is/index.js](https://github.com/jshttp/type-is/blob/c1f4388c71c8a01f79934e68f630ca4a15fffcd6/index.js#L195-L227))
```js
function mimeMatch (expected, actual) {
  ...
  var actualParts = actual.split('/')
  var expectedParts = expected.split('/')
  ...
  if (expectedParts[0] !== '*' && expectedParts[0] !== actualParts[0]) {
    return false
  }
  ...
  if (expectedParts[1] !== '*' && expectedParts[1] !== actualParts[1]) {
    return false
  }
```

**JSON Content-Type**  
Strict parsing by default
```
application/json
```