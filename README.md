# US_Natural_Disaster_Analysis

 ## A thorough analysis studying the correlations and patterns of natural disasters across time and regions in the United States using Python.
 
![](Images/slide1.jpg)
"Climate is what we expect, weather is what we get." - Mark Twain

### Project Overview 

Natural disasters can be catastrophic to the areas and people who are affected by them. In 2022, surveys from Forbes Home indicated that almost a third of the survey respondents cited worsening weather conditions as a reason for them to move. The same articles stated that nearly two-thirds (62%) of US residents who planned on buying or selling their homes were hesitant to do so in areas at risk of natural disasters, severe temperatures, and rising sea levels. Almost three-quarters (71%) of Gen-Z participants stated they would be apprehensive to move to an area that was at risk of these factors as well. 

The primary goal of this analysis is to observe the overall frequency of major disasters by geographical location at the regional and state level over time, and to create a model that predicts future incidents past on past events. The results produced in this analysis could be impactful when deciding where to relocate within the United States. 

In this project, the following questions will be answered to create an analysis to provide prospective residents of the US with: 

* What are the states with most number of major disasters?
* What are the frequency of the different disaster types?
* What is the severity and duration of events over time?
* What are the most disaster prone areas of the United States?
* How does this information help us to predict the frequency, location and type of disasters yet to come?

The following natural disasters will be studied in this analysis:

* Drought
* Fire
* Freezing
* Hurricanes
* Mud/Landslide
* Severe Ice Storm
* Severe Storms
* Snow
* Tsunami
* Volcano

Overall, could this analysis show potential movers climatic incentives or deterrents to assist them in choosing where in the US to live next?  

### Data Sets

The dataset used during this analysis, us_disaster_declarations.csv, was sourced from Kaggle.com. The content includes a high-level summary of all federally declared disasters by FEMA since 1953 and provides metrics such as the incident type, incident time and duration, geography, and whether programs were implemented. 

### Software

* Python 3..13 (Dependencies: Pandas 1.3.5, SciKit-Learn 1.0, Tensorflow 2.10.0)
* Anaconda 2022.10
* Jupyter Notebook 6.4.12
* Amazon Web Services: RDS, S3
* PostgreSQL 13.7
* pgAdmin 6.8
* ArcGIS Pro 3.0
* Google Presentations

### Assigned Roles for Deliverable 4

* Jeanine - Square: Managed the Github repository & README. Continued to clean and transform the dataset to suit the analysis & created visualizations.  
* Deanna - X: Continued to refine, train and test the machine learning models chosen, created visualizations. 
* Kirsten - X: Tested database integration, continued to enhance database functions, created visualizations using ArcGIS Pro 3.0.
* Gilda - Triangle/Circle: Continued to develop and refine the presentation by working on the storyboard, visualizations and dashboard.
* Zoe Lackey - Triangle/Circle: Continued to develop and refine the presentation by working on the storyboard, visualizations and dashboard.

### Data Cleaning & Transforming Process

1.	The original data set, us_disaster_declarations.csv, was loaded into Jupyter Notebook and filtered to only show the incidents occurring from 1980 to 2020 using Pandas. The clean_df.csv was produced from these actions and then used to create the nd_df data frame. From this point, columns housing data that was inconsequential to the analysis were removed from the data set.

![](Images/cleandf.jpg)
![](Images/cleaningdata_removecolumns.jpg)

2.	Outlier incident types that were at risk of skewing the results in this analysis, such as the COVID-19 pandemic, were removed from the dataset.
![](Images/cleaningdata_remove_outlier_disasters.jpg)

3.	The values in the US territories, American Samoa, Guam, Northern Mariana Islands, Puerto Rico and U.S. Virgin Islands, were removed from the dataset to avoid skewing due to these areas having disastrous weather conditions at a higher frequency and to focus more on the data for the mainland US. 
![](Images/cleaningdata_removeterritoriesskew.jpg)

4.	The date strings were changed into proper date format.
![](Images/cleaningdata_changingdateformats.jpg)

5. Duplicate incident reports were removed from the data set. 
![](Images/cleaningdata_removeduplicates.jpg)

6.	A new column was created to house the numeric month value each incident began so analysis could be conducted on what time of the year incidents occurred. 
![](Images/cleaningdata_creatingmonthcolumn.jpg)

7.	A new column was created, incident_duration, by subtracting the incident_begin_date column from the incident_end_date column This allows analysis to be conducted on the duration of each incident. The data type of the column was then changed from an object to an integer. 
![](Images/cleaningdata_creatingincidentdurationcolumn.jpg)

