<img src="https://github.com/dhavalgarg/Prediction-of-Hourly-Bike-Usage-for-Citi-Bike-Stations-in-New-York-City/blob/master/img/logo_main.png" width="1600" title="CitiBike Nyc and DataBricks">

 # Built an end to end machine learning pipeline that can predict the hourly demand of NY Citi-Bikes at a particular station
--------------------------------------------------------------------------------------------------------------------------------------------------

### Content
1. Introduction
2. Platform
3. Methodology
   - ETL
   - EDA
   - ML Model and Registry
   - Application and Real Time Model
5. Conclusion

## INTRODUCTION
Implemented in New York City, the Citi Bike program has become a widely embraced bike-sharing system, catering to the transportation needs of both residents and visitors. Boasting over 1500 stations scattered across New York and Jersey City, this service has evolved into a staple for millions who rely on it for commuting, shopping, and recreational purposes. The challenge of maintaining an ample supply of bikes at each station is effectively addressed through data science. Leveraging a comprehensive machine learning pipeline, bike usage is closely monitored, allowing for accurate hourly predictions of ride demands. This strategic approach empowers the business to discern demand patterns, promptly restock bikes at docking stations, and efficiently distribute bikes among various locations. Ultimately, this data-driven strategy elevates operational efficiency, ensuring a consistent availability of rides and cultivating satisfied customers.

## Platform
To tackle the data-intensive challenge and enhance processing speed, we built the entire application on the Databricks platform. Python and Pyspark SQL served as the primary programming languages for coding purposes.

## Methodology
To efficiently handle the large volume of data and deliver timely insights, a well-structured pipeline was designed. The project plan was divided into four key sections:

1. Building an ETL (Extract, Transform, Load) pipeline to handle the hourly influx of new and historical data.
2. Conducting exploratory data analysis (EDA) to identify relevant features and patterns.
3. Developing a machine learning model to make accurate predictions based on the identified features.
4. Establishing a machine learning model registry for tracking and updating the models over time.

This approach ensured a streamlined process, enabling the team to effectively handle the data, gain insights, and continuously improve the machine learning models.

### ETL
Considering the extensive volume of data involved, it was crucial to devise an optimized and effective data pipeline capable of seamlessly managing both incoming and existing data. The project incorporated two primary data sources: historical data files spanning two years and real-time data updates received every 30 minutes. The goal was to utilize the historical data for training a forecasting model, validate its performance with live data, and employ the model to predict demand for the next 48 hours or beyond.

To realize this objective, distinct table structures and relationships were established for historical and real-time data. The dataset encompassed two years of trip history details, historical weather data spanning two years (with occasional gaps), and three other data sources updated every 30 minutes. Adhering to the Medallion format, the pipeline architecture stored raw data in bronze tables, while cleaned, merged, and model-relevant data found its place in silver tables. API calls were integrated to address missing weather data, with gold tables reserved for model inference and data monitoring. Ensuring immutability, the ETL pipeline was designed to prevent side effects when executed multiple times with the same input data.

<img src="https://github.com/dhavalgarg/Prediction-of-Hourly-Bike-Usage-for-Citi-Bike-Stations-in-New-York-City/blob/master/img/ETL_Arch.png">

This carefully designed architecture ensured a robust and efficient data pipeline, facilitating the extraction, transformation, and loading of data for analysis and modeling purposes.

