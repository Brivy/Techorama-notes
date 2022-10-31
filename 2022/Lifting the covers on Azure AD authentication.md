# Lifting the covers on Azure AD authentication

Some notes:

* Signals are pushed for CA (conditional access). This includes location, application, but also signals like which OS the user is using.
* A good strategy is to keep your access on _block by default_, so you only allow applications that you want to allow.
* The CA is evaluated every time a token is issues like:
  * SAML
  * OpenId tokens
  * OAuth2 tokens
  * Session and refresh tokens
* After you have been evaluated, you get a cookie from Azure AD. Other cookies by the app itself can/will be set as well.
* It will evaluate the refresh token in Azure AD when it starts to expire, most will live for 1 hour (1:05 hours to be exact).

Some login cycle:

* User enters Password -> Azure validates this -> Azure returns the Cookie
* But then multifactor is enabled. User enters Password -> User enters MFA (because this wasn't in the original cookie) -> Azure validates this -> Azure returns the Cookie

You also have CAE (Continuous access evaluation):

* This is for now implemented in for example Outlook and Teams.
* In short, an API subscribes to AD and checks for violations.
* Long version: Timely response to policy violations or security issues really requires a "conversation" between the token issuer (Azure AD), and the relying party (enlightened app). This two-way conversation gives us two important capabilities. The relying party can see when properties change, like network location, and tell the token issuer. It also gives the token issuer a way to tell the relying party to stop respecting tokens for a given user because of account compromise, disablement, or other concerns. The mechanism for this conversation is continuous access evaluation (CAE). The goal for critical event evaluation is for response to be near real time, but latency of up to 15 minutes may be observed because of event propagation time; however, IP locations policy enforcement is instant. See [here](https://learn.microsoft.com/en-us/azure/active-directory/conditional-access/concept-continuous-access-evaluation).

Some very nice tips:

* **Breakglass accounts** are accounts that you want to use when everything else fails.
* Use Fiddler to see network traffic.
