# Asteroid Project
Repository for the final bootcamp project.


## Project Overview: 
Based on the features in the NEO_V2.csv - Excel dataset the team will determine what is the most likely reason something is hazardous. 

## Dataset: 
NEO_V2.csv - Excel 

## Reason for Dataset: 
We believe this data to be reliable as it is from NASA. With 90K rows of data we felt it provided enough data to answer our question. The dataset appeared to be a good fit for machine learning component of the project. Our thinking is the dataset will work well for visualization. 


## Technology Used for the Project: 
	- Python - Sklearn, Pandas, Tensorflow, Numpy, Matplotlib, Imblearn, Keras, Collections, AutoViz, Datetime
	- PostGres - database 
	- Tableau - visulization
	_ *HTML/CSS - will review addition datasets, such as D3 - Celestial to display interesting visuals of asteroids. 


## Team Members and Roles: 

	- Triangle: Christopher Madden (Machine Learning)  
 	- Square: Maryam Hussain and Frank Salvo (managing repository)
	- Circle: Kathleen Yager (SQL)
	- X: Megan Harping and Frank Salvo (what tools to use)


## Team Goal:
Work with team members to sort and analyze asteroid data to find what factors lead to deciding whether or not asteroids are hazardous or nonhazardous. We hope 	to present our data using our knowledge of different databases to create visualizations, machine learning models, and linear regression.
	

## Top Five Takeaways of the Project: 
	1. Considering multiple factors to determine if an asteroid is hazardous or not. 
	2. Comparing factors to determine which impact hazardous classification. 
	3. Visualizing hazardous objects in relation to earth. 
	4. How to interpret data that is scaled for accuracy. 
	5. Analyzing summary statistics to aid in interpretation of data. 


## Machine Learning Models: 

### The story we want to tell. 
	 1. Using various predictive models we are showing what factors in our dataset most impact hazardous objects.
		
#### Models used:
		- Random Forest Classifier 
		- Support Vector Machine
		- Logisic Regression
		- Decision Tree Classification
		- Gradient Boosted Tree
		- Voting Classifier (used to compare all five models at the same time)

Models chosen support classification machine learning.  The intial data was imbalanced, seeing many more values for 'non-hazardous' than for 'hazardous'.  We resampled the data using SMOTEENN combination sampling.

Visuals included in our machine learning are based in plotly. 

	2. We will describe the parameters of the data in the dataset.

	3. Creating visualization in Tableau, presenting using Google Docs we will create a presentation that will include images of asteroids and 		   explanation and images of our work. 


## Visualization:

After cleaning our dataset, we used Tableau to create a story to explain the hazardous versus non-hazardous objects.The link below provides a look at our draft version of our story. 

