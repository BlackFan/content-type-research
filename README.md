# Content-Type Research

## XSS

[Content-Type that can be used for XSS and some related tricks](XSS.md)

## CSRF

Examples of incorrect Content-Type parsing that can be used for CSRF.  
For example, the ability to send an HTTP request that will be interpreted as JSON without a CORS preflight request.  
Can be used in combination with attacks requiring boolean or array in HTTP request (PHP Type Juggling, NoSQL Injection, Prototype Pollution, ...)

 * [Difference of Content-Type processing in browsers](Browsers.md)
 * [Laravel JSON parsing](ct-tricks/Laravel.md)
 * [Laminas, Mezzio, Zend Framework JSON parsing](ct-tricks/Mezzio.md)

## WAF Bypass

### Basic Idea

| HTTP Request                                                                                          | Application                        | WAF                                                | Result                     |
|-------------------------------------------------------------------------------------------------------|------------------------------------|----------------------------------------------------|----------------------------|
| `Content-Type: application/x-www-form-urlencoded`<br><br>`q=' union select '1`                        | ' union select 1'                  | ' union select 1'                                  | :heavy_minus_sign: Blocked |
| `Content-Type: application/json`<br><br>`{"q":"' \u0075nion \u0073elect '1"}`                         | ' union select 1'                  | ' union select 1'                                  | :heavy_minus_sign: Blocked |
| `Content-Type: application/x-www-form-urlencoded;/json`<br><br>`{"q":"' \u0075nion \u0073elect '1"}`  | ' union select 1'                  | {"q":"' \u0075nion \u0073elect '1"}                | :heavy_check_mark: Bypass  |

 * [PHP boundary parsing](ct-tricks/PHP.md)
 * [Laravel JSON parsing](ct-tricks/Laravel.md)
 * [Laminas, Mezzio, Zend Framework JSON parsing](ct-tricks/Mezzio.md)

## Frameworks