8.	All zero values in the incident duration column represent incidents that were less than a day in length and were changed to the number 1 in the data set. 
![](Images/cleaningdata_changingzerovaluestoone.jpg)

9.	A new column was created to house the year each incident began. 
![](Images/cleaningdata_creatingcolumnforyear.jpg)

10.	To conduct analysis on the US regions the disasters occurred in, a dictionary was created that contained the state abbreviations as well as their respective regions. The function “get_region” was created using .apply() to match the region to the states in a new column called “regions”. 

![](Images/cleaningdata_createdictforregions.jpg)
![](Images/cleaningdata_createdictforregions2.jpg)

11.	A new column was created that combined the values from all four “program_declared” columns in the dataset. 
![](Images/cleaningdata_programsdelcared.jpg)

12.	A new column was created that housed the season each incident occured within. 
![](Images/cleaningdata_seasonscolumn.jpg)

13. A new column was created that housed the numeric group for the seasons.
![](Images/cleaningdata_numericseasons.jpg)

14. A new column column was created that housed the numeric group for the regions.
![](Images/cleaningdatanumericregion.jpg)

15.	Additional columns that were proven to be obsolete to this analysis were dropped from the data set. 
![](Images/cleaningdata_droppingadditionalcolumns.jpg)

16.	A new data frame was created to house the disaster number, incident type, incident month, incident begin year and incident duration. 
![](Images/cleaningdata_creatingincidentdeclarationdf.jpg)

17.	A new data frame was created to house the disaster number, incident type, designated area, state, region and programs declared columns. 
![](Images/cleaningdata_creatingincidentlocationdf.jpg)

18. The transformed nd_df.csv was then exported into the Resources folder of the repository alongside the two new data frames, incident_declaration.csv and incident_duration.csv. 

### Machine Learning Model:

The following algorithms will be tested and utilized during this analysis:

##### ARIMA (AutoRegressive Integrated Moving Average):
* ARIMA is a forecasting algorithm that predicts a time series based on its own past values. ARIMA models use differencing to convert a non-stationary time series into stationary ones, predicting future values from historical data. Predicted values are a weighted linear combination of past values. Uses past values and lagged forecast errors to predict.

##### ARMA (Autoregressive Moving Average):
* ARMA is a forecasting algorithm that predicts time series based on its own past values. Uses past values, differencing (difference of consecutive values), and lagged forecast errors to predict.

###### Pros:
* Performs well on short term forecasts, easy to implement. 

###### Cons: 
* Subjectivity involved in determining order of the model, poorer performance for long term forecasts.

##### Preliminary data preprocessing:

* Sum incidents by year
* Create region and state dataframes.
     
##### Data Train and Test Split:
* Train = Incidents in years before 2015
* Test = Incidents in years from 2015 and on (2020)
     
##### Root Mean Squared Error(RMSE)
* The standard deviation of the prediction errors and will be used to determine how accurately the model prediction fits the test. The lower the RMSE, the better the fit.
     
### Top 5 States: time series and preditions using ARIMA (AutoRegressive Integrated Moving Average):

#### Alabama

##### Predictions:
![](Images/Alabama_Predictions.png)

##### Time Series:
![](Images/Alabama_Time_Series.png)

#### California

##### Predictons:
![](Images/California_Predictions.png)

##### Time Series
![](Images/California_Time_Series.png)

#### Florida

##### Predictons:
![](Images/Florida_Predictions.png)

##### Time Series
![](Images/Florida_Time_Series.png)

#### Oklaholma

##### Predictons:
![](Images/Oklahoma_Predictions.png)

##### Time Series
![](Images/Oklahoma_Time_Series.png)

#### Texas

##### Predictons:
![](Images/Texas_Predictions.png)

##### Time Series
![](Images/Texas_Time_Series.png)

### US Regions: time series and preditions using ARIMA (AutoRegressive Integrated Moving Average):

#### Midwest

##### Midwest Prediction
![](Images/Midwest_Predictions.png)

##### Midwest Time Series
![](Images/Midwest_Time_Series.png)

##### Midwest Root Mean Squared Error(RMSE)
* ARMA RMSE:  6.957494778174539
* ARIMA RMSE:  5.582063919229161

#### Southeast

##### Southeast Prediction
![](Images/Southeast_Predictions.png)

