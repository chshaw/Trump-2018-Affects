
# Effects of Trump Agreement on 2018 Elections

## Motivation
<br>

In this project, I'm attempting to learn how a candidate's agreement with the Trump agenda affected their 2018 vote margin.  I wanted to use publicly available data like the recently released 538 datasets, as well as election returns from CNN.  As well as modeling the effects of agreement with Trump, I wanted to visualize the various elements in a more dynamic, interactive way with Bokeh.

## Executive Summary
<br>

Using the Partisan Voting Index, Elasticity, Gender and Trump Agreement Score, was there an effect on a candidate's 2018 vote margin?  Using both linear regression and a random forest regressor, the model was able to predict the vote margin using those features about 86% of the time.

### Contents:
<br>

- [Data Dictionary](#Data-Dictionary)
- [Modeling](#Modeling)
- [Visualizations](#Visualizations)
- [Conclusions](#Conclusions)
- [Challenges and Future Goals](#Challenges-and-Future-Goals)

## Data Dictionary
<br>
I used the publicly available data from Fivethirtyeight and CNN to make the model, and a shapefile for the districts in the 116th congress.
<br>
<br>

- The fivethirtyeight data can be found at https://data.fivethirtyeight.com.
<br>

- The CNN data came from their election site at  https://www.cnn.com/election/2018/results/house 
 and were scraped by a very helpful gentlemen on the Ycombinator site here:  https://news.ycombinator.com/item?id=18504909.
 <br>
 
- The Congressional Shapefiles came from the US Census Bureau and can be found at
 https://koordinates.com/layer/96077-us-116th-congressional-districts/.
 <br>
 
For the meaning of all the features in the shapefile, refer to their documentation at
https://www2.census.gov/geo/pdfs/maps-data/data/FAQ_for_Census_Bureau_Public_Geocoder.pdf.
<br>
<br>

All other features are explained in the table below:
<br>
<br>

|Feature|Type|Dataset|Description|
|---|---|---|---|
|district|string|538|what congressional district| 
|uncontested|string|538|were they uncontested in the election| 
|116first|string|538|first name of the 116th congressional district winner| 
|116last|string|538|last name of the 116th congressional district winner| 
|116gender|int|538|gender of the 116th congressional district winner|
|116party|string|538|political party of the 116th congressional district winner|
|2018votes|int|CNN|raw 2018 vote totals|
|2018pct|float|CNN|percentage of the 2018 vote captured by winner|
|2018margin|float|created|the margin of victory for the winner |
|congress|int|538|what congressional session|
|115last|string|538|last name of the 115th congressional district winner|
|115party|string|538|political party of the 115th congressional district winner|
|115trump_votes_y|int|538|yes votes for trump bills in 115th congress|
|115agree_pct|float|538|percentage of yes votes for trump bills|
|elasticity|float|538|district elasticity or how fluid they are|
|pvi538|float|538|partisan voter index or how they vote in comparison to the national avg|
|trumpagree -20:20|float|created|trump agreement percentages +/- percentage points|
|ypreds -20:20|float|created|predictions from rf model of 2018 margin based on new trump agreement percentages|

## Modeling
<br>

Using the Sklearn Linear regression and Random Forest Regressor modules, I produced two models aimed at predicting the 2018 voter margin based on the other features.  I did a train/test split on the data to ensure cross validation and I also scaled the data.

## Visualizations
<br>

To make the interactive visualizations, I used the bokeh library which is a very powerful tool that was extremely hard for me to get a handle on.

<br>
It required importing shapefiles in geopandas, then into bokeh. To make everything work properly, all the dataframes had to have a similar index for the districts so a lot of regular expressions were used to format them all properly.

<br>
<br>
Then there was the process of making of visualizations themselves. I found an incredibly useful tutorial from Shivangi Patel at:

https://towardsdatascience.com/a-complete-guide-to-an-interactive-geographical-map-using-python-f4c5197e23e0.

<br>
This helped me form the basic structure of the visualization which I was then able to customize for my own dataset.

## Conclusions

With the datasets available to work with, the conclusion I reached with my model was that Trump agreement percentage had an effect but it wasn't nearly as important as the overall makeup of the district itself.
<br>
<br>
When tuning the model with lower or higher Trump agreement percentages, the visualizations made it clear that certain districts became more red and certain districts became more blue.  They were reverting back to their partisan voting index.

## Challenges and Future Goals

One of the biggest challenges I had was making the visualizations work properly.  I was able to create a slider which would dynamically change the agreeableness percentage but I couldn't implement it.  It required the use of a bokeh server to feed the plot the information and I quite figure out how to get the bokeh server working.
<br>
<br>

In the future, I'll try to fine-tune my model to boost it's performance, as well as trying to get the bokeh server to run and make the dynamic slider work.
