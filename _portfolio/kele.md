---
layout: post
title: Kele
short-description: A Ruby gem API client.

---
*See it on [Github](https://github.com/hcbviolet/kele)*

Kele is a Ruby gem API client that accesses Bloc’s API. I chose to build it from scratch as opposed to using Bundler so I wouldn’t have any unnecessary files, and would understand the essential functionality of every line of code I wrote.

Kele’s main function is to get JSON information from Bloc’s API. Via cURL, I needed to be able to first authorize with a Bloc username and password, then get user information, mentor availability, get and post curriculum checkpoints, and use the in-house messaging system.

Most of this was pretty straight forward:  Use httparty to write a method that makes a get or post request with the correct headers and body, and parse the response using the JSON gem. This was also a great opportunity to try using the [VCR](https://github.com/myronmarston/vcr) gem for testing to avoid making real repeat API requests (more about my experience testing a gem with VCR [here](https://hcbviolet.github.io/vcr-4-gems)).

This project gave me a greater understanding of how to build and wield gem API clients, and I could see myself using this knowledge in the future to use a well-established gem API client, make a custom gem for an API that just pulls the functionality I need out of it, or for APIs that don’t have gems already.
