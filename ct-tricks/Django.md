### Django 3.1

**Endpoint**
```py
data = json.loads(request.body)
```

**JSON Content-Type**  
Doesn't have built-in Content-Type checking functionality, attacker can use `application/x-www-form-urlencoded` Content-Type with JSON body.