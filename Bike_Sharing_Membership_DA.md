## Purpose Statement

To help design marketing strategies to convert casual bike riders into
annual members, the marketing analyst explored the company’s historical
bike trip data to answer:

-   How annual members and casual riders differ?;
-   Why would casual riders buy an annual membership?; and
-   How digital media could affect the company’s marketing tactics?

<!-- -->

    install.packages("tidyverse", repos = "http://cran.us.r-project.org")

    ## Installing package into 'C:/Users/danie/OneDrive/Documents/R/win-library/4.1'
    ## (as 'lib' is unspecified)

    ## package 'tidyverse' successfully unpacked and MD5 sums checked
    ## 
    ## The downloaded binary packages are in
    ##  C:\Users\danie\AppData\Local\Temp\Rtmp8WNqoF\downloaded_packages

    install.packages("plyr", repos = "http://cran.us.r-project.org")

    ## Installing package into 'C:/Users/danie/OneDrive/Documents/R/win-library/4.1'
    ## (as 'lib' is unspecified)

    ## package 'plyr' successfully unpacked and MD5 sums checked
    ## 
    ## The downloaded binary packages are in
    ##  C:\Users\danie\AppData\Local\Temp\Rtmp8WNqoF\downloaded_packages

    install.packages("dplyr", repos = "http://cran.us.r-project.org")

    ## Installing package into 'C:/Users/danie/OneDrive/Documents/R/win-library/4.1'
    ## (as 'lib' is unspecified)

    ## package 'dplyr' successfully unpacked and MD5 sums checked

    ## Warning: cannot remove prior installation of package 'dplyr'

    ## Warning in file.copy(savedcopy, lib, recursive = TRUE):
    ## problem copying C:\Users\danie\OneDrive\Documents\R\win-
    ## library\4.1\00LOCK\dplyr\libs\x64\dplyr.dll to C:
    ## \Users\danie\OneDrive\Documents\R\win-library\4.1\dplyr\libs\x64\dplyr.dll:
    ## Permission denied

    ## Warning: restored 'dplyr'

    ## 
    ## The downloaded binary packages are in
    ##  C:\Users\danie\AppData\Local\Temp\Rtmp8WNqoF\downloaded_packages

    install.packages("scales", repos = "http://cran.us.r-project.org")

    ## Installing package into 'C:/Users/danie/OneDrive/Documents/R/win-library/4.1'
    ## (as 'lib' is unspecified)

    ## package 'scales' successfully unpacked and MD5 sums checked
    ## 
    ## The downloaded binary packages are in
    ##  C:\Users\danie\AppData\Local\Temp\Rtmp8WNqoF\downloaded_packages

    library("tidyverse")

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.5     v purrr   0.3.4
    ## v tibble  3.1.4     v dplyr   1.0.7
    ## v tidyr   1.1.3     v stringr 1.4.0
    ## v readr   2.0.1     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

    library("plyr")

    ## ------------------------------------------------------------------------------

    ## You have loaded plyr after dplyr - this is likely to cause problems.
    ## If you need functions from both plyr and dplyr, please load plyr first, then dplyr:
    ## library(plyr); library(dplyr)

    ## ------------------------------------------------------------------------------

    ## 
    ## Attaching package: 'plyr'

    ## The following objects are masked from 'package:dplyr':
    ## 
    ##     arrange, count, desc, failwith, id, mutate, rename, summarise,
    ##     summarize

    ## The following object is masked from 'package:purrr':
    ## 
    ##     compact

    library("dplyr")
    library("scales")

    ## 
    ## Attaching package: 'scales'

    ## The following object is masked from 'package:purrr':
    ## 
    ##     discard

    ## The following object is masked from 'package:readr':
    ## 
    ##     col_factor

    library("zoo")

    ## 
    ## Attaching package: 'zoo'

    ## The following objects are masked from 'package:base':
    ## 
    ##     as.Date, as.Date.numeric

## Data Source

**Note**: The data has been made available by Motivate International
Inc. This is a public data that can be used to explore the customer
demographics of the company.

For this analysis, the marketing analyst used the company’s bike trip
data collected between April, 2020 and March, 2021. Each dataset is
compiled in *csv* extension and organized by per month. Hence, a total
of 12 csv files were obtained.

## Data Cleaning

Per review of the datasets, the analyst noted the data are unclean. The
analyst decided to clean the datasets using R to help arrive to accurate
datasets as possible.

