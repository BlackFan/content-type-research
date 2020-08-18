## Content-Type that can be used for XSS

**Conditions:**
 * X-Content-Type-Options: nosniff 

| Content-Type                  | Format         | Browsers | PoC |
|-------------------------------|----------------|----------|-----|
| text/html                     | html           | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) | x   |
| application/xhtml+xml         | xml            | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) | x   |
| application/xml               | xml            | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) | x   |
| text/xml                      | xml            | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) | x   |
| image/svg+xml                 | xml            | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) | x   |
| text/xsl                      | xml            | ![Chrome](https://black.fan/bl/chrome)                                                                                     | x   |
| text/rdf                      | xml            | ![Firefox](https://black.fan/bl/firefox)                                                                                   | x   |
| application/rdf+xml           | xml            | ![Firefox](https://black.fan/bl/firefox)                                                                                   | x   |
| application/vnd.wap.xhtml+xml | xml            | ![Firefox](https://black.fan/bl/firefox)                                                                                   | x   |
| application/mathml+xml        | xml            | ![Firefox](https://black.fan/bl/firefox)                                                                                   | x   |
| multipart/x-mixed-replace     | multipart html | ![Firefox](https://black.fan/bl/firefox)                                                                                   | x   |
| text/vtt                      | html           | ![EdgeHTML](https://black.fan/bl/edgehtml)                                                                                 | x   |
| text/cache-manifest           | html           | ![EdgeHTML](https://black.fan/bl/edgehtml)                                                                                 | x   |

## Content-Type Tricks

| Trick                 | Separators | Example                              | Browsers | PoC |
|-----------------------|------------|--------------------------------------|----------|-----|
| Multiple Content-Type | ,          | Content-Type: text/plain;, text/html | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) | x  |
| Mime-type separators  | \t \s ( , ;| Content-Type: text/html(xxx          | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) | x  |