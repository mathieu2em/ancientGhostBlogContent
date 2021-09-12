---
title: Setting The Preferred Site Between www And Not www
slug: setting-the-preferred-site-nginx
date_published: 2021-01-29T06:01:40.000Z
date_updated: 2021-01-29T06:01:40.000Z
tags: web, seo, domain
---

As we probably all know, SEO is becoming a really important part regarding the success of a website affluence. 

One of the important points about such a thing is the preferred site between www.yourDomain.com and yourDomain.com. Redirecting traffic from one to the other will make a significant difference in the traffic of your digital domain.

## Do I really have to choose between the two? 

Well... yes. Staying consistent about your canonical domain will contribute to the confidence level of your site for search engines algorithms and bots.

## Use HTTP Redirection 301 with NGINX

If you use a NGINX web-server to do so, here is the way you can redirect your traffic properly from one domain address to the other.

Which one to choose? www.yourDomain.com or yourDomain.com ?
there is no correct answer to this question as even between the big names of the world-wide-web the decision differ.

I personally chose to redirect from not-www to www because of some optimization stuff I read about on the profoundness of the web.

    server {
    	server_name hackercitizen.com;
        	return 301 http://www.hackercitizen.com$request_uri;
    }
