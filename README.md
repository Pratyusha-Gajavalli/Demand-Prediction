# Demand-Prediction
# Problem statement and objective
The lodging industry has seen an unprecedented increase in short-term bookings since Jan 2021 due to COVID-19. Significant number of people shifted from long term planning to short term with respect to hotel bookings. This has made it difficult for economy hotel chains to generate revenue while operating at thin margins and plan their inventory and staffing levels. So, this project is for a hotel renting company where, number of bookings each hotel will get for a staydate in next 48 hours is predicted. 
To solve this problem, historical bookings happened in last 48 hour window for every hotel are taken as input and estimated for future dates using time series prediction algorithms. 

# Data Pre-processing 
Step-1: From the transactional data of all the properties, cancelled transactions are removed. Then, lead time for each transaction is calculated as staydate-bookingdate  and transactions with lead time < 3 are filtered.

Step-2: These filtered transactions are aggregated and no_of_bookings for each hotel on each Staydate is calculated. Now, for each hotel one time series is generated.

# Train-Test split
Step-3: Data is divided into training (last 3 years) and validation (last 3 months) sets.

# Modeling
## SARIMA
Step-4: Stationarity of time series is tested using Dickey-fuller test, time series plot, ACF-PACF plots for few important hotels

Step-5: Time series SARIMA is fitted with selected list of (p,q,d),(P,Q,D) parameters and best model with least AIC is selected.

## Prophet
Step-6: Facebook's Prophet is fitted with multiseasonality parameter and holiday parameter set to True.

## LSTM & RNN
Step-7: Next, to implement deep learning models LSTM and RNN, additional features such as year of Staydate, week_no, weekday, holiday, long_weekend, last 30 lags are calculated. 

Step-8: A sequential deep architecture with 5 LSTM layers (50,25,25,15,10 neurons) and 2 dense layers(5,1 neurons), 1500 epochs and batchsize 64 is fitted. Another model with a sequential LSTM layer(50 neurons) and 5 dense layers(25,25,10,5,1 neurons) with same other hyper parameters is also fitted

# Evaluation
Step-9: MAPE value is calculated for the 4 fitted models on validation dataset and best model with least average MAPE for all the hotels in each category is chosen and used for predicting future bookings.
