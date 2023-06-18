---
title: "Homerwork 1"
author: "Colby Richardson"
date: 2023-05-14
format: 
  docx: default
  html:
    toc: true
    toc_float: true
    code-fold: true
editor: visual
---




# Data Manipulation

## Problem 1: Use logical operators to find flights that:

```         
-   Had an arrival delay of two or more hours (\> 120 minutes)
-   Flew to Houston (IAH or HOU)
-   Were operated by United (`UA`), American (`AA`), or Delta (`DL`)
-   Departed in summer (July, August, and September)
-   Arrived more than two hours late, but didn't leave late
-   Were delayed by at least an hour, but made up over 30 minutes in flight
```



```r
# Had an arrival delay of two or more hours (> 120 minutes)
flights %>% 
  filter(arr_delay>=120)
```

```
## # A tibble: 10,200 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     1     1      811            630       101     1047            830
##  2  2013     1     1      848           1835       853     1001           1950
##  3  2013     1     1      957            733       144     1056            853
##  4  2013     1     1     1114            900       134     1447           1222
##  5  2013     1     1     1505           1310       115     1638           1431
##  6  2013     1     1     1525           1340       105     1831           1626
##  7  2013     1     1     1549           1445        64     1912           1656
##  8  2013     1     1     1558           1359       119     1718           1515
##  9  2013     1     1     1732           1630        62     2028           1825
## 10  2013     1     1     1803           1620       103     2008           1750
## # ℹ 10,190 more rows
## # ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>, time_hour <dttm>
```

```r
# Flew to Houston (IAH or HOU)
flights %>% 
  filter(dest %in% c("IAH","HOU"))
```

```
## # A tibble: 9,313 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     1     1      517            515         2      830            819
##  2  2013     1     1      533            529         4      850            830
##  3  2013     1     1      623            627        -4      933            932
##  4  2013     1     1      728            732        -4     1041           1038
##  5  2013     1     1      739            739         0     1104           1038
##  6  2013     1     1      908            908         0     1228           1219
##  7  2013     1     1     1028           1026         2     1350           1339
##  8  2013     1     1     1044           1045        -1     1352           1351
##  9  2013     1     1     1114            900       134     1447           1222
## 10  2013     1     1     1205           1200         5     1503           1505
## # ℹ 9,303 more rows
## # ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>, time_hour <dttm>
```

```r
# Were operated by United (`UA`), American (`AA`), or Delta (`DL`)
  flights %>% 
  group_by(carrier %in% c("UA","AA","DL"))
```

```
## # A tibble: 336,776 × 20
## # Groups:   carrier %in% c("UA", "AA", "DL") [2]
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     1     1      517            515         2      830            819
##  2  2013     1     1      533            529         4      850            830
##  3  2013     1     1      542            540         2      923            850
##  4  2013     1     1      544            545        -1     1004           1022
##  5  2013     1     1      554            600        -6      812            837
##  6  2013     1     1      554            558        -4      740            728
##  7  2013     1     1      555            600        -5      913            854
##  8  2013     1     1      557            600        -3      709            723
##  9  2013     1     1      557            600        -3      838            846
## 10  2013     1     1      558            600        -2      753            745
## # ℹ 336,766 more rows
## # ℹ 12 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>, time_hour <dttm>,
## #   `carrier %in% c("UA", "AA", "DL")` <lgl>
```

```r
# Departed in summer (July, August, and September)
  flights %>% 
  filter(month %in% c(7,8,9))
```

```
## # A tibble: 86,326 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     7     1        1           2029       212      236           2359
##  2  2013     7     1        2           2359         3      344            344
##  3  2013     7     1       29           2245       104      151              1
##  4  2013     7     1       43           2130       193      322             14
##  5  2013     7     1       44           2150       174      300            100
##  6  2013     7     1       46           2051       235      304           2358
##  7  2013     7     1       48           2001       287      308           2305
##  8  2013     7     1       58           2155       183      335             43
##  9  2013     7     1      100           2146       194      327             30
## 10  2013     7     1      100           2245       135      337            135
## # ℹ 86,316 more rows
## # ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>, time_hour <dttm>
```

```r
# Arrived more than two hours late, but didn't leave late
flights %>% 
  filter(arr_delay>120) %>% 
filter(dep_delay<0)
```

