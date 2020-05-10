---
layout: post
title:      "First project, done! "
date:       2020-05-10 21:56:54 +0000
permalink:  first_project_done
---


I made it to the end of the first project week! And let me tell you it was quite a roller coaster, lots of emotions experienced, but overall I did a really good job of sticking with it and pushing through the tough parts. At the beginning of the week I was really doubting my ability to implement what I had learned through all the Flatiron lessons and labs and now I've got a working program that I feel really proud of! 

I decided that for my project I wanted to go with using an API as opposed to scraping a website for data. API stands for Application Programming Interface and it allows a coder to get huge amounts of data from all across the internet very rapidly. I found a really great article that explains APIs in a clear concise way: [available here.](https://www.freecodecamp.org/news/what-is-an-api-in-english-please-b880a3214a82/)
Although we did learn a bit about APIs in our ruby lessons, I was still feeling pretty confused about them at the beginning of this project and this article really helped clear things up for me! For somebody who hasn't worked with APIs before its really digestable. If you want to start learning about APIs, this would be a good place to start and if you do, let me know what you think in the comments! 

Perhaps the hardest part of this project was just choosing an idea and getting started. So many possibilities. I decided to go with a news reader program because usually in my spare time the first thing I do is go on Reddit or Apple News and look through all the breaking news headlines. I like being able to read articles from any news source and not just be limited to one. So I got to check off my first checkbox: pick an idea, done! 

I found the NewsAPI, available at www.newsapi.org. On their website it says they pull articles from over 50,000 news sources across the world. Wow! The NewsAPI offers three different endpoints. An endpoint is a URL that we can use to send a request for data to the web server and then receive a response. In this case, a response would include the details of many (many!) articles. I decided to use the 'top headlines' endpoint as opposed to the 'everything' endpoint because when I read the news I just want to know the most important stuff, I'm not concerned with the sports or entertainment articles too much. The articles I receive when I send my response (which in this example, would be anytime I run my program) are partially based on how recently the article was published, to be a top headline it needs to be new, so depending on the time of day that you run my program the articles delivered will be different. 

To make my web request to the top headlines within my ruby code, I decided to use the HTTParty gem after reading about it in posts from previous students who had completed the project. And they were right, its super easy to use! Perhaps the greatest benefit of HTTParty is that it does all the parsing automatically, the response you get back is all ready to go for use in your program! Theres a lot of information about HTTParty available online and to be honest I didn't really have enough time to dive into all that it can do. Now that my project is complete I want to go back and learn more about this very helpful tool. Same for the NewsAPI, I'm pretty sure it has a lot more functionality than what I'm aware of. I'm looking forward to experimenting with it more. 

Overall I'm really happy with how my project turned out. I made a CLI program that pulls top headline news articles from an API and displays those headlines to the user in a friendly format and even offers the option to open up the article to read in the web browser! It was great to prove to myself that I really understand what we've been learning about at Flatiron and then implement it appropriately. I learned so much from the experience and I'm really looking forward to whatever is coming next! 

![](https://media.giphy.com/media/EbaEWv3icphQI/giphy.gif)