[Link to Asteroids Dashboard](https://public.tableau.com/app/profile/megan.harpring/viz/NearEarthObjects_16595746214520/Dashboard1?publish=yes)


## Final Presentation Outline:
[Link to Asteroids Presentation - draft](https://docs.google.com/presentation/d/1SSr1upBPCezaDCPN7O02uU3xZ5WMtUKFsdtgQ75Xz0o/edit?usp=sharing)

## Defining Hazardous Asteroids:
 
According to NASA, Center for Near Earth Obeject Studies, near earth objects are defined as: 
"In terms of orbital elements, NEOs are asteroids and comets with perihelion distance q less than 1.3 au . Near-Earth Comets (NECs) are 	further restricted to include only short-period comets (i.e., orbital period P less than 200 years). The vast majority of NEOs are asteroids, referred to as Near-Earth Asteroids (NEAs). NEAs are divided into groups (Atira, Aten, Apollo and Amor) according to their	perihelion distance (q), aphelion distance (Q) and their semi-major axes (a).

Potentially Hazardous Asteroids (PHAs) are currently defined based on parameters that measure the asteroid's potential to make threatening close approaches to the Earth. Specifically, all asteroids with an Earth Minimum Orbit Intersection Distance (MOID) of 0.05 au or less and an absolute magnitude (H) of 22.0 or less are considered PHAs. In other words, asteroids that can't get any closer to the Earth (i.e.,MOID) than 0.05 au (roughly 7,480,000 km or 4,650,000 mi) or are smaller than about 140 m (~500 ft) in diameter (i.e., H = 22.0 with assumed albedo of 14%) are not considered PHAs.										

~https://cneos.jpl.nasa.gov/about/neo_groups.html


# WORK Process: 

## Pandas: 	
In reviewing the data in NEO_V2.csv we discovered multiple entries for some ID's. Our review showed values in the relative_velocity and miss_distance columns vary causing multiple entries for id's. Values in other columns remain constant.

Using Pandas, we separated columns into two dataframes: 
	-'df_new' includes two columns:
		1. relative_velocity
		2. miss_distance

	- 'no_duplicates_df' includes: 
	All columns except relative_velocity and miss_distance

after splitting the data and removing duplicates from 'no_duplicates_df', we created CSV files to be used in our SQL database.

Our description of the data includes summary statistics on the "miss_df" dataframe. Using a loc method on the "miss_df" dataframe, we isolated the true and false values in the hazardous column. This allowed us to create boxplots on other features in the dataset.  

## PostGres (SQL):
	With CSV files created, we created two tables in PostGres:

		1. vel_miss 
		2. no_duplicates
		
	Using a left-join, we created a new table called 'combined_tables'.

See image below of the first 20 rows of the SQL file. 

![combined_table](https://github.com/mhhussain24/AsteroidProject/blob/KY_asteriods/Resources/PostGres_left_join.png)


The image below shows a groupby statement created in PostGres that indicates repeat entries by id. 

![Groupby_ID](https://github.com/mhhussain24/AsteroidProject/blob/main/Resources/Group_by.png) 


## Machine Learning Model: 
The team analyzed near Earth object (NEO) data, using binary classification models to predict whether an object is hazardous to the Earth, or not.  We will be analyzing and comparing our results from a decision tree model and a logistic regression model.

#### Preliminary data preprocessing:
1. Import and read the source data.
2. Display an overview of the dataset and confirm no null values in the dataset.
3. Determine which features to keep and which to drop from the dataset.  We dropped redundant column 'id', and two columns with one unique value each, 'orbiting_body' (all values = 'Earth') and 'sentry_object' (all values = 'False').
4. We used AutoViz dataset auto-visualization library to provide a preliminary look at our source data, once preprocessed.

#### Preliminary feature engineering and feature selection:
1. Define the features set ('est_diameter_min', 'est_diameter_max', 'relative_velocity', 'miss_distance', and 'absolute_magnitude').  We have 5 independent variables in our dataset.
2. Define the target set ('hazardous').  This is the dependent variable, the binary classification of our dataset.  This is the value that we are trying to predict.


#### Splitting the data into training and testing sets:
1. Split the preprocessed data into a training and testing dataset.
  ```python
    X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=420, train_size=0.80)
  ```
2. Check the balance of the dataset.  In our case, the data was imbalanced and overfitting.
3. Rebalance the dataset.  We used SMOTEENN combination sampling.
  ```python
    smote_enn = SMOTEENN(random_state=0)
    X_resampled, y_resampled = smote_enn.fit_resample(X, y)
  ```
4. Create a StandardScaler instance; fit and scale the data.
  ```python
    scaler = StandardScaler()
    X_scaler = scaler.fit(X_train)
    X_train_scaled = X_scaler.transform(X_train)
    X_test_scaled = X_scaler.transform(X_test)
  ```
The benefits of the models selected is that they are well suited to categorical output.  In our supervised machine learning we happen to have a binary classifier, 'hazardous' or 'non-hazardous', which can also be represented as 'True'('hazardous') and 'False'('non-hazardous').  One potential downfall of our model will be overfitting our data, although we resampled the data to try and resolve the issue.  Another downfall our models may face is with the limited number of features, 5 in this case.


#### Tableau:
We used Tableau to create various visuals of the features, specifically: 
	- Hazardous versus non_Hazardous
	- Absolute Magnitude to Relative Velocity (isolating hazardous objects)
	- Absolute Magnitude to Miss Distance (isolating hazardous objects)

The clean dataset also isolates year allowing us to create a visual showing counts of objects by year. This visula supports knowing if more objects are detected in more recent years. 

As we worked with the data, we questioned: 
	1. If more objects can be detected due to better technology 
	2. If there is an increase in polution in the Universe causing more objects to be present. 
Both questions are interesting and plausible. 

 



 				
		




 









