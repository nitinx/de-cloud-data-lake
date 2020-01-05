# Data Engineering
## Project: Cloud Data Lake

## Project Overview
A music streaming startup, Sparkify, has grown their user base and song database even more and want to move their data warehouse to a data lake. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

As their data engineer, you are tasked with building an ETL pipeline that extracts their data from S3, processes them using Spark, and loads the data back into S3 as a set of dimensional tables. This will allow their analytics team to continue finding insights in what songs their users are listening to.

You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.

### Install

This project requires **Python 3.x** and the following Python libraries installed:

- [PySpark](https://spark.apache.org/docs/latest/api/python/index.html)

### Code

This project contains two files:

- `datalake.ipynb`: Exploratory notebook; Serves as input for creation of the ETL script.
- `etl.py`: Main script; reads data from S3, processes that data using Spark, and writes them back to S3. 

### Run

In a terminal or command window, navigate to the top-level project directory (that contains this README) and run following command:

```bash
python3 etl.py
```  

### Data
Dataset for this project is publicly available on AWS S3: 
Song Data: [s3://udacity-dend/song_data](s3://udacity-dend/song_data)
Log Data: [s3://udacity-dend/log_data](s3://udacity-dend/log_data)

1. **Song Dataset**: Dataset is a subset of real data from the [Million Song Dataset](https://labrosa.ee.columbia.edu/millionsong/). Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID.
   - `File Count: 385253` / `Total Size: 103 MB`

2. **Log Dataset**: Dataset consists of log files in JSON format generated by this [event simulator](https://github.com/Interana/eventsim) based on the songs in the dataset above. These simulate app activity logs from an imaginary music streaming app based on configuration settings. Log files in the dataset are partitioned by year and month. 
   - `File Count: 31` / `Total Size: 4 MB`

### Schema for Song Play Analysis
Using the song and log datasets, you'll need to create a star schema optimized for queries on song play analysis. This includes the following tables.

#### Fact Table
1. **songplays** - records in log data associated with song plays i.e. records with page NextSong
   - songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

#### Dimension Tables
2. **users** - users in the app
   - user_id, first_name, last_name, gender, level
3. **songs** - songs in music database
   - song_id, title, artist_id, year, duration
4. **artists** - artists in music database
   - artist_id, name, location, lattitude, longitude
5. **time** - timestamps of records in songplays broken down into specific units
   - start_time, hour, day, week, month, year, weekday