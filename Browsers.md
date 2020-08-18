* In 2020 ![EdgeHTML](https://black.fan/bl/edgehtml) was rebuilt as a ![Chromium](https://black.fan/bl/chromium)-based browser ![Edge](https://black.fan/bl/edge) and now has the same results as ![Chrome](https://black.fan/bl/chrome)

## Request Content-Type Tricks

**HTTP Request Content-Type separators (without preflight request)**

| Separators | Browsers | Example  |
|------------|----------|----------|
| ;          | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) ![Safari](https://black.fan/bl/safari) | Content-Type: text/plain;xxx |
| ,          | ![EdgeHTML](https://black.fan/bl/edgehtml) | Content-Type: text/plain,xxx |

**Allowed symbols in Content-Type options (without preflight request)**

| Symbol     | Browsers | Example  |
|------------|----------|----------|
| 0x01-0x08 0x0E-0x1F : < > ? @ [ \ ] { } 0x7F | ![EdgeHTML](https://black.fan/bl/edgehtml) | Content-Type: text/plain;&lt;xxx |
| 0x09 0x20 ! # $ % & ' * + - . / 0-9 ; = A-Z ^ _ \` a-z \| ~ | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) ![Safari](https://black.fan/bl/safari) | Content-Type: text/plain;#xxx |
| , 0x80-0xFF | ![Chrome](https://black.fan/bl/chrome) ![EdgeHTML](https://black.fan/bl/edgehtml) ![Safari](https://black.fan/bl/safari) | Content-Type: text/plain;,xxx |

**Fetch → headers**

```
fetch("https://victim.tld/", {
  method: 'POST',
  body: 'TEST', 
  headers: {
    'Content-Type': '$Content-Type$'
  }
});
```

:heavy_minus_sign: - CORS preflight request

| Content-Type | ![Chrome](https://black.fan/bl/chrome) | ![Firefox](https://black.fan/bl/firefox) | ![EdgeHTML](https://black.fan/bl/edgehtml) | ![Safari](https://black.fan/bl/safari) |
|--------------|----------------------------------------|------------------------------------------|--------------------------------------------|----------------------------------------|
| text/plain | text/plain | text/plain | text/plain | text/plain |
| TEXT/PLAIN | TEXT/PLAIN | TEXT/PLAIN | TEXT/PLAIN | TEXT/PLAIN |
| text/plain; x=x | text/plain; x=x | text/plain; x=x | text/plain; x=x | text/plain; x=x |
| text/plain; x="x" | :heavy_minus_sign: | :heavy_minus_sign: | text/plain; x="x" | :heavy_minus_sign: |
| text/plain; application/json | text/plain; application/json | text/plain; application/json | text/plain; application/json | text/plain; application/json |
| text/plain;, application/json | text/plain;, application/json | :heavy_minus_sign: | text/plain;, application/json | text/plain;, application/json |
| text/plain;, application/json, text/plain | text/plain;, application/json, text/plain | :heavy_minus_sign: | text/plain;, application/json, text/plain | text/plain;, application/json, text/plain |
| application/json;, text/plain | :heavy_minus_sign: | :heavy_minus_sign:<br>[CVE-2015-7193](https://www.mozilla.org/en-US/security/advisories/mfsa2015-127/) | :heavy_minus_sign: | :heavy_minus_sign: |