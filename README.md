# Case_Study
# Google Data Analytics Case Study
	Introduction

Hi My name is Jesus Carreon, I will perform a case study doing many real world tasks of a junior data analyst, the name of the company is Cyclistic, where you will get insight of the key stakeholders and team members.
I will answer key business questions using the steps of the analysis process to achieve the business goal
I am working in the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director
of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore,
the team wants to understand how casual riders and annual members use Cyclistic bikes differently. 

	Scenario

The director of marketing of Cyclistic, Lily Moreno, believes that the company’s future growth depends on maximizing the number of annual memberships. Hence, the marketing analyst team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, the analytics team could be able to design a new marketing strategy to convert casual riders into annual members. 

Three questions will guide the future marketing campaign:

*1.How do annual members and casual riders use Cyclistic bikes differently?

*2.Why would casual riders buy Cyclistic annual memberships?

*3.How can Cyclistic use digital media to influence casual riders to become members?

I have been assigned by Moreno the first question. 

	The Ask Phase
* A statement of the business task: 

The Cyclistic team has concluded that annual members are much more profitable than casual riders. So, we want to design marketing strategies and a campaign that helps us converting casual riders into annual members. 

* My key stakeholders are: 

1-Lily Moreno: The director of marketing and my manager. Moreno is responsible for the development of campaigns and initiatives to promote the bike-share program. These may include email, social media, and other channels. She is the most important stakeholder

2- Cyclistic executive team: The idea of Lily Moreno is to showcase why annual members and casual riders differ from each other and our job is to demonstrate why the data should be backed up with compelling data insights and professional data vizualizations

	The Prepare Phase
	
Data Source: 
The data consists in a period of 12 months from July 2021 to August 2022 of original bike share data was extracted as 12 zipped .csv files st 12 month of original bike share data set from 01/01/2021 to 31/12/2021 was extracted as 12 zipped .csv. 
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

	The Process Phase
	
I used R Studio software to perform cleaning and verification of the data, it's the most powerful tool you can use and also you can create very nice visualizations

	The Analyze Phase

Installing and loading the necessary packages

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

Importing the data

The selected data consists from the period of July 2021 to August 2022

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

Then the 12 months are merged into 1 big dataframe

all_trips <- bind_rows(X202107_divvy_tripdata, X202108_divvy_tripdata, X202109_divvy_tripdata, X202110_divvy_tripdata, X202111_divvy_tripdata, X202112_divvy_tripdata, X202201_divvy_tripdata, X202202_divvy_tripdata, X202203_divvy_tripdata, X202204_divvy_tripdata, X202205_divvy_tripdata, X202206_divvy_tripdata)

Clean the data and organize it to prepare for analysis
Inspect the new table

colnames(all_trips)
dim(all_trips)
str(all_trips)
head(all_trips)

	




















































