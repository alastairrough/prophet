# open RGui or RStudio in local directory C:/Users/aroug/Source/Repos/prophet/examples/
# run BC Ferries data for specific sailing time and route
# prerequisites
install.packages("prophet")
install.packages("dplyr")
# run
library(prophet)
library(dplyr)
m <- prophet(df)
df <- read.csv('C:/Users/aroug/Source/Repos/prophet/examples/temp0620.csv') %>% mutate(y=log(y))
# view sample data
class(df$ds)
class(df$y)
head(df$y)
head(df$ds)
tail(df$y)
tail(df$ds)
# create forecast: to forecast loading transform to exp(y)
future <- make_future_dataframe(m, periods = 7)
tail(future)
forecast <- predict(m, future)
tail(forecast[c('ds', 'yhat', 'yhat_lower', 'yhat_upper')])
plot(m, forecast)
prophet_plot_components(m, forecast)
