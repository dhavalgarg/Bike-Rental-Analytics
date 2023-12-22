<img src="https://raw.githubusercontent.com/skswar/NYCitibike_Demand_Prediction_ML_Pipeline/master/img/logo_main.png" width="1600" title="CitiBike Nyc and DataBricks">

 # Built an end to end machine learning pipeline that can predict the hourly demand of NY Citi-Bikes at a particular station
--------------------------------------------------------------------------------------------------------------------------------------------------

### Content
1. [Introduction][]
2. Platform
3. Methodology
     i.   Building ETL
     ii.  Performing EDA
     iii. Buidling ML Model and Registry
     iv.  Application and Real Time Model Updation
4. Conclusion

## INTRODUCTION
Implemented in New York City, the Citi Bike program has become a widely embraced bike-sharing system, catering to the transportation needs of both residents and visitors. Boasting over 1500 stations scattered across New York and Jersey City, this service has evolved into a staple for millions who rely on it for commuting, shopping, and recreational purposes. The challenge of maintaining an ample supply of bikes at each station is effectively addressed through data science. Leveraging a comprehensive machine learning pipeline, bike usage is closely monitored, allowing for accurate hourly predictions of ride demands. This strategic approach empowers the business to discern demand patterns, promptly restock bikes at docking stations, and efficiently distribute bikes among various locations. Ultimately, this data-driven strategy elevates operational efficiency, ensuring a consistent availability of rides and cultivating satisfied customers.

## Platform
To tackle the data-intensive challenge and enhance processing speed, we built the entire application on the Databricks platform. Python and Pyspark SQL served as the primary programming languages for coding purposes.

## Methodology
To efficiently handle the large volume of data and deliver timely insights, a well-structured pipeline was designed. The project plan was divided into four key sections:

Building an ETL (Extract, Transform, Load) pipeline to handle the hourly influx of new and historical data.
Conducting exploratory data analysis (EDA) to identify relevant features and patterns.
Developing a machine learning model to make accurate predictions based on the identified features.
Establishing a machine learning model registry for tracking and updating the models over time.
This approach ensured a streamlined process, enabling the team to effectively handle the data, gain insights, and continuously improve the machine learning models.
