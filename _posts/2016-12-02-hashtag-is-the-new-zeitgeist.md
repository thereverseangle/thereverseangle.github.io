---
layout: post
title: Hashtag is the new Zeitgeist
description:
author: author
---

> Honestly, it was very hard for me to understand how I’d have to publish these data without seem at least bit “partisan”.
Well, I don’t work for any political party, either the Italian Govern. This is “just” Science.

Twitter analisys for the **Italian Constitutional Referendum** vote of December, 4th 2016.

Codebook
========

I made this analisys coding with **R** and the complete repository is available at my [GitHub](https://github.com/ukaoskid/ita-ref-twitter-analisys)
(don’t be disgusted by my code, I was just pratical). Always on my repository you can find a better detailed Codebook,
because here I’ll be quite brief just to not write a 20 page book.

The reform that Italians are called to vote is, shortly, a “_Political reform pointing to Senate power reduction, 
number of Senators reduction, Regional competencies resize, Public administration resize”._

So, “pleasantries” are done, now the main dish!

Introduction
------------

Twitter data collection for Italian Referendum Vote Day. This study has to be intended for a experimental purpose.

Prerequisites
-------------

*   Taking tweets by geolocation ﬁltering and hashtag ﬁltering
    *   Negative opinion `#IoVotoNO, #BastaUnNO, #IoDicoNO, #VotaNO`
    *   Positive opinion `#IoVotoSI, #BastaUnSI, #IoDicoSI, #VotaSI, #IoVotoSì, #BastaUnSì, #IoDicoSì, #VotaSì`
*   Geolocation granularity minimum level is Metropolitan City
*   Positive and negative meaning hastags cannot coexsists in the same tweet
*   User are grouped simulating one vote

Output data for YES and NO
--------------------------

*   Daily heatmap and total heatmap
*   Daily trend for Big Area, Geo District and whole Nation
*   All datasets used for build up charts and heatmap

Geopolitic subdivision
----------------------

*   Metropolitan City
*   Big Area
*   Geo District
*   Nation

Subdivision Masterdata
----------------------

Geopolitic subdivision is took from [ISTAT](http://www.istat.it) (Italian National Institute of Statistics).
Population data is referring the last Census survey (2014)

Available datasets after processing
-----------------------------------

*   `tweets_global` (all the extracted tweets)
*   `global_users` (all the users grouped by Geo parameters and willing vote)
*   `vote_results` (aggregate by Geo parameters)
*   `big_area_results` (aggregate by Big Area)
*   `geo_district_results` (aggregate by Geo Disctric)

Extraction and Data process flow
--------------------------------

![data_flow_diagram](/assets/posts/2016-12-02-hashtag-is-the-new-zeitgeist/img/data_flow_diagram.png)

Data extraction and process flow

**R**, is a very powerful programming language. The very interesting thing is that even if you are “noob” with it,
you will be capable of doing what you have in mind thanks to the high amount of libraries available and the huge size of
the developers community. Clearly, if you are already used to code in any OOP language the play is easy. The game can be
even more easy if you come (or feel confident) with any C-like programming language.

Basically, I started by extracting separately the Negative and the Positive opinions. It’s a bit curious,
but before doing this analisys I took for granted a couple of concepts. One of these is “generally people know how to behave
and post/tweet thoughts on a Social Network”. I was wrong. Totally. But, why? Because when we are talking
about sharing thoughts through a Social Network we have to consider two or three things, at least:

1.  Being honest/not deceiptive in filling profile data
2.  Being able to convert into very few words what you have in mind
3.  Using, technically, the features of a Social Network, for instance, the **hashtag**

Guys, I know that many of you at this point thinks I’ve been common, but believe me, this is not so banal.
Up to three weeks ago I would have done the same though, that everyone of us execute the steps I listed above.

I made this conclusion after my first dataset extraction. When I looked at it I remained quite confused:

*   People are putting both the Positive and Negative hashtag in the same tweet
*   People are twitting one time the Positive and another time the Negative hashtags
*   Low usage of the mother tongue (many of them are using dialects)
*   High usage of slangs
*   High percentage of not-honest/deceiptive profiles, like
    *   In the “Location” field you are expecting to see something like “New York”, but I found things like “Mars”,
    “Informatic Engineer”, “Milky Way”, “Not your business”

So, my first reaction after 30 minutes was to have mistaken all the suppositions. At the very first start I made my plan too easy.
What an idiot. After realizing that people are not stupid, I understood why being a Data Scientist is hard.
I tried to put myself in the shoes of an average Twitter user and, out of the blue, here the answers:

*   Users are not aware of what really is and what value have a hashtag. For them it’s something just “trendy”. **#HeyIHadReallyABadIdea**.
*   There is not a course that teaches users “how to use a Social Network” or “Social Network for dummies”, and then,
    came on, who will really do it? Social Networks are not cars, you don’t need any drive license (even if in some cases…)
*   Data Scien… Whaaat?
*   Generally users ignore the layer of statistics made every single day on their behaviors and ignore also the fact
    that a little innocent sharp (**#**) can weight like a rock for many topics (like Elections)

I have not gave up. Solution was:

*   Build up filters to discard tweets with both Positive and Negative meanings
*   Extract tweets by geo-location filter (provided by Twitter Search API)
    *   Cannot rely on data provided by users
    *   Geo-located tweets are really really few
    *   Twitter doesn’t allow us to have the real user geo-location
*   Understand the possibile real location for each user by doing a geographic mean
*   Understand the frequency of Positive and Negative expressions for each user

Poll Results
------------

### Preface

The data observation time-frame started from November, 3rd 2016 and ended on November, 30th 2016.
To make this analisys clear and transparent we have to put some notes on top of the charts, in order to read data in the proper way:

*   Tweets sample: **166576**
*   User sample: **17256**
*   Italian internet users are the **62%** of the population (source is [Statista.com](https://www.statista.com/statistics/262223/number-of-internet-users-in-italy/))
*   Only the **11.74%** (source is [Statista.com](https://www.statista.com/statistics/569968/distribution-of-social-media-used-italy/))
    of the Italian internet users are really active on Twitter. Given that, we can continue in saying that “this is, however,
    a good sample to consider”, but we cannot say that it is representative of the whole nation
*   Twitter users may not vote in real life
*   Twitter users may not vote what they apparently made evident
*   The analisys in topic has an experimental purpose (it is a simple exercise) and it is only representing
    the orientation of the Italian Twitter users
*   The analisys is not making any kind of propaganda. These are scientific data

### Points involved in the Referendum

Unfortunately for non-Italian people, the reform’s original text is in Italian, but a Wikipedia page is present and
summarizes the purpose also in English:

*   [Govern official reform text](https://dl.dropboxusercontent.com/u/52092659/ref/DLAC2613-D.pdf) (only Italian)
*   [Wikipedia Italian consitutional Referendum 2016](https://en.wikipedia.org/wiki/Italian_constitutional_referendum,_2016) (English)

### Charts and Outputs

#### Heatmap

![2016-11-30](/assets/posts/2016-12-02-hashtag-is-the-new-zeitgeist/img/2016-11-30.png)

Italian Constitutional Referendum 2016 Heatmap

#### Big Area

![2016-11-30](/assets/posts/2016-12-02-hashtag-is-the-new-zeitgeist/img/2016-11-301.png)

Italian Constitutional Referendum 2016 Big Area

#### Geo District

![2016-11-30](/assets/posts/2016-12-02-hashtag-is-the-new-zeitgeist/img/2016-11-302.png)

Italian Constitutional Referendum 2016 Geo District

#### Overall

##### Rolling Chart

![2016-11-30](/assets/posts/2016-12-02-hashtag-is-the-new-zeitgeist/img/2016-11-304.png)

Legenda:

*   **YES**: Cumulative YES vote
*   **YES_D**: Daily YES vote
*   **NO**: Cumulative NO vote
*   **NO_D**: Daily NO vote
*   **UD**: Cumulative UNCLEAR vote
*   **UD_D**: Daily UNCLEAR vote

##### National Pie

![2016-11-30](/assets/posts/2016-12-02-hashtag-is-the-new-zeitgeist/img/2016-11-305.png)

*   Yes: **26.65%**
*   No: **62.31%**
*   Unclear: **11.04%**

#### Twitter data

##### Tweets vs Retweets

*   Tweets: **45%**
*   Retweets: **55%**

##### Possible NO user propagation

Just a note about this information. Obviously the propagation needs a separate study, but I want only to show you the possible “potential” of a tweet

*   Possibile NO user propagation: **19.171.959**
*   Possible YES user propagation: **6.196.789**