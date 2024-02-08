* In 2020 ![EdgeHTML](https://black.fan/bl/edgehtml.php) was rebuilt as a ![Chromium](https://black.fan/bl/chromium.php)-based browser ![Edge](https://black.fan/bl/edge.php) and now has the same results as ![Chrome](https://black.fan/bl/chrome.php)

## Content-Type that can be used for XSS

**Conditions:**
 * X-Content-Type-Options: nosniff 

| Content-Type                  | Format         | Browsers | PoC |
|-------------------------------|----------------|----------|-----|
| text/html                     | html           | ![Chrome](https://black.fan/bl/chrome.php) ![Firefox](https://black.fan/bl/firefox.php) ![EdgeHTML](https://black.fan/bl/edgehtml.php) ![Safari](https://black.fan/bl/safari.php) | [link](https://blackfan.ru/mime-type/text-html.php) |
| application/xhtml+xml         | xml            | ![Chrome](https://black.fan/bl/chrome.php) ![Firefox](https://black.fan/bl/firefox.php) ![EdgeHTML](https://black.fan/bl/edgehtml.php) ![Safari](https://black.fan/bl/safari.php) | [link](https://blackfan.ru/mime-type/application-xhtml-xml.php) |
| application/xml               | xml            | ![Chrome](https://black.fan/bl/chrome.php) ![Firefox](https://black.fan/bl/firefox.php) ![EdgeHTML](https://black.fan/bl/edgehtml.php) ![Safari](https://black.fan/bl/safari.php) | [link](https://blackfan.ru/mime-type/application-xml.php) |
| text/xml                      | xml            | ![Chrome](https://black.fan/bl/chrome.php) ![Firefox](https://black.fan/bl/firefox.php) ![EdgeHTML](https://black.fan/bl/edgehtml.php) ![Safari](https://black.fan/bl/safari.php) | [link](https://blackfan.ru/mime-type/text-xml.php) |
| image/svg+xml                 | xml            | ![Chrome](https://black.fan/bl/chrome.php) ![Firefox](https://black.fan/bl/firefox.php) ![EdgeHTML](https://black.fan/bl/edgehtml.php) ![Safari](https://black.fan/bl/safari.php) | [link](https://blackfan.ru/mime-type/image-svg-xml.php) |
| text/xsl                      | xml            | ![Chrome](https://black.fan/bl/chrome.php) ![Safari](https://black.fan/bl/safari.php)        | [link](https://blackfan.ru/mime-type/text-xsl.php)                      |
| text/xsl **(UPD 2024)**       | html           | ![Chrome](https://black.fan/bl/chrome.php)                                                   | [link](https://blackfan.ru/mime-type/text-xsl-html.php)                 |
| application/vnd.wap.xhtml+xml | xml            | ![Firefox](https://black.fan/bl/firefox.php) ![Safari](https://black.fan/bl/safari.php)      | [link](https://blackfan.ru/mime-type/application-vnd-wap-xhtml-xml.php) |
| multipart/x-mixed-replace     | multipart html | ![Firefox](https://black.fan/bl/firefox.php) ![Safari](https://black.fan/bl/safari.php)      | [link](https://blackfan.ru/mime-type/multipart-x-mixed-replace.php)     |
| text/rdf                      | xml            | ![Firefox](https://black.fan/bl/firefox.php)                                             | [link](https://blackfan.ru/mime-type/text-rdf.php)                      |
| application/rdf+xml           | xml            | ![Firefox](https://black.fan/bl/firefox.php)                                             | [link](https://blackfan.ru/mime-type/application-rdf-xml.php)           |
| application/mathml+xml        | xml            | ![Firefox](https://black.fan/bl/firefox.php)                                             | [link](https://blackfan.ru/mime-type/application-mathml-xml.php)        |
| text/vtt                      | html           | ![EdgeHTML](https://black.fan/bl/edgehtml.php)                                           | [link](https://blackfan.ru/mime-type/text-vtt.php)                      |
| text/cache-manifest           | html           | ![EdgeHTML](https://black.fan/bl/edgehtml.php)                                           | [link](https://blackfan.ru/mime-type/text-cache-manifest.php)           |

## Response Content-Type Tricks

| Trick                 | Separators | Example                              | Browsers | PoC |
|-----------------------|------------|--------------------------------------|----------|-----|
| Multiple Content-Type | ,          | [Fetch Spec: Example Extract a Mime Type](https://fetch.spec.whatwg.org/#example-extract-a-mime-type)<br>Content-Type: text/plain; x=x, text/html, foobar | ![Chrome](https://black.fan/bl/chrome.php) ![Firefox](https://black.fan/bl/firefox.php)                                | [link](https://blackfan.ru/mime-type/multiple-content-type.php) |
| Mime-type separators  | 0x09 (     | Content-Type: text/html(xxx          | ![Chrome](https://black.fan/bl/chrome.php) ![Firefox](https://black.fan/bl/firefox.php)                                            | [0x09](https://blackfan.ru/mime-type/0x09-content-type.php) [0x28](https://blackfan.ru/mime-type/0x28-content-type.php) |
| Mime-type separators  | 0x20       | Content-Type: text/html xxx          | ![Chrome](https://black.fan/bl/chrome.php) ![Firefox](https://black.fan/bl/firefox.php) ![EdgeHTML](https://black.fan/bl/edgehtml.php) | [0x20](https://blackfan.ru/mime-type/0x20-content-type.php) |
| Mime-type separators  | , ;        | Content-Type: text/html,xxx          | ![Chrome](https://black.fan/bl/chrome.php) ![Firefox](https://black.fan/bl/firefox.php) ![EdgeHTML](https://black.fan/bl/edgehtml.php) ![Safari](https://black.fan/bl/safari.php) | [0x2C](https://blackfan.ru/mime-type/0x2C-content-type.php) |
