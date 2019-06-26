
### Frequently Asked Questions

#### Why are we telling developers to use phone numbers? They can be hijacked, change ownership, used to track users, etc.

We aren’t telling developers to use phone number; they are already using them. Despite problems, phone numbers are useful for various purposes (see intro). In the absence of alternatives to achieve these useful things, developers will continue to use phone numbers and users will struggle with them. This proposal makes the web more usable in the short term (in particular matching functionality that already existings natively), but in the long run, we hope to move the ecosystem off of phone numbers as alternatives for the need functionality become available. Given the time-scale of such a transition, action in the short-term to reach experience parity seems necessary.

#### Why is this using SMS OTP as a verification mechanism? SMS OTP are slow, expensive, phishable, etc.

SMS is the most common existing verification mechanism; this proposal aims to streamline flows that already exist by mitigating the need for user involvement/action. Although this does not address the more fundamental problems, it may make some situations better (e.g. users don’t handle OTP manually, hence less conditioned to be phished), but starting to move developers to a programmatic model would be a potential stepping stone to better mechanisms.

#### Is this implementable on iOS?

Yes, iOS already uses a declarative model (form annotation “[one-time-code](https://developer.apple.com/documentation/security/password_autofill/enabling_password_autofill_on_an_html_input_element)”) and heuristically extracts and suggests OTP from SMS. They could implement an imperative API or support other alternatives like facilitating interaction with identity providers if desired.

#### Is this implementable on desktop?

Yes, browser need not look for SMS on the local device. For example, if Chromesync is enabled across desktop and mobile devices, Chrome could retrieve on one device and return the SMS content on another. Or locally, a desktop instance of a browser could use Bluetooth to talk to a nearby phone and have an instance of the browser on the mobile device retrieve and return the SMS.

#### Why can’t we use a model like having developer tell us the OTP and let them know if there is a match?

The developer needs something that can be verified on their server, a yes/no response is not sufficient. Claiming that the phone number is active on the device would require a response signed in some way to make it verifiable. This could be done in a number of ways, but is a major departure from the current OTP model and necessitate major changes from developers (i.e. change their backend server logic to process these claims; whereas just returning the SMS contents with the OTP means primarily only a frontend change an minimal backend work ... perhaps only changing the message template format, rather than security-sensitive backend logic). However, the longer-term intent with more comprehensive Identity APIs is to provide verifiable assertions of phone ownership, which would be compelling for developers to adopt and change their system to accept if it meant avoiding the need for sending SMS.
