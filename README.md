# Amazon_Vine_Analysis

## Overview
The purpose of this project is to extract, transform and load a data set to an AWS RDS Database with tables in pgAdmin, chosen at random from [Amazon Review Datasets](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt).

In this analysis, I choose the [Digital Music Reviews](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Digital_Music_Purchase_v1_00.tsv.gz).  The data was broken into four dataframes with pySpark in Google Colab and then loaded to four corresponding tables in a postgres AWS RDS database.  After the tables were populated, further analysis was performed to determine if reviews created through the Amazon Vine program were biased compared to reviews that were not created through the program.  

However, after ETL and analysis it was found that there were no reviews for digital music that were created via Amazon Vine.  I was still able to obtain a percentage of five star reviews to total reviews for the Digital Music Review dataset as well as become familar with AWS services and pySpark.

### Tools
- AWS RDS 
- PGAdmin 4
- Postgres 13.4
- Spark 3.0.3
- Google Colab
- Pandas

## Results

#### There were zero Digital Music Reviews created through Vine
Creating a dataframe with filtered data "vine == Y" produced zero results:

![DataFrameVine](/Images/vine_df.png)

To double check, this was cross-referenced against a query in PGAdmin:

<img src="https://github.com/NinaQuik/Amazon_Vine_Analysis/blob/main/Images/Vine_query.png" width="500" height="500">

OK, so there were no review created through Vine.  How many were there?

#### Music Reviews
