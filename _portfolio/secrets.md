---
layout: post
title: Secrets.yml
short-description: Migration of environment variables for open source project Growstuff.

---

*Growstuff is an open source Rails application that crowdsources information for food gardeners on what members are growing and harvesting all over the world, and makes it available as open data in their API.*

One of the big changes that came with Rails 4 was the inclusion of the config/secrets.yml file. This feature was added as a common storage location for environment-aware keys and configuration. It also allows you to call the secrets stored in this file using ```Rails.application.secrets```. Previously, like many applications, Growstuff was using the [Figaro gem](https://github.com/laserlemon/figaro) to store keys in application.yml and set the Heroku configuration, but expressed interest in migrating application.yml to secrets.yml, and I decided to take on the issue.

After moving all of the variables into secrets.yml, I started changing a few environment variables throughout the application, by calling ```Rails.application.secrets```, but it started to get a little tedious so I decided to add the constant ```SECRETS = Rails.application.secrets``` to simplify the call. The main issue arose when I removed Figaro, and needed to find an alternative that would set the Heroku configuration without having to do it manually. Luckily there’s a gem for that, [heroku_secrets](https://github.com/alexpeattie/heroku_secrets), which does the “deploy variables to heroku” function for secrets.yml.

Testing was difficult for this because I couldn’t deploy to heroku without the proper keys, but I was able to test as much as I could by using the heroku_secrets gem and rake heroku:secrets to send example variables to Heroku, calling variables from the console, and running the app locally in development mode.

The Growstuff community tests pull requests using TravisCI, and since the changes I made modified the way variables were stored, I  broke the Travis build, which was still trying to match variables to application.yml, requiring the keys in secrets.yml to be ported over by an administrator to finish testing at a later date.

It was especially cool for me as a junior developer to be able to try my hand at implementing a new tool on an existing project, and it was a great learning experience. There are definitely pros and cons to using secrets.yml that I didn't foresee, like how much work goes into making an application-wide change like this for the sake of integrating a tool that mostly maintains the status quo. I'm really impressed at the level of dedication that goes into maintaining an open source project and managing contributions--a logistically difficult task that's met only with patience and hard work, and I look forward to contributing more in the future.
