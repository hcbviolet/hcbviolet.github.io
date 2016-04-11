---
layout: post
title: Blocmetrics
thumbnail-path: "img/blocmetrics.png"
short-description: A simple API tracking tool and report generator that can be used to monitor activity on web apps.

---

{:.center}
![]({{ site.baseurl }}/img/blocmetrics.png)<br>
*See it on [Github](https://github.com/hcbviolet/blocmetrics). See it in [action](#).*

Blocmetrics is a simple analytics service that monitors activity on web applications, developed during the Rails portion of Bloc’s full-stack developer program.

Features:

  - User authentication with Devise
  - Users can register and track web applications by URL
  - A client-side Javascript snippet that allows users to track events on their website
  - Implementation of cross-origin resource sharing (CORS)
  - A server-side API that saves events to a database
  - Graphs displaying the data using Chartkick
  - PostgreSQL database
  - Deployed on Digital Ocean

The biggest issue with this project was navigating CORS. The Javascript code needs to send an Ajax request to the Blocmetrics API, so I needed to work around Rails’ built-in cross-site request forgery (CSRF) protection. Because the app isn’t dealing with sensitive information and because of the scope of the project, I chose to disable CSRF protection for JSON requests, but I could have instead attached a X-CSRF-Token to Javascript requests or required API authentication for requests.

Another issue that arose was the Devise gem blocking requests because the tracked application wasn’t signed in to Blocmetrics. I was able to work around verifying the authorization, but if I had been taking this into production I would have customized Devise to allow API requests, or made my own user auth system.

Navigating CORS is fascinating because you’re simultaneously opening your application up to outside requests, but then using a variety of methods to keep that scope as narrow and specific as possible to protect it from attacks. This project helped me see the underpinnings of an analytics service, and how much goes into making it secure.
