
#  YouTube Insights - Data Analysis Using SQL
*__I am sharing Global YouTube Statistics Insights - A Data Analysis Project performed on SQL in my journey into Data Science.__*
                         
 # About dataset
 
  A collection of YouTube giants, this dataset offers a perfect avenue to analyze and gain valuable insights from the luminaries of the platform. With comprehensive details on top creators' subscriber counts, video views, upload frequency, country of origin, earnings and more

### Key Features

* *__Rank__* : Position of the YouTube channel based on the number of subscribers<br>
* *__Youtuber__* : Name of the YouTube channel<br>
* *__subscribers__* : Number of subscribers to the channel<br>
* *__video views__* : Total views across all videos on the channel<br>
* *__category__* : Category or niche of the channel<br>
* *__Title__* : Title of the YouTube channel<br>
* *__uploads__* : Total number of videos uploaded on the channel<br>
* *__Country__* : Country where the YouTube channel originates<br>
* *__Abbreviation__* : Abbreviation of the country<br>
* *__channel_type__* : Type of the YouTube channel (e.g., individual, brand)<br>
* *__video_views_rank__* : Ranking of the channel based on total video views
* *__country_rank__* : Ranking of the channel based on the number of subscribers within its country<br>
* *__.channel_type_rank__*: Ranking of the channel based on its type (individual or brand)<br>
* *__.video_views_for_the_last_30_days__* : Total video views in the last 30 days<br>
* *__.lowest_monthly_earnings__* : Lowest estimated monthly earnings from the channel<br>
* *__.highest_monthly_earnings__* : Highest estimated monthly earnings from the channel<br>
* *__.lowest_yearly_earnings__* : Lowest estimated yearly earnings from the channel<br>
* *__.highest_yearly_earnings__* : Highest estimated yearly earnings from the channel<br>
* *__.subscribers_for_last_30_days__* : Number of new subscribers gained in the last 30 days<br>
* *__.created_year__* : Year when the YouTube channel was created<br>
* *__.created_month__* : Month when the YouTube channel was created<br>
* *__.created_date__* : Exact date of the YouTube channel's creation<br>
* *__.Gross tertiary education enrollment (%)__* : Percentage of the population enrolled in tertiary education in the country<br>
* *__.Population__* : Total population of the country<br>
* *__.Unemployment rate__* : Unemployment rate in the country<br>
* *__.Urban_population__* : Percentage of the population living in urban areas<br>
* *__.Latitude__* : Latitude coordinate of the country's location<br>
* *__.Longitude__* : Longitude coordinate of the country's location<br>

# Technologies Used

* *__Excel__*: [Excel](https://www.coursera.org/account/accomplishments/certificate/K7VQVJNJFY6T)
* *__Mysql__*: [Mysql](https://www.coursera.org/account/accomplishments/certificate/X5VJVTQD2SXT)

# Data Analysis performed SQL

### Problem Statements

* 1.find the no of youtubers in the table
* 2.which is the most earliest channel
* 3.calculate the no of youtubers in each country
* 4.for each country which category has more youtubers
* 5.which youtuber got more views in the last 30 days
* 6.which youtuber earned more money in every month and every year
* 7.who got more subscribers in the last 30 days
* 8.find top 5 youtubers for each country containing highest subscribers
* 9.find top youtubers for each country who uploaded more videos
* 10.calculate which category youtubers are earning more in each country monthly and round it to 2 decimal
* 11.which category youtubers are getting more views in each country monthly

# Data Analysis using SQL
*__1.find the no of youtubers in the table__*

```
select count(distinct youtuber) from youtube_data_2023
```

*__2. which is the most earliest channel__*

```
select  youtuber,created_year,created_month,created_date,
dense_rank() over(order by created_year,created_month,created_date) from youtube_data_2023
```

*__3.calculate the no of youtubers in each country__*

```
select country,count(youtuber) as cnt from youtube_data_2023
group by country
```

*__4.for each country which category has more youtubers__*

 ```
select country,category ,count(youtuber) as cnt from youtube_data_2023
group by country,category 
order by country,category
 ```

*__5.which youtuber got more views in the last 30 days__*

```
select country,youtuber,video_views_for_the_last_30_days from youtube_data_2023
order by video_views_for_the_last_30_days desc
limit 1
```

*__6.which youtuber earned more money in every month and every year__*

```
select youtuber,highest_monthly_earnings from youtube_data_2023
where highest_monthly_earnings=(select max(highest_monthly_earnings) from youtube_data_2023)

select youtuber,highest_yearly_earnings from youtube_data_2023
where highest_yearly_earnings=(select max(highest_yearly_earnings) from youtube_data_2023)
```

*__7.who got more subscribers in the last 30 days__*

```
select youtuber,subscribers_for_last_30_days from youtube_data_2023 
where subscribers_for_last_30_days <> "nan"
order by subscribers_for_last_30_days desc
```

*__8.find top 5 youtubers for each country containing highest subscribers__*

```
with cte as(select youtuber,country,subscribers,dense_rank() over(partition by country order by subscribers desc) as rn from youtube_data_2023)
select country,subscribers,youtuber from cte
where rn<=5
```

*__9.find top youtubers for each country who uploaded more videos__*

```
with cte as (select country,youtuber,uploads,dense_rank() over(partition by country order by uploads desc) as rn from youtube_data_2023)
select country,youtuber,uploads from cte
where rn =1
```

*__10.calculate which category youtubers are earning more in each country monthly and round it to 2 decimal__*

```
select country,category,round(sum(highest_monthly_earnings),2) as total from youtube_data_2023
group by country,category
order by total desc
```

*__11.which category youtubers are getting more views in each country monthly__*

```
select country,category,sum(video_views_for_the_last_30_days) as total_views from youtube_data_2023
group by country,category
order by total_views desc
```

# Conclusion
Through SQL queries and analysis of the YouTube dataset, several insights regarding video trends, engagement, views and income were uncovered

# Resources
*__For more Details__*: [DataSet](https://www.kaggle.com/datasets/nelgiriyewithana/global-youtube-statistics-2023)

# For Any Queries/Doubts 
[linkedin](https://www.linkedin.com/in/punith-yc-2240b6267/)  [Leetcode](https://leetcode.com/punithyc8688/) [HackerRank](https://www.hackerrank.com/profile/punithyc8688)

