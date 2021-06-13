# Warren Shea's Notes for JavaScript
v20191221

## IIFE - Immediate-invoked Function Expressions
To execute functions immediately, as soon as they are created
Don't pollute the global object, simple way to isolate variables declarations

```javascript
(function() {
  /* */
})()

(function doSomething() {
  /* */
})()

(() => {
  /* */
})()
```

## Vanilla JS IE11 Friendly AJAX Request
```javascript
Vanilla JS IE11 Friendly AJAX Requestfunction jsonp(uri) {
  return new Promise(function(resolve, reject) {
    var id = '_' + Math.round(10000 * Math.random());
    var callbackName = 'jsonp_callback_' + id;
    window[callbackName] = function(data) {
      delete window[callbackName];
      var ele = document.getElementById(id);
      ele.parentNode.removeChild(ele);
      resolve(data);
    }

    var src = uri + '&callback=' + callbackName;
    var script = document.createElement('script');
    script.src = src;
    script.id = id;
    script.addEventListener('error', reject);
    (document.getElementsByTagName('head')[0] || document.body || document.documentElement).appendChild(script)
  });
}

if (navigator.userAgent.toLowerCase().indexOf('msie') > -1 && window.XDomainRequest) {
  // Use Microsoft XDR
  var xdr = new XDomainRequest();
  xdr.open("get", url);
  xdr.onload = function() {
    // XDomainRequest doesn't provide responseXml, so if you need it:
    var dom = new ActiveXObject("Microsoft.XMLDOM");
    dom.async = false;
    dom.loadXML(xdr.responseText["data"][0]);
  };
  xdr.send();
} else {
  jsonp(url).then(function(data){
    temp_get_symbol_payload = data["data"][0];

    /*if there are more than 1 result(s)*/
    if (temp_get_symbol_payload) {
      if (temp_get_symbol_payload.length > 0) {
        get_holding_payload.classList.remove("display:none");
        get_holding_payload.innerHTML = "";
        /*iterate through*/
        for(let i=0;i<temp_get_symbol_payload.length;i++) {
          get_holding_payload.insertAdjacentHTML('beforeend', self.render_autocomplete_result(query,i,input_id,autocomplete_id,temp_get_symbol_payload[i]));
          if (i === results_max_results) {
            break;
          }
        }
      }
    }
  });
}
```