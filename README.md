# Sparkify
## Data Modeling with Cassandra

Sparkify, a startup wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. With particularly focus on understanding what songs users are listening to. To do this, a Apache Cassandra database with tables designed to optimize queries on song play analysis needed to be created. Currently, the data resides in csv files in the event_data folder.

## Files
`event_data\ ` CSV files partitioned by date containing data of user sessions
`images\ ` an image of how the data looks

`Data_Modeling_Cassandra.ipynb` Contains the ETL pipeline that processes the `event_data` to produce the `event_datafile_new.csv' file and three data modeling examples.

## THe Data 
From the notebook:
>The event_datafile_new.csv contains the following columns:
>artist
>firstName of user
>gender of user
>item number in session
>last name of user
>length of the song
>level (paid or free song)
>location of the user
>sessionId
>song title
>userId
>The image below is a screenshot of what the denormalized data should appear like in the event_datafile_new.csv:
![The image below is a screenshot of what the denormalized data should appear like in the event_datafile_new.csv](images/image_event_datafile_new.jpg)

## Queries
The notebook caontains three example queries:
1. Give me the artist, song title and song's length in the music app history that was heard during sessionId = 338, and itemInSession = 4

For the table we need artist, song_title, song_length, session_id and item_in_session. A composite primary key of (session_id, item_in_session) is used as neither session_id nor item_in_session is unique. Also because we wish to include both columns in the where clause.

2. Give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182

For the table we need user_id, session_id, item_in_session, artist text, song_title, user_firstname and user_lastname.
A primary key of (user_id, session_id) and (session_id, item_in_session, item_in_session) as composite primary key were used. The data is partitioned by user_id, session_id and clustered by item_in_session


3. Give me every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'

For the table we need user_id, song_title, user_firstname and user_lastname.
A primary key of (song_title,user_id) was used as neither song_title nor user_id is unique in the table. As we want to know who listened to what song, the data is partitioned by song_title andclustered by user_id.
