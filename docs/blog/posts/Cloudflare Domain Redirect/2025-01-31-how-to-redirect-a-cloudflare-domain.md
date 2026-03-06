---
title: "How to Redirect a Cloudflare Domain"
date: 2025-01-31
tags:
  - blog
---

# How to Redirect a Cloudflare Domain

My love of puns and desire for branding opportunities won over when I choose the domain: *waterwemaking.com*. However, I've was concerned that people would mistype the domain as *whatarewemaking.com*. The solution was to purchase both domains, then redirect *whatarewemaking.com* to *waterwemaking.com*. 

Cloudflare has a guide on setting up a domain redirect: [Redirect one domain to another](https://developers.cloudflare.com/fundamentals/setup/manage-domains/redirect-domain/). However, my configuration is different than the one directly laid out in the guide leading to issues when setting up the redirect. Below are the steps I took in order to get the redirect working for my domains. **Note**: These steps assume the primary domain (e.g *waterwemaking.com* in my example) has already been configured.

## Create a DNS A or CNAME Record

The domain to be redirect must still have an A or a CNAME record configured. 
The A or CNAME record should be the same as the primary domain. 
In my case I created two CNAME records; one for the root domain (i.e. @) and one for the "www" prefix. Both records point to my web host. 

![](Cloudflare-DNS_Records.png)

## Create a Redirect Rule

Create a redirect rule by going to `Rules -> Redirect Rules -> New Rule`. 
The example that Cloudflare gives maintains the subdomain/query in the redirect (e.g. `aliasdomain.com/store` redirects to `primarydomain.com/store`). 
I choose to keep the rule simple by redirecting any traffic sent to the alias domain to the **root** of the primary domain. 

This is accomplished by configuring the rule to forward `All incoming requests` to *Type* `Static`, to the URL of the primary domain (e.g. `waterwemaking.com`), with Status Code `301`. 

![](Cloudflare-RedirectRules.png)

## Purge Cache, if Required

The above settings should be all that's needed for the domain redirect to work. However, when I configured the redirect, I wasn't able to get it to work during testing. Trying to navigate to `whatarewemaking.com`would return error messages, rather than load `waterwemaking.com`. This issue persisted across multiple browsers (e.g. Edge, Chrome, Firefox) and multiple devices (i.e. Cell Phone, Desktop, and Laptop). I learned that not only do browsers keep a cache, but that domain hosts also keep a configuration cache. The Cloudflare Configuration changes I made didn't take effect until I cleared the Cloudflare cache. The Cloudflare Configuration Cache can be cleared by going to `Caching -> Configuration -> Purge Cache -> Custom Purge or Purge Everything`.

![](Cloudflare-Cache_Configuration.png)

## Conclusion

By creating an A or CNAME DNS Record that matches the primary domain, creating a static redirect rule, then purging the Cloudflare Configuration Cache my alias domain (`whatarewemaking.com`) now successfully loads my primary domain (`waterwemaking.com`). 