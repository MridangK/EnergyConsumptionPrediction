# Energy Consumption Time Series Prediction using XGBoost

This project focuses on predicting energy consumption using the powerful XGBoost algorithm. Accurately forecasting energy consumption is crucial for efficient resource allocation, demand planning, and sustainable energy management in various domains, including residential, commercial, and industrial sectors.

## Introduction

In this project, we leverage XGBoost, a popular gradient boosting technique renowned for its excellent performance in handling time series data. By combining decision trees and boosting techniques, XGBoost provides highly accurate predictions and robust feature selection capabilities.

The primary objective of this project is to develop a reliable model that can predict future energy consumption based on historical data. By analyzing and understanding the underlying patterns and trends in the energy consumption time series, we aim to build a predictive model capable of capturing complex dependencies and variations.

## Project Highlights

- Implementation of the energy consumption prediction pipeline using XGBoost.
- Clear and well-documented code available in this GitHub repository.
- Detailed explanations accompanying the code to aid understanding.
- Inclusion of relevant visualizations and insights gained from the analysis.

## Types of Time Series Data Analysis

During the course of this project, we consider the following types of time series data analysis:

1. **Purely Random Error - No Recognizable Pattern**

   This type of time series data is characterized by random fluctuations or noise without any discernible pattern. It indicates that the energy consumption values are randomly distributed around a mean value without any significant trends or dependencies.

2. **Curvilinear Trend (quadratic, exponential)**

   Curvilinear trends in time series data exhibit a nonlinear relationship between the time variable and energy consumption. It can take different forms, such as quadratic or exponential growth/decay. Understanding the curvilinear trend helps capture the nonlinear behavior and make more accurate predictions.

3. **Increasing Linear Trend**

   An increasing linear trend indicates a consistent and steady rise in energy consumption over time. It suggests a linear relationship where energy consumption increases at a constant rate. Identifying this trend helps predict future energy consumption based on the linear growth pattern.

4. **Seasonal Pattern**

   Seasonal patterns refer to regular and predictable fluctuations in energy consumption that occur within a specific time frame. For example, energy consumption might follow a yearly, monthly, or weekly cycle. Analyzing seasonal patterns helps identify recurring patterns and adjust predictions accordingly.

5. **Seasonal Pattern Plus Linear Growth**

   This type of time series data combines both seasonal patterns and a linear growth component. It implies that energy consumption exhibits regular fluctuations while gradually increasing or decreasing over time. Modeling both the seasonal pattern and the linear growth allows for capturing more complex variations in energy consumption.

These different types of time series data analysis enable us to gain insights into the underlying patterns and trends in energy consumption. By considering and addressing these variations, we can build accurate predictive models using the powerful XGBoost algorithm.

![TypesOfTimeSeries](Pictures/TimeSeriesTypes.jpg)


## Dataset

The dataset used in this project was obtained from Kaggle. It consists of the following two features:

1. **PJME_MW**: This feature represents the energy consumption in megawatts (MW). It provides the primary data for our analysis and prediction.

2. **Datetime**: This feature represents the timestamp or date and time associated with each energy consumption measurement. It allows us to analyze the energy consumption patterns over time.

## Data Visualization

To facilitate data visualization, we utilized the `to_datetime` function from the pandas library. This function allows us to convert the datetime strings in the dataset into datetime objects, enabling easier manipulation and plotting of the data.

Visualization plays a crucial role in understanding the underlying patterns and trends in the dataset. It helps us gain insights into the relationships between the features and identify any significant temporal variations in energy consumption.

By effectively visualizing the dataset, we can make informed decisions and develop accurate models for energy consumption time series prediction.

![DataVisualization](Pictures/Energy_Consumption_plot.png)

## Train-Test Split

To assess the performance and accuracy of our predictive model, we divide the dataset into two subsets: the training dataset and the test dataset. The split is based on the following criterion:

- All data points before 1st Jan 2015 are included in the training dataset.
- All data points after 1st Jan 2015 are included in the test dataset.

By separating the data in this way, we ensure that our model is trained on historical observations and evaluated on future unseen data. This split allows us to simulate real-world scenarios where the model predicts energy consumption on new and unknown data.

## Data Visualization

Visualizing the train-test split can help us understand the distribution of the data and the separation between the training and test sets. This visualization aids in assessing the temporal order and ensuring that the split aligns with our intended division of the dataset.

