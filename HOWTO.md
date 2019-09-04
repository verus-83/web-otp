# How to use the SMS Receiver API

## Trying it out

The SMS Receiver API is currently available in chrome canaries under a flag. Here is how to try it out:

1) Download chrome canary for [android](https://play.google.com/store/apps/details?id=com.chrome.canary) in your personal profile, **not** your work profile (known [bug](https://bugs.chromium.org/p/chromium/issues/detail?id=1000548)).
2) Navigate to `chrome://flags` and enable `Experimental Web Platform features`.
3) Restart your chrome canary browser (make sure to use your personal profile, **not** your work profile (known [bug](https://bugs.chromium.org/p/chromium/issues/detail?id=1000548)).
4) Navigate to the following test page: https://sms-retriever-sample.glitch.me/

## Developing

To implement this in your app, you want to use the following snippet in your page:

```html
<script>
async function main() {
  if (!navigator.sms) {
    alert("feature not available :(");
    return;
  }
  try {
    let {content} = await navigator.sms.receive();
    alert("sms received! " + content);
  } catch (e) {
    alert("time out!");
  }
}

main();
</script>
```

Start your local server, e.g.:

```
python -m SimpleHTTPServer 8080
```

Connect it to your local web server through your favorite method:

```
adb reverse tcp:8080 tcp:8080
```

And send an SMS to your phone, following the [server side convention](https://github.com/samuelgoto/sms-receiver#formatting). For example:

```
Your OTP is 123ABC.
For: http://localhost:8080/?otp=123ABC&app=PqEvUq15HeK
```

While developing, make sure to include in the URL in the `For` parameter of your SMS:

1) The app hash for `chrome chanaries` is `PqEvUq15HeK` and
2) The OTP value in a parameter named `otp`.

## Deploy

Outside of your local development, it is important to know that this API only works over HTTPS:

1) Make sure you deploy to your https endpoints
2) Make sure to send SMSes formatted against your https endpoints

```
Your OTP is 123ABC.
For: https://example.com/?otp=123ABC&app=PqEvUq15HeK
```

## Origin Trials

For origin trials, the only bit that changes is that your users won't be using chrome canaries anymore. So, you want to replace the hash from `PqEvUq15HeK` to the production release channel's `EvsSSj4C6vl`. For example:

```
Your OTP is 123ABC.
For: https://example.com/?otp=123ABC&app=PqEvUq15HeK
```

## Common Issues

Here is a checklist of common issues:

[ ] I downloaded [chrome canary](https://play.google.com/store/apps/details?id=com.chrome.canary) in my **personal** profile.
[ ] I enabled `Experimental Web Platform features` under `chrome://flags`.
[ ] I navigated to `https://sms-retriever-sample.glitch.me/` being careful not to drop the `https` scheme.
[ ] While developing locally, I made sure to include the canary app hash `PqEvUq15HeK` **and** the `otp` parameter.
[ ] While deploying, I made sure to use my `https` endpoint and update the SMS format accordingly.
[ ] While in origin trials, I made sure to update the app hash to chrome prod `EvsSSj4C6vl`.

## App Hashes for different channels

The instructions above should work for chrome canaries. For other release channels, use the following app hashes:

| Browser        | App Hash      |
| -------------  | ------------- |
| Local chrome   | s3LhKBB0M33   |
| Canary chrome  | PqEvUq15HeK   |
| Beta chrome    | xFJnfg75+8v   |
| Prod chrome    | EvsSSj4C6vl   |

For other browser implementations, here is how to [compute app hashes](https://developers.google.com/identity/sms-retriever/verify#computing_your_apps_hash_string).

