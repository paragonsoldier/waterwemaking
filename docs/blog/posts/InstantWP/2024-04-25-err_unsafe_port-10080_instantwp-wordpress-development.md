---
title: "InstantWP"
date: 2024-04-25
tags:
  - blog
---

A friend hired me to design their Wordpress website. They already have a home page with their business details published live to production. I need a development environment to prevent the production environment from being affected until all changes are approved and ready to be pushed. 

My first thought was to start using Docker ([Get Started with Docker](https://www.docker.com/get-started/)). However, Docker requires macOS 12.0 or later. The latest version of macOS that my 2012 MacBook Pro supports is macOS 10.15.7. 

So, I reviewed WordPress.org's installation guide for [Running a Development Copy of WordPress](https://developer.wordpress.org/advanced-administration/before-install/development/). Since I use multiple computers, I didn't want the development environment to require multiple, locally installed dependencies. Therefore, I chose to use [InstantWP](https://instantwp.com/) since it's a portable, self-contained development environment. 

I was able to launch the InstantWP app successfully. However, when the site-in-development was pulled up from a browser, the browser returned error:
![](ERR_UNSAFE_PORT.png)

Browsers started blocking port 10080 to mitigate NAT Slipstreaming attacks ([source](https://chromestatus.com/feature/6510270304223232)). A [NAT Slipstream](https://samy.pl/slipstream/) attack allows an attacker to bypass a victim's Firewall and remotely access any TCP/UDP service that's bound to any system behind the victim's NAT, all just by the victim visiting a website.

Some developers have been able to work around the blocked port in Chrome ([source]((https://www.partitionwizard.com/partitionmanager/err-unsafe-port.html) ) and Edge ([source]((https://answers.microsoft.com/en-us/microsoftedge/forum/all/error-open-in-browser-microsoft-edge/505f95e7-4e9f-407f-96eb-bfa925f521e8)) by creating custom browser shortcuts with the `-explicitly-allows-ports` flag set. 

`“C:\Program Files (x86)\Google\Chrome\Application\chrome.exe” –explicitly-allowed-ports=10080`

`"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe" -explicitly-allowed-ports=10080`

If the custom Chrome/Edge browser shortcuts don't work ([source](https://www.oneminutevideotutorials.com/2021/06/21/how-to-keep-using-port-10080-after-many-browsers-block-it-as-an-unsafe-port/)), or if Firefox is your preferred browser, then in Firefox: 
1. Navigate to `about:config` in the address bar. 
2. Search for the preference name `network.security.ports.banned.override`. 
3. Select `String`, then select the `+` button. 
4. Enter the port number to be allowed (in my case `10080`), then select the Checkmark to save the change. 



