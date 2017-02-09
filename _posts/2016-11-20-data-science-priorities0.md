---
layout: post
title: Google Analytics for Product Analysis
date: 2016-08-08T00:00:00.000Z
desc: Why your startup should not use Google Analytics for Product Analysis
keywords: Data Science
categories:
  - Data Science
tags:
  - Data Science
icon: icon-phone-gap
---

The most common question I receive when I talk about our data pipeline and the solution to process event data is:

Why not just use google analytics?

The simplest answer is that Google Analytics is not designed to be a product analytics tool (insight into your web/app product and user behavior) but rather marketing analytics (number of sessions, number of hits). With the pervasiveness of Google analytics, it's name is somewhat synonymous with event tracking and analytics itself. but beyond a certain scope it fails to serve the most crucial analytics needs.

# Delivering a Flexible and Comprehensive Analytics Product is Difficult

Let me give you an example company that provides a two-sided marketplace. This company offers a platform for _sellers_ to offer services to _buyers_, in between there are lurking _free users_ we either hope to convert to _buyers_ and _sellers_. Where buying and selling behavior is concerned, there are 4 locational segments.

- 3 user types
- 4 different regional segments.

Outside of user attributes, behavior on key features allows us to segment based on that features usage and on the users who use them. Let's just look at a simplified version of purchasing. We could have two pricing models, where examples of different pricing models could be directly buying, bulk buying, bidding between other buyers on the product, a subscription service etc. For simplicity's sake, _sellers_ on our platform are able to offer their services with two different pricing models. Additionally, although you sell one type of service, there are 5-6 subcategories of services a _seller_ can offer. Even now, with a fairly simple business, you have:

- 6 subcategories of services
- 2 different pricing models.

Already we have 3_4_6*2 = 144 different ways to look at any one or any group of users and their behavior. This does not take into account, some users buy or sell from multiple subcategories or use two different pricing models. It's very important to note that some users and behaviors are more important in terms of value to the business and so it's useful to segment according to value. Determining these value-based segments is an (important) task in of itself. But it's safe to say that if you have a data analyst, she or he is already overwhelmed and Google analytics is struggling to allow for such complicated slicing and dicing of data.

Compared to the fake website I illustrated above, most businesses products are much more complicated in reality.

This is a rough breakdown of italki's analytic complexity:

User segmentation

- 3 Overall User types
- 2 Teacher subtypes
- 3 Buyer value-based subtypes
- 4 relevant Onboarding types
- 100 countries, 6-8 regional groupings
- > 100 languages (product of interest)

For specific feature behavior or concepts:

- 3 pricing models
- 4 community features (non-monetized)
- Buyer Activity (active, re-activated, churn)
- Login Activity (active, re-activated, churn)
- Funnel (flow from one step of on-boarding to another)
- Registering
- Search
- Viewing products
- Checkout pages
- Purchasing
- Misc (edit profile, view friends)
- example: User of type XX performed purchased Y in 7 days after registering
- example: All users of type XX who purchased in timeframe Z searched for Y in 24 hours.
- Individual Product view (same as above)
- example: User of type XX performed search Y within timeframe Z
- example: User of type XX performed viewed product page Y within timeframe Z
- example: User of type XX performed viewed product page Y within timeframe Z and more.

# Analysis is about exploration

Google analytics is easy to setup and extremely capable at gauging where your traffic is coming from and where it's going. Where it fails in comparison to product analytics solutions (MixPanel, Segment etc) is in it's ability to tackle complicated segmentation and a view of user's longterm behavior and interactions with the product.

Google analytics can technically allow for segmentation, but because Google Analytics show's data in aggregate, your analysts need to be almost prophetic in all the types of different segmentations and the most important patterns in user behavior. If you capture data in Google Tag Manager incorrectly, there's no going back and reanalyzing. **We know that the data science process is largely explorative**, so the google analytics approach to collecting data isn't well suited for these problems.

# Machine Learning

An additional concern is that, eventually, your data scientists will want to build predictive models out of your data. Wether or not this is used on a machine learning product that actually effects your users or that it is simply used to understand user behavior, these models require significant feature engineering. This requires that

a) You can view and manipulate raw event data. b) You have complete ownership of that data.

Unfortunately, Google Analytics does not allow you to accomplish either point. MixPanel and Segment make much more ground on both points, but still largely fail to give a data science team the ability to build and refine any models.

# Closing thoughts

Depending on the size of your business, most likely you need to build your own solution sooner than you think. You can certainly pay for other companies to track data (MixPanel, Segment), store and analyze them, or you can build them yourself. I have much to say about this question. But I'll

```
ionic plugin add cordova-plugin-splashscreen
```
