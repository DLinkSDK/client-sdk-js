# Integrating JS-SDK

### Introduction to JS-SDK

Using the JS-SDK allows landing pages to quickly integrate with Dlink for event reporting, which is a prerequisite for user attribution.

### Integration Steps

**Step 1:** Obtain Account ID and utmCode

Register an account at https://console.dlink.cloud.  After creating an app on the platform, obtain the corresponding Account ID  for App Setting,  obtain the corresponding utmCode  for Partner Marketplace

**Step 2:** Integrate the SDK and complete event reporting

JS-SDK: https://jssdk.deeplink.dev/sdk/2.1.1/deeplink.min.js

**Step 3:** Integration Example

```html
<script type='text/javascript'>
    (function (e, t, n) {
        if (e.deeplink) return;
        var a = e.deeplink = function () {
            a.handleRequest ? a.handleRequest.apply(a, arguments) : a.queue.push(arguments)
        };
        a.queue = [];
        var s = 'script';
        r = t.createElement(s);
        r.async = !0;
        r.src = n;
        var u = t.getElementsByTagName(s)[0];
        u.parentNode.insertBefore(r, u);
    })(window, document, 'https://jssdk.deeplink.dev/sdk/2.1.1/deeplink.min.js');

    deeplink('init', {
        appid: '{Account ID}',
        utmCode: '{utmCode}'
    });

    // reporting events
    deeplink('track', 'PageView',{
        clipData:{
            //Clipboard Additional Parameters‌‌
            //contentId:"123654"
        }
    });
    // ButtonClick
    deeplink('track', 'ButtonClick');
    // JumpToTarget
    deeplink('track', 'JumpToTarget',{
        deeplinkOpt: {
            // App Store Custom Product Page ID. The ID appended to the link url or redirect URL letting Apple knows which product page to redirect users to.
            // https://developer.apple.com/app-store/custom-product-pages/
            // https://help.adjust.com/en/article/app-store-custom-product-pages
            ppid: undefined 
        },
        urlParams:{
         // URL parameters
          //contentId: "123654"
        }
    });
</script>

```
### Extensible Component‌

##### Optional background reporting with ServiceWorker

> This is used to enhance the attribution success rate.

**Step 1:** Download sw.js file

 sw.js：`https://jssdk.deeplink.dev/sdk/2.1.1/sw.js`

**Step 2:** Integration Example

```html

<script>
    window.addEventListener("load", async () => {
        "serviceWorker" in navigator && navigator.serviceWorker.register(`./sw.js?time=${(new Date).getTime()}`).then(e => {
            console.log("Service Worker registered successfully.")
        })
    });
</script>
```




