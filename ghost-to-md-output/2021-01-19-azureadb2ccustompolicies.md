---
title: Uncovering Effective B2C Authentification through Azure AD Custom Policies
slug: azureadb2ccustompolicies
date_published: 2021-01-19T08:27:35.000Z
date_updated: 2021-01-20T04:00:35.000Z
tags: authentication, security, programmer life, Getting Started, authorization, webapp
excerpt: Azure AD B2C : Custom policies, How to create effective ones and how I discovered them as a solution for a Business-to-Client web-app authentication solution.
---

Few weeks ago, I was required to create an authentication and authorization system for a Single Page Application using Angular at the Front-end connected to an API using ASP.Net Core 3.1  at the Back-End.

The requirements were that the authentication system would be intuitive, flawless, 100% secure and that... Wait for it...  It should support SSO *moment of panic* (we'll see later what does it means). 

First of all, you need to know that I went through this journey while still being an intern. This was all stuff that, at the time, while really attractive to me, was still pretty much a mystery.

For the time being, I didnt have a clue what the heck was an access, ID or refresh token. Open-ID-Connect or OAuth 2.0. were still some strange namings from far away countries. The only certainty was that it looked and sounded really cool to play with and that I wanted to do something stunning with them so that my CTO, and the company for which I was an Intern at the time would be amazed. I wanted to give the feeling that I was someone they needed in their team and that I was gonna add great value to their startup... So yeah. This is how it started.

so one day at the office My room, in the midst of the pandemic, my boss anounces me that he would like me to work on the authentication and authorisation system of the web app we're developing. He tells me that it should support SSO, which means that employees of a company should use their organisation email to connect to our webapp directly. He tells me that it has to be finished in three months for the launching of our product.

I accept. Then I panic. Then I calm down. Then I start searching, Studying the subject and fiddling some proof-of-concepts of potential solutions.

I think I posted some of it on [my github](www.github.com/mathieu2em) but be aware. My github is a complete mess lol... Anyway.

After a lot of tries what got my attention was finally [**Azure Active Directory Business To Consumer**](/what-is-azure-ad-b2c/).

If you want to know at this point how you get to handle and work with a technology you've never used before in an efficient way, look-up for my next blog article in wich I will dive into it in details.

To receive it you can subscribe to my blog or come take a look somedays !

## Azure AD B2C Custom policies

From what I personally experienced, tried and researched,  Azure AD B2C offers the possibility to create special security sequences of actions resulting in a custom Login, Logout, Password reset or other authentication security actions. It is also some kind of middleman between you and all the others Identity Providers.

[check out my article about Azure AD B2C for more informations about it !](/what-is-azure-ad-b2c/)

It the article I just suggested you to read above this line, I explain that you can use custom policies from Azure AD B2C's Identity Experience Framework to create completely custom behaviours between your system and your client's IDPs. 
The custom policies files are .xml config-like files inside which all the important stuff is contained in blocks.

They are hierarchically made, so each one inherit from a parent or else is a parent. This kind of inheritancy is decided in the <BasePolicy> block. By default, you will have the **TrustFrameworkBase.xml** which will state all the basic stuff and which will contain all the elements you will be able to copy paste in child policies xml files to create custom behaviours.

You will also have the TrustFrameworkExtensions file which will be useful to instate the userJourney. The TrustFrameworkExtensions file is the child of the Trust

TrustFrameworkBase file. I Highly recommand, when developing custom policies, to start from base policies you you can get from the microsoft azure ad b2c policies starterpack.

you will also have to setup your azuread b2c tenant in your azure portal in order to be able to use the custom policies by enabling the identity experience framework  (the custom policies framework name).

(this article is still being written thus incomplete, you can subscribe to my blog mailing list to be informed of the following).
