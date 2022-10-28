# Google Data Analytics Cyclistic Case Study-first project

The dataset was taken from <a href="https://divvy-tripdata.s3.amazonaws.com/index.html">Divvy trip data</a>  under the <a href="https://ride.divvybikes.com/data-license-agreement">licence</a>

<h2>Scenario</h2>

Cyclistic is a bike-share company in Chicago that features more than 5,800 bicycles and 600 docking stations. The bikes can be unlocked from one station and returned to any other station in the system anytime.

Customers who purchase single-ride or full-day passes are referred to as casual riders and customers who purchase annual memberships are Cyclistic members.

Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders.

Therefore, there is a clear goal: Convert casual riders into annual members.

<h2>Business question:</h2>

How do annual members and casual riders use Cyclistic bikes differently?

In order to answer the business question, the six phases of the data analysis process will be followed:

Ask, Prepare, Process, Analyze, Share and Act.

<h3>1.Ask</h3>

First step is to identify the business task. The task is to discover how members and casual use the bikes differently during 2021.

The stakeholders are:

Lily Moreno: The director of marketing and your manager.

Cyclistic marketing analytics team: A team of data analysts who are responsible for collecting, analyzing, and reporting data that helps guide Cyclistic marketing strategy.

Cyclistic executive team: The notoriously detail-oriented executive team will decide whether to approve the recommended marketing program.

<h3>2.Prepare</h3>

After downloading the 12 months of the Cyclistic trip data of 2021 from the link given by Google Data Analytics course, I saved it on my computer in separated folders ordered by month.

Since the data given is taken from the website ride.divvybikes.com we have the following information:

When start or end station is offline maybe the rides are not properly recorded
Bikes missing for longer than 24h are considered taken or stolen
The longer ride is 3 hours (day pass 15$) and then every minute is charged 0.16$ which mean an hour costs 9.6$
After exploring Chicago map and ride stations it’s almost impossible not to find a minutes distance station so to avoid extra charge that is not affordable. So I will consider max ride length: 3 hours/180min/10800 sec.

<b>Spreadsheet program: Excel Sheets</b>

Files are in .csv format.

I made a copy for each month to keep raw data intact, and I opened the files in .xlsx format.

I sorted by started_at and applied filter to check for inappropriate values.

<h3>3.Process</h3>

Different format type detected in ride_id column (numbers instead of letters and numbers) are deleted.

Two columns were added: ride_length, which calculates the time ride in HH:MM:SS (37:30:55), and day_of_week, which extracts the day of the week that the ride took place (=WEEKDAY | custom format ‘dddd’).

Filtering, I discovered many negative time values in ride_length column, which can’t be right, so it was assumed that values were mistakenly inputted into the wrong column by the system and continue by putting them in the right column.

Ride length longer than 24:00:00 is deleted in case of import error in SQL database. Due to big size data the rest will be cleaned in SQL database.

Empty cells also observed in start_station_name, start_station_id, end_station_name, end_station_id, end_lat, end_lng columns. Due to big size data the cleaning will be done in SQL database.

After research I found out that Chicago’s coordinates are:

41.878113–87.629799

So I have to fix latitude and longitude columns (length and format)

=IFS(LEN(K2)=4;K2&”00000";LEN(K2)=5;K2&”0000";LEN(K2)=6;K2&”000";LEN(K2)=7;K2&”00";LEN(K2)=8;K2&”0";LEN(K2)=9;K2;LEN(K2)>9;LEFT(K2;9)) =IF(ISNUMBER(SEARCH(“.”;L2));LEFT(L2;2);LEFT(L2;2))&”.”&IF(ISNUMBER(SEARCH(“.”;L2));MID(L2;4;6);MID(L2;3;6))


<h3>4.Analyse</h3>

View <a href="https://github.com/Dimitra-Nikoloutsou/Google_Data_Analytics_Cyclistic_Case_Study_first-project/blob/4b4eb68bcf2dc94975581e240557d131429ecab9/SQL%20File">SQL File</a>

I exported it in .txt file and imported it in Tableau Public.

<h3>5.Share</h3>

<a href="https://public.tableau.com/app/profile/dimitra.nikoloutsou/viz/BikeData2021-GoogleDataAnalytics/Story1">Tableau link</a> (Interactive Dashboard)

![Story 1](https://user-images.githubusercontent.com/114480002/198726863-3a131a48-e390-4fd7-88dd-bccedd3490ae.png)

<h1>INSIGHTS</h1>

· There are more members than casual riders.

· However casuals ride longer than members.

· Casuals rent more bikes at the weekends while members use bikes all weekdays. The peak of bike share program is in summer season (June, July, August). For that reason, we can say that casuals are visitors.

· Classic bike is the most popular bike for both customers while members rarely use docked bike.


<h3>6.Act</h3>

The marketing analyst team should advertise the campaign before summer season.

In order to convert casual riders into annual members, the company should promote special prices for new members.

Also the company could promote special offers for members making a rewards points system with special deals in local companies.

The marketing team should also consider the possibility of creating another type of membership such as weekend pass.

Another approach would be to raise the price of single-ride or full-day passes and make special deals for new members. From the analysis appears that the average time of casual riders is greater than the average time of members as well as the mean time. That means that they ride longer than members. That way casuals will realise that buying the annual membership is more profitable than buying day passes.

<b>Published in <a href="https://medium.com/@dimitra.nikoloutsou/google-data-analytics-cyclistic-case-study-e164d1f62add">Medium</a></b>

