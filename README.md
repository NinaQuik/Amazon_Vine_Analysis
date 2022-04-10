# Amazon_Vine_Analysis

## Overview
The purpose of this project is to extract, transform and load a data set to an AWS RDS Database with tables in pgAdmin, chosen at random from [Amazon Review Datasets](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt).

In this analysis, I choose the [Digital Music Reviews](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Digital_Music_Purchase_v1_00.tsv.gz).  The data was broken into four dataFrames with pySpark in Google Colab and then loaded to four corresponding tables in a postgres AWS RDS database.  After the tables were populated, further analysis was performed to determine if reviews created through the Amazon Vine program were biased compared to reviews that were not created through the program.  

However, after ETL and analysis it was found that there were no reviews for digital music that were created via Amazon Vine.  I was still able to obtain a percentage of five star reviews to total reviews for the Digital Music Review dataset as well as become familiar with AWS services and PySpark.

### Tools
- AWS RDS 
- PGAdmin 4
- Postgres 13.4
- Spark 3.0.3
- Google Colab
- Pandas

## Results

#### There were zero Digital Music Reviews created through Vine
A dataFrame with filtered data "vine == Y" produced zero results:

![DataFrameVine](/Images/vine_df.png)

To double check, this was cross-referenced against a query in PGAdmin:

<img src="https://github.com/NinaQuik/Amazon_Vine_Analysis/blob/main/Images/Vine_query.png" width="500" height="500">

OK, so there were no reviews created through Vine.  How many were there?

#### Music Reviews

A query in PGAdmin shows that there are 1,688,881 reviews for digital music that were not created through vine:

<img src="https://github.com/NinaQuik/Amazon_Vine_Analysis/blob/main/Images/nonvine_reviews.png" width="500" height="500">

This is a large number and to create a more focused study, the results were filtered down into DataFrames that have rows where the total_votes count  was greater than or equal to 20, and again where the number of helpful_votes divided by total_votes is greater than or equal to 50%.  

Using this more relevant DataFrame, the total number of reviews, the number of 5-star reviews and the percentage of 5-star reviews were calculated and placed into a Pandas DataFrame for easy consumption.

![Five_star](/Images/Five_star_summary.png)

## Summary
Because there were zero reviews through the Vine Program, it is impossible to conclude that there is any positivity bias for reviews in the Vine Program.

However, Five Star Reviews make up over 55% of Total Reviews for digital music.  

![stars](/Images/Stars.png)

![Barchart](/Images/Barchart.png)

The distribution of ratings does not follow a normal bell curve, and there is a clear bias for ratings that are very favorable - 5 stars at 55%. There are more one star ratings (816) than two or three star ratings combined (270 and 325 respectively). Because the data is skewed, further analysis could be performed to determine if the filtering to reduce the sample set (total_votes >= 20) and (helpful_votes to total_votes >= .5) altered the distribution.
Additionally, understanding the algorithm that determines "helpful_votes" might shed more light.   Qualitatively, people may be more compelled to write reviews if they have a strong reaction (good or bad) to the music.  Understanding the customer base that gave five star reviews could also determine if there were marketing forces that biased reviews. 
