# Data Modeling with Apache Cassandra Projec #

-------------------------------------------------------------------------------

## Summary ##
This project is a training project in data modeling using Apache Cassandra, with
a mock startup called Sparkify, and utilizing real data from [Million Song Dataset](https://labrosa.ee.columbia.edu/millionsong/)
provided by Udacity, which also provided the skeleton code and structure to this
project.

### Primary Key Descriptions ###
  1. Sessions Table
  
     The primary key selected for the session table is `(session_id, item_in_session)`.
	 This would make sure that each event is inserted to the table, since there might
	 be more than two rows with the same session_id.
	 
  2. User Sessions Table
  
     The primary key for this table is `((user_id, session_id), item_in_session)`. This
	 is so that the `WHERE` query for particular `user_id` and `session_id` would work.
	 The table would then be partitioned by a composite key `(user_id, session_id)` to
	 make sure that both of them are not in a separate partition. Also, the additional
	 `item_in_session` clustering key is there to enable multiple events in a session
	 by a given user_id would be successfully inserted. This would also mean that the
	 output of the query of `user_id` and `session_id` would then be sorted based on
	 `item_in_session`.
	 
  3. Song Sessions Table
  
     The primary key for this table is `(song_title, user_id)`. This is so that the
	 `WHERE` query for a particular `song_title` would work. The `user_id` clustering 
	 key is there to make sure all users listening to a song are recorded: otherwise,
	 there would only be one row for one song title.
	 

## Usage ##
  * Requirements:
    * cassandra-driver 3.25.0
	* python 3.9.5
	* jupyter 1.0.0
	* pandas 1.2.4
	* numpy 1.20.2
  * Open the Jupyter notebook `Project_1B_Project_Template.ipynb` and follow along
    the cells and run them to run the code.

## File Description ##
  * `event_data` folder contains CSV files of events.
  * `event_datafile_new.csv` is the output of the ETL process: subset of all the event data.
  * `Project_1B_Project_Template.ipynb` is the Jupyter notebook where all the work of this
     project is.
  * `images` folder contains image files to be used in the Jupyter notebook.

## Contribution ##
If you want to contribute to this project and make it beter, your help is very
welcome.

The following is the general guide on how to contribute to this project:
   1. Fork this project & clone it on your local machine
   2. Create an *upstream* remote and sync your local copy before you branch
   3. Branch for each piece of work
   4. Do the work
   5. Push to your origin repository
   6. Create a new pull request on GitHub

## License ##
The content of this app is coverend under the [MIT License](./license.txt).
