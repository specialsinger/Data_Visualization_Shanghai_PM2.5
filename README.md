# Data_Visualization_Shanghai_PM2.5 - Bing Yu

## Summary

This chart shows the key air quality index - PM2.5 value (particulate matter less than 2.5 micrometers in diameter) of Shanghai varies with time, from 2012 Jan to 2015 Jun.  The line shows a clear seasonal pattern, PM2.5 value is highly related with season, summer is better and winter is worse. And the reader could drill down and up to view different level of details.

## Design

The source data is the hourly recording of PM2.5 value, loading from www.stateair.net
After analyzing data for Shanghai, I figured out a clear pattern of PM2.5 value varies along with time. Summer time (July and August) has lower PM2.5 value while winter time (Jan and Dec) has higher value. It means that PM 2.5 value has strong relation with seasons.
The targeting readers of the charts are for those who are living in Shanghai or planning to visit to Shanghai. The key message is PM2.5 value is highly related with season, summer is a good time to visit Shanghai with clean air or arrange any outdoor event, while in winter it is better to stay inside. The chart should also give user an idea on the overall air quality of Shanghai in the past few years.

### Initial design
In order to clearly show the PM2.5 value varies with time, I chose line chart as chart type. Use time as x- axis and PM2.5 value as y-axis, and I created two charts as initial trying. 

The first one (please refer to index_initial1.html for more details) use Date as x-axis, the data series is the average PM2.5 value of all of the hourly recording for that date. The line shows the PM2.5 value of each day, and I have set the x-axis time period to month for a clearer view.

The second one (please refer to index_intial2.html for more details) uses Month as x-axis, and use year as different category for creating the data series. So the line shows average PM2.5 value for each month, and different color of lines indicate the year of 2012 to 2015.

### Updated design

For Chart One, the feedback is has too much noise and takes too long to load, and it is hard to locate the data point and read the value. So I made the following changes in the updated chart one (please refer to the file of index_initial1_update.html):
-	Change the x-axis to year-month, to summarize the data for each month
-	Update the data series to the monthly average PM value, it will smooth the line and reduce the noise
-	Increase the line weight to 5 and enable line markers, so the data points are more clear
-	Add one event handler for clicking on the data points, which will drill down to myMonthChart so the reader could still see the daily value as before.
-	Create myMonthChart to show the daily average PM value for the selected month
-	Add event handler for daily view chart, which will drill up to the monthly view
For Chart two, reviewers would like to filter the data by different year, so they could compare the data for selected years more easily.
-	Add interactive legend of years, when clicking the legend, it will show/hide the line for the specific year data 
-	Set font size to ‘Auto’ so it could be more clear to the reader
-	Set the series line weight to 5 and enable line markers so the data points are more clear

### Final design 
After considering all of the feedback I got, Chart two does not deliver more information since there is no clear message after comparing the data of different years. And it is a little bit distracting while having different color and lines. So I choose Chart one as the final chart and re-write the codes to improve the performance and one more level of drilling down to hourly data:
-	Clean up the data file to remove the unnecessary data points, leave only two columns of ‘Datetime’ and ‘Value’, this will reduce the time and data size while loading the data.
-	Define three different view: ‘month’, ‘date’ and ‘hour’ to show different level of data, use the variant ‘currentSize’ to indicate the current view. Then readers could drill up/down to see different level of information. 
-	Add background to SVG, and add the event for handling clicking on the background, link the action to drill up function
-	Create global variables ‘start’ and ‘end’ to capture the selected data time period, and use  ‘dataCache’ to store the data for drawing of different views.
-	In the drill up/down and draw function, use switch function on currentSize to capture the current view and draw the view required.
-	In the draw function, calculate the mean value of the data before drawing by using d3 nest function, this is to help improve the performance of drawing.
-	Add a title of time period to show the current start/end time along with the selected view

## Feedback

### For initial design
###### Xu, Polly (colleague from GE, IT leader for global commercial & service)
I like the first one, it looks more professional in the first chart. But it is hard to see the specific value for a date, the number needs to be larger.

###### Bu, Tracy (colleague from GE, working as IT project manager for digital marketing and communication)
The chart shows the same as I feel, shanghai has better air quality in summer. For both charts, the data point is not too clear for each given date or month on the line, reader is hard to get the exact value.

###### Chen, Chenjia (Friend from college, working at Yahoo right now)
Chart one has too much noise and it is hard to read. It is easier to see the PM value change trend with months through chart two, as the line is smoother, and clearly shows the same pattern among different years. For chart two, can I have the function of selecting two years like 2015 and 2012? Then it would be easy to compare the data from two years and see if there is any big improvement. And you may want to use bigger fond for user to read it easily.

###### Zhou, Lijie (Friend from high school, studying computer science at US right now)
I like both of the charts, they all look clean and straight forward, from which I could easily see the trend of the PM value changing with time. It is useful to let people know that July and Aug is a good time to visit Shanghai with a clean air. I think the second one is better, since it is a little hard to identify the year start/end time of a year from the first chart, while it shows clearly through the 4 lines in chart two. 

###### Bao, Lin (Friend, working for EA)
If you want to show that PM2.5 is highly related with season, both charts work well. But chart one takes too long to load the data. I used Timeline tool to check, chart one takes 25000ms, while chart two takes 6000ms.This needs to be improved.


### For updated design:
###### Bu, Tracy
Chart one is more clear now, and the drill down function works well, only drill up is too slow. For Chart Two, the four different line is a little bit distracting, I did not see any specific results from the yearly comparison. I think it is more clear in Chart One, where you can see the up and down over the years, and the wave pattern of each year is more obvious.

###### Chen, Chenjia
The drill-down function is good for Chart One, but drill – up is too slow. For Chart Two, it is good to have the interactive legend for comparing yearly data, but I did not see a clear message from this comparison, it seems there is not significant improvement over the years.

###### Zhou, Lijie
I like the Chart One drill-down function to view the PM value for a specific date. I heard the PM2.5 value is lower in the morning and higher at night. Not sure if it is sure, can I further drill down the hourly view to verify this?

###### Bao, Lin
It still takes too long to load the chart one, you may want to clean the data to make it quicker.

### For final design
###### Tracy
The chart is clear now. It is simple and clear regarding to the PM2.5 change with time and the guidance for drill down and drill up is useful.

###### Zhou, Lijie
The performance is good, and I like it is drilling down from monthly to daily to hourly. I checked a few days’ hourly view, it turns out there is not a clear pattern for the hourly PM2.5 value, sometimes morning is better, while sometimes night is better.
 
###### Bao, Lin
It works pretty well now and the overall performance has been improved.

## Resource
Thanks Hanson Wang who has helped me setting up the local web server through Windows IIS manager. And Thanks Bao, Lin, who has helped me on using nest function of d3 while handling the data to improve the performance.
For the online resource reference , please refer to the file of reference.

### Data
Shanghai PM 2.5 historical data is downloaded from stateair.net and the detailed definition of each column could be found the fact sheet file,
I have firstly loaded shanghai historical data csv files from the website above for 2012 to 2015 Jun, and then consolidated the separated yearly files into one file. I removed all of the invalid values, which was indicated as ‘Missing’, the consolidated data file is ‘ShanghaiHourlyPM25.csv’, which was used in the initial and updated design.
I kept only the two columns of ‘DateTime’ and ‘Value’ in the updated data file ’data.csv’ for improving the performance, which was used in the final design of index.html