```
## # A tibble: 26 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     1    27     1419           1420        -1     1754           1550
##  2  2013    10     7     1357           1359        -2     1858           1654
##  3  2013    10    16      657            700        -3     1258           1056
##  4  2013    11     1      658            700        -2     1329           1015
##  5  2013     3    18     1844           1847        -3       39           2219
##  6  2013     4    17     1635           1640        -5     2049           1845
##  7  2013     4    18      558            600        -2     1149            850
##  8  2013     4    18      655            700        -5     1213            950
##  9  2013     5    22     1827           1830        -3     2217           2010
## 10  2013     6     5     1604           1615       -11     2041           1840
## # ℹ 16 more rows
## # ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>, time_hour <dttm>
```

```r
# Were delayed by at least an hour, but made up over 30 minutes in flight
flights %>% 
  filter(dep_delay>=60) %>%
  filter(dep_delay-arr_delay> 30)
```

```
## # A tibble: 1,844 × 19
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     1     1     2205           1720       285       46           2040
##  2  2013     1     1     2326           2130       116      131             18
##  3  2013     1     3     1503           1221       162     1803           1555
##  4  2013     1     3     1839           1700        99     2056           1950
##  5  2013     1     3     1850           1745        65     2148           2120
##  6  2013     1     3     1941           1759       102     2246           2139
##  7  2013     1     3     1950           1845        65     2228           2227
##  8  2013     1     3     2015           1915        60     2135           2111
##  9  2013     1     3     2257           2000       177       45           2224
## 10  2013     1     4     1917           1700       137     2135           1950
## # ℹ 1,834 more rows
## # ℹ 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
## #   hour <dbl>, minute <dbl>, time_hour <dttm>
```


## Problem 2: What months had the highest and lowest proportion of cancelled flights? Interpret any seasonal patterns. To determine if a flight was cancelled use the following code

<!-- -->

```         
flights %>% 
  filter(is.na(dep_time)) 
```



```r
cancelled_flights <- flights %>%
  filter(is.na(dep_time)) %>% 
  group_by(month) %>%
  summarise(total_cancelled = n())

take_offs <- flights %>% 
  group_by(month) %>%
  summarise(total_flights=n())

take_offs %>% 
  left_join(cancelled_flights, by="month") %>% 
mutate(proportion = (total_cancelled/total_flights)*100) %>% 
  arrange(desc(proportion))
```

```
## # A tibble: 12 × 4
##    month total_flights total_cancelled proportion
##    <int>         <int>           <int>      <dbl>
##  1     2         24951            1261      5.05 
##  2    12         28135            1025      3.64 
##  3     6         28243            1009      3.57 
##  4     7         29425             940      3.19 
##  5     3         28834             861      2.99 
##  6     4         28330             668      2.36 
##  7     5         28796             563      1.96 
##  8     1         27004             521      1.93 
##  9     8         29327             486      1.66 
## 10     9         27574             452      1.64 
## 11    11         27268             233      0.854
## 12    10         28889             236      0.817
```

```r
#February had the highest proportion of cancelled flights, and October had the lowest.
```


## Problem 3: What plane (specified by the `tailnum` variable) traveled the most times from New York City airports in 2013? Please `left_join()` the resulting table with the table `planes` (also included in the `nycflights13` package).

For the plane with the greatest number of flights and that had more than 50 seats, please create a table where it flew to during 2013.



```r
flights %>% 
  filter(!is.na(dep_time)) %>%
  left_join(planes, by = "tailnum") %>% 
  group_by(tailnum) %>% 
  summarise(count_nyc_takeoff = n()) %>% 
  arrange(desc(count_nyc_takeoff))
```

```
## # A tibble: 4,037 × 2
##    tailnum count_nyc_takeoff
##    <chr>               <int>
##  1 N725MQ                546
##  2 N722MQ                487
##  3 N723MQ                480
##  4 N711MQ                467
##  5 N713MQ                455
##  6 N258JB                422
##  7 N353JB                403
##  8 N298JB                402
##  9 N351JB                392
## 10 N328AA                389
## # ℹ 4,027 more rows
```

