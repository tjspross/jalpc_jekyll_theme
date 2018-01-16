---
layout: post
title: Analyzing rental listings - finding a cheap Shanghai apartment
date: 2018-01-09T00:00:00.000Z
desc: 
keywords: Shanghai,apartment hunting,rental
categories:
  - Shanghai
tags:
  - Shanghai
icon: icon-phone-gap
---



For the past several months I've been scraping listings data from [SmartShanghai](smartshanghai.com). Since the rental market for foreigners is large and robust enough to perform simple data analysis, I might be able to provide some tips for finding cheap apartments in Shanghai.


SmartShanghai’s listing service is the most widely used online apartment hunting service for foreigners new to Shanghai. Before we dig into the data there are a couple points that we should be clear on.




1. Very, very cheap apartments (<4000 CNY) are rarely listed, so any summary statistic below (median, average price)  is a little bit skewed to a higher value - but not by much. If you want to find these apartments you can walk into an agency and ask. These apartments often have some sort of catch (shared bathroom, shared bed, fake landlord etc) whereas SmartShanghai listings I analyze below are more standard, standalone apartments, not sublets.

2. The foreign rental market is on average more expensive than the market for Chinese renters. The biggest reason is that the makeup and salary of these two groups of renters is different. If we control for full apartments (non-sublets) the price for a two bedroom a foreigner might find though an English-speaking agent is not going to be much higher than the price a local might find. If it is higher it’s likely possible you can negotiate to the same price point. 


# **How to get the best deal on your apartment rental in Shanghai**

## **1. Move to less obvious, but still central neighborhoods.**

On a map, you can cover the most expensive swathe of Shanghai if you draw a diagonal line from the Bund to Xujiahui. Anywhere near West Nanjing Road, Xintiandi, IAPM (South Shaanxi Metro Station) or Yongkang street appears to be the most expensive. 

{% include 2br_median_price.html %}

Once you start moving north or west of Jing’an Temple, prices for rentals start to drop dramatically. Rental prices near Changping Road, Jiangsu Road, and even West Yuyuan Rd are 20-30% cheaper than apartments in central Jing'An and French Concession. Median price for a 2 Bedroom near Jiangsu Road Metro Station is 10,350 RMB, compared to the 14500 RMB median price near Jing An Temple, just 1 metro stop away. 

Other areas I find interesting or what I call border districts. They are on the border of western-friendly central Shanghai and the border of the concrete high-rise sprawl of the surrounding areas. These border districts include Changping Road, Jiangning Road to the north, and Jiashan Road and Dupuqiao to the south. These districts are interesting because just by crossing one street you see drastically different prices.


## **2.  Understand what drives prices up.**
If I made ranking of what factors determine apartment prices it would be:

1. Square meterage
2. Amenities, furnishings and “niceness” of the apartment
3. Location
4. Other factors...
	
Square meterage is number 1 by far. Square meterage is very strongly correlated with the price of the apartment. You could build a fairly accurate model that predicts apartments prices just by using the size of the apartments alone. Number of bedrooms does not provide any further influence on price than square meterage does so we can ignore it. Same goes for number of bathrooms.

This is helpful, because now we can calculate for each listing it’s _**monthly rental price per square meter**_ and compare different districts using their apartments price per square meter. Apartments with a high price per square meter for an area are either very nice and well furnished or they are overpriced. This also helps us better compare districts (see below).

For Changshu Road, one of Shanghai's the most expensive areas in the middle of the French Concession, on average the price per square meter is 165 RMB. Meaning a 60 sqm apartment in Changshu Rd will cost you 9900 RMB per month.

![My gif](/assets/smartshanghai/ppm_changshu.gif)

If you are paying 12,000 RMB a month for 60 sqm, you are paying 200 RMB per square meter. Either you have a very well-furnished apartment with nice amenities or the apartment is in a historic building **or** you are overpaying. In the Changshu Road area, 200 RMB per square meter is in the top 15% of price per square meter apartments. 

Because quality of furnishings, style and amenities are hard to quantify from listings data, only you can justify wether a high price per meter or a low price per meter suits the apartment you are looking at. 

For example, my apartment near Jing'an temple was 4500 RMB a month for a 40sqm 1 bedroom. This comes down to 112.5 RMB per month per square meter, significantly cheaper than the average 150 RMB per month per square meter apartment in the same area. Part of the reason we were paying so little is because 1) the landlord was just managing property for overseas family and didn’t care about money  and 2) the kitchen is separated from the main room by a flight of stairs.

## **3. Use a calculator to determine standard rental rate for that area**

Here’s the breakdown of average price per square meter by area.

{% include avg_ppm.html %}

As a starting point you can use the average price per square meter in an area to figure __how much you should be paying__. 


Like in the Changshu Rd plot above, theirs decently large variation in price per square meter for a given area. The standard deviation in price per meter is between 30 and 40 RMB per square meter. This means that if you’re lucky and you find an apartment in the bottom 15% of price per square meter in Jing'an temple, you will pay 6500 RMB a month instead of the average 9000 RMB a month. If you are very lucky and find an apartment in the bottom 2.5%, you could be paying 4400 RMB for a 60sqm apartment!! 

It’s likely you are giving up some amenities and overall quality, but I think the main point is:

**If you look hard enough and are patient you can find significantly underpriced apartments.**
	
If you go up north to Changing Rd or Zhenping Rd, the variability in quality of apartments starts to diminish and price per square meter seems more standardized. The standard deviation for price per square meter is 20 RMB per square meter in those areas. I suspect this is because the high-rise apartment buildings in these areas are developed by a handful of companies and apartments are more standardized. It might be harder to find good deals or really well-furnished apartments outside of the French Concession.

## **4. Choose between a laofang or a high-rise apartment building.**


![LaoFang Apartment](/assets/smartshanghai/laofang_inside.jpg)

**Laofang Apartment/ Walk-up/ Lane House**

![High-rise Apartment](/assets/smartshanghai/highrise_inside.jpg)

**High-rise Apartment**

<br>
<br>

People tend to think that Lane houses (laofang 老房) are cheaper and that lane houses are more likely to be really nice, or really really squalid. So they have higher variability in quality.

<br>

This might be true when you central Shanghai to areas outside of central Shanghai. But in central Shanghai or in the French Concession area, neither point is true. For the first point, it’s true 1 bedroom or 2 bedroom laofangs are cheaper than places in apartment buildings. But this is only because laofangs tend to be smaller. **If we look at price per meter, laofangs and apartment buildings are exactly the same in the French Concession.** The graph below also suggest that laofang and apartment buildings are just as likely to be overpriced or underpriced according to the mean. So you’re just as likely to find well-furnished high-rise apartments as you would find well-furnished laofang apartments. The same goes for underpriced or poor-quality apartments.

![High-rise Apartment](/assets/smartshanghai/ffc_2br_laofang_vs_hr_ppm.png)

Although the data suggests the price differences aren’t huge, subjectively, I do believe these two types of apartments have pretty different style and aesthetics, so it’s best to choose the apartment style that suits your preferences. You do not have to worry that you are overpaying or underpaying because you chose one type over the other.
