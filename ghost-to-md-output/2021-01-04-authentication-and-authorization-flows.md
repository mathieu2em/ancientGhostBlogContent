---
title: Authentication and Authorization Flows.
slug: authentication-and-authorization-flows
date_published: 2021-01-05T04:10:33.000Z
date_updated: 2021-01-13T02:37:50.000Z
tags: security, Getting Started, webapp, authentication, authorization, flows
excerpt: A little discussion about authentication and authorization flows
---

## **Authentication and Authorization Flows**

Hey guys, it's Mathieu2em here, let's talk about authentication and authorization!

First, make sure to differenciate Authorization Code flow from Authorization Code Flow with PKCE!

one is secure for an SPA and the other is not recommended !

### **Authorization Code Flow**

Because regular web apps are server-side apps where the source code is not publicly exposed, they can use the **Authorization Code Flow** , which exchanges an Authorization Code for a token.

Pretty simple, right? I got a code, you got a secret room, I give you the code, you say : 'come in, my dude. '

Well for this obvious reason, if your code is all visible from the browser you shouldnt use it !

**You  shouldn't use this flow if you develop an SPA (single page application) which is exposed to the web.**

THE SOLUTION ? 

### Authorization Code Flow with Proof Key for Code Exchange (PKCE)

This flow is an OpenId Connect flow! It is designed to authenticate native or mobile apps as well as SPAs for which it is (as of 2021) considered the best practice.

PKCE reduces security risks for native apps, as embedded secrets aren’t required in source code, which limits exposure to reverse engineering.

> During authentication, mobile and native applications can use the OAuth 2.0 Authorization Code Flow, but they require additional security. Additionally, single-page apps have special challenges. To mitigate these, OAuth 2.0 provides a version of the Authorization Code Flow which makes use of a Proof Key for Code Exchange (PKCE)->recommended in pluralsight class [Authentication and Authorization in ASP.NET Core](https://app.pluralsight.com/courses/0976bff0-13bd-4862-aa92-f1b740d56973/table-of-contents)

#### How does it work?

*In place of the **client_secret ***(the code I talked about for authorization code flow)*, the client app creates a unique string value,the  **code_verifier**, which it hashes and encodes as a **code_challenge**. When the client app initiates the first part of the Authorization Code flow, it sends a hashed **code_challenge**.*

*Once the user authenticates and the authorization code is returned to the client app, it requests an access_token in exchange for the authorization code.*

*In this step, the client app must include the original unique string value in the **code_verifier** parameter. If the codes match, the authentication is complete and an **access_token** is returned.*

So if you still dont understand, let's speak human language: 
You need to proove to the Identity Provider (click here to read the article about what is an IDP) that when you receive the token, you are the same than whom asked for the tokens and provided the credentials.

So the code_verifier and code_challenge part is where everything happens

you send some hashed value (the challenge) that cannot be decrypted without the Code Verifier and you send the authorization code. 

Then the user is redirected to the IDP login page, enters his login stuff and consents to whatever there is to consent to without reading the terms of use (obviously).

Now, the Idp send you back to your site with a one-use code.

You then send back from your site this one-use code as well as your code-verifier to the IdP to proove that you are indeed the one who initiated all this process.

The IDP validates the code verifier with the code challenge , because your code challenge can only be correctly decifered with the code verifier, then WOOHOOO he FINALLY sends you your precious little tokens

#### PKCE sequence diagram . source : [https://auth0.com/docs/flows/concepts/auth-code-pkce](https://auth0.com/docs/flows/concepts/auth-code-pkce)
![](/content/images/2021/01/image-3.png)![](blob:https://edilexpert.atlassian.net/1cbc0d40-3662-440d-b247-55729035bbf9#media-blob-url=true&amp;id=516475a8-a1a3-4b74-a7c8-c2a7577ffb56&amp;collection=contentId-752025611&amp;contextId=752025611&amp;mimeType=image%2Fpng&amp;name=image-20200729-143921.png&amp;size=127959&amp;width=1500&amp;height=1220)
another example :
![](/content/images/2021/01/image-5.png)
source : [source link](https://developer.okta.com/blog/2019/08/22/okta-authjs-pkce#:~:text=The%20response%20is%20returned%20on,be%20in%20your%20browser%20history.&amp;text=The%20fact%20that%20the%20tokens,secure%20than%20the%20Implicit%20flow)

### **Implicit grant Flow with Form Post**

> As an alternative to the Authorization Code Flow, the OAuth 2.0 spec includes the Implicit Flow intended for *Public Clients*, or applications which are unable to securely store *Client Secrets*. This is no longer considered a best practice for requesting Access Tokens

> But when used with Form Post response mode, it offers an ok workflow if the application needs only an *ID Token* to perform user authentication.

> **deprecated since 2018**

![](/content/images/2021/01/image-6.png)
source : [source link](https://developer.okta.com/blog/2019/08/22/okta-authjs-pkce#:~:text=The%20response%20is%20returned%20on,be%20in%20your%20browser%20history.&amp;text=The%20fact%20that%20the%20tokens,secure%20than%20the%20Implicit%20flow)

#### the implicit grant flow vs the PKCE flow

SECURITY DANGER : Notice that after you authenticate, the Authorization Server (like Google) responds directly with tokens. This means that the tokens are in your browser’s address bar as a result of the redirect. That’s problematic since Google can’t definitively know that your browser (the intended recipient) actually received the response. It’s also problematic because modern browsers can do browser history syncing and they support browser extensions that could be actively scanning for tokens in the browser address bar. Leaking tokens is a big security risk.

These security issues led to a reassessment of the value of the Implicit flow, and in November of 2018, new guidance was released that effectively deprecated this flow.

### **Others:**

I will not discuss these flows here but they exist : Client Credentials Flow(pretty obvious) , Device Authorization Flow.

I hope this article has been helpful for you !

**Dont hesitate to leave a comment and share me what you tought about this post! :D **

Have a great and secure day/night/apocalypse/whatever .

Math
