# AsteroidProject
Repository for the final bootcamp project.


## Project Overview: 
Based on the features in the NEO_V2.csv - Excel dataset the team will determine what is the most likely reason something is hazardous. 

## Dataset: 
NEO_V2.csv - Excel 

## Reason for Dataset: 
We believe this data to be reliable as it is from NASA. With 90K rows of data we felt it provided enough data to answer our question. The dataset appeared to be a good fit for machine learning component of the project. Our thinking is the dataset will work well for visualization. 

## Machine Learning Model: 
The team will train and test hazardous data using a classification model.

## Technology Used for the Project: 
	- Python - Sklearn, Pandas, Tensorflow
	- PostGres - database 
	- Tableau - visulization
	_ *HTML/CSS - will review addition datasets, such as D3 - Celestial to display interesting visuals of asteroids. 


## Team Members and Roles: 

	- Triangle: Christopher Madden (Machine Learning)  
 	- Square: Maryam Hussain and Frank Salvo (managing repository)
	- Circle: Kathleen Yager (SQL)
	- X: Megan Harping and Frank Salvo (what tools to use)


## Visualization Outline:

### The story we want to tell. 
	 1. Using various predictive models we are showing what factors in our dataset most impact hazardous objects.
		
#### Models used: 
		- Decision Tree
		- Neuro Network 
		- Linear Regression

		The Decision Tree and Neuro Network models indicate an imbalance in the data. This is an indicator that we need to balance the model. 

		Visuals included in our machine learning are based in plotly. 

	2. We will describe the parameters of the data in the dataset.

	3. Create a visualization using Google Docs we will create a presentation that will include images of asteroids and explanation and images of 	   our work. 

## Team Goal:
	Work with team members to sort and analyze asteroid data to find what factors lead to deciding whether or not asteroids are hazardous or 	nonhazardous. We hope to present our data using our knowledge of different databases to create visualizations, machine learning models, and 	linear regression.
	

## Top Five Takeaways of the Project: 
	1. Manipulating an already existing dataset to tell our story. 
	2. Applying skills learned in class to a NASSA dataset, using our knowledge of different concepts and databases to present 
	3. 
	4. 
	5. 	 



# NOTES: 
## Work Process
	
	July 16, 2022

		- Maryam and Kathleen reviewed NEO_V2.csv and discovered multiple entries for some ID's. Review showed data in the lative_velocity and 			miss_distance columns was different with all other columns remaining constant.

		Using Pandas, we separated columns into two dataframes: 
			- 'df_new' includes two columns:
				1. relative_velocity
				2. miss_distance

			- 'no_duplicates_df' includes: 
				All columns except relative_velocity and miss_distance

		after splitting the data and removing duplicates from 'no_duplicates_df', we created CSV files. 


		With CSV files created, we created two tables in PostGres:

			1. vel_miss 
			2. no_duplicates
		
		Using a left-join, we created a new table called 'combined_tables'.

See image below of the first 20 rows of the SQL file. 

![combined_table](https://github.com/mhhussain24/AsteroidProject/blob/KY_asteriods/Resources/PostGres_left_join.png)

We attempted to export combined_table to a csv and received a 'columns error' message. We checked in with the balance of the group for assistance.  				
			




 









