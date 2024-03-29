# Time_Series_Regression
Mean temperature for countries by year 1901-2022 data from Kaggle 
https://www.kaggle.com/datasets/palinatx/mean-temperature-for-countries-by-year-2014-2022
library(forecast)
library(stats)
install.packages("tidyverse")
library(tidyverse)
install.packages("ggplot2")
library(ggplot2)
View(data)
str(data)
um(is.na(data))
sum(is.null(data))
AnnualMean<- data$ AnnualMean # str(UnitedStates$AnnualMean)#null
UnitedStates<-data[123:244,]
ten<-c(8.60, 8.40, 7.97, 8.10,8.41,8.45,8.33,8.63,8.09,8.68,8.61,8.08,8.5,8.83,8.62,8.06,7.63,8.44,8.41,8.01,9.45,8.63,8.65,7.9,8.9,9.03,8.59,8.74,8.35,8.62,9.46,8.41,8.97,9.74,8.65,8.89,8.67,9.38,9.25,8.96 , 9.22, 8.82, 8.89, 8.77, 8.58, 9.06, 8.74, 8.34, 8.79, 8.48, 8.26, 8.83, 9.41, 9.24, 8.40, 8.54,8.97, 8.86, 8.69, 8.54, 8.46, 8.75, 8.91, 8.31, 8.47, 8.29,8.70, 8.34, 8.59, 8.54, 8.31, 8.21, 8.76, 8.68, 8.26, 8.41,9.09, 8.58, 8.40,8.93, 9.53, 8.33, 8.73, 8.62, 8.40, 9.38,9.45, 9.07, 8.66, 9.37, 9.35,8.90, 8.72, 9.24, 9.25, 8.59,8.76, 9.81, 9.23,9.21,9.43, 9.45, 9.44, 9.39, 9.67, 9.82,9.64, 8.79, 8.94,9.35, 9.38,10.07, 9.09, 9.43, 10.22, 10.64,10.22, 9.89, 9.73, 10.02, 10.01, 9.73)
USA<-data.frame(cbind(UnitedStates$Year,ten))
USA<-data.frame(Year=USA$V1,meantepm=USA$ ten)
ggplot(USA, aes(x = USA$ meantepm, y = USA $Year)) +
  geom_line() +
  labs(title = "Time Series Plot of USA ",
       x = " Annual Mean",
       y = " Year ")
# Fit ARIMA model
arima_model <- auto.arima(USA$meantepm)

# Summary of the model
summary(arima_model)
# Plot ACF and PACF of residuals
acf_res <- acf(arima_model$residuals)
pacf_res <- pacf(arima_model$residuals)
plot(acf_res, main = "ACF of Residuals")
plot(pacf_res, main = "PACF of Residuals"
# Forecast future values
forecast_temperature <- forecast(arima_model, h = 12)  # Forecast for 12 month
# Plot forecast
plot(forecast_temperature, main = "Forecasted Temperature In a Year ")
# Plot forecast using ggplot2
autoplot(forecast_temperature) +
  labs(title = "Forecasted Temperature")
# Calculate accuracy measures
accuracy(forecast_temperature)
Box.test(forecast_temperature$residuals, lag = 20, type = 'Ljung-Box')



