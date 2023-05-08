---
layout: post
title: "Single Sign-On (SSO)"
description: "An introduction to Single Sign-On (SSO)"
comments: true
keywords: "sso, security, authentication, identity"
---
### What is SSO?

- It is an authentication method by which users are authenticated to multiple applications or websites with a single set of credentials.

### How does SSO work?

It is based on the trusted relationship established between the Service Provider (websites / apps that users want to use) and Identity Provider like OneLogin, Okta, etc.The trust relationship is often based on sharing a certificate or token between the Service Provider and the Identity Provider. The certificate / token usually contains information like the user’s email or username, etc. The is the flow that happens when a user tries to login to a SSO-backed website or app.

1. A User tries to login to the website (i.e. Service Provider) which is SSO-backed.
2. The service provider sends a token containing user’s information like username or email to the Identity provider.
3. The identity provider checks to see if the user is already signed-in, in which case the user is granted the access to the service provider and skips to step 5.
4. If the user hasn’t logged-in, the user is prompted to do so by providing the credentials required the Identity Provider. This could be simply be username and password or OTP.
5. The user’s credentials are validated and it will send back the token when the user is authenticated successfully.
6. The token is passed through the user’s browser to the service provider.
7. The token received by the service provider is validated to see if it really came from the identity provider.
8. The user is granted access to the service provider

### Flow Diagram
![SSO flow diagram](https://github.com/sanjeevpr/sanjeevpr.github.io/raw/main/assets/images/sso.png)

### Reference
[https://www.onelogin.com/learn/how-single-sign-on-works](https://www.onelogin.com/learn/how-single-sign-on-works)
