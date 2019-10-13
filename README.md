Mandy's question: How has the househoulds energy consumption changed over time? 
```{r}
data1 <- read_csv(file= "household_power_consumption.txt")
macpath <- "~/Desktop/household_power_consumption.txt"
```
```{r}
data1 <- read_delim(file=macpath, delim=';',na=c('?'),
                    col_types=cols(
                      Date = col_date(format="%d/%m/%Y"),
                      Time = col_time(format="%H:%M:%S"),
                      Global_active_power = col_double(),
                      Global_reactive_power = col_double(),
                      Voltage = col_double(),
                      Global_intensity = col_double(),
                      Sub_metering_1 = col_double(),
                      Sub_metering_2 = col_double(),
                      Sub_metering_3 = col_double()
                    ))
```
```{r}
data1 <- data1 %>% mutate(year=substr(Date,1,4), month=substr(Date, 6,7), day=substr(Date, 9,10))
data1 <- data1 %>% mutate(hour=substr(Time,1,2), minute=substr(Time, 4,5), second=substr(Time, 7,8))
data1 <- data1 %>% mutate( day=as.integer(day),
                  month=as.integer(month),
                  year=as.integer(year),
                  hour=as.integer(hour),
                  minute=as.integer(minute),
                  second=as.integer(second))
```
```{r}
first.data <- data1 %>% filter(year == 2006)
```
```{r}
last.data <- data1 %>% filter(year == 2010)
```
```{r}
ggplot(first.data)+
  geom_point(mapping = aes(x= Voltage, y= minute))
```
```{r}
ggplot(last.data)+
  geom_point(mapping=aes(x= Voltage, y=minute))
```
Mandy's Analysis: Comparing the first year (2006) to the last year (2010), the amount of energy used has increased heavily. By looking at the graph from 2006 and comparing it to the graph from 2010, we see a more filled in plot for 2010, proving that their energy consumption has gone way up. There are many theories as to why that might be. There could be an increase in residents in the house. There could be an increase in the amount of appliances, particularly in the kitchen. I think the most logical assumption is that residents in the house were staying home more in 2010 than in 2006, since the 2010 graph shows more 
concentration of voltage in the center of the graph, which would be the middle of the day.