The marketing analyst imported each dataset as individual dataframes.

    bike_ride_202004 <- read_csv(file = "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\202004-divvy-tripdata.csv")

    ## Rows: 84776 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    bike_ride_202005 <- read_csv(file = "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\202005-divvy-tripdata.csv")

    ## Rows: 200274 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    bike_ride_202006 <- read_csv(file = "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\202006-divvy-tripdata.csv")

    ## Rows: 343005 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    bike_ride_202007 <- read_csv(file = "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\202007-divvy-tripdata.csv")

    ## Rows: 551480 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    bike_ride_202008 <- read_csv(file = "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\202008-divvy-tripdata.csv")

    ## Rows: 622361 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    bike_ride_202009 <- read_csv(file = "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\202009-divvy-tripdata.csv")

    ## Rows: 532958 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    bike_ride_202010 <- read_csv(file = "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\202010-divvy-tripdata.csv")

    ## Rows: 388653 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    bike_ride_202011 <- read_csv(file = "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\202011-divvy-tripdata.csv")

    ## Rows: 259716 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    bike_ride_202012 <- read_csv(file = "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\202012-divvy-tripdata.csv")

    ## Rows: 131573 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
    ## dbl  (4): start_lat, start_lng, end_lat, end_lng
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    bike_ride_202101 <- read_csv(file = "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\202101-divvy-tripdata.csv")

    ## Rows: 96834 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
    ## dbl  (4): start_lat, start_lng, end_lat, end_lng
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    bike_ride_202102 <- read_csv(file = "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\202102-divvy-tripdata.csv")

    ## Rows: 49622 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
    ## dbl  (4): start_lat, start_lng, end_lat, end_lng
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    bike_ride_202103 <- read_csv(file = "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\202103-divvy-tripdata.csv")

    ## Rows: 228496 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (7): ride_id, rideable_type, start_station_name, start_station_id, end_...
    ## dbl  (4): start_lat, start_lng, end_lat, end_lng
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

The marketing analyst determined to change the columns data type from
*character* to *double* to help merge all the datasets into one. Per
warning messages from the console, the marketing analyst noted the
datasets contain NULL observations.

    bike_ride_202012$start_station_id <- as.double(bike_ride_202012$start_station_id)

    ## Warning: NAs introduced by coercion

    bike_ride_202012$end_station_id <- as.double(bike_ride_202012$end_station_id)

    ## Warning: NAs introduced by coercion

    bike_ride_202101$start_station_id <- as.double(bike_ride_202101$start_station_id)

    ## Warning: NAs introduced by coercion

    bike_ride_202101$end_station_id <- as.double(bike_ride_202101$end_station_id)

    ## Warning: NAs introduced by coercion

    bike_ride_202102$start_station_id <- as.double(bike_ride_202102$start_station_id)

    ## Warning: NAs introduced by coercion

    bike_ride_202102$end_station_id <- as.double(bike_ride_202102$end_station_id)

    ## Warning: NAs introduced by coercion

    bike_ride_202103$start_station_id <- as.double(bike_ride_202103$start_station_id)

    ## Warning: NAs introduced by coercion

    bike_ride_202103$end_station_id <- as.double(bike_ride_202103$end_station_id)

    ## Warning: NAs introduced by coercion

The analyst decided to export the datasets with the updated data types
to compile them with others.

    write.csv(bike_ride_202012, "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\Dataset\\updated_202012.csv", row.names = FALSE )
    write.csv(bike_ride_202101, "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\Dataset\\updated_202101.csv", row.names = FALSE )
    write.csv(bike_ride_202102, "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\Dataset\\updated_202102.csv", row.names = FALSE )
    write.csv(bike_ride_202103, "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\Dataset\\updated_202103.csv", row.names = FALSE )

