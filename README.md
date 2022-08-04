
---
title: "Cyclistic"
author: "Jesus Carreon"
date: "2022-08-04"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
#### Special thanks to https://github.com/elmaandimahmoud it help me a lot to comprehend what I needed to do.
## Introduction

Hi My name is Jesus Carreon, I will perform a case study doing many real world tasks of a junior data analyst, the name of the company is Cyclistic, where you will get insight of the key stakeholders and team members.
I will answer key business questions using the steps of the analysis process to achieve the business goal
I am working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director
of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore,
the team wants to understand how casual riders and annual members use Cyclistic bikes differently. 

## Scenario

The director of marketing of Cyclistic, Lily Moreno, believes that the company’s future growth depends on maximizing the number of annual memberships. Hence, the marketing analyst team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, the analytics team could be able to design a new marketing strategy to convert casual riders into annual members. 

Three questions will guide the future marketing campaign:

*1.How do annual members and casual riders use Cyclistic bikes differently?

*2.Why would casual riders buy Cyclistic annual memberships?

*3.How can Cyclistic use digital media to influence casual riders to become members?

I have been assigned by Moreno the first question. 

## The Ask Phase

* A statement of the business task: 

The Cyclistic team has concluded that annual members are much more profitable than casual riders. So, we want to design marketing strategies and a campaign that helps us converting casual riders into annual members. 

* My key stakeholders are: 

1-Lily Moreno: The director of marketing and my manager. Moreno is responsible for the development of campaigns and initiatives to promote the bike-share program. These may include email, social media, and other channels. She is the most important stakeholder

2- Cyclistic executive team: The idea of Lily Moreno is to showcase why annual members and casual riders differ from each other and our job is to demonstrate why the data should be backed up with compelling data insights and professional data vizualizations

## The Prepare Phase

