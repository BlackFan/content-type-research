# Content-Type Research

## XSS

[Content-Type that can be used for XSS and some related tricks](XSS.md)

## CSRF

> **All frameworks were analyzed with disabled default token-based CSRF protection**

Examples of incorrect Content-Type parsing that can be used for CSRF.  
For example, the ability to send an HTTP request that will be interpreted as JSON without a CORS preflight request.  
Can be used in combination with attacks requiring boolean or array in HTTP request (PHP Type Juggling, NoSQL Injection, Prototype Pollution, ...)

**Interesting results**
 * [Difference of Content-Type processing in browsers](Browsers.md)
 * [Laravel JSON Content-Type parsing](ct-tricks/Laravel.md)
 * [Laminas, Mezzio, Zend Framework JSON Content-Type parsing](ct-tricks/Mezzio.md)
 * [Wordpress JSON Content-Type parsing](ct-tricks/Wordpress.md)

## WAF Bypass

### Basic Idea

| HTTP Request                                                                                      | Application         | WAF                                   | Result                     |
|---------------------------------------------------------------------------------------------------|---------------------|---------------------------------------|----------------------------|
| Content-Type: application/x-www-form-urlencoded<br><br>q=' union select '1                        | ' union select 1'   | ' union select 1'                     | :heavy_minus_sign: Blocked |
| Content-Type: application/json<br><br>{"q":"' \u0075nion \u0073elect '1"}                         | ' union select 1'   | ' union select 1'                     | :heavy_minus_sign: Blocked |
| Content-Type: application/x-www-form-urlencoded;/json<br><br>{"q":"' \u0075nion \u0073elect '1"}  | ' union select 1'   | {"q":"' \u0075nion \u0073elect '1"}   | :heavy_check_mark: Bypass  |

**Interesting results**
 * [PHP multipart boundary parsing](ct-tricks/PHP.md)
 * [Laravel JSON Content-Type parsing](ct-tricks/Laravel.md)
 * [Symfony JSON/XML Content-Type parsing](ct-tricks/Symfony.md)
 * [Laminas, Mezzio, Zend Framework JSON Content-Type parsing](ct-tricks/Mezzio.md)
 * [Flask JSON Content-Type parsing](ct-tricks/Flask.md)
 * [CherryPy multipart & JSON Content-Type parsing](ct-tricks/CherryPy.md)

## Programming languages / Frameworks

| Name | CSRF friendly | WAF Bypass friendly |
|------|---------------|---------------------|
| [PHP](ct-tricks/PHP.md)                                   |                    | :heavy_check_mark: |
| [Laravel](ct-tricks/Laravel.md)                           | :heavy_check_mark: | :heavy_check_mark: |
| [Symfony](ct-tricks/Symfony.md)                           |                    | :heavy_check_mark: |
| [Laminas, Mezzio, Zend](ct-tricks/Mezzio.md)              | :heavy_check_mark: | :heavy_check_mark: |
| [Yii](ct-tricks/Yii.md)                                   | :question:         |                    |
| [Wordpress](ct-tricks/Wordpress.md)                       | :question:         | :question:         |
| [CakePHP](ct-tricks/CakePHP.md)                           | :question:         | :question:         |
| [CodeIgniter](ct-tricks/CodeIgniter.md)                   | :question:         | :question:         |
| [Django](ct-tricks/Django.md)                             | :question:         | :heavy_check_mark: |
| [Flask](ct-tricks/Flask.md)                               |                    | :heavy_check_mark: |
| [CherryPy](ct-tricks/CherryPy.md)                         |                    | :heavy_check_mark: |
| [Express body-parser](ct-tricks/Express_body-parser.md)   |                    |                    |
| [Express multer](ct-tricks/Express_multer.md)             |                    | :heavy_check_mark: |
