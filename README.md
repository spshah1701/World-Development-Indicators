
# World Development Indicators Analysis

## Introduction

The World Development Indicators (WDI) is the World Bank's most comprehensive collection of cross-country development data. It's website basically provides access to data as well as information about data coverage, curation and methodologies and allow users to discover what type of indicators are available.

+ [World Bank](https://www.worldbank.org/en/home)
+ [World Development Indicators](https://databank.worldbank.org/source/world-development-indicators)


## Technologies

+ Databricks 
+ Apache Spark
+ Scala

## Data Description

1. **Country.csv**

 247 rows representing the countries. \
 31 columns describing various attributes of the countries.

2. **Indicators.csv**

5656458 rows representing data instances. \
6 columns describing indicators of the countries. 

#### Need for using Big Data Technologies

The size of this file is about 550MB, necessitating the use of Apache Spark implemented in Scala on Databricks. This combination provides a powerful and scalable framework for efficiently processing large-scale datasets.

## My Implementation
+ [Published Notebook](https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/1225760005808135/549596638656775/7992345167110499/latest.html)

**Note**: This link will be valid till 01-06-2024.


## Project Setup and Replication

- Create a free Databricks Community Edition account
- Create a new cluster and wait till it is active and running
- Upload the *World Development Indicators.dbc* Notebook to Databricks and connect it to the above cluster.
- Upload the data (CSV files) to Databricks after downloading it from the [source](https://databank.worldbank.org/source/world-development-indicators).
- Run the cells, view and analyse the data as desired.



### Access the data 


```
%scala 

val Indicators = sqlContext.read.format("csv")
  .option("header", "true")
  .option("inferSchema", "true")
  .load("/FileStore/tables/Indicators.csv")

display(Indicators)
```

### Create or Replace Temporary view

Temporary view allows to use SQL queries on the DataFrame as if it were an SQL table.

```
%scala

Indicators.createOrReplaceTempView("Indicators")
```

### Write desired SQL queries for data visualization and analysis

```
%sql 

select value as Youth_Literacy_Rate,ShortName from Indicators A JOIN Country N ON A.CountryCode = N.CountryCode  where IndicatorCode  = "SE.ADT.1524.LT.ZS" and Year = 2010 order by Youth_Literacy_Rate Desc; 
```


