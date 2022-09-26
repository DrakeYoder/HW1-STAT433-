HW1
================
2022-09-21

``` r
#Q1)
na_rows = flights %>% filter(is.na(dep_time))
na_rows
```

    ## # A tibble: 8,255 × 19
    ##     year month   day dep_time sched_de…¹ dep_d…² arr_t…³ sched…⁴ arr_d…⁵ carrier
    ##    <int> <int> <int>    <int>      <int>   <dbl>   <int>   <int>   <dbl> <chr>  
    ##  1  2013     1     1       NA       1630      NA      NA    1815      NA EV     
    ##  2  2013     1     1       NA       1935      NA      NA    2240      NA AA     
    ##  3  2013     1     1       NA       1500      NA      NA    1825      NA AA     
    ##  4  2013     1     1       NA        600      NA      NA     901      NA B6     
    ##  5  2013     1     2       NA       1540      NA      NA    1747      NA EV     
    ##  6  2013     1     2       NA       1620      NA      NA    1746      NA EV     
    ##  7  2013     1     2       NA       1355      NA      NA    1459      NA EV     
    ##  8  2013     1     2       NA       1420      NA      NA    1644      NA EV     
    ##  9  2013     1     2       NA       1321      NA      NA    1536      NA EV     
    ## 10  2013     1     2       NA       1545      NA      NA    1910      NA AA     
    ## # … with 8,245 more rows, 9 more variables: flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>, and abbreviated variable names
    ## #   ¹​sched_dep_time, ²​dep_delay, ³​arr_time, ⁴​sched_arr_time, ⁵​arr_delay

``` r
dim(na_rows)
```

    ## [1] 8255   19

-8,255 -dep_delay, arr_time, arr_delay, air_time, -The flights that
never took off

``` r
#Q2)
flight_alt_time = flights %>% mutate(dep_time=((floor(dep_time/100))*60)+(dep_time%%100), sched_dep_time=((floor(sched_dep_time/100))*60)+(sched_dep_time%%100))
flight_alt_time %>% select(dep_time, sched_dep_time)
```

    ## # A tibble: 336,776 × 2
    ##    dep_time sched_dep_time
    ##       <dbl>          <dbl>
    ##  1      317            315
    ##  2      333            329
    ##  3      342            340
    ##  4      344            345
    ##  5      354            360
    ##  6      354            358
    ##  7      355            360
    ##  8      357            360
    ##  9      357            360
    ## 10      358            360
    ## # … with 336,766 more rows

``` r
#Q3)
flight_alt_time %>% select(year, month, day, dep_time, sched_dep_time, dep_delay) %>% group_by(year, month, day) %>% mutate(na_num = sum(is.na(dep_time)), avg_dep_delay=mean(dep_delay, na.rm=T), n = n()) %>% ggplot(aes(x=(na_num/n) ,y=avg_dep_delay)) + geom_point() + xlab("Proportion of Cancelled FLights") + ylab("Average Departure Delay") + ggtitle("Proportion of Cancelled Flights vs. Average Departure Delay")
```

![](README_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->