The analyst combined all 12 month data into one dataframe (“bikerides”).

    bikerides <- list.files(path = "C:\\Users\\danie\\Documents\\Google Data Analytics Cert\\Dataset", pattern = "*.csv", full.names = TRUE) %>% 
        lapply(read_csv) %>%
        bind_rows

    ## Rows: 84776 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## Rows: 200274 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## Rows: 343005 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## Rows: 551480 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## Rows: 622361 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## Rows: 532958 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## Rows: 388653 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## Rows: 259716 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## Rows: 131573 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## Rows: 96834 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## Rows: 49622 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## Rows: 228496 Columns: 13

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr  (5): ride_id, rideable_type, start_station_name, end_station_name, memb...
    ## dbl  (6): start_station_id, end_station_id, start_lat, start_lng, end_lat, e...
    ## dttm (2): started_at, ended_at

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    glimpse(bikerides)

    ## Rows: 3,489,748
    ## Columns: 13
    ## $ ride_id            <chr> "A847FADBBC638E45", "5405B80E996FF60D", "5DD24A79A4~
    ## $ rideable_type      <chr> "docked_bike", "docked_bike", "docked_bike", "docke~
    ## $ started_at         <dttm> 2020-04-26 17:45:14, 2020-04-17 17:08:54, 2020-04-~
    ## $ ended_at           <dttm> 2020-04-26 18:12:03, 2020-04-17 17:17:03, 2020-04-~
    ## $ start_station_name <chr> "Eckhart Park", "Drake Ave & Fullerton Ave", "McClu~
    ## $ start_station_id   <dbl> 86, 503, 142, 216, 125, 173, 35, 434, 627, 377, 508~
    ## $ end_station_name   <chr> "Lincoln Ave & Diversey Pkwy", "Kosciuszko Park", "~
    ## $ end_station_id     <dbl> 152, 499, 255, 657, 323, 35, 635, 382, 359, 508, 37~
    ## $ start_lat          <dbl> 41.8964, 41.9244, 41.8945, 41.9030, 41.8902, 41.896~
    ## $ start_lng          <dbl> -87.6610, -87.7154, -87.6179, -87.6975, -87.6262, -~
    ## $ end_lat            <dbl> 41.9322, 41.9306, 41.8679, 41.8992, 41.9695, 41.892~
    ## $ end_lng            <dbl> -87.6586, -87.7238, -87.6230, -87.6722, -87.6547, -~
    ## $ member_casual      <chr> "member", "member", "member", "member", "casual", "~

To build an index of station IDs to find the missing
“start\_station\_id”, the analyst grouped and created a dataframe of the
distinct “start\_station\_id” and “start\_station\_name”; the analyst
noted that the station names and IDs are unique regardless of start or
end station qualifier.

    station_id <- bikerides %>% 
      filter(!is.na(start_station_id), !is.na(end_station_id)) %>%
      select(start_station_id, start_station_name) %>%
      group_by(start_station_id, start_station_name) %>%
      distinct(start_station_id, start_station_name, .keep_all = TRUE)

    station_ids = as.data.frame(station_id)

The marketing analyst matched the ID to names, using the dataframe
created above.

    bikerides$start_station_id <- station_ids[match(bikerides$start_station_name, station_ids$start_station_name), 1]
    bikerides$end_station_id <- station_ids[match(bikerides$end_station_name, station_ids$start_station_name), 1]

The analyst then checked to see if the updated dataframe has any NULL
observations.

    glimpse(bikerides %>% filter(is.na(start_station_name)))

    ## Rows: 122,175
    ## Columns: 13
    ## $ ride_id            <chr> "60742256DFFFCA29", "EBBD4FE9C8A95116", "976336C649~
    ## $ rideable_type      <chr> "electric_bike", "electric_bike", "electric_bike", ~
    ## $ started_at         <dttm> 2020-07-31 08:30:34, 2020-07-29 19:02:25, 2020-07-~
    ## $ ended_at           <dttm> 2020-07-31 08:57:54, 2020-07-29 19:22:40, 2020-07-~
    ## $ start_station_name <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,~
    ## $ start_station_id   <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,~
    ## $ end_station_name   <chr> "Racine Ave & 35th St", "Western Ave & Walton St", ~
    ## $ end_station_id     <dbl> 367, 374, 251, NA, NA, 621, 174, NA, 89, 495, NA, N~
    ## $ start_lat          <dbl> 41.90, 41.90, 41.94, 41.92, 41.91, 41.86, 41.87, 41~
    ## $ start_lng          <dbl> -87.69, -87.69, -87.65, -87.70, -87.68, -87.63, -87~
    ## $ end_lat            <dbl> 41.83070, 41.89840, 41.96784, 41.91000, 41.92000, 4~
    ## $ end_lng            <dbl> -87.65608, -87.68659, -87.64999, -87.68000, -87.700~
    ## $ member_casual      <chr> "member", "member", "member", "member", "member", "~

    glimpse(bikerides %>% filter(is.na(end_station_name)))

    ## Rows: 143,242
    ## Columns: 13
    ## $ ride_id            <chr> "5E2BD03BCA180FBA", "BD5813A6101E9BF4", "228691849C~
    ## $ rideable_type      <chr> "docked_bike", "docked_bike", "docked_bike", "docke~
    ## $ started_at         <dttm> 2020-04-07 11:53:08, 2020-04-20 12:24:48, 2020-04-~
    ## $ ended_at           <dttm> 2020-04-07 12:28:35, 2020-04-20 12:29:46, 2020-04-~
    ## $ start_station_name <chr> "Wells St & Concord Ln", "Racine Ave & Wrightwood A~
    ## $ start_station_id   <dbl> 289, 343, 15, 137, 157, 350, 53, 106, 113, 508, 579~
    ## $ end_station_name   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,~
    ## $ end_station_id     <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,~
    ## $ start_lat          <dbl> 41.9121, 41.9289, 41.8582, 41.8624, 41.9367, 41.896~
    ## $ start_lng          <dbl> -87.6347, -87.6590, -87.6565, -87.6511, -87.6368, -~
    ## $ end_lat            <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,~
    ## $ end_lng            <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,~
    ## $ member_casual      <chr> "member", "member", "member", "casual", "member", "~