##### Southeast Time Series
![](Images/Southeast_Predictions.png)

##### Southeast Root Mean Squared Error(RMSE)
* ARMA RMSE:  3.735358277541541
* ARIMA RMSE:  2.1542422431320745

#### Northeast

##### Northeast Prediction
![](Images/Northeast_Predictions.png)

##### Northeast Time Series
![](Images/Northeast_Predictions.png)

##### Northeast Root Mean Squared Error(RMSE)
* ARMA RMSE:  4.741406279911125
* ARIMA RMSE: 3.087479272233823

#### Southwest

##### Southwest Prediction
![](Images/Southwest_Predictions.png)

##### Southwest Time Series
![](Images/Southwest_Predictions.png)

##### Southwest Root Mean Squared Error(RMSE)
* ARMA RMSE:  0.8008248266417702
* ARIMA RMSE: 0.8456739625167564

#### West

##### West Prediction
![](Images/West_Predictions.png)

##### West Time Series
![](Images/West_Predictions.png)

##### West Root Mean Squared Error(RMSE)
* ARMA RMSE:  4.95668562717005
* ARIMA RMSE:  5.342802335311312

### Database Workflow:

* Raw data was imported from source into Postgres database
* Dataframes from Python/Pandas were imported into database
* Final cleaned joined table was created in Postgres
* Data was uploaded to AWS to be available for Machine Learning and Visualization
* ERD was created

##### Database:
![](Images/PostgresDatabase_Final.PNG)

##### ERD:
![](Images/ERD.png)

### Visualization Workflow:

Tableau and ArcGIS Pro 3.0 will be used to create visualizations for this presentation.  Visualizations will include USA maps and choropleth maps and interpretations of top states divided up by counties (California and Texas) will be used to give further analysis in the presentation. 

##### ArcGIS Pro 3.0 video visualization of the number of incidents in each state by year:
![](Images/EventsPerStateByYearFormat.webp)

##### ArcGIS Pro 3.0 video visualization of the number of incidents in each region by year:
![](Images/EventsbyRegion.webp)

#### A link to the Tableau dashboard in progress is below:
https://public.tableau.com/views/US_Natural_Disaster_Analysis/Story1?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link

##### Area chart displaying total disasters over time, from 1980-2020, by disaster type:
![](Images/total_incidents_time.jpg)

##### Map of the US (excluding territories and commonwealths) displaying total recorded disasters by state:
![](Images/total_incidents_map.jpg)

##### Stacked bar chart displaying the total recorded incidents by state and incident type:
![](Images/total_incidents_state.jpg)

##### Density chart displaying the total number of incidents by incident type and month of occurrence:
![](Images/total_incidents_month.jpg)

##### Snapshot of the Tableau dashboard in progress:
![](Images/tableau_dashboard_snapshot.jpg)

Additional visualizations will be used to analyze temporal, seasonal data to identify peak seasons for certain kinds of natural disasters in the top 10 states that are proven to be hot spots as well as the states with the least disasters during those seasons. These will be used to give insights to clients about potential states where they can pass pleasant seasons if they live somewhere with a high number of natural disasters. 

#### Visualization Dashboard overview and proposal link below:
https://docs.google.com/presentation/d/1hPUla483eCj7iZsOuy-jvjMu_lQ1LE9z70fLbF-9IEc/edit#slide=id.g1f88252dc4_0_162

### Presentation

The Google presentation is in progress (link below). The presentation was edited for grammar as well as style in order to rework the language to suit the purpose of a professional presentation to a client. The presentation was edited to include more visuals, more succinct language, and speaker notes. 

https://docs.google.com/presentation/d/1F354MDtHzS25DnSC8x3uH112HeP4gVl2OF8Yy9zkmKw/edit#slide=id.p

A mock final presentation was conducted with the participants of this analysis and uploaded to Youtube:

https://www.youtube.com/watch?v=laYOgs7zY-o

### Summary and Results
* California had the most declared disasters overall, with 67 nationally declared natural disasters.
* There has been an overall increase in events over time as seen in the time series maps. This indicates an increasing level of severity of natural events.
* Where are the most declared disaster prone areas of the United States? XXX
* How can we predict disasters in various areas based on past events? XXXX

### Recommendations
Our recommendation to improve this analysis would be to add a secondary dataset for a comparative analysis, such as monetary impact, population impact or climate change. Seasonal ARIMA and other models for time series and forecasting should be explored, as well as problems delcared in relation to other provided variables in the dataset. 
