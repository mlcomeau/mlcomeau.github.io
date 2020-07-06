---
layout: post
title:      "Using the dotenv gem in your rails app"
date:       2020-07-06 02:43:37 +0000
permalink:  using_the_dotenv_gem_in_your_rails_app
---


Today I want to talk about a very nifty gem to use when developing your code...

**# Dotenv**

What Is It?

-Gem to load environment variables from .env into ENV when the environment is bootstraped.

Why?

-When devloping your code its important that you frequently commit to github. But there are some things, such as personal credentials for external services, that we don't want to be posted to github. 

How? 

-Okay this is the best part, its super duper easy to use. I love a nice straight-forward gem.

-Step1: Add this line to your Gemfile: `gem 'dotenv-rails'`

-Step2: In the command line run: `$ bundle install `

-At this point Rails takes care of initalization for you with this line of code in config/application.rb: `Bundler.require(*Rails.groups)`, cool! 

-Step3: okay now in your root directory go ahead and make a file named ".env", this is where you will put all your super cool secrets....

SECRET_KEY = randomnumbersandletters

SECRET_PASSWORD = topsecretpassword

-Step4: THIS IS **IMPORTANT!** Add the .env file to your .gitignore file (also in the root directory) by adding this: 
`/.env`

(If your miss this step then your .env file and all its secrets will be uploaded to your source control! Yikes!)

-Thats it, you're all set up to store your personal credentials as environment variables that won't get loaded to public facing source control. So once you get your API password or your Oauth key, you can put it in the .env file as the value of a local variable. Anytime your application runs those variables will be available via ENV. ENV is basically a hash so accessing your variables later on in your code is as easy as using the syntax: 
`ENV['SECRET_NAME_GOES_HERE']. `
For example, if you're setting up your Rails app to use omniauth, you'd call the variable in your /config/initializers/omniauth.rb file. And as you continue to modify your code you can upload to Github confident that your secrets haven't been put on display for the entire interwebs....What a relief! 
