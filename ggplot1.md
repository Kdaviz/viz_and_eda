ggplot1
================
Keyanna Davis
9/26/2019

creat the weather data
----------------------

``` r
weather_df = 
  rnoaa::meteo_pull_monitors(c("USW00094728", "USC00519397", "USS0023B17S"),
                      var = c("PRCP", "TMIN", "TMAX"), 
                      date_min = "2017-01-01",
                      date_max = "2017-12-31") %>%
  mutate(
    name = recode_factor (id, USW00094728 = "CentralPark_NY", 
                      USC00519397 = "Waikiki_HA",
                      USS0023B17S = "Waterhole_WA"),
    tmin = tmin / 10,
    tmax = tmax / 10) %>%
  select(name, id, everything())
```

    ## Registered S3 method overwritten by 'crul':
    ##   method                 from
    ##   as.character.form_file httr

    ## Registered S3 method overwritten by 'hoardr':
    ##   method           from
    ##   print.cache_info httr

    ## file path:          /Users/keyannadavis/Library/Caches/rnoaa/ghcnd/USW00094728.dly

    ## file last updated:  2019-09-26 10:31:53

    ## file min/max dates: 1869-01-01 / 2019-09-30

    ## file path:          /Users/keyannadavis/Library/Caches/rnoaa/ghcnd/USC00519397.dly

    ## file last updated:  2019-09-26 10:32:07

    ## file min/max dates: 1965-01-01 / 2019-09-30

    ## file path:          /Users/keyannadavis/Library/Caches/rnoaa/ghcnd/USS0023B17S.dly

    ## file last updated:  2019-09-26 10:32:11

    ## file min/max dates: 1999-09-01 / 2019-09-30

``` r
scatter_plot =
  ggplot(weather_df, aes(x= tmin, y= tmax)) + geom_point()
```

adding color . . . .

``` r
scatter_plot =
  ggplot(weather_df, aes(x= tmin, y= tmax)) + geom_point(aes(color=name), alpha = .4) +
  geom_smooth(se = FALSE) 
```

``` r
scatter_plot3 =
  ggplot(weather_df, aes(x= tmin, y= tmax)) + geom_point(aes(color=name), alpha = .4) +
  geom_smooth(se = FALSE) +
  facet_grid(~name)
```

``` r
scatter_plot2 =
  ggplot(weather_df, aes(x= tmin, y= tmax,color=name)) + geom_point() 
```

``` r
weather_df %>% 
  ggplot(aes(x= date, y= tmax, color =name)) +
  geom_point(aes(size = prcp), alpha = .5) +
  geom_smooth(size = 2, se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

    ## Warning: Removed 3 rows containing non-finite values (stat_smooth).

    ## Warning: Removed 3 rows containing missing values (geom_point).

![](ggplot1_files/figure-markdown_github/unnamed-chunk-5-1.png)
