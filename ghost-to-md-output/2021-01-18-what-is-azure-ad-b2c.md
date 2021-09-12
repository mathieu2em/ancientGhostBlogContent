---
title: What Is Azure AD B2C?
slug: what-is-azure-ad-b2c
date_published: 2021-01-19T03:25:31.000Z
date_updated: 2021-01-19T03:40:32.000Z
excerpt: Hi guys ! 
It's Mathieu2em, and I will talk about Azure Active Directory Business To Consumer. 
---

What does it eat during winter? Is it useful ? Should you use it ?

# what is it

Azure Active Directory B2C provides business-to-customer identity as a service.

It is a **customer identity access management (CIAM).**

I like to talk about it as a kind of virtual usb hub that, instead of usb stuff, can receive connections from IDPs.

If you dont know yet what is an IDP [here is a post I made explaining what is an IDP.](/identity-provider-s/)

It can also act (because it is always associated with an Azure Active Directory) as a kind of gateway between your active directory and other ones.

It can be pretty usefull for an organization that need some kind of system permitting them to connect progressively new entreprises accounts systems to their application users.

It can also be usefull if you want people connecting to your application with their social accounts !

You can them exploit their informations in order to do interesting API calls for example !

And, yes, we can Customize every page displayed by Azure AD B2C.
![](/content/images/2021/01/image-29.png)AD B2C as some kind of usb hub to connect IDPS to your apps or apis
Azure AD B2C offers a system of **Policies **which you can use to create/integrate custom login pages, forgotten password protocols, account creation pages, Multi-Factor Authentication, passwordless login process and even more.

IF you want to do some unusual behaviours, you can decide to use their system of custom policies. It is pretty useful if your login process contains api calls, special verifications systems, content analysis and other marginalities.

If you choose to **use custom policies, you can integrate with a RESTful API in a user journey to add your own business logic to the journey. **For example, Azure AD B2C can exchange data with a RESTful service to:

- Display custom user-friendly error messages.
- Validate user input to prevent malformed data from persisting in your user directory. For example, you can m**odify the data entered by the user**, such as capitalizing their first name if they entered it in all lowercase.
- **Enrich user data **by further **integrating with your corporate line-of-business application.**
- Using RESTful calls, you can send push notifications,** update corporate databases**, run a **user migration **process, **manage permissions**, **audit databases**, and more.

You can add a REST API call at **any step in the user journey **defined by a custom policy. For example, you can call a REST API:

- During sign-in, just before Azure AD B2C validates the credentials
- Immediately after sign-in
- Before Azure AD B2C creates a new account in the directory
- After Azure AD B2C creates a new account in the directory
- **Before Azure AD B2C issues an access token ← IMPORTANT FOR US**

**What is a User Journey? :** It is the sequence of steps that happens at Azure AD B2C Identity Experience Framework side during the execution of a custom policy which represents an authentication or authorization action happening.

An Example of a call to a custom policy that will make a call to a Restful API with a userID as a claim to receive a Loyalty number as a claim in the API response.
![](/content/images/2021/01/image-30.png)
source : [https://docs.microsoft.com/en-us/azure/active-directory-b2c/technical-overview](https://docs.microsoft.com/en-us/azure/active-directory-b2c/technical-overview)

An example of use with an [ASP.Net](http://asp.net/) core v3.1 web app :
![](blob:https://edilexpert.atlassian.net/9a633e1e-76c5-465f-a368-cda1b718af36#media-blob-url=true&amp;id=6c215b38-b1c7-453a-bcc3-c893ead6ebcb&amp;collection=contentId-752025611&amp;contextId=752025611&amp;mimeType=image%2Fpng&amp;name=image-20200730-170603.png&amp;size=52029&amp;width=788&amp;height=342)![](/content/images/2021/01/image-31.png)
I hope you liked this video and Thanks for reading! 

You can comment your thoughts and suggestions below.

See ya !
