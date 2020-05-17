# Problem Statement

A music streaming startup, Sparkify, has grown their user base and song database and want to move their processes and data onto the cloud. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

You are tasked with building an ETL pipeline that extracts their data from S3, stages them in Redshift, and transforms data into a set of dimensional tables for their analytics team to continue finding insights in what songs their users are listening to.


# Objectives

- Define fact and dimension table for star schema for a particular analytic focus.
- To implement ETL pipeline to extract data from S3, stage it in Redshift and transform it into dimensional tables


# Dataset

Datasets reside in S3. Here are the S3 links for each:
- Song data: s3://udacity-dend/song_data
- Log data: s3://udacity-dend/log_data
- Log data json path: s3://udacity-dend/log_json_path.json


# Database Schema

### Staging tables
- staging_events_table
- staging_songs_table

### Fact Table
#### songplay_table : records in event data associated with song plays i.e. records with page NextSong 
songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

### Dimension tables:
#### users : users in the app
user_id, first_name, last_name, gender, level

#### songs : songs in music database
song_id, title, artist_id, year, duration

#### artists : artists in music database
artist_id, name, location, lattitude, longitude

#### time - timestamps of records in songplays broken down into specific units
start_time, hour, day, week, month, year, weekday


# File structure

- **create_table.py:** is where we'll create the fact and dimension tables for the star schema in Redshift. 
- **etl.py:** is where we'll load data from S3 into staging tables on Redshift and then process that data into the analytics tables on Redshift.
- **sql_queries.py:** is where we'll define the SQL statements, which will be imported into the two other files above. 
- **cluster_create.ipynb:** creates a cluster on AWS  
- **test.ipynb:** used to check if the pipeline is successfully created by running a few analytical queries
- **dwh.cgf:** configurations file which needs to be filled before running the project


# Project steps:
1. **Create Table Schemas**
 - Write a SQL CREATE statement for each of these tables in sql_queries.py
 - Complete the logic in create_tables.py to connect to the database and create these tables
 - Write SQL DROP statements to drop tables in the beginning of create_tables.py if the tables already exist. This way, you can run create_tables.py whenever you want to reset your database and test your ETL pipeline. 
 - Launch a redshift cluster and create an IAM role that has read access to S3.
 - Add redshift database and IAM role info to dwh.cfg.
 - Test by running create_tables.py and checking the table schemas in your redshift database. You can use Query Editor in the AWS Redshift console for this.
 
2. **Build ETL Pipeline** 
 - Implement the logic in etl.py to load data from S3 to staging tables on Redshift.
 - Implement the logic in etl.py to load data from staging tables to analytics tables on Redshift.
 - Test by running etl.py after running create_tables.py and running the analytic queries on your Redshift database to compare your results with the expected results.
 - Delete your redshift cluster when finished.
 
# Running the project:
- First write sql queries to create and insert data in tables in sql_queries.py.
- Create a IAM role that has read access to S3 in AWS and fill in the dwh.config file with the necessary parameters.
- Run create_cluster.ipynb file to create and connect to cluster.
- Run create_tables.py to create the tables in redshift database. 
- Run etl.py to insert data into staging tables and then into dimensional tables
- Run test.ipynb to check if the data is inserted into the tables correctly.