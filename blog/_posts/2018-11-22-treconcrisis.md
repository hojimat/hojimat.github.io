---
layout: post
title: The future of economic publishing
lang: english
categ: blog
keywords: statistical consulting, economic consulting, data analytics, econometrics, economics, Turkey
tags: economics finance
---

I finished my thesis on Financial Economics at the beginning of this summer. I performed simulations for different investment strategies for Turkish households, to see which investment option is the best.

Of course, I used in my study the main economic indicators for Turkey, like inflation and 10-year Treasury yields.

Then I went on a summer break to visit [_Kyrgyzstan_](https://en.wikipedia.org/wiki/Kyrgyzstan) and my supervisor spent the summer planning for his wedding.

Meanwhile, I didn't read a single article about Turkey, as I was busy swimming in the river and having fun, trying to forget everything related to my grad school experience.

I didn't return to Turkey, but in October, I got in touch with my advisor via email, and he suggested that we publish the thesis in a journal. I happily agreed and started editing my thesis to satisfy the journal's guideline.

But then I decided to check the numbers, and realized that I missed the [_Turkish currency and debt crisis of summer, 2018_](https://en.wikipedia.org/wiki/Turkish_currency_and_debt_crisis,_2018) altogether. The numbers changed by hundreds of percentage points!

I am still incorporating all the changes, because I didn't keep my _R_-codes organized, and had to work my way through half-forgotten chaos. But even if I had clean R-codes, I still would have spent time, incorporating changes into the LaTeX file.

And then I thought, how many more articles and journal issues that have already been printed, are like mine. Their data is obsolete, their conclusions are wrong. I've always known that economics is not physics, but I have never experienced this first-hand. This thought never left me since --- printing economic papers seems useless. But what can we do?

The only answer that I could come up with is to force the empirical works to have a web-based dynamic pages, which would change the resulting numbers by automatically updating the input data every month. This is not too hard to execute, but it will be very expensive --- the journals will have to rent a lot of cloud storage with virtual machines running on them (to run RStudio and LaTeX).

Also, the archive of publications should be created, where everyone can keep track of historical versions of the paper.

And, of course, the article authors should think about all the possibililites beforehand, and write their text with "if-then" conditionals. The text will change together with the data. There is no need to do comprehensive text changes --- just  2-3 versions of text, linked to critical values.

This all seems overly complicated, and it really is inconvenient, if your only incentive is to graduate/publish/whatever. However, if you really care about economic research, you should understand that there is no other way to ensure the survival of the empirical economics in the future.