Data Source: 
The data consists in a period of 12 months from the period of July 2021 to August 2022 of original bike share data was extracted as 12 zipped .csv files st 12 month of original bike share data set from 01/01/2021 to 31/12/2021 was extracted as 12 zipped .csv. 
*Source(https://divvy-tripdata.s3.amazonaws.com/index.html). The data is made available and licensed by Motivate International Inc under this [license](https://ride.divvybikes.com/data-license-agreement).

Data Organization & Description:

File naming convention: YYYY_MM

File Type:  .csv  format 

File Content: Each .csv file consist of 13 columns which contain information related to ride id, rider type, ride start and end time, start and end location  etc. Number of rows varies between 49k to 531k from different excel files.

Data credibility: 

The data set is reliable, the data is complete from the time window specified (June 2021-June 2022).

The data's original, it comes from a first party source.

The data's easy to comprehend, the data contains all the information needed to answer key questions.

The data's free of bias.

The data's current, the data consists of information from the past year and this year.

The data's cited and vetted by Chicago department of transportation.

Data Security: Riders’ personal and identifiable information is hidden.

Data Limitations: Data-privacy issues prohibit you from using riders’ personally identifiable information. This means that you won’t be able to connect pass purchases to credit card numbers to determine if casual riders live in the Cyclistic service area or if they have purchased multiple single passes.

## The Process Phase 

I used R Studio software to perform cleaning and verification of the data, it's the most powerful tool you can use and also you can create very nice visualizations

## The Analyze Phase

Installing and loading the necessary packages

```{r}
install.packages("tidyverse")
install.packages("janitor")
install.packages("skimr")
install.packages("here")
install.packages("hablar")
install.packages("readxl")
install.packages("data.table")
install.packages("chron")
install.packages("readr")
install.packages("lubridate")
install.packages("magrittr")
install.packages("DescTools")
install.packages("metR")
```

```{r}
library(tidyverse)
library(janitor)
library(skimr)
library(here)
library(hablar)
library(readxl)
library(data.table)
library(chron)
library(readr)
library(lubridate)
library(magrittr)
library(DescTools)
library(metR)
```
Importing the data 

The selected data consists from the period of July 2021 to August 2022
```{r}
> X202107_divvy_tripdata <- read_csv("Cyclistic/202107-divvy-tripdata.csv")
> X202108_divvy_tripdata <- read_csv("Cyclistic/202108-divvy-tripdata.csv")
> X202109_divvy_tripdata <- read_csv("Cyclistic/202109-divvy-tripdata.csv")
> X202110_divvy_tripdata <- read_csv("Cyclistic/202110-divvy-tripdata.csv")
> X202111_divvy_tripdata <- read_csv("Cyclistic/202111-divvy-tripdata.csv")
> X202112_divvy_tripdata <- read_csv("Cyclistic/202112-divvy-tripdata.csv")
> X202201_divvy_tripdata <- read_csv("Cyclistic/202201-divvy-tripdata.csv")
> X202202_divvy_tripdata <- read_csv("Cyclistic/202202-divvy-tripdata.csv")
> X202203_divvy_tripdata <- read_csv("Cyclistic/202203-divvy-tripdata.csv")
> X202204_divvy_tripdata <- read_csv("Cyclistic/202204-divvy-tripdata.csv")
> X202205_divvy_tripdata <- read_csv("Cyclistic/202205-divvy-tripdata.csv")
> X202206_divvy_tripdata <- read_csv("Cyclistic/202206-divvy-tripdata.csv")
```

```{r}
all_trips <- bind_rows(X202107_divvy_tripdata, X202108_divvy_tripdata, X202109_divvy_tripdata, X202110_divvy_tripdata, X202111_divvy_tripdata, X202112_divvy_tripdata, X202201_divvy_tripdata, X202202_divvy_tripdata, X202203_divvy_tripdata, X202204_divvy_tripdata, X202205_divvy_tripdata, X202206_divvy_tripdata)
```
Clean the data and organize it to prepare for analysis
Inspect the new table

```{r}
colnames(all_trips)
dim(all_trips)
str(all_trips)
head(all_trips)
```

Then,  columns that list the date, month, day, day_of_week and year of each ride are added. days of the week are assigned the numbers 1:Monday, 2:Tuesday, etc.
This will allow the aggregation of the data by each day, month or day_of_week.

```{r}
all_trips$date <- as.Date(all_trips$started_at) #The default format is yyyy-mm-dd
all_trips$month <- format(as.Date(all_trips$date), "%m")
all_trips$day <- format(as.Date(all_trips$date), "%d")
all_trips$year <- format(as.Date(all_trips$date), "%Y")
all_trips$day_of_week <- format(as.Date(all_trips$date), "%u") #"%A" would deliver names of weekdays
```

Add a ride_length calculation column to all_trips in seconds and minutes (2 columns)

```{r}
all_trips$ride_length <- difftime(all_trips$ended_at,all_trips$started_at)
all_trips$ride_length_m <- (difftime(all_trips$ended_at,all_trips$started_at))/60
```

Inspect the new 2 columns added

```{r}
str(all_trips)
```

Convert c(ride_length, ride_length_m, day and month) to numeric so that calculation can be executed.

```{r}
all_trips$ride_length <- as.numeric(as.character(all_trips$ride_length))
all_trips$ride_length_m <- as.numeric(as.character(all_trips$ride_length_m))
all_trips$month <- as.numeric(all_trips$month)
all_trips$day <- as.numeric(all_trips$day)
is.numeric(all_trips$ride_length)
is.numeric(all_trips$ride_length_m)
is.numeric(all_trips$month)
is.numeric(all_trips$day)
```

After converting and inspecting data, it was noticed that col:ride_length has some negative values, probably because start_time and end_time were swapped for these rides, or the system simply registered and recorded the rides incorrectly. So, negative-seconds rides must be excluded.

```{r}
all_trips_v1 <- all_trips[!( all_trips$ride_length < 0),]
```

First analysis step is to obtain the ride length in min 

```{r}
all_trips_v1 %>% 
  summarise(max(ride_length_m),min(ride_length_m),mean(ride_length_m))
```
The overall average ride length is 20.3 minutes

After, the mode weekday is calculated to see which weekday had more rented bikes

```{r}
all_trips_v1 %>% 
  group_by(day_of_week) %>% 
  summarise(number_of_rides = n()) %>% 
  ggplot(mapping = aes(x = day_of_week, y = number_of_rides)) + geom_col()
```

The scatter shows us that saturday is the bussiest day of the week with almost a million bikes rented, also we can see that the weekend has the most amount of bikes rented

Then a plot for the average duration in minutes for every day of the week for members and casuals
```{r}
all_trips_v1 %>% 
  group_by(member_casual, day_of_week) %>% 
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length_m)) %>% 
  arrange(member_casual, day_of_week)  %>% 
  ggplot(aes(x = day_of_week, y = average_duration, fill = member_casual)) +
  geom_col(position = "dodge")
```

The plot demonstrate that casual riders rent bikes almost twice the time members do it, specially Saturday, Sunday and Monday. Members tend to ride a little longer on the weekend.

Here, number of rides per day for casuals and members

```{r}
all_trips_v1 %>% 
  group_by(member_casual, day_of_week) %>% 
  summarise(number_of_rides = n()
            ,average_duration = mean(ride_length_m)) %>% 
  arrange(member_casual, day_of_week)  %>% 
  ggplot(aes(x = day_of_week, y = number_of_rides, fill = member_casual)) +
  geom_col(position = "dodge")
```

In contrast to the previous plot, members begin more rides  and have higher number of rides on every day except Saturday and Sunday.

The last plot is line plot to see contionus change of number of rides during the whole period (Month number 1 on the plot is equivalent to July)

```{r}
all_trips_v1%>%
  group_by(month, member_casual) %>%   
  summarise(number_of_rides = n()						 
  ,avg_ride_length = mean(ride_length_m)) %>% 
ggplot() + geom_line(mapping = aes(x = month, y = number_of_rides, color = member_casual)) + scale_x_continuous(breaks = seq(1, 12, by = 1))
```
The plot indicates that July and august 2021 and june 2022 were the weakest months for Casuals. Then it started to grow from October to reach its peak on January but then it started to go down every month. 
For members on August 2021 it started to grow continously to reach its peak on decembe, then on January wnt down a little bit February and march went up, on May the line started to go down

##The Share Phase

*Members and casuals differ on how much time they use their bikes, and how much trips they have.

*Casual and members both peak at the end of the year, probably due to being holidays, a lot of people probably visit the town and rented the bike to sightsee

*Casual riders peak on weekends, also due to the probability of more tourists visiting town 

*Ride duration for members are relatively low compared to casuals, it could mean members are people who work and they are using the bike to work and casuals are riding longer due to it could be tourists being more calm.

## The act Phase

* There could be some type of loyalty points to the people who complete certain amount of hours during the month or certain amount or rides.
* The marketing campaing should be launched during the end of the year, because there are more people in town
* For people what will be only on the weekend there could be special plans for the 3 days they are staying
* If casuals reach certain amount of hours and trips comnbined they could become members



















































