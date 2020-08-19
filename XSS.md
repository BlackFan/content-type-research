* In 2020 ![EdgeHTML](https://black.fan/bl/edgehtml) was rebuilt as a ![Chromium](https://black.fan/bl/chromium)-based browser ![Edge](https://black.fan/bl/edge) and now has the same results as ![Chrome](https://black.fan/bl/chrome)

## Content-Type that can be used for XSS

**Conditions:**
 * X-Content-Type-Options: nosniff 

| Content-Type                  | Format         | Browsers | PoC |
|-------------------------------|----------------|----------|-----|
| text/html                     | html           | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) ![Safari](https://black.fan/bl/safari) | x   |
| application/xhtml+xml         | xml            | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) ![Safari](https://black.fan/bl/safari) | x   |
| application/xml               | xml            | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) ![Safari](https://black.fan/bl/safari) | x   |
| text/xml                      | xml            | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) ![Safari](https://black.fan/bl/safari) | x   |
| image/svg+xml                 | xml            | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) ![Safari](https://black.fan/bl/safari) | x   |
| text/xsl                      | xml            | ![Chrome](https://black.fan/bl/chrome) ![Safari](https://black.fan/bl/safari)                                                                                     | x   |
| application/vnd.wap.xhtml+xml | xml            | ![Firefox](https://black.fan/bl/firefox) ![Safari](https://black.fan/bl/safari)                                                                                   | x   |
| multipart/x-mixed-replace     | multipart html | ![Firefox](https://black.fan/bl/firefox) ![Safari](https://black.fan/bl/safari)                                                                                   | x   |
| text/rdf                      | xml            | ![Firefox](https://black.fan/bl/firefox)                                                                                                                          | x   |
| application/rdf+xml           | xml            | ![Firefox](https://black.fan/bl/firefox)                                                                                                                          | x   |
| application/mathml+xml        | xml            | ![Firefox](https://black.fan/bl/firefox)                                                                                                                          | x   |
| text/vtt                      | html           | ![EdgeHTML](https://black.fan/bl/edgehtml)                                                                                                                        | x   |
| text/cache-manifest           | html           | ![EdgeHTML](https://black.fan/bl/edgehtml)                                                                                                                        | x   |

## Response Content-Type Tricks

| Trick                 | Separators | Example                              | Browsers |
|-----------------------|------------|--------------------------------------|----------|
| Multiple Content-Type | ,          | Content-Type: text/plain;, text/html | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox)                                            |
| Mime-type separators  | 0x09 (     | Content-Type: text/html(xxx          | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox)                                            |
| Mime-type separators  | 0x20       | Content-Type: text/html xxx          | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) |
| Mime-type separators  | , ;        | Content-Type: text/html,xxx          | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) ![Safari](https://black.fan/bl/safari) |