```r
#Plane N725MQ flew the most out of NYC in 2013.

N725MQ <- flights %>%
  filter(tailnum=="N725MQ") %>% 
   select(origin,dest,time_hour)

#Print the table of N725MQ's destinations from NYC.

print(N725MQ)
```

```
## # A tibble: 575 × 3
##    origin dest  time_hour          
##    <chr>  <chr> <dttm>             
##  1 LGA    RDU   2013-01-01 08:00:00
##  2 LGA    DTW   2013-01-01 13:00:00
##  3 LGA    CRW   2013-01-01 18:00:00
##  4 LGA    RDU   2013-01-02 12:00:00
##  5 LGA    BNA   2013-01-02 18:00:00
##  6 LGA    CLE   2013-01-03 11:00:00
##  7 LGA    DTW   2013-01-03 16:00:00
##  8 LGA    DTW   2013-01-04 06:00:00
##  9 LGA    CMH   2013-01-04 11:00:00
## 10 LGA    RDU   2013-01-04 16:00:00
## # ℹ 565 more rows
```


## Problem 4: The `nycflights13` package includes a table (`weather`) that describes the weather during 2013. Use that table to answer the following questions:

```         
-   What is the distribution of temperature (`temp`) in July 2013? Identify any important outliers in terms of the `wind_speed` variable.
-   What is the relationship between `dewp` and `humid`?
-   What is the relationship between `precip` and `visib`?
```



```r
#distribution of temperature in July 2013
julyweather <- weather %>% 
  filter(month == 7)

#outliers in wind_speed
ggplot(julyweather, aes(x=wind_speed, y=temp)) + geom_point()
```

```
## Warning: Removed 2 rows containing missing values (`geom_point()`).
```

<img src="/blogs/homework1_files/figure-html/unnamed-chunk-5-1.png" width="672" />

```r
#temperature range in July
julyweather %>% 
  arrange(temp) %>% 
  summarise(max(temp)-min(temp))
```

```
## # A tibble: 1 × 1
##   `max(temp) - min(temp)`
##                     <dbl>
## 1                      36
```

```r
#Range was 36 degrees Fahrenheit.

#relationship between humidity and dew
ggplot(weather, aes(x =humid, y =dewp)) + 
  geom_point() +
  geom_smooth(method=lm, se=FALSE)
```

```
## `geom_smooth()` using formula = 'y ~ x'
```

```
## Warning: Removed 1 rows containing non-finite values (`stat_smooth()`).
```

```
## Warning: Removed 1 rows containing missing values (`geom_point()`).
```

<img src="/blogs/homework1_files/figure-html/unnamed-chunk-5-2.png" width="672" />

```r
#relationship between visibility and precipitation
ggplot(weather, aes(x =visib, y=precip)) +
  geom_point() +
  geom_smooth(method=lm, se=FALSE)
```

```
## `geom_smooth()` using formula = 'y ~ x'
```

<img src="/blogs/homework1_files/figure-html/unnamed-chunk-5-3.png" width="672" />


## Problem 5: Use the `flights` and `planes` tables to answer the following questions:

```         
-   How many planes have a missing date of manufacture?
-   What are the five most common manufacturers?
-   Has the distribution of manufacturer changed over time as reflected by the airplanes flying from NYC in 2013? (Hint: you may need to use case_when() to recode the manufacturer name and collapse rare vendors into a category called Other.)
```



```r
#No. of planes w/o manufacturing dates.
planes %>%
  count(is.na(year)) 
```

```
## # A tibble: 2 × 2
##   `is.na(year)`     n
##   <lgl>         <int>
## 1 FALSE          3252
## 2 TRUE             70
```

```r
# 70 planes do not have a manufacturing date

#Summarising plane manufacturers.
planes_manufacturers <-planes %>%
add_count(manufacturer) %>% 
  group_by(manufacturer) %>%
  summarise(models = mean(n))

#Identifying top manufacturers.
top_manu <-planes_manufacturers %>% 
  arrange(desc(models)) %>%
  top_n(models,n=5)

print(planes_manufacturers)
```