The analyst exported the NULL observations into separate dataframes
(“bikerides\_start\_null” and “bikerides\_end\_null”) with a total of
*195,185* observations \[(start station NULL, 122,175) + (end station
NULL, 143242) - (NULL values on both start and end station, 71,232).

    bikerides_start_null <- bikerides %>% 
       filter(is.na(start_station_name)) 

    bikerides_end_null <- bikerides %>% 
       filter(is.na(end_station_name))

    bikerides_null <- bikerides %>% 
       filter(is.na(start_station_name), is.na(end_station_name))

    tibble(bikerides_start_null)

    ## # A tibble: 122,175 x 13
    ##    ride_id          rideable_type started_at          ended_at           
    ##    <chr>            <chr>         <dttm>              <dttm>             
    ##  1 60742256DFFFCA29 electric_bike 2020-07-31 08:30:34 2020-07-31 08:57:54
    ##  2 EBBD4FE9C8A95116 electric_bike 2020-07-29 19:02:25 2020-07-29 19:22:40
    ##  3 976336C6499A7189 electric_bike 2020-07-30 22:02:45 2020-07-30 22:17:54
    ##  4 EC549CDABDE45F98 electric_bike 2020-07-31 15:54:41 2020-07-31 16:00:35
    ##  5 70F53BFE303499AC electric_bike 2020-07-31 16:08:26 2020-07-31 16:15:29
    ##  6 11814668BAB6FCA3 electric_bike 2020-07-31 12:56:53 2020-07-31 13:13:27
    ##  7 D66AC7ACF66F8FF6 electric_bike 2020-07-30 08:32:14 2020-07-30 08:40:04
    ##  8 5196A992F09481DB electric_bike 2020-07-30 17:25:18 2020-07-30 17:25:35
    ##  9 2DB97E499E497D3D electric_bike 2020-07-30 17:28:20 2020-07-30 17:44:40
    ## 10 3C5018A592AB147C electric_bike 2020-07-31 18:40:31 2020-07-31 18:48:56
    ## # ... with 122,165 more rows, and 9 more variables: start_station_name <chr>,
    ## #   start_station_id <dbl>, end_station_name <chr>, end_station_id <dbl>,
    ## #   start_lat <dbl>, start_lng <dbl>, end_lat <dbl>, end_lng <dbl>,
    ## #   member_casual <chr>

    tibble(bikerides_end_null)

    ## # A tibble: 143,242 x 13
    ##    ride_id          rideable_type started_at          ended_at           
    ##    <chr>            <chr>         <dttm>              <dttm>             
    ##  1 5E2BD03BCA180FBA docked_bike   2020-04-07 11:53:08 2020-04-07 12:28:35
    ##  2 BD5813A6101E9BF4 docked_bike   2020-04-20 12:24:48 2020-04-20 12:29:46
    ##  3 228691849C2081EE docked_bike   2020-04-16 08:41:56 2020-04-16 11:33:48
    ##  4 ED7750BCEEE87174 docked_bike   2020-04-09 15:33:45 2020-04-09 16:34:54
    ##  5 1E00C457DCDA0835 docked_bike   2020-04-25 06:52:02 2020-04-25 07:17:54
    ##  6 0F7201752882C449 docked_bike   2020-04-30 20:47:40 2020-04-30 21:19:00
    ##  7 97C00C77F12AF5AE docked_bike   2020-04-10 11:54:44 2020-04-10 12:02:39
    ##  8 E0AFDC4D2358B027 docked_bike   2020-04-20 13:37:30 2020-04-20 14:27:48
    ##  9 8BAB90CEE039C959 docked_bike   2020-04-28 16:21:26 2020-04-28 17:03:01
    ## 10 8BC76B362DA665B7 docked_bike   2020-04-19 13:23:39 2020-04-19 13:58:52
    ## # ... with 143,232 more rows, and 9 more variables: start_station_name <chr>,
    ## #   start_station_id <dbl>, end_station_name <chr>, end_station_id <dbl>,
    ## #   start_lat <dbl>, start_lng <dbl>, end_lat <dbl>, end_lng <dbl>,
    ## #   member_casual <chr>

    tibble(bikerides_null)

    ## # A tibble: 71,232 x 13
    ##    ride_id          rideable_type started_at          ended_at           
    ##    <chr>            <chr>         <dttm>              <dttm>             
    ##  1 EC549CDABDE45F98 electric_bike 2020-07-31 15:54:41 2020-07-31 16:00:35
    ##  2 70F53BFE303499AC electric_bike 2020-07-31 16:08:26 2020-07-31 16:15:29
    ##  3 5196A992F09481DB electric_bike 2020-07-30 17:25:18 2020-07-30 17:25:35
    ##  4 836BE807C2FFC1DB electric_bike 2020-07-31 18:39:02 2020-07-31 18:39:13
    ##  5 D53BD878D7CF3DDA electric_bike 2020-07-30 17:17:45 2020-07-30 17:35:15
    ##  6 FA92AAEFE87BD7EA electric_bike 2020-07-15 10:20:31 2020-07-15 10:20:57
    ##  7 9D93190F92EC2DF7 electric_bike 2020-07-15 10:37:55 2020-07-15 10:41:08
    ##  8 0D1D3909251E0A97 electric_bike 2020-07-15 10:47:04 2020-07-15 10:50:04
    ##  9 782976003D0BB41E electric_bike 2020-07-15 13:53:58 2020-07-15 13:54:48
    ## 10 1A3B9ACE80464646 electric_bike 2020-07-15 11:25:35 2020-07-15 11:34:22
    ## # ... with 71,222 more rows, and 9 more variables: start_station_name <chr>,
    ## #   start_station_id <dbl>, end_station_name <chr>, end_station_id <dbl>,
    ## #   start_lat <dbl>, start_lng <dbl>, end_lat <dbl>, end_lng <dbl>,
    ## #   member_casual <chr>

The analyst filtered out the NULL observations from the dataframe to
contain complete data.

    bikerides <- bikerides %>% 
       filter(!is.na(start_station_name), !is.na(end_station_name)) %>%
       filter(!is.na(start_station_name)) %>%
       filter(!is.na(end_station_name))

    glimpse(bikerides)

    ## Rows: 3,295,563
    ## Columns: 13
    ## $ ride_id            <chr> "A847FADBBC638E45", "5405B80E996FF60D", "5DD24A79A4~
    ## $ rideable_type      <chr> "docked_bike", "docked_bike", "docked_bike", "docke~
    ## $ started_at         <dttm> 2020-04-26 17:45:14, 2020-04-17 17:08:54, 2020-04-~
    ## $ ended_at           <dttm> 2020-04-26 18:12:03, 2020-04-17 17:17:03, 2020-04-~
    ## $ start_station_name <chr> "Eckhart Park", "Drake Ave & Fullerton Ave", "McClu~
    ## $ start_station_id   <dbl> 86, 503, 142, 216, 125, 173, 35, 434, 627, 377, 508~
    ## $ end_station_name   <chr> "Lincoln Ave & Diversey Pkwy", "Kosciuszko Park", "~
    ## $ end_station_id     <dbl> 152, 499, 255, 657, 323, 35, 635, 382, 359, 508, 37~
    ## $ start_lat          <dbl> 41.8964, 41.9244, 41.8945, 41.9030, 41.8902, 41.896~
    ## $ start_lng          <dbl> -87.6610, -87.7154, -87.6179, -87.6975, -87.6262, -~
    ## $ end_lat            <dbl> 41.9322, 41.9306, 41.8679, 41.8992, 41.9695, 41.892~
    ## $ end_lng            <dbl> -87.6586, -87.7238, -87.6230, -87.6722, -87.6547, -~
    ## $ member_casual      <chr> "member", "member", "member", "member", "casual", "~

## Data Preparation

The analyst created two additional attributes (“trip\_duration” and
“day\_of\_week”) to help understand the casual and member groups’ bike
usage better.

The analyst added “trip\_duration” attribute by calculating the
difference between the trip end time and start time in minutes.

    bikerides$trip_duration <- difftime(bikerides$ended_at, bikerides$started_at, units = 'mins')

The analyst then added “day\_of\_week” and “month” attributes by
identifying the weekday and month of the trip start dates.

    bikerides$day_of_week <- weekdays(as.Date(bikerides$started_at))
    bikerides$month <- months(as.Date(bikerides$started_at))
    bikerides$month_yr <- as.yearmon(bikerides$started_at)

## Data Analysis

Through the analysis, the analyst wanted to understand: \* How do casual
and member groups use the bike-share service differently?; and \* Why
would a casual rider get the annual bike-share membership?

The analyst first calculated the historic bike-share usage trend of the
two groups.

    bikerides %>% group_by(member_casual) %>%
      dplyr::summarize(Mean = mean(trip_duration))

    ## # A tibble: 2 x 2
    ##   member_casual Mean         
    ##   <chr>         <drtn>       
    ## 1 casual        44.14996 mins
    ## 2 member        12.05742 mins

      count(bikerides, "member_casual")

    ##   member_casual    freq
    ## 1        casual 1351707
    ## 2        member 1943856

Per results above, the analyst noted that the casual riders take longer
rides than the members whereas the members take shorter but more
frequent rides than the casual riders.

The analyst wanted to understand where are the most frequently visited
stations for both casual riders and members.

    bikeride_trips_casual <- bikerides %>% group_by(member_casual) %>%
    dplyr::count(start_station_name, end_station_name) %>%
    filter(member_casual == 'casual')

    bikeride_trips_member <- bikerides %>% group_by(member_casual) %>%
    dplyr::count(start_station_name, end_station_name) %>%
    filter(member_casual == 'member')

    bikeride_trips_casual <- bikeride_trips_casual[order(bikeride_trips_casual$n, decreasing = TRUE), ]
    bikeride_trips_member <- bikeride_trips_member[order(bikeride_trips_member$n, decreasing = TRUE), ]

Per analysis performed above, the analyst noted that the casual riders
tend start and end trips at the same stations whereas the members tend
to start and end trips at different stations.

## Results Sharing

Refer to the graphs and tables below for the summary of the ridership
dataset from April, 2020 to March, 2021 analysis:

    #Total ridership count comparison
    ggplot(data=bikerides) + 
      geom_bar(mapping=aes(x=member_casual, fill = member_casual)) +
      labs(title = "Total count of trips: Casual Riders vs Members", subtitle = "From April, 2020 to March, 2021") +
      scale_y_continuous(labels = comma)

![](Bike_Sharing_Membership_DA_files/figure-markdown_strict/unnamed-chunk-16-1.png)

    #Ridership Trend per Month
    ridership_graph <- setNames(data.frame(table(bikerides$month_yr)), c("Month_Yr", "Count"))
    month_yr_index <- c("Apr 2020", "May 2020", "Jun 2020", "Jul 2020", "Aug 2020", "Sep 2020", "Oct 2020", "Nov 2020", "Dec 2020", "Jan 2021", "Feb 2021", "Mar 2021")
    ridership_graph <- ridership_graph %>% arrange(match(Month_Yr, month_yr_index))

    ggplot(data=ridership_graph) + 
     geom_line(mapping=aes(x=(ordered(Month_Yr, month_yr_index)), y=Count, group = 1)) +
      labs(title = "Number of Trips per Month", subtitle = "From April, 2020 to March, 2021") +
      scale_y_continuous(labels = comma) +
      labs(x = "Month, Year") +
      theme(axis.text.x = element_text(angle = 45))

![](Bike_Sharing_Membership_DA_files/figure-markdown_strict/unnamed-chunk-16-2.png)

    #Popular days
    day_index <- c("Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday")

    ggplot(data=bikerides %>%
             group_by(day_of_week) %>%
             summarize(day_of_week)) + 
      geom_bar(mapping=aes(x=(ordered(day_of_week, day_index)))) +
      labs(title = "Number of Trips per Days by Member and Casual Riders", subtitle = "From April, 2020 to March, 2021", x = "
           Day", y = "Number of Trips") +
      #scale_x_discrete(labels = day_index) +
      scale_y_continuous(labels = comma) +
      theme(axis.text.x = element_text(angle = 45)) +
      facet_wrap(~bikerides$member_casual)

![](Bike_Sharing_Membership_DA_files/figure-markdown_strict/unnamed-chunk-16-3.png)

    #Top 10 Trip Courses for Casual Riders
    head(bikeride_trips_casual, n = 10)

    ## # A tibble: 10 x 4
    ## # Groups:   member_casual [1]
    ##    member_casual start_station_name         end_station_name               n
    ##    <chr>         <chr>                      <chr>                      <int>
    ##  1 casual        Streeter Dr & Grand Ave    Streeter Dr & Grand Ave     6093
    ##  2 casual        Lake Shore Dr & Monroe St  Lake Shore Dr & Monroe St   5934
    ##  3 casual        Millennium Park            Millennium Park             4998
    ##  4 casual        Buckingham Fountain        Buckingham Fountain         4844
    ##  5 casual        Indiana Ave & Roosevelt Rd Indiana Ave & Roosevelt Rd  3887
    ##  6 casual        Michigan Ave & Oak St      Michigan Ave & Oak St       3576
    ##  7 casual        Fort Dearborn Dr & 31st St Fort Dearborn Dr & 31st St  3161
    ##  8 casual        Michigan Ave & 8th St      Michigan Ave & 8th St       3134
    ##  9 casual        Shore Dr & 55th St         Shore Dr & 55th St          2993
    ## 10 casual        Theater on the Lake        Theater on the Lake         2878

    #Top 10 Trip Courses for Members
    head(bikeride_trips_member, n = 10)

    ## # A tibble: 10 x 4
    ## # Groups:   member_casual [1]
    ##    member_casual start_station_name           end_station_name                 n
    ##    <chr>         <chr>                        <chr>                        <int>
    ##  1 member        MLK Jr Dr & 29th St          State St & 33rd St            1259
    ##  2 member        State St & 33rd St           MLK Jr Dr & 29th St           1119
    ##  3 member        Clark St & Elm St            Clark St & Elm St             1100
    ##  4 member        Lake Shore Dr & Wellington ~ Lake Shore Dr & Wellington ~  1080
    ##  5 member        Lakefront Trail & Bryn Mawr~ Lakefront Trail & Bryn Mawr~  1043
    ##  6 member        Lake Shore Dr & Belmont Ave  Lake Shore Dr & Belmont Ave   1033
    ##  7 member        Burnham Harbor               Burnham Harbor                1026
    ##  8 member        Theater on the Lake          Theater on the Lake            983
    ##  9 member        Dearborn St & Erie St        Dearborn St & Erie St          971
    ## 10 member        Lake Shore Dr & North Blvd   Lake Shore Dr & North Blvd     965

Per analysis performed, the marketing analyst noted the following :

-   Members ride *shorter* but have *more frequent* trips than the
    casual riders;
-   The historical data indicate that *August* is the month with the
    *highest ridership*, and *February* is the month with the *lowest
    ridership*.;
-   The historical data indicate that *Saturday* is the day with the
    *highest ridership*, and *Monday* is the month with the *lowest
    ridership*
-   The historical data indicate *“Streeter Dr & Grand Ave” to “Streeter
    Dr & Grand Ave”* and *“Lake Shore Dr & Monroe St” to “Lake Shore Dr
    & Monroe St”* were the most popular courses for the *casual riders*.
-   The historical data indicate *“MLK Jr Dr & 29th St” to “State St &
    33rd St”* and *“State St & 33rd St” to “MLK Jr Dr & 29th St”* were
    the most popular courses for the *members*.

## Recommendations

The marketing analyst recommends the following based on the analysis
performed:

-   Focus marketing campaign around “Streeter Dr & Grand Ave” and “Lake
    Shore Dr & Monroe St” stations on weekends to better target annual
    membership products to the casual riders.
-   Focus marketing campaign around “MLK Jr Dr & 29th St” and “State St
    & 33rd St” stations to better target membership retention programs
    to the members.
-   Launch marketing campaign by June to maximize the summer season.
