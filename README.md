# Uber Data Analysis

## Description

This project demonstrates data analysis skills using SQL and Python. The main goal was to explore a real dataset from the Kaggle platform, containing Uber rides, and extract relevant insights to answer business-related questions.

## Dataset

The dataset was taken from Kaggle, titled "Uber Data Analytics Dashboard", and contains information about 150,000 recorded rides.  
Dataset Link: [Link to dataset from Kaggle](https://www.kaggle.com/datasets/yashdevladdha/uber-ride-analytics-dashboard)

## Data Cleaning

* In this stage, I focused on preparing the data for analysis. I identified a significant number of missing values (NaN) using the `.isnull()` function from the Pandas library, and replaced the missing values with relevant ones. For example, for `Avg VTAT` I filled missing values using the median with the `.median()` function, so it would not negatively affect future statistical calculations such as the mean. In columns where a missing value clearly represents `0`, I filled accordingly; for example, in the `Cancelled Rides by Customer` column, it is clear that where no values exist, no rides were cancelled. For text columns, such as `Driver Cancellation Reason`, I filled missing values with `Unknown`.
* I checked for duplicate rows, specifically if there were duplicates in the `Booking ID` column, and then removed them, totaling `1233` duplicates.  
![Screenshot from code](/Screenshot_duplicates.png)
* I further checked if the unique values in text columns were correct using the `.unique()` function. Everything was fine.
* Additionally, I considered the potential presence of outliers. I used the median to fill missing values, a strategic choice ensuring that the analysis results are not distorted by extreme values, as the median is not affected by them.

## Analysis and Conclusions
* Next, we will find answers to 5 relevant questions related to Uber's operational performance, according to the provided table.

### Relevant Questions
* 1. What are the revenues and success rates by vehicle type?  
![Screenshot from code query1](/Screenshot%20query1.png)  
As we can see, a simple query provided the desired information for the 6 types of vehicles. For example, for the `Premier Sedan` vehicle, the total revenue was `8599586.0` and the ride success rate was `62.161560%`.  
These results are conclusive, and we can draw insights from the query, such as `Auto` being the vehicle type with the highest total revenue of `17711434.0`, while the `Uber XL` category has the highest ride success rate at `62.528268%`.

* 2. What are the peak hours and most popular pickup locations?  
I decided to split the two questions into two separate queries, `query2_hours` and `query2_Pickup_Location`.  
![Screenshot from code query2](/Screenshot%20query2_hours.png)  
According to this query, the peak hour is `18` with `12298` total rides, and the busiest period is between 16–19, probably because people return home from work during this interval.  
![Screenshot from code query2](/Screenshot%20query2_pickup_locations.png)  
The pickup locations query provides information about the top 10 locations with the most rides. For example, the most frequented pickup location is `Khandsa` with `947` rides.

* 3. What are the ride cancellation reasons and their impact?  
![Screenshot from code query3](/Screenshot%20query3.png)  
This query grouped in a table both driver and customer cancellation reasons. As seen, the largest number of cancelled rides is due to `Unknown`, resulting from many missing values (NaN) that were labeled this way during data cleaning. This indicates that the data collection process was not fully optimal, or both customers and drivers cancelled many rides without providing a clear reason, resulting in a potential revenue loss of `11090646.0`.  
The most frequent known cancellation reason is `Wrong Address`, with `2348` cancelled rides and a potential revenue loss of `972072.0`. Considering the sample size, this is not severe; it may occur due to inattention, frequent orders from different locations, or technical issues such as incorrect pickup checkpoints. A universal fix does not necessarily exist, but improving the app software and adding customer warnings when ordering could reduce cancellations due to address errors.

* 4. Comparison of ratings between drivers and customers, by vehicle type.  
![Screenshot from code query4](/Screenshot%20query4.png)  
I calculated the average using `AVG()` for `Driver Ratings` and `Customer Rating` and grouped results by vehicle type. The descending order based on driver ratings showed which vehicle type is most appreciated by customers. According to results, `Uber XL` has an average driver rating of `4.238590`, suggesting it is the most favored by customers. A recommendation would be to use as many vehicles of this type as possible to improve brand image and customer satisfaction.  

It is also observed that the average rating received by customers from drivers `4.403978` is slightly higher than the rating drivers receive from customers. This difference, visible across all vehicles, suggests that drivers are generally more lenient with customers than vice versa.  

The least appreciated vehicle according to driver ratings is `eBike`, with a score of `4.225571`. Although the difference is small, minor service improvements in this segment could be beneficial.

* 5. Revenue distribution by payment methods.  
This query analyzed revenue distribution by payment method. Results show that the `UPI` payment method is by far the most profitable, generating a total revenue of `21104861.0`. It is followed by `Cash` payments, with a total revenue of `11661552.0`, showing a clear preference for digital payments. This analysis suggests the company should continue optimizing and promoting the `UPI` system to maintain and grow this revenue source.

### Conclusion
In conclusion, this project aimed to demonstrate my skills in data processing and analysis, particularly the knowledge I acquired working with databases (SQL), using a real dataset from Kaggle. Through Python (Pandas) and SQL, I was able to extract valuable insights and transform raw data into business-relevant conclusions, highlighting practical knowledge in data analysis.

## Technologies Used

* Python
* Pandas
* SQLite 
* Jupyter Notebook