```
## # A tibble: 35 × 2
##    manufacturer           models
##    <chr>                   <dbl>
##  1 AGUSTA SPA                  1
##  2 AIRBUS                    336
##  3 AIRBUS INDUSTRIE          400
##  4 AMERICAN AIRCRAFT INC       2
##  5 AVIAT AIRCRAFT INC          1
##  6 AVIONS MARCEL DASSAULT      1
##  7 BARKER JACK L               1
##  8 BEECH                       2
##  9 BELL                        2
## 10 BOEING                   1630
## # ℹ 25 more rows
```

```r
print(top_manu)
```

```
## # A tibble: 5 × 2
##   manufacturer     models
##   <chr>             <dbl>
## 1 BOEING             1630
## 2 AIRBUS INDUSTRIE    400
## 3 BOMBARDIER INC      368
## 4 AIRBUS              336
## 5 EMBRAER             299
```

```r
#The top manufacturers were Boeing, Airbus Industries, Bombardier, Airbus, and Embraer. 
```


## Problem 6: Use the `flights` and `planes` tables to answer the following questions:

```         
-   What is the oldest plane (specified by the tailnum variable) that flew from New York City airports in 2013?
-   How many airplanes that flew from New York City are included in the planes table?
```



```r
#Filtering out cancelled flights and isolating tail number.
planes_nyc_2013 <- flights %>% 
  filter(!is.na(dep_time)) %>%
  select(tailnum)

#filtering planes list for tail numbers that flew out of NYC in 2013.
oldest_planes_nyc_2013 <- planes %>% 
  filter(tailnum %in% planes_nyc_2013 & !is.na(year)) %>% 
  select(tailnum, manufacturer, year) %>% 
  arrange(year)

print(oldest_planes_nyc_2013) 
```

```
## # A tibble: 0 × 3
## # ℹ 3 variables: tailnum <chr>, manufacturer <chr>, year <int>
```

```r
# The oldest plane that flew out of NYC in 2013 was made in 1956 (Tail No. N381AA)

#Identifying number of planes from table that flew out of NYC 2013.
number_planes_nyc_2013 <- planes %>% 
  filter(tailnum %in% planes_nyc_2013 & !is.na(year)) %>% 
  select(tailnum, manufacturer, year) %>%
  count(year) %>% 
  mutate(total = sum(n)) %>%
  select(total)

print(number_planes_nyc_2013)
```

```
## # A tibble: 0 × 1
## # ℹ 1 variable: total <int>
```

```r
#2819 tail numbers that flew out of NYC airports in 2013 are included in the planes table.
```


## Problem 7: Use the `nycflights13` to answer the following questions:

```         
-   What is the median arrival delay on a month-by-month basis in each airport?
-   For each airline, plot the median arrival delay for each month and origin airport.
```



```r
#median arrival delay by month
med_arr_delay_mon <- flights %>% 
  filter(!is.na(dep_time)) %>% 
  group_by(dest, month) %>% 
  summarise(med_arr_delay = median(arr_delay, na.rm=TRUE))
```

```
## `summarise()` has grouped output by 'dest'. You can override using the
## `.groups` argument.
```

```r
print(med_arr_delay_mon)
```

```
## # A tibble: 1,112 × 3
## # Groups:   dest [104]
##    dest  month med_arr_delay
##    <chr> <int>         <dbl>
##  1 ABQ       4          14  
##  2 ABQ       5         -19  
##  3 ABQ       6          -2.5
##  4 ABQ       7          -6  
##  5 ABQ       8         -14  
##  6 ABQ       9         -16  
##  7 ABQ      10         -10  
##  8 ABQ      11          -6  
##  9 ABQ      12          27  
## 10 ACK       5          -8  
## # ℹ 1,102 more rows
```

```r
#median arrival delay by carrier
med_arr_delay_carrier <- flights %>% 
  filter(!is.na(dep_time) & year == 2013) %>% 
  group_by(carrier, month) %>%
  summarise(med_arr_delay = median(arr_delay, na.rm=TRUE)) 
```

```
## `summarise()` has grouped output by 'carrier'. You can override using the
## `.groups` argument.
```

```r
ggplot(med_arr_delay_carrier, 
                   aes(x = month, y = med_arr_delay)) +
  geom_bar(stat = "identity") +
  facet_wrap(. ~ carrier) +
  scale_x_continuous(breaks = seq(1,12, by = 1))+
  labs(title = "Median Arr Delay", x = "Month", y = "Mins")
```

