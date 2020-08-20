* In 2020 ![EdgeHTML](https://black.fan/bl/edgehtml) was rebuilt as a ![Chromium](https://black.fan/bl/chromium)-based browser ![Edge](https://black.fan/bl/edge) and now has the same results as ![Chrome](https://black.fan/bl/chrome)

## Content-Type in cross origin requests

Browsers can send a cross origin request without `OPTIONS` preflight only for safe requests.  
CORS-safelisted methods: `GET`, `HEAD`, `POST`  
CORS-safelisted request-headers: `Accept`, `Accept-Language`, `Content-Language`, `Content-Type`  
CORS-safelisted content-types: `application/x-www-form-urlencoded`, `multipart/form-data`, `text/plain`  

## Request Content-Type Tricks

### HTTP Request Content-Type separators (without preflight request)

| Separators | Browsers | Example  |
|------------|----------|----------|
| ;          | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) ![Safari](https://black.fan/bl/safari) | Content-Type: text/plain;xxx |
| ,          | ![EdgeHTML](https://black.fan/bl/edgehtml) | Content-Type: text/plain,xxx |

### Allowed symbols in Content-Type options (without preflight request)

| Symbol     | Browsers | Example  |
|------------|----------|----------|
| [Fetch Spec: CORS-unsafe request-header byte](https://fetch.spec.whatwg.org/#cors-unsafe-request-header-byte)<br>0x01-0x08 0x0E-0x1F : < > ? @ [ \ ] { } 0x7F | ![EdgeHTML](https://black.fan/bl/edgehtml) | Content-Type: text/plain;&lt;xxx |
| 0x09 0x20 ! # $ % & ' * + - . / 0-9 ; = A-Z ^ _ \` a-z \| ~ | ![Chrome](https://black.fan/bl/chrome) ![Firefox](https://black.fan/bl/firefox) ![EdgeHTML](https://black.fan/bl/edgehtml) ![Safari](https://black.fan/bl/safari) | Content-Type: text/plain;#xxx |
| , 0x80-0xFF | ![Chrome](https://black.fan/bl/chrome) ![EdgeHTML](https://black.fan/bl/edgehtml) ![Safari](https://black.fan/bl/safari) | Content-Type: text/plain;,xxx |

### fetch, XMLHttpRequest headers

```js
fetch("http://localhost/", {
  method: "POST", 
  headers: {
    "Content-Type": "$Content-Type$"
  }
  credentials: "include",
  body: "test"
});
```

```js
xhr = new XMLHttpRequest();
xhr.open("POST", "http://localhost/", true);
xhr.setRequestHeader("Content-Type", "$Content-Type$");
xhr.withCredentials = true;
xhr.send("test");
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

### sendBeacon, fetch, XMLHttpRequest blob

```js
ct = '$Content-Type$';
blob = new Blob(["test"], {type: ct});

fetch("http://localhost/", { 
  method: 'POST', 
  credentials: "include",
  body: blob 
});

navigator.sendBeacon("http://localhost/", blob);

xhr = new XMLHttpRequest();
xhr.open("POST", "http://localhost/", true);;
xhr.withCredentials = true;
xhr.send(blob);
```

:heavy_minus_sign: - CORS preflight request

| Content-Type | ![Chrome](https://black.fan/bl/chrome) | ![Firefox](https://black.fan/bl/firefox) | ![EdgeHTML](https://black.fan/bl/edgehtml) | ![Safari](https://black.fan/bl/safari) |
|--------------|----------------------------------------|------------------------------------------|--------------------------------------------|----------------------------------------|
| text/plain | text/plain | text/plain | text/plain | text/plain |
| TEXT/PLAIN | text/plain | text/plain | text/plain | text/plain |
| text/plain; x=x | text/plain; x=x | text/plain; x=x | text/plain; x=x | text/plain; x=x |
| text/plain; x="x" | :heavy_minus_sign: | :heavy_minus_sign: | text/plain; x="x" | :heavy_minus_sign: |
| text/plain; application/json | fetch: text/plain; application/json<br>sendBeacon: without CT<br>xhr: without CT | text/plain; application/json | text/plain; application/json | text/plain; application/json |
| text/plain;, application/json | fetch: text/plain;, application/json<br>sendBeacon: without CT<br>xhr: without CT | :heavy_minus_sign: | text/plain;, application/json | text/plain;, application/json |
| text/plain;, application/json, text/plain | fetch: text/plain;, application/json, text/plain<br>sendBeacon: without CT<br>xhr: without CT | :heavy_minus_sign: | text/plain;, application/json, text/plain | text/plain;, application/json, text/plain |
| application/json;, text/plain | fetch: :heavy_minus_sign:<br>sendBeacon: without CT<br>xhr: without CT | :heavy_minus_sign: | :heavy_minus_sign: | :heavy_minus_sign: |

### fetch, XMLHttpRequest multiple Content-Type

```js
fetch("https://localhost/", {
  method: "POST",
  headers: [
    ["Content-Type", "text/plain"],
    ["Content-Type", "application/json"]
  ],
  credentials: "include",
  body: "test"
});
```

```js
xhr = new XMLHttpRequest();
xhr.open("POST", "https://localhost/", true);
xhr.setRequestHeader("Content-Type", "text/plain");
xhr.setRequestHeader("Content-Type", "application/json");
xhr.withCredentials = true;
xhr.send("test");
```

:heavy_minus_sign: - CORS preflight request

| Content-Type                      | ![Chrome](https://black.fan/bl/chrome) | ![Firefox](https://black.fan/bl/firefox) | ![EdgeHTML](https://black.fan/bl/edgehtml) | ![Safari](https://black.fan/bl/safari) |
|-----------------------------------|----------------------------------------|------------------------------------------|--------------------------------------------|----------------------------------------|
| text/plain<br>multipart/form-data | :heavy_minus_sign: | fetch: multipart/form-data<br>xhr: :heavy_minus_sign: | text/plain, multipart/form-data | :heavy_minus_sign: |
| text/plain<br>application/json    | :heavy_minus_sign: | :heavy_minus_sign:                                    | text/plain, application/json    | :heavy_minus_sign: |
| application/json<br>text/plain    | :heavy_minus_sign: | :heavy_minus_sign:                                    | :heavy_minus_sign:              | :heavy_minus_sign: |