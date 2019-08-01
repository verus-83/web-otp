# How to use the SMS Receiver API

The SMS Receiver API is currently available in chrome canaries under a flag:

1) Download chrome canary ([android](https://play.google.com/store/apps/details?id=com.chrome.canary), [desktop](https://www.google.com/chrome/canary/)).
2) Navigate to `chrome://flags` and enable `Experimental Web Platform features`.
3) Navigate to a test page, e.g. https://code.sgo.to/tmp/sms.html
4) Send a SMS to your phone, following the [server side convention](https://github.com/samuelgoto/sms-receiver#formatting):

```
Your OTP is 123ABC.
For: https://code.sgo.to/?otp=123ABC&app=PqEvUq15HeK
```

The app hash for `chrome chanaries` is `PqEvUq15HeK`.

[Here](https://code.sgo.to/tmp/sms-receiver.js) is a concrete example of how to use the API, but here is the baseline of how to use it:

```javascript
async function main() {
  if (navigator.sms) {
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
```

# App Hashes for different channels

| Browser        | App Hash      |
| -------------  | ------------- |
| Local chrome   | s3LhKBB0M33   |
| Canary chrome  | PqEvUq15HeK   |
| Beta chrome    | xFJnfg75+8v   |
| Prod chrome    | EvsSSj4C6vl   |

For other browser implementations, here is how to [compute app hashes](https://developers.google.com/identity/sms-retriever/verify#computing_your_apps_hash_string).