<img src="/blogs/homework1_files/figure-html/unnamed-chunk-8-1.png" width="672" />

```r
#median arrival delay by airport of origin
med_arr_delay_origin <- flights %>% 
  filter(!is.na(dep_time)) %>% 
  group_by(carrier, origin) %>%
  summarise(med_arr_delay = median(arr_delay, na.rm=TRUE)) 
```

```
## `summarise()` has grouped output by 'carrier'. You can override using the
## `.groups` argument.
```

```r
ggplot(med_arr_delay_origin, 
                   aes(x = origin, y = med_arr_delay)) +
  geom_bar(stat = "identity") +
  facet_wrap(. ~ carrier) +
  labs(title = "Median Arr Delay by Carrier", x = "Origin", y = "Mins")+
  labs(title = "Median Arr Delay by Carrier", x = "Origin", y = "Mins")
```

<img src="/blogs/homework1_files/figure-html/unnamed-chunk-8-2.png" width="672" />


## Problem 8: Let's take a closer look at what carriers service the route to San Francisco International (SFO). Join the `flights` and `airlines` tables and count which airlines flew the most to SFO. Produce a new dataframe, `fly_into_sfo` that contains three variables: the `name` of the airline, e.g., `United Air Lines Inc.` not `UA`, the count (number) of times it flew to SFO, and the `percent` of the trips that that particular airline flew to SFO.



```r
#total flights out of NYC 2013 by carrier
flights_airlines <- flights %>%
  left_join(airlines, by = "carrier") %>%
  group_by(name) %>%
  summarise(total_flights = n())

#flights to SFO by carrier
fly_into_sfo <- flights %>%
  left_join(airlines, by = "carrier") %>%
  filter(dest == "SFO") %>%
  group_by(name) %>%
  summarise(count = n()) %>% 
  left_join(flights_airlines, by = "name") %>% 
  mutate(percent = count/total_flights) %>% 
  select(name, count, percent) %>% 
  arrange(desc(percent))

print(fly_into_sfo)
```

```
## # A tibble: 5 × 3
##   name                   count percent
##   <chr>                  <int>   <dbl>
## 1 Virgin America          2197  0.426 
## 2 United Air Lines Inc.   6819  0.116 
## 3 American Airlines Inc.  1422  0.0434
## 4 Delta Air Lines Inc.    1858  0.0386
## 5 JetBlue Airways         1035  0.0189
```


And here is some bonus ggplot code to plot your dataframe



```r
fly_into_sfo %>% 
  
  # sort 'name' of airline by the numbers it times to flew to SFO
  mutate(name = fct_reorder(name, count)) %>% 
  
  ggplot() +
  
  aes(x = count, 
      y = name) +
  
  # a simple bar/column plot
  geom_col() +
  
  # add labels, so each bar shows the % of total flights 
  geom_text(aes(label = percent),
             hjust = 1, 
             colour = "white", 
             size = 5)+
  
  # add labels to help our audience  
  labs(title="Which airline dominates the NYC to SFO route?", 
       subtitle = "as % of total flights in 2013",
       x= "Number of flights",
       y= NULL) +
  
  theme_minimal() + 
  
  # change the theme-- i just googled those , but you can use the ggThemeAssist add-in
  # https://cran.r-project.org/web/packages/ggThemeAssist/index.html
  
  theme(#
    # so title is left-aligned
    plot.title.position = "plot",
    
    # text in axes appears larger        
    axis.text = element_text(size=12),
    
    # title text is bigger
    plot.title = element_text(size=18)
      ) +

  # add one final layer of NULL, so if you comment out any lines
  # you never end up with a hanging `+` that awaits another ggplot layer
  NULL
```

<img src="/blogs/homework1_files/figure-html/ggplot-flights-toSFO-1.png" width="672" />


## Problem 9: Let's take a look at cancellations of flights to SFO. We create a new dataframe `cancellations` as follows



```r
cancellations <- flights %>% 
  
  # just filter for destination == 'SFO'
  filter(dest == 'SFO') %>% 
  
  # a cancelled flight is one with no `dep_time` 
  filter(is.na(dep_time))

#To create the following plot: 

#Filter the data for flights originating from EWR and JFK. 

#Group the filtered data by month, carrier, airport of orgin.

#Summarize the number of cancelled flights. 

#Plot the data w/ geom_col. Add labels.
```


