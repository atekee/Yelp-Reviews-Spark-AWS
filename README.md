# Analyzing 10GB of Yelp Reviews Data

For this project I analyzed Yelp Reviews Dataset with business, checkins, review, tip, and user data that I downloaded from Kaggle.com and uploaded into my AWS S3 Bucket.

```
s3://yelp-dataset-cis9760/yelp_academic_dataset_business.json
s3://yelp-dataset-cis9760/yelp_academic_dataset_checkin.json
s3://yelp-dataset-cis9760/yelp_academic_dataset_review.json
s3://yelp-dataset-cis9760/yelp_academic_dataset_tip.json
s3://yelp-dataset-cis9760/yelp_academic_dataset_user.json
```

I provisioned a Spark cluster on AWS EMR, and connected it to Jupyter Notebook to run data analysis with PySpark.

## Tech Used
AWS EMR, S3, PySpark, Python, NLTK


## Cluster Configuration

![alt text](https://github.com/atekee/Yelp-Reviews-Spark-AWS/blob/main/Assets/Cluster_Configuration.png)


## Notebook Configuration

![alt text](https://github.com/atekee/Yelp-Reviews-Spark-AWS/blob/main/Assets/Notebook_Configuration.png)


## Part I: Installation and Initial Setup
```
sc.install_pypi_package("pandas==1.0.3")
sc.install_pypi_package("matplotlib==3.2.1")
sc.install_pypi_package("scipy==1.7.1")
sc.install_pypi_package("seaborn==0.11.1")
```
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import re
import nltk
from nltk.tokenize import RegexpTokenizer
from nltk.stem.porter import PorterStemmer
from nltk import FreqDist
from scipy import stats
from scipy.stats import skew
from pyspark.sql.types import StructType,StructField, StringType, IntegerType
from pyspark.sql.functions import mean, stddev, col, abs, split, explode, avg
from pyspark.sql import functions as F
```

```
business = spark.read.json('s3://yelp-dataset-cis9760/yelp_academic_dataset_business.json')
review = spark.read.json('s3://yelp-dataset-cis9760/yelp_academic_dataset_review.json')
user = spark.read.json('s3://yelp-dataset-cis9760/yelp_academic_dataset_user.json')
```

## Part II: Analyzing Categories
Built an association table by mapping single business_id multiple times to each distinct category, and created a barchart of top 20 categories.

## Part III: Do Yelp Reviews Skew Negative?
Analyzed review and business data to compare the avg written reviews stars with business stars to find out if Yelp reviews skew negative.

## Part IV: Should the Elite be Trusted?
Calculated the avg review stars by multiple elite users for each business_id, and compared it with the business stars to find out if elite user reviews be trusted. 

## Part V: What are the Most Common Unigrams and Bigrams in Yelp Hotels & Travel Reviews?
Pre-processed and tokenized the text review data for all Hotels & Travel category, and analyzed it with nlkt FreqDist to find out the most common unigrams and bigrams.


