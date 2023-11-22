# Integrating JS-SDK

### Introduction to JS-SDK

Using the JS-SDK allows landing pages to quickly integrate with Dlink for event reporting, which is a prerequisite for user attribution.

### Integration Steps

**Step 1:** Obtain Account ID and utmCode

Register an account at https://console.dlink.cloud.  After creating an app on the platform, obtain the corresponding Account ID  for App Setting,  obtain the corresponding utmCode  for Partner Marketplace

**Step 2:** Integrate the SDK and complete event reporting

JS-SDK: https://jssdk.deeplink.dev/sdk/1.7.2/deeplink.min.js

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
    })(window, document, 'https://jssdk.deeplink.dev/sdk/1.7.2/deeplink.min.js');

    deeplink('init', {
        appid: '{Account ID}',
        utmCode: '{utmCode}'
    });
    // reporting events
    deeplink('track', 'PageView');
    deeplink('track', 'ButtonClick');
    deeplink('track', 'JumpToTarget');
</script>

```


