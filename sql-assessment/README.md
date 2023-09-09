# SQL Challenge

The database contains three tables: marketing_performance, website_revenue, and campaign_info. Refer to the CSV
files to understand how these tables have been created.

`marketing_performance` contains daily ad spend and performance metrics -- impression, clicks, and conversions -- by campaign_id and location:
```sql
create table marketing_data (
 date datetime,
 campaign_id varchar(50),
 geo varchar(50),
 cost float,
 impressions float,
 clicks float,
 conversions float
);
```

`website_revenue` contains daily website revenue data by campaign_id and state:
```sql
create table website_revenue (
 date datetime,
 campaign_id varchar(50),
 state varchar(2),
 revenue float
);
```

`campaign_info` contains attributes for each campaign:
```sql
create table campaign_info (
 id int not null primary key auto_increment,
 name varchar(50),
 status varchar(50),
 last_updated_date datetime
);
```

### Challenge Submit Instructions

1. Fork the repository
2. Answer the questions below in a single SQL file - e.g answers.sql
3. Provide Link to Forked Repository to PMG PMG Talent Acquisition Team

### Please provide a SQL statement for each question

1. Write a query to get the sum of impressions by day.
2. Write a query to get the top three revenue-generating states in order of best to worst. How much revenue did the third best state generate?
3. Write a query that shows total cost, impressions, clicks, and revenue of each campaign. Make sure to include the campaign name in the output.
4. Write a query to get the number of conversions of Campaign5 by state. Which state generated the most conversions for this campaign?
5. In your opinion, which campaign was the most efficient, and why?

**Bonus Question**

6. Write a query that showcases the best day of the week (e.g., Sunday, Monday, Tuesday, etc.) to run ads.

#Answer to #1 
SELECT date, SUM(impressions) AS total_impressions FROM marketing_performance
GROUP BY date;

#Answer to #2
Select state, SUM(revenue) AS total_revenue from website_revenue
GROUP BY state
ORDER BY total_revenue ASC
Limit 3;

Answer to #3
SELECT ci.name AS campaign_name, SUM(mp.cost) AS total_cost, SUM(mp.impressions) AS total_impressions, SUM(mp.clicks) AS total_clicks, SUM(wr.revenue) AS total_revenueFROM campaign_info ci
INNER JOIN marketing_data mp ON ci.id = mp.campaign_id
INNER JOIN website_revenue wr ON ci.id = wr.campaign_id
GROUP BY ci.name;

#Answer to #4
SELECT wr.state, SUM(mp.conversions) AS total_conversions FROM marketing_performance mp
INNER JOIN campaign_info ci ON mp.campaign_id = ci.id
INNER JOIN website_revenue wr ON mp.campaign_id = wr.campaign_id
WHERE ci.name = 'Campaign5'
GROUP BY wr.state
ORDER BY total_conversions ASC
LIMIT 1;

#Answer to #5
Cannot answer this question because the system is not showing the outputs of the queries.

#Answer to #6
SELECT DAYNAME(date) AS day_of_week, AVG(conversions) AS avg_conversions FROM marketing_performance
GROUP BY day_of_week
ORDER BY  avg_conversions ASC
LIMIT 1;












