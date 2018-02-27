---
layout: single
title:  "Echo of Today: a Twitter Bot reminding us what happened today, years ago"
date:   2015-09-18 15:00:00 -0800
categories: Twitter Bot PHP
permalink: /echo-of-today-twitter-bot
---
Twitter bots are everywhere. An article from [Quartz](https://qz.com/248063/twitter-admits-that-as-many-as-23-million-of-its-active-users-are-actually-bots/) dated last year states that _up to approximately 8.5% of the accounts considered active are automatically updated_. That means 23 million of Twitter’s 271 million monthly active users are bots. 
Yes, bots on Twitter are extremely popular so I decided to make one myself. I called it [Echo Of Today](https://twitter.com/EchoOfToday). 
Let's see how I did it and what was the result!

<figure>
  <img src="{{site.url}}/assets/images/2015-09-18/mecha-twitter.jpg" alt="funny Twitter Logo"/>
  <figcaption>Twitter is becoming increasingly automated</figcaption>
</figure>

## What should my bot do?

When I first started to think about my upcoming Twitter bot, I had to come up with **something interesting** yet not already done to death. With 20 million bots around, you may guess that a lot of the most simple and obvious concepts are already implemented. I wanted to do something at least partially **original**, not your usual bot that just follows random people.

This meant that my bot would have to sport a certain level of complexity - let's say I didn't want to make something too simple but I also wanted to avoid losing myself in something utterly complex. 
Then I had the idea: make a bot that tweets news articles published exactly one year ago, two years ago, three years ago (and so on, until an arbitrary number _n_ of previous years to work on). I'll explain better this idea with an example. If today is the 21st September, the bot would look up news published on the 21st September of one year ago and tweet them. It will also find and tweet news published on the 21st September of two years ago, of three years ago and so on (the number of years it goes backwards is configurable). In other words, the bot would remind us what was happening exactly one and two, and three and so on years ago.

Sounds like a nice idea right? But how to implement it?

<figure>
  <img src="{{site.url}}/assets/images/2015-09-18/news.jpg" alt="newspapers"/>
  <figcaption>Do you remember what happened today, two years ago?</figcaption>
</figure>

## Getting the pieces together

First of all, I had to decide **which language** I would use to code the bot. I chose to go with PHP, only because I knew it fairly well. But it can be any language you like, for example, I know many Twitter bots are written in Python or JavaScript. Just be sure that the language you choose can serve your purpose right.

After that, I had to put together the basics: create a new Twitter account for the bot, set up a new app on the newly created account, get all the API keys I needed and start writing the code necessary to create **basic** features for the bot, such as tweeting. For this purpose, I found Abraham Williams library [twitteroauth](https://github.com/abraham/twitteroauth) very useful.

Next I was in front of the biggest challenge I faced when coding this bot: **how the get the information** I needed (old news articles, in this case). After a bit of brainstorm and research, I found out that the New York Times offers awesome APIs through their [Times Developer Network](http://developer.nytimes.com/). After studying their APIs, I managed to get the news I needed as a nicely formatted json response, perfect for my needs. This required a bit of coding (not much, really) but what I needed was there in the end.

Next there was the **140 characters challenge**. I decided to structure my tweets as follows:

> #nYearsAgoToday Article Headline http://article.uri #EchoOfToday

The first hashtag indicates how old the news is, in years (6 years old is the oldest I wanted to go back). Next we have the article's headline, the article's URI and the last hashtag is simply the name of the bot. 
As you know, each Tweet can be long at most 140 chars and since I wanted to stick in a couple of lengthy hashtags too, not many characters were left for the headline and the URI. Headlines tend to be short enough, though after doing a bit of math I coded an **upper limit** on how long can I allow a headline to be for a news article to be tweeted. The biggest problem was actually the URI, which can get quite long. The obvious solution was to **shorten it**, which is what I did. I got my [goo.gl](https://goo.gl/) API key and with the help of [googl-php](https://github.com/sebi/googl-php), a simple PHP class that facilitates the use of goo.gl APIs, I got the job done: now all URIs were much shorter and of the same length.

## A final touch and the results

Now that the bot was done I had to decide how much it I wanted it to tweet. I decided to make it tweet **12 times a day**, hourly, from around 11:30 CEST to around 22:30 CEST. I chose this time frame since it's good for Europeans but also fills part of the day for people in the US. 
I then divided the tweets into **groups of twos**: the first two tweets would show news from 6 years ago, the following two from 5 years ago and so on, until the last two tweets, which contain news from exactly one year ago. 
To achieve this, in addition to standard PHP coding, I used [cron](https://en.wikipedia.org/wiki/Cron) jobs on my server. This allowed me to automatically call the bot 12 times a day, just when I need it to tweet.

<figure>
  <img src="{{site.url}}/assets/images/2015-09-18/eotTwitter.png" alt="twitter profile screenshot"/>
  <figcaption>The Twitter page where the bot is working 12 hours shift - be sure to follow his hard work!</figcaption>
</figure>

The outcome was nice. It took me about a day to finish everything, but I'm sure a seasoned programmer can achieve this in much less time. If there's enough interest in this I may open source it in the future, but just to give you an idea the bot consists in just about **200 lines** of code. Very simple.

As always, good APIs make work much easier, no surprises here! Actually, there was a surprise... 
And it was each time I opened [Echo Of Today](https://twitter.com/EchoOfToday)! There's something joyful, sometimes sad, in reading and remembering what was happening today, years ago.

___

Thank you for reading! It was very fun to code this bot, I hope you found interesting what's written here.

If you have any question about this, please do ask in the comments, I'm happy to answer and help. 
Should you find any mistake, technical or grammatical, please don't hesitate to let me know!