**Link to code** - [ETL](https://github.com/dhavalgarg/Prediction-of-Hourly-Bike-Usage-for-Citi-Bike-Stations-in-New-York-City/blob/master/final_project/01%20etl.py)

### EDA
Exploratory data analysis (EDA) played a pivotal role in this study as it provided valuable insights into the usage patterns and operational demand of Citi Bikes. Key findings from the analysis include:

- Seasonal Variations: Seasonal variations played a crucial role in ride counts. During winter, ride counts decreased due to snowfall and unfavorable weather conditions, whereas ride counts increased during summer and fall.

<p align="center">
<img src="https://github.com/dhavalgarg/Prediction-of-Hourly-Bike-Usage-for-Citi-Bike-Stations-in-New-York-City/blob/master/img/yearmonth_1.png" width="400px" height="200px"/>
<img src="https://github.com/dhavalgarg/Prediction-of-Hourly-Bike-Usage-for-Citi-Bike-Stations-in-New-York-City/blob/master/img/yearmonth_2.png" width="400px" height="200px"/>
</p>
  
+ Weekend Effect: There was a noticeable decrease in ride counts during weekends, suggesting a shift in user behavior. Factors such as visibility, cloud cover, and rain emerged as significant contributors to this trend.
<p align="center">
<img src="https://github.com/dhavalgarg/Prediction-of-Hourly-Bike-Usage-for-Citi-Bike-Stations-in-New-York-City/blob/master/img/weekend-effect.png" width="500" height="200"/>
</p>

+ Hourly Patterns: Ride counts exhibited distinct patterns based on the hour of the day. Increased ride activity was observed during early morning and evening hours, corresponding to office commute times. This finding indicated a substantial user base consisting of daily office goers.
<p align="center">
<img src="https://github.com/dhavalgarg/Prediction-of-Hourly-Bike-Usage-for-Citi-Bike-Stations-in-New-York-City/blob/master/img/hourofday-effect.png" width="500" height="200"/>
</p>

+ Holiday Impact: Holidays had a notable impact on ride counts, with a decline observed during these periods. In the are plot below, significant dips in bike usage were observed on specific dates, including Thanksgiving (Nov 25, 2021), Christmas Day (Dec 25, 2021), a snowstorm (Jan 29, 2022), President's Day (Feb 21, 2022), Easter (Apr 17), and Independence Day (Jul 4). These events and holidays contributed to reduced bike activity, indicating the influence of such occasions on Citi Bikes' usage.
<p align="center">
<img src="https://github.com/dhavalgarg/Prediction-of-Hourly-Bike-Usage-for-Citi-Bike-Stations-in-New-York-City/blob/master/img/holiday-effect.png" width="400px" height="200px"/>
<img src="https://github.com/dhavalgarg/Prediction-of-Hourly-Bike-Usage-for-Citi-Bike-Stations-in-New-York-City/blob/master/img/monthly-effect.png" width="400px" height="200px"/>
</p>

+ Temperature Influence: While not a dominant factor, a significant rise in temperature was found to reduce ride counts. This observation underscores the sensitivity of ridership to changes in weather conditions.
<p align="center">
<img src="https://github.com/dhavalgarg/Prediction-of-Hourly-Bike-Usage-for-Citi-Bike-Stations-in-New-York-City/blob/master/img/temp-effect.png" width="500" height="200"/>
</p>

+ Cloud/Visibility Effect: The graph clearly illustrates that snowy and rainy weather conditions resulted in a significant decrease in the number of rides, while riders continued to use the service during cloudy and clear sky conditions.
<p align="center">
<img src="https://github.com/dhavalgarg/Prediction-of-Hourly-Bike-Usage-for-Citi-Bike-Stations-in-New-York-City/blob/master/img/cloudvisibility-effect.png" width="500" height="200"/>
</p>

These findings played a **critical role in informing the subsequent data modeling** process, enabling the development of models tailored to improve prediction accuracy.

**Link to Code**: [EDA File](https://github.com/dhavalgarg/Prediction-of-Hourly-Bike-Usage-for-Citi-Bike-Stations-in-New-York-City/blob/master/final_project/02%20eda.py)

### ML Model and Registry
Following the essential steps of data storage and preprocessing, the subsequent phase entailed constructing the forecasting model. In this project, we opted for the widely recognized FB-Prophet model, incorporating insights from the exploratory data analysis (EDA) to address monthly, daily, and hourly seasonality patterns. The model also factored in holiday effects. For streamlined tracking and management of model artifacts, parameters, and metrics, Databricks' MLflow Tracking was instrumental. This feature enabled us to compare different models, identify the optimal one, and effortlessly reuse the selected model. Furthermore, the use of MLflow Registry facilitated a seamless transition from staging to production for the chosen model, ensuring its continual utilization based on incoming data. Despite the option to add various versions of our model to the ML Model Registry, the superior performance of the FB-Prophet model led to its exclusive inclusion in the registry, marking a successful transition to the production stage.

**Link to Code**: [ML Model File](https://github.com/dhavalgarg/Prediction-of-Hourly-Bike-Usage-for-Citi-Bike-Stations-in-New-York-City/blob/master/final_project/03%20mdl.py)

### Application and Real Time Model
In the final phase of our project, we focused on monitoring the performance of the forecasting model as new data arrived every 30 minutes. To accomplish this, we utilized the gold tables to track the live performance of the model. This allowed us to promptly take action if the model's performance fell below a predefined threshold and update the model accordingly.

The implementation involved loading both the production and staging models, which were trained during the Model Development stage. We then loaded real-time data on the bike status at a specific station, along with real-time and forecasted weather data. The forecasted weather data served as regressors to predict bike availability in the next 48 hours. Using both the staging and production models, we forecasted the bike inventory.

To compare the performance of the staging and production models, we examined the residuals data until the ground truth data was available. Based on the residuals plot, the code was designed to promote the staging model to production when deemed appropriate.

The following image depicts the forecast that was made to understand demand at a particular station
<p align="center">
<img src="https://github.com/dhavalgarg/Prediction-of-Hourly-Bike-Usage-for-Citi-Bike-Stations-in-New-York-City/blob/master/img/forecast_1.png" width="600" height="150"/>
</p>

**Link to Code**: [Application Monitoring File](https://github.com/dhavalgarg/Prediction-of-Hourly-Bike-Usage-for-Citi-Bike-Stations-in-New-York-City/blob/master/final_project/04%20app.py)


## Conclusion
The objective of this project was to create a holistic machine learning application to support businesses like NY Citi Bike in comprehending and managing the demand for their services, ultimately enhancing operational efficiency. Leveraging Databricks, renowned for its robust capabilities, proved pivotal in efficiently processing extensive data volumes. Moreover, it served as a comprehensive platform for data visualization, Python/SQL coding, and the deployment and monitoring of multiple models, consolidating various tasks under one umbrella. Juggling multiple machine learning models, identifying optimal hyperparameters, and monitoring model artifacts can pose challenges, but Databricks simplified these complexities with the incorporation of ML-Flow and ML-Registry. This becomes particularly beneficial for visualizing, maintaining, and enhancing prediction performance while automating the overall workflow. In summary, this project was an invaluable learning experience, showcasing the strides in technology and their potential to drive business growth in a competitive market.


