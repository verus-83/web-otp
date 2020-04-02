# Web OTP

This repository documents an API for accessing one time passwords to verify credentials (e.g. phone numbers).

* The [explainer](explainer.md) is a developer-oriented preview of the API.
* the [specification draft](https://wicg.github.io//WebOTP/index.html) is aimed at browser developers.

The API has a [test suite](https://github.com/web-platform-tests/wpt/tree/master/sms) in the Web Platform Test project.

* Read the [how-to](HOWTO.md) instructions for example usage.

# Resources

This API is inspired by and loosely based on the following discussions:

* [SMS Verification on Android](https://developers.google.com/identity/sms-retriever/overview)
* [The one-time-code autocomplete API](https://developer.apple.com/documentation/security/password_autofill/enabling_password_autofill_on_an_html_input_element)
* [https://github.com/whatwg/html/issues/3745#issuecomment-395327173](https://github.com/whatwg/html/issues/3745#issuecomment-395327173)

The Web OTP API has also been discussed in the following places:

* [discourse thread](https://discourse.wicg.io/t/sms-otp-retrieval/3499)
* Blink [intent-to-implement](https://groups.google.com/a/chromium.org/forum/#!msg/blink-dev/Drmmb_t4eE8/khjMpM9qBAAJ)
* Blink [intent-to-experiment](https://groups.google.com/a/chromium.org/d/msg/blink-dev/-bdqHhCyBwM/yFoKtQQRAQAJ)
* [TAG Review](https://github.com/w3ctag/design-reviews/issues/391)
* [Origin Trials](https://web.dev/sms-receiver-api-announcement/)
