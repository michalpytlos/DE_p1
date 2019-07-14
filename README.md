# DEP1
Project 1 of the Data Engineering Nanodegree <br>
Michal Pytlos, June 2019

## Overview
DEP1 is a collection of scripts which create PostgreSQL database and transfer data on songs and user activity from JSON files to the database.

### Database
The database is optimized for queries on song play analysis and utilizes the star schema with the following tables:
* Fact table
    * songplays - records in log data associated with song plays
* Dimension tables
    * users - users in the app
    * songs - songs in music database
    * artists - artists in music database
    * time - timestamps of records in songplays broken down into specific units

### ETL pipeline
The pipeline transfers data from two types of JSON files to the database: 
* files with songs metadata saved in **data/song_data**. Each file contains metadata on a single song in the JSON format with the following fields: num_songs, artist_id, artist_latitude, artist_longitude, artist_location, artist_name, song_id, title, duration and year. 
* files with user activity saved in **data/log_data**. Each file contains data on user activity from a given day. Each line of this file contains data on a single activity of a user in JSON format with the following fields: artist, auth, firstName, gender, itemInSession, lastName, length, level, location, method, page, registration, sessionId, song, status, ts, userAgent and userId.

## Prerequisites
This project has been written specifically for the environment provided by Udacity as part of the Data Engineering Nanodegree - Project: Data Modelling with Postgres (Python 3.6 and PotsgreSQL 9.5)

## Usage
To create sparkify database and its tables:
1. Navigate to the directory containing **create_tables.py**
2. Run `python create_tables.py`

To load data from song and log files to sparkify database:
1. Navigate to the directory containing **etl.py**
2. Run `python etl.py`

## How it works
### create_tables.py
1. Connect to PostgreSQL database studentdb using psycopg2
2. Create sparkifydb database
3. Close connection to studentdb
4. Open connection to sparkifydb
5. Create tables: songplays, time, users, songs and artists
6. Close connection to sparkifydb

### etl.py
1. Connect to PostgreSQL database sparkify using psycopg2
2. Process each song file:
    * load data from file to pandas DataFrame
    * insert data into songs and artists tables
3. Process each log file:
    * load data from file to pandas DataFrame
    * filter, transform and enrich data
    * insert data into users, time and songplays tables
4. Close connection to sparkifydb

## File structure
The file structure of the project is outlined below.
```
etl.py
create_tables.py
sql_queries.py
data/
  song_data/
  log_data/
```
The components are briefly described in the table below.

| File/directory   | Description               |
| -----------------| --------------------------|
| etl.py           | Script loading data from song and log files to sparkify database |
| create_tables.py | Script creating sparkify database and its tables |
| sql_queries.py   | SQL statements used by etl.py and create_tables.py |
| song_data/       | Directory containing song files |
| log_data/        | Directory containing log files |
