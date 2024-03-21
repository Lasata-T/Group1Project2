# National COVID Data: 2020-2024

Group1Project2 Group Members: Katherine Driebe (kad5fwz), Ramya Tangirala (rt4an), and Lasata Tuladhar (lt9vx)

The topic that this project will be focusing on is national COVID data between the years 2020 and early 2024. The two time-series datasets used are the new weekly hospitalizations due to COVID and the weekly deaths due to COVID. Both datasets were downloaded on the week of February 22nd, 2024, from the Center of Disease Control’s (CDC) online COVID tracker [1, 2]. The raw data includes the geographical location the data was taken, the date the data was entered, and the actual data value. 

Our group cleaned the original data to remove NA values, then merged the two datasets. The link to our full data dictionary can be found here: 
[Data Dictionary](/DATA/Data_Dictionary.md)

Our initial stance was that an increase in the number of weekly hospitalizations will result in an increase in the rate of weekly deaths, and for the time-series forecasting section, the ARIMA model should be able to predict both weekly hospitalizations and deaths for the future. After our exploratory analysis, we reaffirmed that our hypothesis was sufficient, except for the fact that we would be looking at the _number_ or _count_ of weekly deaths, rather than the rate. Therefore, our updated hypothesis for the project is as follows: **an increase in the number of weekly hospitalizations will result in an increase in the _number_ of weekly deaths. The ARIMA model should be able to predict both weekly hospitalizations and deaths for the future using time-series forecasting.** 

This project is targeted toward hospital staffers and policymakers to understand how to best combat COVID-19 in the future. 

## Section 1: Software and Platform
For this project, our group downloaded the `.csv` files directly from the CDC’s COVID tracker website [1, 2]. After receiving the data and downloading it into our Python script in Google Colab, we imported the following libraries: `numpy`, `pandas`, `DataFrame` from `pandas`, `matplotlib.pyplot`, `matplotlib.dates`, `files` from `google.colab`, `ARIMA` from `statsmodels.tsa.arima.model`, `autocorrelation_plot` from `pandas.plotting`, `sqrt` from `math`, `mean_squared_error` from `sklearn.metrics`, and `statsmodel.api`. All of the code was run on a Macbook Pro laptop supporting the MacOS platform and two different Lenovo laptops, both supporting the Windows platform.

## Section 2: Documentation Map
Our Project 2 repository is titled Group1Project2. It contains three folders (SCRIPTS, DATA, and OUTPUT), a MIT LICENSE file, and a README.md file. The SCRIPTS folder contains a master script which contains all the code needed to reproduce our data and analysis. The DATA folder contains the original datasets used for the analysis as well as the complete data dictionary. The OUTPUT folder contains all plots, including the initial exploratory plots, finals plots, and plots produced by the ARIMA model.

## Section 3: Reproduction of Results
Below is a step-by-step procedure of how to reproduce our group’s results:

1. Obtain both datasets from the following links:  https://covid.cdc.gov/covid-data-tracker/#trends_weeklyhospitaladmissions_select_00 [1] and https://covid.cdc.gov/covid-data-tracker/#trends_weeklydeaths_select_00 [2]. Read in the data as `pandas` dataframes.

2. Subset the dataset so that there is only data from February 22nd, 2024 or earlier. Clean the datasets so that there are no NA values. Merge both datasets on the `Date` and `Geography` columns into a single dataframe. This should reduce the size of the dataset from 215 data points to 185 data points.

3. Create and display a stacked line graph by plotting the merged dataframe with `Date` in the x-axis and `Count` in the y-axis.

4. Start with the weekly deaths data. Create an autocorrelation plot using the `pandas.plotting` library to review the correlation of the data.

5. Create the ARIMA model using the `statsmodels` library, and print and review the summary.

6. Create and display the line and density plot, and the summary statistics of the residuals for review.

7. To start rolling the forecasting, split the data into training and testing sets. Continue with the walk-forward validation.

8. Display the evaluations of the forecasts by calculating the root mean square error (RMSE) value.

9. Plot the forecasts (predictions) against the actual outcomes.

10. Repeat steps 4-9 for the weekly hospitalizations.

11. To determine the accuracy of the ARIMA model, run the Ljung-Box (autocorrelation) and Jarque-Bera (normality) tests using the `statsmodel.api` library. For the Ljung-Box test, the null hypothesis should be that there is no autocorrelation. For the Jarque-Bera test, the null hypothesis should be that the data is normally distributed. If the p-value < a * 0.05, reject the null.

12. The following are the results for the model accuracy check: Ljung-Box p-value for weekly deaths = 0.95, Ljung-Box p-value for weekly hospitalizations = 0.08, Jarque-Bera p-value for weekly deaths = 1.26E-21, and Jarque-Bera p-value for weekly hospitalizations = 3.66E-100. 

13. Therefore, the null hypothesis was rejected for both data in the Jarque-Bera test, but only rejected for the weekly hospitalizations in the Ljung-Box test. From this, we can conclude that the ARIMA model is acceptable for the weekly hospitalizations data, but not for the weekly deaths data.

## References (IEEE Format):
- [1] CDC, “COVID Data Tracker,” Centers for Disease Control and Prevention, Mar. 28, 2020. https://covid.cdc.gov/covid-data-tracker/#trends_weeklyhospitaladmissions_select_00 

- [2] CDC, “COVID Data Tracker,” Centers for Disease Control and Prevention, Mar. 28, 2020. https://covid.cdc.gov/covid-data-tracker/#trends_weeklydeaths_select_00 