I want you to think how we would organise our data manipulation to create the following plot. No need to write the code, just explain in words how you would go about it.

![](images/sfo-cancellations.png)

## Problem 10: On your own -- Hollywood Age Gap

|     |
|:----|
|     |



```r
age_gaps <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2023/2023-02-14/age_gaps.csv')
```

```
## Rows: 1155 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (6): movie_name, director, actor_1_name, actor_2_name, character_1_gend...
## dbl  (5): release_year, age_difference, couple_number, actor_1_age, actor_2_age
## date (2): actor_1_birthdate, actor_2_birthdate
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
#typical age difference
age_gaps %>%
 ggplot()+
 aes(x=age_difference)+
 geom_histogram()
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

<img src="/blogs/homework1_files/figure-html/unnamed-chunk-12-1.png" width="672" />

```r
age_gaps %>% 
summarize(median_agedifference = median(age_difference))
```

```
## # A tibble: 1 × 1
##   median_agedifference
##                  <dbl>
## 1                    8
```

```r
#Checking the Half+7 Rule
half_7_rule <- age_gaps %>% 
mutate(minage = ((actor_1_age / 2)+7),
 maxage = ((actor_1_age - 7)*2),
 acceptable = ifelse(actor_2_age > minage, TRUE, FALSE))

#most number of love interests
love_interests <- age_gaps %>% 
  select(movie_name,couple_number) %>% 
arrange(desc(couple_number))

#actors/actresses with most number of love interests
most_appearances1 <- age_gaps %>% 
  count(actor_1_name) %>% 
  arrange(desc(n))

print(most_appearances1)
```

```
## # A tibble: 567 × 2
##    actor_1_name          n
##    <chr>             <int>
##  1 Keanu Reeves         24
##  2 Adam Sandler         18
##  3 Roger Moore          17
##  4 Sean Connery         15
##  5 Harrison Ford        13
##  6 Johnny Depp          12
##  7 Pierce Brosnan       12
##  8 Leonardo DiCaprio    11
##  9 Richard Gere         10
## 10 Brad Pitt             9
## # ℹ 557 more rows
```

```r
most_appearances2 <- age_gaps %>% 
  count(actor_2_name) %>% 
  arrange(desc(n))

print(most_appearances2)
```

```
## # A tibble: 647 × 2
##    actor_2_name           n
##    <chr>              <int>
##  1 Keira Knightley       13
##  2 Scarlett Johansson    13
##  3 Emma Stone            11
##  4 Renee Zellweger       11
##  5 Drew Barrymore         9
##  6 Jennifer Lawrence      9
##  7 Julia Roberts          9
##  8 Amanda Seyfried        8
##  9 Audrey Hepburn         8
## 10 Jennifer Aniston       8
## # ℹ 637 more rows
```

```r
#change over time: median age difference (1935 - 2022)
age_gaps %>%
 group_by(release_year) %>%
 summarize(median_agedifference = median(age_difference)) %>%
 ggplot()+
 aes(x = release_year, y = median_agedifference)+
 geom_point() + geom_smooth(method=lm, se=FALSE)
```

```
## `geom_smooth()` using formula = 'y ~ x'
```

<img src="/blogs/homework1_files/figure-html/unnamed-chunk-12-2.png" width="672" />

```r
#the median age difference has decreased since 1935.

#Frequency of appearances of same-gender couples
same_gender <- age_gaps %>%
 mutate(acceptable = ifelse(character_1_gender == character_2_gender, TRUE, FALSE)) %>% 
  count(acceptable)

print(same_gender)
```

```
## # A tibble: 2 × 2
##   acceptable     n
##   <lgl>      <int>
## 1 FALSE       1132
## 2 TRUE          23
```

```r
#The dataset lists only 23 occurences of same-gendered couples.
```


# Details

-   Who did you collaborate with: Saagar Hemrajani, Brent Lewis, Jenna Thomas
-   Approximately how much time did you spend on this problem set: 3 hours
-   What, if anything, gave you the most trouble: making the plots look decent

