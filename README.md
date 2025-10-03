# How to detect what browser you're using
Without user agent

## 1. The syntax error method
```js
try {
    eval("(function if(){ var const i = 0 -1 **4/t\\\\\\ }[(//\\.3\@[1/g)]})!!");
} catch (error) {
    String(error);
}
```

Different browser engines return different strings.

Chromium/Blink:
```yaml
SyntaxError: Unexpected token 'if'
```

Gecko/Servo:
```yaml
SyntaxError: missing ( before formal parameters
```

Trident:
```yaml
SyntaxError: The use of a keyword for an identifier is invalid
```
(IE10/11)
```yaml
SyntaxError: expected '('
```
(IE8/9)
```yaml
[object Error]
```
(IE7 and below)

## 2. The ActiveXObject method.
If you see ActiveXObject, you're most likely on IE or old Opera. IE11 hides the API a bit, so you can use this trick to detect IE11.
```js
String(window.ActiveXObject).indexOf('function ActiveXObject') > -1 && typeof window.ActiveXObject === 'undefined' && (window.ActiveXObject == undefined && window.ActiveXObject !== undefined)
```