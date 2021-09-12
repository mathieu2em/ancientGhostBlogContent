---
title: What is an Identity Provider?
slug: identity-provider-s
date_published: 2021-01-13T01:32:34.000Z
date_updated: 2021-01-18T21:56:59.000Z
excerpt: Hey guys, in this post I explain to you  what is an Identity Provider!
---

I had to implement an authentification and authorisation system, and I would have liked that someone could, at the time, explain to me in human language what is an Identity Provider and some of the important security concepts linked with it!

so let's start by a formal description ( I know, I know, you can get it everywhere but hey! if you want to skip directly from the personnalised fun part, you can skip directly to the second section !  Just scroll down a bit! ;) )

FORMAL DESCRIPTION

An Identity Provider is a special kind of API that is added to the application landscape.

It facilitates a **centralized way to authenticate** that works across all of the different parts of the application. It is centralized because authentication doesnt take place at the application used by the user but **at the identity provider.** At the same time , there is **only one identity provider for all applications in an organization.** You don’t need one for every single application.

When users use different web applications that **all trust the same token service**, they have to log in only once in order to use all of these applications… Which is pretty convenient.

**the effect mentioned above is know as SSO (single sign-on)**

Examples of Identity Providers are 

- Facebook.
- Google
- Instagram.
- Fitbit.
- Microsoft.
- Box.
- Amazon Web Services (AWS)

Popular IdPs for enterprise/corporate use include the following:

- AD 
- Azure AD Native
- G Suite
- Lightweight Directory Access Protocol ([LDAP](https://searchmobilecomputing.techtarget.com/definition/LDAP))
- PingFederate
- [SharePoint](https://searchcontentmanagement.techtarget.com/definition/Microsoft-SharePoint-2016)

Auth0 can also act as an Identity Provider.

## Less Formal Description

An Identity Provider Act as an intermediary between the actor and the application.
Let's do a metaphor. Let's say someone named Kevin need to access a special place in the American White house, but only some SPECIAL people can access this place.

So when Kevin arrives at the entrance, a guard asks him if he has a proof of his identity. Kevin tells him he indeed is himself. Well the guard should not believe him lol. The guard will only believe him IF SOMEONE HE KNOWS AND TRUST CERTIFIES  that he is who he says he is ! 
![](/content/images/2021/01/image-27.png)![](/content/images/2021/01/image-28.png)

This is where the Identity Provider will be important ! Lets now change the scenario: When the guard asks him to proove who he is, Kevin opens his wallet and show his passport issued by the government. This passport has some special printing that can only be made by some special tools only owned by the government whom issued the passport. 

Now, the guard obviously trust the government ! (lol let's say we can) 
So if this passport is effectively delivered by the government, which the guard has validated, then Kevin has proven successfully his identity and can now enter in this room ! 

Let's now link the element of this story with the way an Identity Provider is used in an IT context: Here, the governement is the identity provider; it's the trusted entity whom is able to certify that kevin is himself !  To do so the government MUST deliver some type of key to Kevin, this key is his passport ! Now, in our programming world, this passport is split in three parts . 
![](/content/images/2021/01/image-22.png)

1.	The refresh token ( like the passport used by kevin to ask the government for a new entrance passport once his actual passport is expired)

2.	The Identity Token ( The passport kept by kevin to remember him who he is lol , maybe a birth certificate but with an expiry date ? He has one, it certifies him from the government that he has an identity, but Kevin don'd show it to others)

3.	The Access Token ( The actual passport used by Kevin to proove his identity to other actors, like the guard ! This one will have a shorter expiry time because of the risks associated with the fact that Kevin shows it to a lot of people, and we dont necessarily trust all these persons ! Well at least we shouldnt lol...)

This is a first draft as an article about Identity providers , let me know if you appreciated it !

Have a great and secure day!

Math

attributions for the 2d characters : [Infographic vector created by vectorpocket - www.freepik.com](https://www.freepik.com/vectors/infographic) and some google image memes.
