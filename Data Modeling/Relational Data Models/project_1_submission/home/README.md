### QUESTION: Discuss the purpose of this database in the context of the startup, Sparkify, and their analytical goals.

##### The Purpose of this database is:
- to consolidate the user activity data from disparate json files into a central database.
- to bring structure that ease data retrieval efforts.


### QUESTION: State and justify your database schema design and ETL pipeline.

##### Database SCHEMA
songplay_table_create = ("""
    CREATE TABLE songplays (songplay_id SERIAL,
    start_time TIMESTAMP NOT NULL,
    user_id INT NOT NULL, 
    level VARCHAR NOT NULL,
    song_id VARCHAR(18),
    artist_id VARCHAR(18),
    session_id INT NOT NULL,
    location VARCHAR NOT NULL,
    user_agent VARCHAR NOT NULL, 
    PRIMARY KEY (songplay_id)
)
""")


user_table_create = ("""
CREATE TABLE users (
    user_id INT,
    first_name VARCHAR NOT NULL,
    last_name VARCHAR NOT NULL,
    gender CHAR(1) NOT NULL,
    level VARCHAR NOT NULL,
    PRIMARY KEY (user_id)
)
""")

song_table_create = ("""
CREATE TABLE songs (
    song_id VARCHAR(18),
    title VARCHAR NOT NULL,
    artist_id VARCHAR(18) NOT NULL,
    year INT NOT NULL,
    duration FLOAT NOT NULL,
    PRIMARY KEY (song_id)
)
""")

artist_table_create = ("""
CREATE TABLE artists (
    artist_id VARCHAR(18),
    name VARCHAR NOT NULL,
    location VARCHAR NOT NULL,
    latitude FLOAT,
    longitude FLOAT,
    PRIMARY KEY (artist_id)
)
""")

time_table_create = ("""
CREATE TABLE time (
    start_time TIMESTAMP NOT NULL,
    hour int NOT NULL,
    day int NOT NULL,
    week int NOT NULL,
    month int NOT NULL,
    year int NOT NULL,
    weekday int NOT NULL
)
""")

##### JUSTIFICATION OF SCHEMA
- The Schema is patterned after the Star Schema, which comprises of a fact table and dimension tables.

###### Attributes/Column Properties

- songplay_id: SERIAL
- start_time : TIMESTAMP, NOT NULL
- user_id    : INTEGER, NOT NULL
- level      : VARCHAR, NOT NULL
- song_id    : VARCHAR(18)
- artist_id  : VARCHAR(18)
- session_id : INTEGER, NOT NULL
- location   : VARCHAR, NOT NULL
- user_agent : VARCHAR, NOT NULL
- first_name : VARCHAR, NOT NULL
- last_name  : VARCHAR, NOT NULL
- gender     : CHAR(1), NOT NULL
- duration   : FLOAT, NOT NULL
- name       : VARCHAR, NOT NULL
- location   : VARCHAR, NOT NULL
- latitude   : FLOAT
- longitude  : FLOAT
- hour       : INTEGER, NOT NULL
- day        : INTEGER, NOT NULL
- week       : INTEGER, NOT NULL
- month      : INTEGER, NOT NULL
- year       : INTEGER, NOT NULL
- weekday    : INTEGER, NOT NULL

##### JUSTIFICATION OF ETL Pipeline
- With the data stored in folders, we Extracted the data from the log folder, load and transform them into respective dimension tables