By visually inspecting the train-test split, we can verify that the division accurately represents the temporal sequence of the data and enables reliable evaluation of our predictive model's performance.

![TrainTest](Pictures/Test_train_plot_2.PNG)

## Feature Creation

As part of the feature creation process, the `create_features` function is utilized to extract additional features from the dataset. These features provide supplementary information that has the potential to enhance the accuracy of the energy consumption prediction model.

The `create_features` function adds the following features to the dataset:

- **hour**: Extracted from the timestamp index, indicating the hour of the day.
- **dayofweek**: Extracted from the timestamp index, indicating the day of the week (0 for Monday, 6 for Sunday).
- **quarter**: Extracted from the timestamp index, indicating the quarter of the year.
- **month**: Extracted from the timestamp index, indicating the month of the year.
- **year**: Extracted from the timestamp index, indicating the year.
- **dayofyear**: Extracted from the timestamp index, indicating the day of the year.

By incorporating these additional features into the energy consumption prediction model, we capture temporal patterns and seasonality present in the data. This information can be invaluable for modeling and accurately predicting energy consumption.

The inclusion of these extracted features is expected to enhance the performance and predictive capabilities of the energy consumption prediction model.

## Visualizing Feature-Target Relationship

To understand the relationship between our extracted features and the target variable (energy consumption), we can visualize the patterns and trends in the data. This visualization provides insights into how the features vary with respect to the target variable.

### Feature: Hour of the Day

By plotting the energy consumption against the hour of the day, we can observe the following:

![VisualizeRelationshipHour](Pictures/VisualizeRelationshipHour.png)

In the early morning hours, there is a dip in energy consumption, which gradually increases throughout the day. This pattern indicates that energy usage tends to be lower during the early hours and progressively rises as the day progresses.

### Feature: Seasonality (Winter, Spring, Summer)

To analyze the relationship between energy consumption and seasonality, we can plot the energy consumption against the seasons:

![VisualizeRelationshipMonth](Pictures/VisualizeRelationshipMonth.png)

From the visualization, we can observe that there is a peak in energy consumption during the winter season. As the winter season is associated with colder temperatures, this increase in energy consumption can be attributed to the higher demand for heating systems. On the other hand, energy consumption tends to be relatively lower during the spring season. As we transition into summer, there is another rise in energy consumption, potentially due to increased usage of cooling systems.

By visualizing the feature-target relationship, we can gain valuable insights into how the extracted features are related to energy consumption. This understanding helps in developing a more accurate energy consumption prediction model.


## Model Creation

For our energy consumption prediction, we utilized the XGB Regressor model. To prevent overfitting and improve the model's generalization ability, we applied the following techniques:

- **Reduced learning rate**: We set the learning rate to 0.01, which controls the step size during the boosting process. A lower learning rate helps prevent overfitting and allows for a more stable convergence of the model.

- **Early stopping rounds**: We implemented early stopping with a patience of 50 rounds. Early stopping monitors the evaluation metric (e.g., mean squared error) on a validation set and stops the training process if the metric does not improve after a certain number of rounds. This technique helps prevent overfitting by stopping the training when the model's performance plateaus.

We determined these parameter values based on our observation of the evaluation set data obtained during the model's fitting process. By evaluating the model's performance on both the training and testing data (X_train and X_test), we obtained a better estimate of the optimal parameters.

## Feature Importance

After training the XGB Regressor model, we can assess the importance of different features in predicting energy consumption. By plotting the feature importance, we can observe the following:

![Feature Importance Plot](Pictures/FeatureImportance_2.PNG)

From the visualization, we can see that the "hour" feature is the most important feature in predicting energy consumption. This indicates that the time of day has a significant impact on energy consumption patterns.

## Interpreting the Results

![RawVSPrediction](Pictures/RawvsPrediction_2.PNG)


Upon analyzing the prediction results, it is evident that the model did not perform well in accurately predicting energy consumption. To improve the model's performance and increase the prediction score, further parameter tuning is necessary.

By fine-tuning the model's hyperparameters, such as adjusting the learning rate, maximum depth of trees, and regularization parameters, we can enhance the model's ability to capture complex dependencies and variations in the data. Additionally, exploring other feature engineering techniques and incorporating additional relevant features may also contribute to improving the model's prediction accuracy.
