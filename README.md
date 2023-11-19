# Uber_Data_Analysis
Objective: To estimate the revenue figure of Uber in a year in NY and its growth and also aimed to expose all the interesting insights that can be derived from a detailed analysis of the dataset
First of all, we imported the necessary libraries that will be used in this Uber data analysis.
Here we imported matplotlib, seaborn, pandas, NumPy, data time, etc.
We then read the Uber data file. This Uber dataset contains data about Uber’s ridership between September 2014 and August 2015. This dataset contains ~31 million rows and columns of origin, destination, pickup date and time, trip distance, and duration.
The combination of trip distance and duration allows for estimating Uber’s revenue for each trip in NYC. The pickup and drop-off locations were anonymized and grouped as taxi zones instead of geographic coordinates.

Data preprocessing:
We checked data information using the Data.info () command which shows columns and their datatype and memory usage.
Missing data handling:
Here we checked for duplicates and there were no duplicates. Then, I checked the missing values and found that the destination column has around 12 lakh missing values, and trip distance and trip duration have only 38 missing values. I Also checked unique origin and destination points.

Feature engineering:
Here at first, we converted the pickup_datatime datatype into Datetime datatype using pd.to_datetime(df.pickup_datetime) then created a year, month, day, hour, and weekday column for ridership analysis and calculated the average speed for each trip and estimated fair for each trip.
 find holidays to check how it will affect trips.
I converted trip duration into minutes using the Python function.

Then we calculated the mean distance and duration for each origin-destination pair and Replaced 38 missing values with the average distance and duration for the respective origin-destination pair

Outliers Detection:
 An outlier is an observation that appears far away and diverse from the overall pattern. Outlier tends to make our data skewed and reduces accuracy.
We plotted a box plot for trip duration and trip distance to check outliers.
1.	Checked very long-duration entries and the effect on revenue numbers. Greater than 100h: 7 entries (erroneous): system error? fraud? Total revenue is relevant: $14,459,978 (2.4% of total) probable system error.
The effect on revenue is relevant only for the trips higher than 100h of duration, which are most likely a result of some system error, and driving more than 16h (960 minutes) non-stop per day represents unreliable data, these additional 116 cases will also be excluded from analysis.
2.	We calculated a trip for which both trip distance and duration are zero which means that the trip was cancelled. There is at least one case almost daily. The 24866 cases represent a revenue of 198,928, 𝑏𝑎𝑠𝑒𝑑 𝑜𝑛198,928, based on 8 minimum fares.
3.	origin and destination are not the same, but trip distance and duration is zero. did these trips in fact occur? There is generally a fee associated with trip cancellation, so unless these trips represent a system error or fraud, there was no loss of the minimum fare revenue.
4.	Checked cases with distance equal to zero but duration greater than zero, The median duration for trips with zero distance is 10 seconds (mean 2.4 minutes), so most of these 85,515 cases possibly represent trips that were cancelled right after they were registered
5.	Bad traffic conditions so average speed is less than 3 km/h 

Here we found some conclusions:
(1) 2.4% to total revenue estimated by considering a trip duration greater than 100 hours would be a system error and should not be considered for revenue estimation and even a trip duration greater than 16 hours is also not reliable and is also excluded from revenue estimation.
 (2) 24866 cases are cancelled trips that should not be included in revenue estimation.
(3) Average speed less than 3km (i.e. less than walking speed) could be error, fraud or really bad traffic

Data Visualization:
Here we are using data for which the trip duration is less than 16 hours
Created a plot with the total number of trips per day, highlighting some changepoints associated with major holidays and other weather and touristic/cultural events.
And found negative impacts on rides on Thanksgiving, Christmas, Memorial Day, and Independence Day. The plot also highlights which events have positively impacted the number of trips that year, with the International Marathon and the Gay Pride Week standing out as the strongest contributors

The effect of time on demand for Uber rides: distribution per hour, weekday, and month are plotted using a bar chart plot 
•	In the bar charts , we can see that the demand for Uber is higher from 4 PM until around midnight.
•	Found demand is gradually increases from Monday to Saturday and Saturday has the highest demand. Interestingly, Sunday shows a level of demand similar to Wednesday, which is higher than Monday or Tuesday.
•	When looking at the total demand per month along the period analyzed, seasonal effects are masked by the consistent month-to-month growth.
Estimated Monthly Base Revenue: how much was the NYC market worth in the period?
•	It’s important to note that from the gross estimated revenue, Uber’s share is about 25% of the total. Therefore, we can conservatively estimate that Uber’s gross margin in NYC from September 2014 to August 2015 was in the order of 150 million dollars. The estimated gross margin, considering the 27 average fare previously mentioned, was of the order of 210 million dollars.
•	The total revenue of Uber in 1 Year is 595M and the Gross margin of 149M.
•	In bar plot we observed that revenue per month generally increases month by month in that period except for the month of January and June, this may happen because of 2 Federal holiday's in the month of January and summer vacation starting from july
Plotted Month over Month Base Revenue Growth: how fast has Uber grown in the period.
Plotted Cumulative Base Revenue Growth Over the Period
•	In the above two analyses, we get to know that revenue per month generally increases month by month in that period except for the month of January and June, this may be happened because of 2 Federal holidays in month of January and summer vacation starting from july.
•	We get to know that revenue increased by ~84% in a period of one year
A created plot similar to the above but with the count of trips per hour, comparing weekday vs weekend and distances >=5 versus < 5 miles. Indeed, the plots show that there is a higher demand for trips that go beyond miles (outside Manhattan) from 5 to 7 AM on weekdays, and from 6 to 8 AM on weekends (Saturday and Sunday). We found that number of long trips is greater than the number of short trips, and this occurs both on weekdays and weekends, although at slightly different times: the demand is higher for longer trips from about 5 to 7 AM on weekdays, and from 6 to 8 AM on weekends
most popular pickup and drop-off taxi zones
•	The top 5 locations for origin and destination are the same: 2A, 15, 4C, 1, and 6B (likely all in Manhattan).
•	The top location for pick up and drop off, 2A, accounts for more than the total trips for the next two popular locations.
•	Top origin codes are probably based in Manhattan. In this case, the top destination codes are also based in Manhattan

The relation between a trip’s duration and distance is not entirely linear. Rather, it approximates to a power function because the shorter trips, occurring mostly within busy areas of traffic, tend to result in lower average trip speed.
Plotted the total number of trips per month during peak hours and off-peak hours
