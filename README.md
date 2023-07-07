# Cleaning Data in R

<img src="media/image1.png" style="width:1.43125in;height:1.43125in" />

### Course Description

It's commonly said that data scientists spend 80% of their time cleaning
and manipulating data and only 20% of their time actually analyzing it.
For this reason, it is critical to become familiar with the data
cleaning process and all of the tools available to you along the way.
This course provides a very basic introduction to cleaning data in R, so
that you can get from raw data to awesome insights as quickly and
painlessly as possible!

#### 1Introduction and exploring raw data

This chapter will give you an overview of the process of data cleaning
with R, then walk you through the basics of exploring raw data.

#### 

#### 2Tidying data 

This chapter will give you an overview of the principles of tidy data,
how to identify messy data, and what to do about it.

#### 

#### 3Preparing data for analysis 

This chapter will teach you how to prepare your data for analysis. We
will look at type conversion, string manipulation, missing and special
values, and outliers and obvious errors.

#### 

#### 4Putting it all together 

In this chapter, you will practice everything you've learned from the
first three chapters in order to clean a messy dataset using R.

**  
**

**The data cleaning process**

50xp

Which of the following is NOT an essential part of the data cleaning
process as outlined in the previous video?

**Possible Answers**

- ![](media/image2.wmf)Preparing data for analysis

- ![](media/image2.wmf)Exploring raw data

- ![](media/image2.wmf)Removing or replacing missing data

- ![](media/image2.wmf)Tidying data

Great work! No one likes missing data, but it is dangerous to assume
that it can simply be removed or replaced. Sometimes missing data tells
us something important about whatever it is that we're measuring (i.e.
The value of the variable that is missing may be related to the reason
it is missing). Such data is called Missing not at Random, or MNAR.

# Here's what messy data look like

100xp

In the final chapter of this course, you will be presented with a messy,
real-world dataset containing an entire year's worth of weather data
from Boston, USA. Among other things, you'll be presented with variables
that contain column names, column names that should be values, numbers
coded as character strings, and values that are missing, extreme, and
downright erroneous!

## Instructions

We've placed some R code in the script to the right. Run the code as-is
to see just how messy the weather data really are!

\# View the first 6 rows of data

```{r}
head(weather)
```

\# View the last 6 rows of data

tail(weather)

\# View a condensed summary of the data

str(weather)

\> \# View the first 6 rows of data

\> head(weather)

X year month measure X1 X2 X3 X4 X5 X6 X7 X8 X9 X10 X11 X12 X13 X14

1 1 2014 12 Max.TemperatureF 64 42 51 43 42 45 38 29 49 48 39 39 42 45

2 2 2014 12 Mean.TemperatureF 52 38 44 37 34 42 30 24 39 43 36 35 37 39

3 3 2014 12 Min.TemperatureF 39 33 37 30 26 38 21 18 29 38 32 31 32 33

4 4 2014 12 Max.Dew.PointF 46 40 49 24 37 45 36 28 49 45 37 28 28 29

5 5 2014 12 MeanDew.PointF 40 27 42 21 25 40 20 16 41 39 31 27 26 27

6 6 2014 12 Min.DewpointF 26 17 24 13 12 36 -3 3 28 37 27 25 24 25

X15 X16 X17 X18 X19 X20 X21 X22 X23 X24 X25 X26 X27 X28 X29 X30 X31

1 42 44 49 44 37 36 36 44 47 46 59 50 52 52 41 30 30

2 37 40 45 40 33 32 33 39 45 44 52 44 45 46 36 26 25

3 32 35 41 36 29 27 30 33 42 41 44 37 38 40 30 22 20

4 33 42 46 34 25 30 30 39 45 46 58 31 34 42 26 10 8

5 29 36 41 30 22 24 27 34 42 44 43 29 31 35 20 4 5

6 27 30 32 26 20 20 25 25 37 41 29 28 29 27 10 -6 1

\>

\> \# View the last 6 rows of data

\> tail(weather)

X year month measure X1 X2 X3 X4 X5 X6 X7 X8

281 281 2015 12 Mean.Wind.SpeedMPH 6 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\>

282 282 2015 12 Max.Gust.SpeedMPH 17 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\>

283 283 2015 12 PrecipitationIn 0.14 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\>

284 284 2015 12 CloudCover 7 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\>

285 285 2015 12 Events Rain \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\>

286 286 2015 12 WindDirDegrees 109 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\>

X9 X10 X11 X12 X13 X14 X15 X16 X17 X18 X19 X20 X21 X22 X23

281 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

282 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

283 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

284 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

285 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

286 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

X24 X25 X26 X27 X28 X29 X30 X31

281 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

282 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

283 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

284 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

285 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

286 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

\>

\> \# View a condensed summary of the data

\> str(weather)

'data.frame': 286 obs. of 35 variables:

\$ X : int 1 2 3 4 5 6 7 8 9 10 ...

\$ year : int 2014 2014 2014 2014 2014 2014 2014 2014 2014 2014 ...

\$ month : int 12 12 12 12 12 12 12 12 12 12 ...

\$ measure: chr "Max.TemperatureF" "Mean.TemperatureF"
"Min.TemperatureF" "Max.Dew.PointF" ...

\$ X1 : chr "64" "52" "39" "46" ...

\$ X2 : chr "42" "38" "33" "40" ...

\$ X3 : chr "51" "44" "37" "49" ...

\$ X4 : chr "43" "37" "30" "24" ...

\$ X5 : chr "42" "34" "26" "37" ...

\$ X6 : chr "45" "42" "38" "45" ...

\$ X7 : chr "38" "30" "21" "36" ...

\$ X8 : chr "29" "24" "18" "28" ...

\$ X9 : chr "49" "39" "29" "49" ...

\$ X10 : chr "48" "43" "38" "45" ...

\$ X11 : chr "39" "36" "32" "37" ...

\$ X12 : chr "39" "35" "31" "28" ...

\$ X13 : chr "42" "37" "32" "28" ...

\$ X14 : chr "45" "39" "33" "29" ...

\$ X15 : chr "42" "37" "32" "33" ...

\$ X16 : chr "44" "40" "35" "42" ...

\$ X17 : chr "49" "45" "41" "46" ...

\$ X18 : chr "44" "40" "36" "34" ...

\$ X19 : chr "37" "33" "29" "25" ...

\$ X20 : chr "36" "32" "27" "30" ...

\$ X21 : chr "36" "33" "30" "30" ...

\$ X22 : chr "44" "39" "33" "39" ...

\$ X23 : chr "47" "45" "42" "45" ...

\$ X24 : chr "46" "44" "41" "46" ...

\$ X25 : chr "59" "52" "44" "58" ...

\$ X26 : chr "50" "44" "37" "31" ...

\$ X27 : chr "52" "45" "38" "34" ...

\$ X28 : chr "52" "46" "40" "42" ...

\$ X29 : chr "41" "36" "30" "26" ...

\$ X30 : chr "30" "26" "22" "10" ...

\$ X31 : chr "30" "25" "20" "8" ...

\>

Nicely done! You may have already noticed messy aspects of the dataset.
If not, don't worry! We'll get to that soon.

# Here's what clean data look like

100xp

In this course, you will acquire many new tools in your data cleaning
toolbox for whipping the weather data into shape!

## Instructions

Run the code provided to see what the weather dataset will look like by
the time you are done cleaning it. If it's not immediately clear what's
changed, don't worry! You will have a much deeper understanding by the
end of this course.

\# View the first 6 rows of data

head(weather_clean)

\# View the last 6 rows of data

tail(weather_clean)

\# View a condensed summary of the data

str(weather_clean)

\> \# View the first 6 rows of data

\> head(weather_clean)

date events cloud_cover max_dew_point_f max_gust_speed_mph

1 2014-12-01 Rain 6 46 29

2 2014-12-02 Rain-Snow 7 40 29

3 2014-12-03 Rain 8 49 38

4 2014-12-04 None 3 24 33

5 2014-12-05 Rain 5 37 26

6 2014-12-06 Rain 8 45 25

max_humidity max_sea_level_pressure_in max_temperature_f
max_visibility_miles

1 74 30.45 64 10

2 92 30.71 42 10

3 100 30.40 51 10

4 69 30.56 43 10

5 85 30.68 42 10

6 100 30.42 45 10

max_wind_speed_mph mean_humidity mean_sea_level_pressure_in

1 22 63 30.13

2 24 72 30.59

3 29 79 30.07

4 25 54 30.33

5 22 66 30.59

6 22 93 30.24

mean_temperature_f mean_visibility_miles mean_wind_speed_mph
mean_dew_point_f

1 52 10 13 40

2 38 8 15 27

3 44 5 12 42

4 37 10 12 21

5 34 10 10 25

6 42 4 8 40

min_dew_point_f min_humidity min_sea_level_pressure_in min_temperature_f

1 26 52 30.01 39

2 17 51 30.40 33

3 24 57 29.87 37

4 13 39 30.09 30

5 12 47 30.45 26

6 36 85 30.16 38

min_visibility_miles precipitation_in wind_dir_degrees

1 10 0.01 268

2 2 0.10 62

3 1 0.44 254

4 10 0.00 292

5 5 0.11 61

6 0 1.09 313

\>

\> \# View the last 6 rows of data

\> tail(weather_clean)

date events cloud_cover max_dew_point_f max_gust_speed_mph

361 2015-11-26 None 6 49 28

362 2015-11-27 None 7 52 32

363 2015-11-28 Rain 8 50 23

364 2015-11-29 None 4 33 20

365 2015-11-30 None 6 26 17

366 2015-12-01 Rain 7 43 17

max_humidity max_sea_level_pressure_in max_temperature_f

361 100 30.87 59

362 100 30.63 64

363 93 30.20 60

364 79 30.42 44

365 75 30.53 38

366 96 30.40 45

max_visibility_miles max_wind_speed_mph mean_humidity

361 10 22 79

362 10 26 78

363 10 18 80

364 10 16 58

365 10 14 65

366 10 15 83

mean_sea_level_pressure_in mean_temperature_f mean_visibility_miles

361 30.77 49 9

362 30.41 56 9

363 30.16 51 9

364 30.26 38 10

365 30.46 33 10

366 30.24 39 8

mean_wind_speed_mph mean_dew_point_f min_dew_point_f min_humidity

361 10 42 34 57

362 14 49 47 56

363 10 43 36 67

364 10 23 15 36

365 9 23 18 54

366 6 35 25 69

min_sea_level_pressure_in min_temperature_f min_visibility_miles

361 30.64 38 5

362 30.15 48 5

363 30.11 41 4

364 30.19 32 10

365 30.39 28 10

366 30.01 32 1

precipitation_in wind_dir_degrees

361 0.00 180

362 0.00 209

363 0.21 358

364 0.00 326

365 0.00 65

366 0.14 109

\>

\> \# View a condensed summary of the data

\> str(weather_clean)

'data.frame': 366 obs. of 23 variables:

\$ date : POSIXct, format: "2014-12-01" "2014-12-02" ...

\$ events : chr "Rain" "Rain-Snow" "Rain" "None" ...

\$ cloud_cover : num 6 7 8 3 5 8 6 8 8 8 ...

\$ max_dew_point_f : num 46 40 49 24 37 45 36 28 49 45 ...

\$ max_gust_speed_mph : num 29 29 38 33 26 25 32 28 52 29 ...

\$ max_humidity : num 74 92 100 69 85 100 92 92 100 100 ...

\$ max_sea_level_pressure_in : num 30.4 30.7 30.4 30.6 30.7 ...

\$ max_temperature_f : num 64 42 51 43 42 45 38 29 49 48 ...

\$ max_visibility_miles : num 10 10 10 10 10 10 10 10 10 10 ...

\$ max_wind_speed_mph : num 22 24 29 25 22 22 25 21 38 23 ...

\$ mean_humidity : num 63 72 79 54 66 93 61 70 93 95 ...

\$ mean_sea_level_pressure_in: num 30.1 30.6 30.1 30.3 30.6 ...

\$ mean_temperature_f : num 52 38 44 37 34 42 30 24 39 43 ...

\$ mean_visibility_miles : num 10 8 5 10 10 4 10 8 2 3 ...

\$ mean_wind_speed_mph : num 13 15 12 12 10 8 15 13 20 13 ...

\$ mean_dew_point_f : num 40 27 42 21 25 40 20 16 41 39 ...

\$ min_dew_point_f : num 26 17 24 13 12 36 -3 3 28 37 ...

\$ min_humidity : num 52 51 57 39 47 85 29 47 86 89 ...

\$ min_sea_level_pressure_in : num 30 30.4 29.9 30.1 30.4 ...

\$ min_temperature_f : num 39 33 37 30 26 38 21 18 29 38 ...

\$ min_visibility_miles : num 10 2 1 10 5 0 5 2 1 1 ...

\$ precipitation_in : num 0.01 0.1 0.44 0 0.11 1.09 0.13 0.03 2.9 0.28
...

\$ wind_dir_degrees : num 268 62 254 292 61 313 350 354 38 357 ...

\>

Good work! Doesn't this dataset already look nicer than in the previous
exercise?

# Getting a feel for your data

100xp

The first thing to do when you get your hands on a new dataset is to
understand its structure. There are several ways to go about this in R,
each of which may reveal different issues with your data that require
attention.

In this course, we are only concerned with data that can be expressed in
table format (i.e. two dimensions, rows and columns). As you may recall
from earlier courses, tables in R often have the type data.frame. You
can check the class of any object in R with the class() function.

Once you know that you are dealing with tabular data, you may also want
to get a quick feel for the contents of your data. Before printing the
entire dataset to the console, it's probably worth knowing how many rows
and columns there are. The dim() command tells you this.

## Instructions

We've loaded a dataset called bmi into your workspace. The data, which
give the (age standardized) mean body mass index (BMI) among males in
each country for the years 1980-2008, come from the [School of Public
Health, Imperial College
London](https://www1.imperial.ac.uk/publichealth/departments/ebs/projects/eresh/majidezzati/healthmetrics/metabolicriskfactors/).

- Check the class of bmi

- Find the dimensions of bmi

- Print the bmi column names

\# Check the class of bmi

class(bmi)

\# Check the dimensions of bmi

dim(bmi)

\# View the column names of bmi

names(bmi)

\> \# Check the class of bmi

\> class(bmi)

\[1\] "data.frame"

\>

\> \# Check the dimensions of bmi

\> dim(bmi)

\[1\] 199 30

\>

\> \# View the column names of bmi

\> names(bmi)

\[1\] "Country" "Y1980" "Y1981" "Y1982" "Y1983" "Y1984" "Y1985"

\[8\] "Y1986" "Y1987" "Y1988" "Y1989" "Y1990" "Y1991" "Y1992"

\[15\] "Y1993" "Y1994" "Y1995" "Y1996" "Y1997" "Y1998" "Y1999"

\[22\] "Y2000" "Y2001" "Y2002" "Y2003" "Y2004" "Y2005" "Y2006"

\[29\] "Y2007" "Y2008"

\>

Nice job! We'll be working with the BMI data for the remainder of this
chapter, so it's good you're familiar with it now.

# Viewing the structure of your data

100xp

Since bmi doesn't have a huge number of columns, you can view a quick
snapshot of your data using the str() (for *structure*) command. In
addition to the class and dimensions of your *entire
dataset*, str() will tell you the class of *each variable* and give you
a preview of its contents.

Although we won't go into detail on the dplyr package in this lesson
(see the [Data Manipulation in R with
dplyr](https://www.datacamp.com/courses/dplyr-data-manipulation-r-tutorial) course),
the glimpse() function from dplyr is a slightly cleaner alternative
to str(). str() and glimpse() give you a preview of your data, which may
reveal issues with the way columns are labelled, how variables are
encoded, etc.

You can use the summary() command to get a better feel for how your data
are distributed, which may reveal unusual or extreme values, unexpected
missing data, etc. For numeric variables, this means looking at means,
quartiles (including the median), and extreme values. For character or
factor variables, you may be curious about the number of times each
value appears in the data (i.e. counts), which summary() also reveals.

## Instructions

- View the structure of bmi using the traditional method

- Load the dplyr package

- View the structure of bmi using dplyr

- Look at a summary() of bmi

\# Check the structure of bmi

str(bmi)

\# Load dplyr

library(dplyr)

\# Check the structure of bmi, the dplyr way

glimpse(bmi)

\# View a summary of bmi

summary(bmi)

\> \# Check the structure of bmi

\> str(bmi)

'data.frame': 199 obs. of 30 variables:

\$ Country: chr "Afghanistan" "Albania" "Algeria" "Andorra" ...

\$ Y1980 : num 21.5 25.2 22.3 25.7 20.9 ...

\$ Y1981 : num 21.5 25.2 22.3 25.7 20.9 ...

\$ Y1982 : num 21.5 25.3 22.4 25.7 20.9 ...

\$ Y1983 : num 21.4 25.3 22.5 25.8 20.9 ...

\$ Y1984 : num 21.4 25.3 22.6 25.8 20.9 ...

\$ Y1985 : num 21.4 25.3 22.7 25.9 20.9 ...

\$ Y1986 : num 21.4 25.3 22.8 25.9 21 ...

\$ Y1987 : num 21.4 25.3 22.8 25.9 21 ...

\$ Y1988 : num 21.3 25.3 22.9 26 21 ...

\$ Y1989 : num 21.3 25.3 23 26 21.1 ...

\$ Y1990 : num 21.2 25.3 23 26.1 21.1 ...

\$ Y1991 : num 21.2 25.3 23.1 26.2 21.1 ...

\$ Y1992 : num 21.1 25.2 23.2 26.2 21.1 ...

\$ Y1993 : num 21.1 25.2 23.3 26.3 21.1 ...

\$ Y1994 : num 21 25.2 23.3 26.4 21.1 ...

\$ Y1995 : num 20.9 25.3 23.4 26.4 21.2 ...

\$ Y1996 : num 20.9 25.3 23.5 26.5 21.2 ...

\$ Y1997 : num 20.8 25.3 23.5 26.6 21.2 ...

\$ Y1998 : num 20.8 25.4 23.6 26.7 21.3 ...

\$ Y1999 : num 20.8 25.5 23.7 26.8 21.3 ...

\$ Y2000 : num 20.7 25.6 23.8 26.8 21.4 ...

\$ Y2001 : num 20.6 25.7 23.9 26.9 21.4 ...

\$ Y2002 : num 20.6 25.8 24 27 21.5 ...

\$ Y2003 : num 20.6 25.9 24.1 27.1 21.6 ...

\$ Y2004 : num 20.6 26 24.2 27.2 21.7 ...

\$ Y2005 : num 20.6 26.1 24.3 27.3 21.8 ...

\$ Y2006 : num 20.6 26.2 24.4 27.4 21.9 ...

\$ Y2007 : num 20.6 26.3 24.5 27.5 22.1 ...

\$ Y2008 : num 20.6 26.4 24.6 27.6 22.3 ...

\>

\> \# Load dplyr

\> library(dplyr)

Attaching package: 'dplyr'

The following objects are masked from 'package:stats':

filter, lag

The following objects are masked from 'package:base':

intersect, setdiff, setequal, union

\>

\> \# Check the structure of bmi, the dplyr way

\> glimpse(bmi)

Observations: 199

Variables: 30

\$ Country \<chr\> "Afghanistan", "Albania", "Algeria", "Andorra",
"Angola", "...

\$ Y1980 \<dbl\> 21.48678, 25.22533, 22.25703, 25.66652, 20.94876,
23.31424,...

\$ Y1981 \<dbl\> 21.46552, 25.23981, 22.34745, 25.70868, 20.94371,
23.39054,...

\$ Y1982 \<dbl\> 21.45145, 25.25636, 22.43647, 25.74681, 20.93754,
23.45883,...

\$ Y1983 \<dbl\> 21.43822, 25.27176, 22.52105, 25.78250, 20.93187,
23.53735,...

\$ Y1984 \<dbl\> 21.42734, 25.27901, 22.60633, 25.81874, 20.93569,
23.63584,...

\$ Y1985 \<dbl\> 21.41222, 25.28669, 22.69501, 25.85236, 20.94857,
23.73109,...

\$ Y1986 \<dbl\> 21.40132, 25.29451, 22.76979, 25.89089, 20.96030,
23.83449,...

\$ Y1987 \<dbl\> 21.37679, 25.30217, 22.84096, 25.93414, 20.98025,
23.93649,...

\$ Y1988 \<dbl\> 21.34018, 25.30450, 22.90644, 25.98477, 21.01375,
24.05364,...

\$ Y1989 \<dbl\> 21.29845, 25.31944, 22.97931, 26.04450, 21.05269,
24.16347,...

\$ Y1990 \<dbl\> 21.24818, 25.32357, 23.04600, 26.10936, 21.09007,
24.26782,...

\$ Y1991 \<dbl\> 21.20269, 25.28452, 23.11333, 26.17912, 21.12136,
24.36568,...

\$ Y1992 \<dbl\> 21.14238, 25.23077, 23.18776, 26.24017, 21.14987,
24.45644,...

\$ Y1993 \<dbl\> 21.06376, 25.21192, 23.25764, 26.30356, 21.13938,
24.54096,...

\$ Y1994 \<dbl\> 20.97987, 25.22115, 23.32273, 26.36793, 21.14186,
24.60945,...

\$ Y1995 \<dbl\> 20.91132, 25.25874, 23.39526, 26.43569, 21.16022,
24.66461,...

\$ Y1996 \<dbl\> 20.85155, 25.31097, 23.46811, 26.50769, 21.19076,
24.72544,...

\$ Y1997 \<dbl\> 20.81307, 25.33988, 23.54160, 26.58255, 21.22621,
24.78714,...

\$ Y1998 \<dbl\> 20.78591, 25.39116, 23.61592, 26.66337, 21.27082,
24.84936,...

\$ Y1999 \<dbl\> 20.75469, 25.46555, 23.69486, 26.75078, 21.31954,
24.91721,...

\$ Y2000 \<dbl\> 20.69521, 25.55835, 23.77659, 26.83179, 21.37480,
24.99158,...

\$ Y2001 \<dbl\> 20.62643, 25.66701, 23.86256, 26.92373, 21.43664,
25.05857,...

\$ Y2002 \<dbl\> 20.59848, 25.77167, 23.95294, 27.02525, 21.51765,
25.13039,...

\$ Y2003 \<dbl\> 20.58706, 25.87274, 24.05243, 27.12481, 21.59924,
25.20713,...

\$ Y2004 \<dbl\> 20.57759, 25.98136, 24.15957, 27.23107, 21.69218,
25.29898,...

\$ Y2005 \<dbl\> 20.58084, 26.08939, 24.27001, 27.32827, 21.80564,
25.39965,...

\$ Y2006 \<dbl\> 20.58749, 26.20867, 24.38270, 27.43588, 21.93881,
25.51382,...

\$ Y2007 \<dbl\> 20.60246, 26.32753, 24.48846, 27.53363, 22.08962,
25.64247,...

\$ Y2008 \<dbl\> 20.62058, 26.44657, 24.59620, 27.63048, 22.25083,
25.76602,...

\>

\> \# View a summary of bmi

\> summary(bmi)

Country Y1980 Y1981 Y1982

Length:199 Min. :19.01 Min. :19.04 Min. :19.07

Class :character 1st Qu.:21.27 1st Qu.:21.31 1st Qu.:21.36

Mode :character Median :23.31 Median :23.39 Median :23.46

Mean :23.15 Mean :23.21 Mean :23.26

3rd Qu.:24.82 3rd Qu.:24.89 3rd Qu.:24.94

Max. :28.12 Max. :28.36 Max. :28.58

Y1983 Y1984 Y1985 Y1986

Min. :19.10 Min. :19.13 Min. :19.16 Min. :19.20

1st Qu.:21.42 1st Qu.:21.45 1st Qu.:21.47 1st Qu.:21.49

Median :23.57 Median :23.64 Median :23.73 Median :23.82

Mean :23.32 Mean :23.37 Mean :23.42 Mean :23.48

3rd Qu.:25.02 3rd Qu.:25.06 3rd Qu.:25.11 3rd Qu.:25.20

Max. :28.82 Max. :29.05 Max. :29.28 Max. :29.52

Y1987 Y1988 Y1989 Y1990

Min. :19.23 Min. :19.27 Min. :19.31 Min. :19.35

1st Qu.:21.50 1st Qu.:21.52 1st Qu.:21.55 1st Qu.:21.57

Median :23.87 Median :23.93 Median :24.03 Median :24.14

Mean :23.53 Mean :23.59 Mean :23.65 Mean :23.71

3rd Qu.:25.27 3rd Qu.:25.34 3rd Qu.:25.37 3rd Qu.:25.39

Max. :29.75 Max. :29.98 Max. :30.20 Max. :30.42

Y1991 Y1992 Y1993 Y1994

Min. :19.40 Min. :19.45 Min. :19.51 Min. :19.59

1st Qu.:21.60 1st Qu.:21.65 1st Qu.:21.74 1st Qu.:21.76

Median :24.20 Median :24.19 Median :24.27 Median :24.36

Mean :23.76 Mean :23.82 Mean :23.88 Mean :23.94

3rd Qu.:25.42 3rd Qu.:25.48 3rd Qu.:25.54 3rd Qu.:25.62

Max. :30.64 Max. :30.85 Max. :31.04 Max. :31.23

Y1995 Y1996 Y1997 Y1998

Min. :19.67 Min. :19.71 Min. :19.74 Min. :19.77

1st Qu.:21.83 1st Qu.:21.89 1st Qu.:21.94 1st Qu.:22.00

Median :24.41 Median :24.42 Median :24.50 Median :24.49

Mean :24.00 Mean :24.07 Mean :24.14 Mean :24.21

3rd Qu.:25.70 3rd Qu.:25.78 3rd Qu.:25.85 3rd Qu.:25.94

Max. :31.41 Max. :31.59 Max. :31.77 Max. :31.95

Y1999 Y2000 Y2001 Y2002

Min. :19.80 Min. :19.83 Min. :19.86 Min. :19.84

1st Qu.:22.04 1st Qu.:22.12 1st Qu.:22.22 1st Qu.:22.29

Median :24.61 Median :24.66 Median :24.73 Median :24.81

Mean :24.29 Mean :24.36 Mean :24.44 Mean :24.52

3rd Qu.:26.01 3rd Qu.:26.09 3rd Qu.:26.19 3rd Qu.:26.30

Max. :32.13 Max. :32.32 Max. :32.51 Max. :32.70

Y2003 Y2004 Y2005 Y2006

Min. :19.81 Min. :19.79 Min. :19.79 Min. :19.80

1st Qu.:22.37 1st Qu.:22.45 1st Qu.:22.54 1st Qu.:22.63

Median :24.89 Median :25.00 Median :25.11 Median :25.24

Mean :24.61 Mean :24.70 Mean :24.79 Mean :24.89

3rd Qu.:26.38 3rd Qu.:26.47 3rd Qu.:26.53 3rd Qu.:26.59

Max. :32.90 Max. :33.10 Max. :33.30 Max. :33.49

Y2007 Y2008

Min. :19.83 Min. :19.87

1st Qu.:22.73 1st Qu.:22.83

Median :25.36 Median :25.50

Mean :24.99 Mean :25.10

3rd Qu.:26.66 3rd Qu.:26.82

Max. :33.69 Max. :33.90

\>

Nice job! Take a moment to notice the slight differences in the output
generated by str() and glimpse()

[  
DataCamp](https://www.datacamp.com/)

[Course
Outline](https://campus.datacamp.com/courses/cleaning-data-in-r/chapter-1-introduction-and-exploring-raw-data?ex=9)

# Looking at your data

100xp

You can look at all the summaries you want, but at the end of the day,
there is no substitute for looking at your data -- either in raw table
form or by plotting it.

The most basic way to look at your data in R is by printing it to the
console. As you may know from experience, the print() command is not
even necessary; you can just type the name of the object. The downside
to this option is that R will attempt to print the entire dataset, which
can be a nuisance if the dataset is too large.

One way around this is to use the head() and tail() commands, which only
display the first and last 6 rows of data, respectively. You can view
more (or fewer) rows by providing as a second argument to the function
the number of rows you wish to view. These functions provide a useful
method for quickly getting a sense of your data without overly
cluttering the console.

## Instructions

- Print the full dataset to the console (you don't need print()to do
  this)

- View the first 6 rows of bmi

- View the first 15 rows of bmi

- View the last 6 rows of bmi

- View the last 10 rows of bmi

\# Print bmi to the console

print(bmi)

\# View the first 6 rows

head(bmi, n = 6)

\# View the first 15 rows

head(bmi, n = 15)

\# View the last 6 rows

tail(bmi, n = 6)

\# View the last 10 rows

tail(bmi, n = 10)

\> \# Print bmi to the console

\> print(bmi)

Country Y1980 Y1981 Y1982 Y1983

1 Afghanistan 21.48678 21.46552 21.45145 21.43822

2 Albania 25.22533 25.23981 25.25636 25.27176

3 Algeria 22.25703 22.34745 22.43647 22.52105

4 Andorra 25.66652 25.70868 25.74681 25.78250

5 Angola 20.94876 20.94371 20.93754 20.93187

6 Antigua and Barbuda 23.31424 23.39054 23.45883 23.53735

7 Argentina 25.37913 25.44951 25.50242 25.55644

8 Armenia 23.82469 23.86401 23.91023 23.95649

9 Australia 24.92729 25.00216 25.07660 25.14938

10 Austria 24.84097 24.88110 24.93482 24.98118

11 Azerbaijan 24.49375 24.52584 24.56064 24.60150

12 Bahamas 24.21064 24.30814 24.42750 24.54415

13 Bahrain 23.97588 24.09045 24.20617 24.32335

14 Bangladesh 20.51918 20.47766 20.43741 20.40075

15 Barbados 24.36372 24.43455 24.49314 24.54713

16 Belarus 24.90898 24.90986 24.91623 24.91568

17 Belgium 25.09879 25.12474 25.16059 25.18982

18 Belize 24.54345 24.63418 24.71853 24.76496

19 Benin 20.80754 20.83999 20.88208 20.90821

20 Bermuda 25.07881 25.19625 25.31163 25.43990

21 Bhutan 21.81929 21.80187 21.78799 21.77328

22 Bolivia 23.00319 23.04351 23.07385 23.08641

23 Bosnia and Herzegovina 25.32025 25.33178 25.35258 25.37304

24 Botswana 19.54182 19.57970 19.62362 19.66629

25 Brazil 22.63867 22.72772 22.81802 22.89804

26 British Virgin Islands 23.74249 23.79803 23.85294 23.91227

27 Brunei 23.23982 23.27246 23.30495 23.33870

28 Bulgaria 25.28913 25.34139 25.39515 25.44814

29 Burkina Faso 20.03144 20.06225 20.09198 20.11975

30 Burundi 21.08872 21.11359 21.12784 21.13206

31 Cambodia 19.69966 19.70779 19.71740 19.73194

32 Cameroon 21.78602 21.86229 21.94666 22.03968

33 Canada 25.24074 25.33069 25.41020 25.48895

34 Cape Verde 20.65607 20.71493 20.77269 20.84066

35 Central African Rep. 20.95858 20.96244 20.96119 20.94252

36 Chad 20.22551 20.22710 20.23140 20.25014

37 Chile 24.48362 24.56329 24.62478 24.67812

38 China 21.57840 21.58356 21.59550 21.61408

39 Colombia 22.07035 22.17690 22.26799 22.36244

40 Comoros 20.98163 21.00660 21.04036 21.07561

41 Congo, Dem. Rep. 20.74786 20.73587 20.72111 20.70907

42 Congo, Rep. 20.63666 20.69499 20.76571 20.83255

43 Cook Islands 26.20250 26.43064 26.67362 26.90854

44 Costa Rica 23.69370 23.76567 23.82701 23.88394

45 Cote d'Ivoire 21.12741 21.18081 21.22675 21.27402

46 Croatia 25.28752 25.31690 25.34765 25.37672

47 Cuba 22.73085 22.80724 22.89338 22.98056

48 Cyprus 25.33529 25.37046 25.42285 25.48050

49 Czech Rep. 26.30589 26.35295 26.40544 26.45339

50 Denmark 24.56320 24.56873 24.57527 24.58004

51 Djibouti 21.23864 21.31928 21.40683 21.48918

52 Dominica 22.31900 22.38872 22.46119 22.51509

53 Dominican Rep. 22.92812 22.97861 23.02566 23.07558

54 Ecuador 23.79064 23.85029 23.90204 23.94343

55 Egypt 24.25654 24.34966 24.44688 24.54141

56 El Salvador 23.77156 23.83422 23.89040 23.94184

57 Equatorial Guinea 21.08890 21.10687 21.12008 21.13055

58 Eritrea 20.01453 20.04318 20.06819 20.09359

59 Estonia 24.68737 24.69421 24.70221 24.70975

60 Ethiopia 19.47815 19.50485 19.52747 19.55625

61 Fiji 22.28238 22.43676 22.57832 22.71827

62 Finland 25.46078 25.48010 25.50321 25.52352

63 France 24.70702 24.73514 24.76177 24.78531

64 French Polynesia 25.41759 25.60073 25.78890 25.97905

65 Gabon 22.27217 22.32139 22.37964 22.44393

66 Gambia 19.94139 19.97059 20.00107 20.03257

67 Georgia 24.61762 24.66646 24.71051 24.76342

68 Germany 25.46227 25.50636 25.55565 25.59814

69 Ghana 21.01212 21.01867 21.01856 21.01256

70 Greece 24.80837 24.85004 24.88029 24.91068

71 Greenland 24.46978 24.52714 24.57298 24.62106

72 Grenada 23.27113 23.31463 23.36183 23.40248

73 Guatemala 23.18719 23.26498 23.33675 23.39964

74 Guinea 21.14949 21.17170 21.19272 21.21010

75 Guinea-Bissau 20.71293 20.72467 20.74743 20.76258

76 Guyana 22.71432 22.73525 22.74163 22.74203

77 Haiti 22.90655 22.93626 22.95830 22.97473

78 Honduras 23.13391 23.19850 23.25895 23.31384

79 Hong Kong, China 21.63375 21.75267 21.86784 21.98671

80 Hungary 25.28424 25.35008 25.42012 25.48757

81 Iceland 24.82734 24.92462 25.00838 25.07729

82 India 21.09132 21.04581 21.00317 20.96066

83 Indonesia 19.85723 19.90366 19.94077 19.98318

84 Iran 23.16184 23.23424 23.31364 23.40150

85 Iraq 24.98391 25.07866 25.16866 25.25453

86 Ireland 25.80942 25.83961 25.86538 25.88202

87 Israel 24.76857 24.79572 24.84701 24.89470

88 Italy 25.41060 25.41417 25.41974 25.42467

89 Jamaica 22.33166 22.35883 22.38478 22.41510

90 Japan 22.10080 22.11807 22.13820 22.15686

91 Jordan 24.65223 24.77498 24.90362 25.03078

92 Kazakhstan 24.57360 24.61631 24.66513 24.71128

93 Kenya 20.31468 20.36356 20.40880 20.45230

94 Kiribati 25.48169 25.55256 25.62888 25.70594

95 Korea, Dem. Rep. 21.79468 21.84316 21.89581 21.94895

96 Korea, Rep. 22.06965 22.07588 22.10213 22.13054

97 Kuwait 25.49319 25.59347 25.69393 25.79244

98 Kyrgyzstan 24.36430 24.38836 24.40658 24.42736

99 Laos 19.59954 19.63955 19.67721 19.71391

100 Latvia 25.12425 25.14042 25.15379 25.16715

101 Lebanon 23.88020 23.98402 24.07560 24.18211

102 Lesotho 20.57660 20.59964 20.62078 20.63468

103 Liberia 21.12546 21.15314 21.18413 21.21202

104 Libya 24.39546 24.50966 24.61506 24.71525

105 Lithuania 25.99960 25.99385 25.98854 25.98756

106 Luxembourg 24.99432 25.03678 25.09048 25.14088

107 Macao, China 22.65022 22.75827 22.86494 22.97370

108 Macedonia, FYR 25.39905 25.42642 25.45236 25.48184

109 Madagascar 20.69690 20.71678 20.73192 20.74784

110 Malawi 20.79355 20.81847 20.84065 20.85144

111 Malaysia 21.58003 21.68427 21.78490 21.89074

112 Maldives 20.44454 20.50850 20.56406 20.63904

113 Mali 20.28129 20.30682 20.32526 20.33895

114 Malta 25.70377 25.75106 25.79222 25.82924

115 Marshall Islands 24.66611 24.82211 24.97811 25.14127

116 Mauritania 20.85381 20.90764 20.95424 21.00572

117 Mauritius 21.98902 22.10120 22.20631 22.30447

118 Mexico 24.45367 24.60031 24.73697 24.86073

119 Micronesia, Fed. Sts. 24.40224 24.53078 24.65937 24.78983

120 Moldova 24.73103 24.71636 24.70478 24.69535

121 Mongolia 23.49880 23.52186 23.54675 23.56861

122 Montenegro 25.50200 25.52961 25.54953 25.57340

123 Morocco 23.21760 23.29614 23.37691 23.45429

124 Mozambique 20.43321 20.45127 20.46667 20.47859

125 Myanmar 19.66279 19.69720 19.73897 19.78487

126 Namibia 21.08291 21.10802 21.13112 21.14890

127 Nauru 28.12449 28.35509 28.58248 28.81528

128 Nepal 20.96360 20.92431 20.88984 20.85290

129 Netherlands 24.12897 24.15129 24.17799 24.20056

130 Netherlands Antilles 24.61514 24.75996 24.89463 25.01301

131 New Zealand 25.26155 25.31869 25.37423 25.43056

132 Nicaragua 24.02412 24.08819 24.14205 24.19660

133 Niger 20.52134 20.56417 20.60781 20.64086

134 Nigeria 21.00792 21.04177 21.07423 21.09329

135 Norway 24.68457 24.73764 24.78809 24.83173

136 Oman 23.03985 23.12850 23.22638 23.33009

137 Pakistan 21.53642 21.54144 21.55069 21.56113

138 Palau 25.42376 25.55124 25.67951 25.81130

139 Panama 23.52611 23.60551 23.69240 23.77497

140 Papua New Guinea 21.76194 21.89020 22.01556 22.14111

141 Paraguay 23.40858 23.48692 23.56611 23.63013

142 Peru 23.03994 23.08686 23.12890 23.15487

143 Philippines 21.21647 21.28866 21.35576 21.42220

144 Poland 25.14062 25.15950 25.16896 25.18511

145 Portugal 25.04993 25.04398 25.04309 25.04187

146 Puerto Rico 24.80369 24.87429 24.94592 25.02585

147 Qatar 24.96196 25.06774 25.16338 25.23498

148 Romania 24.67017 24.69330 24.72487 24.75422

149 Russia 25.00430 25.00232 24.99679 24.99353

150 Rwanda 21.61922 21.66140 21.71239 21.76031

151 Saint Kitts and Nevis 25.26100 25.33652 25.40736 25.47582

152 Saint Lucia 22.82916 22.85923 22.88790 22.92127

153 Saint Vincent and the Grenadines 23.06618 23.11392 23.16536 23.21704

154 Samoa 25.83472 25.99935 26.15725 26.31038

155 Sao Tome and Principe 21.27399 21.31334 21.36899 21.41756

156 Saudi Arabia 25.02500 25.17207 25.30601 25.41727

157 Senegal 20.26700 20.31774 20.37281 20.41856

158 Serbia 25.60380 25.64709 25.68167 25.71951

159 Seychelles 22.15891 22.26575 22.36578 22.46072

160 Sierra Leone 21.36041 21.40767 21.45595 21.49821

161 Singapore 22.56816 22.63397 22.69746 22.76362

162 Slovak Republic 25.54614 25.58635 25.62135 25.65713

163 Slovenia 25.69628 25.73622 25.77252 25.80809

164 Solomon Islands 23.98967 24.11103 24.23121 24.34351

165 Somalia 20.92911 20.96415 20.99438 21.02672

166 South Africa 23.13811 23.17439 23.20612 23.23626

167 Spain 25.34477 25.37087 25.39528 25.41502

168 Sri Lanka 20.38152 20.44378 20.49434 20.54698

169 Sudan 20.71915 20.75761 20.79627 20.82779

170 Suriname 23.29584 23.36229 23.42391 23.48051

171 Swaziland 21.41393 21.44680 21.47732 21.49897

172 Sweden 24.71797 24.75768 24.79446 24.82977

173 Switzerland 25.15845 25.17901 25.20452 25.22270

174 Syria 24.34752 24.47281 24.59099 24.69695

175 Taiwan 22.40238 22.47259 22.54484 22.62341

176 Tajikistan 24.19187 24.21477 24.23035 24.25412

177 Tanzania 21.27393 21.30234 21.33163 21.36444

178 Thailand 20.26858 20.36836 20.46200 20.55553

179 Timor-Leste 19.92875 19.94611 19.95992 19.97382

180 Togo 20.90726 20.93318 20.95090 20.95109

181 Tonga 26.38245 26.53977 26.71129 26.87732

182 Trinidad and Tobago 24.81322 24.89256 24.96594 25.02672

183 Tunisia 22.19206 22.27883 22.36236 22.44939

184 Turkey 23.66064 23.72726 23.79751 23.86535

185 Turkmenistan 24.36178 24.39382 24.42410 24.45290

186 Uganda 21.26771 21.27590 21.30671 21.34758

187 Ukraine 24.91605 24.92332 24.93381 24.94412

188 United Arab Emirates 24.88388 25.07570 25.23880 25.36219

189 United Kingdom 24.72216 24.78911 24.86057 24.93208

190 United States 25.46406 25.57524 25.67883 25.78812

191 Uruguay 24.24001 24.31948 24.39260 24.44209

192 Uzbekistan 24.56500 24.60077 24.62187 24.64780

193 Vanuatu 23.20701 23.32990 23.46016 23.60431

194 Venezuela 24.58052 24.69666 24.80082 24.89208

195 Vietnam 19.01394 19.03902 19.06804 19.09675

196 West Bank and Gaza 24.31624 24.40192 24.48713 24.57107

197 Yemen, Rep. 22.90384 22.96813 23.02669 23.07279

198 Zambia 19.66295 19.69512 19.72538 19.75420

199 Zimbabwe 21.46989 21.48867 21.50738 21.52936

Y1984 Y1985 Y1986 Y1987 Y1988 Y1989 Y1990 Y1991

1 21.42734 21.41222 21.40132 21.37679 21.34018 21.29845 21.24818
21.20269

2 25.27901 25.28669 25.29451 25.30217 25.30450 25.31944 25.32357
25.28452

3 22.60633 22.69501 22.76979 22.84096 22.90644 22.97931 23.04600
23.11333

4 25.81874 25.85236 25.89089 25.93414 25.98477 26.04450 26.10936
26.17912

5 20.93569 20.94857 20.96030 20.98025 21.01375 21.05269 21.09007
21.12136

6 23.63584 23.73109 23.83449 23.93649 24.05364 24.16347 24.26782
24.36568

7 25.61271 25.66593 25.72364 25.78529 25.84428 25.88510 25.92482
25.99177

8 24.00181 24.04083 24.08736 24.13334 24.17219 24.19556 24.20618
24.19790

9 25.22894 25.31849 25.41017 25.50528 25.60001 25.70050 25.80568
25.90295

10 25.02208 25.06015 25.10680 25.14747 25.19333 25.24928 25.30882
25.37186

11 24.64121 24.67566 24.71906 24.75799 24.78894 24.82277 24.83167
24.83972

12 24.66558 24.78408 24.90724 25.03166 25.14778 25.26173 25.35641
25.44039

13 24.43174 24.53684 24.63328 24.74914 24.86604 24.98644 25.11479
25.25103

14 20.36524 20.32983 20.29654 20.26401 20.23497 20.20736 20.18246
20.15921

15 24.59913 24.64998 24.71728 24.77976 24.84265 24.90790 24.96113
25.00859

16 24.91640 24.92013 24.93057 24.94083 24.96638 24.99085 25.01652
25.05106

17 25.21949 25.25266 25.28532 25.32356 25.37574 25.42939 25.49029
25.55918

18 24.81656 24.85631 24.90216 24.95997 25.01621 25.08335 25.16254
25.23639

19 20.96054 21.00726 21.05137 21.07871 21.12584 21.16916 21.20891
21.25774

20 25.56404 25.69903 25.82431 25.94406 26.06962 26.19307 26.30429
26.40672

21 21.76640 21.75421 21.74839 21.75695 21.76646 21.78100 21.79810
21.81922

22 23.10750 23.13397 23.16541 23.20657 23.25603 23.30494 23.35095
23.39988

23 25.39811 25.42164 25.44097 25.44440 25.43763 25.41851 25.39629
25.34749

24 19.72270 19.77501 19.82815 19.89551 19.98147 20.07896 20.18715
20.30422

25 22.97890 23.07389 23.17442 23.27956 23.38452 23.49948 23.60242
23.71304

26 23.97016 24.02379 24.07072 24.13198 24.20123 24.26937 24.36658
24.49622

27 23.37014 23.39392 23.40646 23.41929 23.44076 23.45710 23.48593
23.50616

28 25.50580 25.55694 25.61303 25.66821 25.72108 25.77352 25.79169
25.78741

29 20.14327 20.17957 20.22333 20.25441 20.29278 20.31980 20.34378
20.37212

30 21.12775 21.14807 21.17456 21.19978 21.23035 21.24526 21.27423
21.30618

31 19.74852 19.77075 19.79420 19.81391 19.83981 19.86195 19.88134
19.90519

32 22.11848 22.21209 22.30308 22.35705 22.39403 22.42781 22.45710
22.48289

33 25.57519 25.66346 25.75539 25.85306 25.94492 26.04039 26.13240
26.22243

34 20.91738 20.99708 21.07982 21.19000 21.30276 21.39508 21.48587
21.57392

35 20.92022 20.89449 20.87539 20.85032 20.83262 20.82311 20.81775
20.81553

36 20.27327 20.31534 20.34928 20.37757 20.41912 20.46667 20.50477
20.54673

37 24.73825 24.79547 24.84530 24.89825 24.96211 25.04196 25.12311
25.21000

38 21.64363 21.67833 21.71745 21.76390 21.81317 21.85731 21.90382
21.95193

39 22.45181 22.54068 22.63499 22.73777 22.84228 22.94990 23.05701
23.16434

40 21.10763 21.14296 21.18685 21.24550 21.30362 21.36185 21.41916
21.47534

41 20.70142 20.69308 20.68853 20.68344 20.67990 20.67300 20.66681
20.65040

42 20.90094 20.96044 21.00631 21.05228 21.09124 21.12095 21.14711
21.16591

43 27.15532 27.40135 27.63931 27.86856 28.09469 28.31247 28.52606
28.74348

44 23.94700 24.02210 24.09956 24.18361 24.26875 24.37064 24.48617
24.60423

45 21.31013 21.34647 21.39242 21.43551 21.47739 21.52854 21.56519
21.60217

46 25.41073 25.44008 25.47011 25.50221 25.53267 25.56232 25.58771
25.58618

47 23.07165 23.16927 23.26024 23.34879 23.43399 23.51321 23.58502
23.63893

48 25.54387 25.60054 25.66655 25.72550 25.77662 25.84370 25.92588
25.99995

49 26.49958 26.54167 26.57995 26.62097 26.66796 26.71839 26.77285
26.80636

50 24.58269 24.59358 24.61120 24.62859 24.65583 24.68136 24.71040
24.74973

51 21.57510 21.65800 21.74279 21.82127 21.89558 21.96332 22.03327
22.08923

52 22.57613 22.63925 22.71689 22.82212 22.95088 23.06797 23.17038
23.27171

53 23.12295 23.16528 23.21672 23.27431 23.32603 23.38897 23.44034
23.48433

54 23.98012 24.02461 24.06992 24.10850 24.18380 24.25491 24.31515
24.37246

55 24.63365 24.72495 24.81456 24.90070 24.98559 25.06945 25.15310
25.23388

56 23.99645 24.05124 24.10831 24.16901 24.23836 24.31059 24.38845
24.47169

57 21.15667 21.16472 21.17019 21.18436 21.19979 21.21889 21.24399
21.26717

58 20.11151 20.12814 20.14323 20.15587 20.17161 20.18797 20.20741
20.23979

59 24.71732 24.72067 24.73069 24.74468 24.75588 24.77373 24.79018
24.79900

60 19.57007 19.57426 19.58084 19.58116 19.59220 19.59811 19.61111
19.61798

61 22.86411 23.01144 23.15024 23.27566 23.40989 23.53817 23.68988
23.83829

62 25.54429 25.56019 25.58275 25.61171 25.64807 25.69802 25.73860
25.77032

63 24.80748 24.82895 24.85285 24.87929 24.90935 24.94199 24.97491
25.01122

64 26.17356 26.37292 26.58224 26.79378 27.01086 27.21275 27.41426
27.62614

65 22.52077 22.58744 22.64612 22.68952 22.74415 22.80386 22.85174
22.91242

66 20.06460 20.08321 20.11353 20.15348 20.19417 20.24274 20.29888
20.35389

67 24.80930 24.85546 24.89456 24.93330 24.97082 25.00293 25.02149
25.00377

68 25.64293 25.69249 25.74425 25.79212 25.85154 25.91132 25.97675
26.05322

69 21.04529 21.07916 21.12201 21.16956 21.22088 21.27398 21.30206
21.36352

70 24.94193 24.97295 24.99539 25.01424 25.06154 25.10876 25.14763
25.18922

71 24.66469 24.69663 24.74168 24.78147 24.83124 24.88810 24.93611
24.98535

72 23.44967 23.50168 23.55609 23.62251 23.68593 23.74835 23.81588
23.88011

73 23.46354 23.52726 23.58663 23.64597 23.70560 23.77519 23.84902
23.92220

74 21.22866 21.24527 21.26469 21.28652 21.30961 21.34284 21.38083
21.42148

75 20.78623 20.83811 20.89059 20.93714 20.98369 21.04060 21.09450
21.14396

76 22.73863 22.73909 22.74348 22.75543 22.76465 22.76998 22.76845
22.77741

77 22.98937 23.00320 23.01128 23.01336 23.01286 23.01159 23.01501
23.02191

78 23.36687 23.42180 23.47703 23.53606 23.60608 23.67884 23.74195
23.80441

79 22.11127 22.23343 22.36179 22.49845 22.64054 22.78243 22.92726
23.07181

80 25.55388 25.61893 25.68529 25.75694 25.82174 25.88606 25.93988
25.96832

81 25.13832 25.20076 25.27223 25.33542 25.39311 25.45393 25.50969
25.57076

82 20.92134 20.88185 20.84291 20.80062 20.76272 20.72949 20.70240
20.67306

83 20.03233 20.07793 20.12761 20.17621 20.23084 20.29108 20.35126
20.41887

84 23.49059 23.57426 23.64439 23.70826 23.75791 23.81757 23.90194
23.99346

85 25.33199 25.40363 25.47775 25.55415 25.62027 25.68940 25.74914
25.71613

86 25.90272 25.92826 25.95512 25.98481 26.02015 26.06396 26.12140
26.18222

87 24.94352 24.98970 25.04481 25.10475 25.17435 25.23233 25.30622
25.37606

88 25.42456 25.43023 25.44088 25.45918 25.48011 25.50611 25.53778
25.57722

89 22.44398 22.46556 22.49161 22.53213 22.57322 22.61526 22.65921
22.70581

90 22.17225 22.18911 22.20966 22.23754 22.27578 22.31904 22.36753
22.42054

91 25.15302 25.28247 25.40708 25.52928 25.64378 25.72128 25.80050
25.88009

92 24.75603 24.80378 24.85316 24.89028 24.93086 24.96555 24.99543
25.01690

93 20.48854 20.52727 20.57398 20.61483 20.66073 20.71295 20.76428
20.81422

94 25.79347 25.88021 25.97192 26.06400 26.17248 26.27602 26.39606
26.52029

95 22.00332 22.05701 22.10736 22.15829 22.20420 22.24927 22.28636
22.31865

96 22.16327 22.19934 22.23220 22.29200 22.35878 22.43610 22.52903
22.62556

97 25.90140 25.99631 26.09362 26.18917 26.28548 26.39680 26.45012
26.52780

98 24.44845 24.46970 24.48991 24.50398 24.52412 24.53841 24.54697
24.53643

99 19.75092 19.78267 19.81244 19.84167 19.86999 19.90187 19.93683
19.96869

100 25.18238 25.20249 25.21924 25.23322 25.25345 25.28678 25.31766
25.33516

101 24.30688 24.44256 24.57106 24.69291 24.79828 24.87539 24.96990
25.11042

102 20.64601 20.64596 20.64452 20.64342 20.65339 20.66906 20.68597
20.69714

103 21.23418 21.26864 21.30005 21.33355 21.37133 21.37889 21.37232
21.38477

104 24.80350 24.88258 24.95610 25.02871 25.10423 25.17578 25.23568
25.30868

105 25.99007 25.98661 25.98031 25.97981 25.97800 25.97939 25.98296
25.98461

106 25.19478 25.25380 25.31911 25.38969 25.47533 25.56535 25.66131
25.76898

107 23.08299 23.18620 23.28912 23.39836 23.50617 23.61729 23.72873
23.83763

108 25.50533 25.52948 25.55564 25.56933 25.57418 25.57386 25.56535
25.55013

109 20.76609 20.78503 20.80859 20.83242 20.86045 20.88876 20.92158
20.95133

110 20.86300 20.87576 20.88920 20.89811 20.90349 20.90734 20.91860
20.93791

111 22.00053 22.10504 22.20184 22.29582 22.39520 22.49698 22.60640
22.71714

112 20.73497 20.83734 20.93894 21.03828 21.13978 21.24048 21.32886
21.41354

113 20.35725 20.37219 20.39957 20.42252 20.45123 20.48889 20.53095
20.57916

114 25.86289 25.90376 25.93342 25.97413 26.02576 26.08931 26.15002
26.23524

115 25.30169 25.45539 25.62721 25.81112 26.00013 26.19721 26.39335
26.59011

116 21.03823 21.07181 21.11438 21.16486 21.21562 21.26856 21.32159
21.37271

117 22.40026 22.50229 22.61191 22.73157 22.85638 22.98164 23.10631
23.23364

118 24.97602 25.09166 25.19845 25.29718 25.39259 25.48460 25.58431
25.69054

119 24.92259 25.06607 25.20833 25.34769 25.48999 25.62898 25.77362
25.92188

120 24.69167 24.68037 24.66774 24.65955 24.65856 24.65603 24.65421
24.63374

121 23.59294 23.61857 23.65152 23.68385 23.71549 23.74836 23.78044
23.79683

122 25.59635 25.61765 25.63735 25.65933 25.68741 25.71230 25.74268
25.76415

123 23.52726 23.60259 23.68938 23.76385 23.85318 23.94904 24.03563
24.13242

124 20.48482 20.47810 20.48316 20.50792 20.54160 20.58594 20.63906
20.68369

125 19.83216 19.87848 19.92212 19.95474 19.96996 19.97640 19.98742
19.99667

126 21.16460 21.17665 21.18981 21.20287 21.21441 21.22541 21.23260
21.25007

127 29.04548 29.28105 29.52002 29.75319 29.97877 30.20436 30.42198
30.63617

128 20.81872 20.78904 20.75913 20.72783 20.70202 20.67723 20.65819
20.64725

129 24.22622 24.25089 24.28017 24.31371 24.35609 24.40036 24.46741
24.53565

130 25.11061 25.19954 25.28359 25.36058 25.42579 25.51157 25.59446
25.67834

131 25.49691 25.56261 25.63663 25.71278 25.78555 25.85735 25.92780
25.98728

132 24.25427 24.30151 24.35246 24.39314 24.43531 24.47409 24.51608
24.55510

133 20.65010 20.64729 20.65594 20.66154 20.66368 20.66718 20.67435
20.67518

134 21.10216 21.11996 21.14383 21.16731 21.20638 21.26245 21.33302
21.42180

135 24.88225 24.93555 24.99121 25.05209 25.10225 25.15460 25.20980
25.26717

136 23.44716 23.56629 23.68203 23.79362 23.90753 24.02710 24.14473
24.26554

137 21.57176 21.58268 21.59759 21.61532 21.63534 21.65368 21.67267
21.69424

138 25.95121 26.09220 26.23760 26.38045 26.55388 26.73779 26.93610
27.13085

139 23.86279 23.95022 24.03780 24.13173 24.19482 24.26210 24.34073
24.42244

140 22.26208 22.38668 22.51598 22.64344 22.76684 22.89698 23.02485
23.15420

141 23.69463 23.76862 23.82157 23.87321 23.92801 23.98979 24.05131
24.12454

142 23.18981 23.23261 23.29090 23.36432 23.42941 23.46155 23.47687
23.49980

143 21.47510 21.51568 21.55869 21.60986 21.66246 21.72042 21.78691
21.84904

144 25.20527 25.22662 25.25539 25.28185 25.31771 25.35477 25.37587
25.39355

145 25.03374 25.03827 25.05478 25.09686 25.14198 25.20641 25.28416
25.36382

146 25.10865 25.19510 25.27972 25.37373 25.47403 25.58268 25.69013
25.80270

147 25.31202 25.38300 25.44971 25.51719 25.59487 25.67348 25.75640
25.84907

148 24.78878 24.81455 24.82589 24.82688 24.82019 24.80314 24.78799
24.75188

149 24.98785 24.98302 24.97976 24.96914 24.97129 24.97609 24.98775
24.99100

150 21.78135 21.81261 21.82631 21.83247 21.82560 21.84076 21.81502
21.79399

151 25.55506 25.63500 25.72520 25.82189 25.91584 26.00314 26.08753
26.17170

152 22.97072 23.01605 23.06768 23.11783 23.17762 23.24659 23.32514
23.40686

153 23.27733 23.33821 23.40612 23.47805 23.55157 23.62715 23.71626
23.79168

154 26.46727 26.64126 26.80807 26.98565 27.15731 27.31196 27.45165
27.57865

155 21.46420 21.51928 21.56152 21.60658 21.64982 21.69960 21.75361
21.80610

156 25.51095 25.57572 25.63769 25.69672 25.76424 25.82999 25.91673
26.01571

157 20.46449 20.51621 20.56741 20.61342 20.66175 20.70301 20.74356
20.79289

158 25.75549 25.78928 25.82077 25.85356 25.89123 25.92414 25.96170
25.99304

159 22.55543 22.66130 22.76010 22.86179 22.97205 23.09156 23.21328
23.34457

160 21.53877 21.57846 21.61450 21.65417 21.68635 21.71679 21.74587
21.77198

161 22.82848 22.88449 22.93952 22.99660 23.06131 23.12883 23.19591
23.26571

162 25.69851 25.73811 25.77931 25.81626 25.85951 25.90598 25.94697
25.97514

163 25.85281 25.88685 25.92372 25.95768 25.99316 26.03286 26.06808
26.09041

164 24.45388 24.56463 24.66985 24.77464 24.87843 24.99609 25.11838
25.24286

165 21.05783 21.08966 21.12220 21.15619 21.19051 21.23726 21.27975
21.31888

166 23.27040 23.30367 23.33707 23.37885 23.42474 23.47430 23.52675
23.58051

167 25.43313 25.46042 25.48971 25.53439 25.58617 25.65028 25.72032
25.79976

168 20.59544 20.63366 20.67478 20.70746 20.73936 20.77225 20.80921
20.85393

169 20.84730 20.86213 20.88240 20.90864 20.93535 20.96653 20.99367
21.03162

170 23.52685 23.57228 23.61061 23.64374 23.68688 23.73931 23.79644
23.87112

171 21.52619 21.55783 21.59290 21.63469 21.68481 21.74249 21.79222
21.83435

172 24.86689 24.90539 24.94952 24.99710 25.05041 25.10748 25.16444
25.21542

173 25.24600 25.26813 25.29805 25.32245 25.35413 25.38598 25.42673
25.46021

174 24.78259 24.86739 24.93725 24.99488 25.06755 25.11164 25.16734
25.23955

175 22.70801 22.78902 22.87436 22.96184 23.04687 23.13216 23.21114
23.29005

176 24.27539 24.29276 24.31117 24.31859 24.32583 24.31905 24.30014
24.26272

177 21.39463 21.41743 21.43652 21.45773 21.48072 21.50454 21.53365
21.56672

178 20.65286 20.75336 20.84919 20.95146 21.06203 21.18918 21.31953
21.45581

179 19.98943 20.00549 20.02296 20.03980 20.06136 20.08093 20.10669
20.14658

180 20.96319 20.97264 20.97971 20.98591 21.00101 21.02166 21.05222
21.07697

181 27.05085 27.22789 27.40442 27.58062 27.75135 27.91988 28.09517
28.26486

182 25.07835 25.11966 25.14045 25.15129 25.14310 25.12705 25.11359
25.11614

183 22.53428 22.62118 22.70853 22.79393 22.87136 22.95095 23.04268
23.13144

184 23.94047 24.02091 24.10812 24.20839 24.31877 24.43041 24.54882
24.66999

185 24.48779 24.50808 24.53527 24.55679 24.57425 24.58731 24.59178
24.57935

186 21.36312 21.37401 21.38591 21.40204 21.42637 21.45810 21.49764
21.53288

187 24.95250 24.95528 24.97105 24.98551 24.99758 25.01783 25.03725
25.05170

188 25.51162 25.63167 25.70268 25.79164 25.83178 25.90462 25.98216
26.06863

189 25.00774 25.08727 25.17483 25.26661 25.36885 25.47263 25.58043
25.68395

190 25.90690 26.02568 26.13740 26.25939 26.37687 26.49269 26.60827
26.71961

191 24.49525 24.54516 24.59804 24.67024 24.73972 24.80593 24.86952
24.95229

192 24.66890 24.69832 24.72305 24.74603 24.77115 24.78287 24.78404
24.77866

193 23.75134 23.89466 24.03171 24.15571 24.27529 24.39727 24.52964
24.66287

194 24.98440 25.07104 25.15587 25.24624 25.35274 25.43322 25.52678
25.63444

195 19.13046 19.16397 19.19740 19.23481 19.27090 19.31105 19.35150
19.39625

196 24.65582 24.74148 24.82984 24.91615 25.00108 25.08593 25.17834
25.27187

197 23.12566 23.16944 23.20933 23.25043 23.29401 23.33879 23.38236
23.42152

198 19.78070 19.80335 19.82396 19.85065 19.88320 19.92451 19.96680
20.00746

199 21.53383 21.54341 21.54859 21.54590 21.55396 21.56903 21.58005
21.59694

Y1992 Y1993 Y1994 Y1995 Y1996 Y1997 Y1998 Y1999

1 21.14238 21.06376 20.97987 20.91132 20.85155 20.81307 20.78591
20.75469

2 25.23077 25.21192 25.22115 25.25874 25.31097 25.33988 25.39116
25.46555

3 23.18776 23.25764 23.32273 23.39526 23.46811 23.54160 23.61592
23.69486

4 26.24017 26.30356 26.36793 26.43569 26.50769 26.58255 26.66337
26.75078

5 21.14987 21.13938 21.14186 21.16022 21.19076 21.22621 21.27082
21.31954

6 24.45644 24.54096 24.60945 24.66461 24.72544 24.78714 24.84936
24.91721

7 26.07642 26.17288 26.27872 26.37522 26.47182 26.57778 26.68714
26.79005

8 24.12982 24.05854 24.02297 24.01570 24.02627 24.03885 24.07100
24.11699

9 26.00624 26.10586 26.20077 26.29241 26.38256 26.47351 26.56314
26.65506

10 25.43668 25.50507 25.56626 25.61814 25.66410 25.71737 25.75996
25.81773

11 24.81781 24.76250 24.69113 24.61946 24.55527 24.49745 24.47179
24.47842

12 25.51294 25.58479 25.65514 25.72418 25.79938 25.89374 25.99417
26.12080

13 25.40173 25.56146 25.71611 25.87566 26.03138 26.18600 26.34294
26.50245

14 20.14118 20.12952 20.11823 20.10770 20.10489 20.11304 20.12622
20.13361

15 25.05249 25.09414 25.14401 25.20411 25.26850 25.35236 25.42067
25.51681

16 25.07413 25.09742 25.10406 25.10237 25.11362 25.14026 25.17221
25.20688

17 25.64048 25.70620 25.77927 25.84461 25.91482 25.98577 26.05275
26.12240

18 25.34573 25.45261 25.54387 25.64134 25.72576 25.80637 25.88939
25.97705

19 21.30311 21.35252 21.40226 21.45576 21.52050 21.58523 21.64874
21.71747

20 26.53011 26.65258 26.75763 26.88993 27.01108 27.12503 27.24352
27.34456

21 21.84349 21.87072 21.90149 21.93914 21.98528 22.03650 22.09205
22.14998

22 23.45185 23.50266 23.55810 23.61766 23.68542 23.75520 23.81981
23.88573

23 25.26577 25.17015 25.09667 25.07033 25.12328 25.22345 25.33549
25.44956

24 20.41434 20.50823 20.58939 20.66838 20.74696 20.82805 20.90699
20.99408

25 23.82606 23.92823 24.03524 24.14789 24.25992 24.37651 24.48850
24.60608

26 24.65423 24.83680 25.04243 25.26959 25.48898 25.70132 25.89812
26.08206

27 23.52962 23.55589 23.61052 23.64776 23.69483 23.75058 23.81059
23.84890

28 25.78690 25.78218 25.77516 25.78474 25.77704 25.76761 25.77903
25.80308

29 20.40300 20.43103 20.46465 20.49193 20.52809 20.56636 20.60729
20.66053

30 21.33931 21.35314 21.35172 21.34265 21.33228 21.31820 21.30669
21.30712

31 19.93750 19.96919 20.00377 20.03927 20.08239 20.12625 20.16351
20.21073

32 22.50597 22.53125 22.56063 22.59547 22.63932 22.69765 22.76663
22.83120

33 26.31568 26.40651 26.49979 26.58874 26.67114 26.75346 26.83631
26.91646

34 21.66202 21.74446 21.83323 21.95150 22.04010 22.13422 22.24215
22.35591

35 20.80177 20.78856 20.78073 20.78063 20.77539 20.78390 20.79623
20.81486

36 20.58760 20.61301 20.63280 20.66849 20.70319 20.74174 20.78687
20.83189

37 25.32067 25.43773 25.55295 25.66344 25.77917 25.88624 25.98953
26.08188

38 22.00604 22.07320 22.15110 22.23897 22.31367 22.38700 22.44676
22.49909

39 23.27852 23.39628 23.51334 23.63950 23.75218 23.86203 23.95979
24.05208

40 21.52733 21.57169 21.60407 21.63794 21.66373 21.68527 21.70443
21.72285

41 20.61508 20.55550 20.48951 20.40021 20.31166 20.22254 20.14174
20.05896

42 21.18663 21.20412 21.21799 21.23934 21.27222 21.30124 21.33138
21.35159

43 28.96110 29.18297 29.40326 29.61475 29.82420 30.02693 30.23299
30.44719

44 24.73446 24.84882 24.95523 25.05350 25.14893 25.24253 25.33913
25.45658

45 21.64058 21.67979 21.70943 21.75006 21.80476 21.85798 21.91746
21.97590

46 25.57456 25.55173 25.55107 25.57994 25.61993 25.66831 25.72217
25.78556

47 23.67952 23.68752 23.70158 23.71862 23.75730 23.80301 23.86160
23.94593

48 26.09039 26.18266 26.25772 26.36080 26.43776 26.52202 26.60921
26.69027

49 26.84969 26.89619 26.93426 26.98314 27.04343 27.10100 27.16112
27.22247

50 24.80236 24.85176 24.90462 24.96431 25.02533 25.09952 25.17054
25.24724

51 22.14750 22.21000 22.26702 22.33623 22.39746 22.45329 22.50722
22.56731

52 23.37355 23.46711 23.53829 23.61304 23.70171 23.79924 23.88361
23.96444

53 23.53831 23.60267 23.67182 23.73003 23.79631 23.87457 23.96611
24.05981

54 24.44259 24.50867 24.58842 24.65281 24.71664 24.79187 24.84832
24.91341

55 25.31826 25.40298 25.48856 25.57944 25.67577 25.76764 25.86074
25.95852

56 24.56273 24.65915 24.75942 24.86310 24.96370 25.07297 25.18381
25.30405

57 21.29670 21.33208 21.35662 21.40690 21.47658 21.61891 21.77227
21.96034

58 20.28294 20.32333 20.38827 20.45346 20.52008 20.58793 20.65244
20.70602

59 24.79527 24.79123 24.79648 24.82701 24.88001 24.94357 25.02112
25.12637

60 19.63097 19.64647 19.66306 19.68413 19.71305 19.74240 19.76632
19.79587

61 23.98230 24.13829 24.28999 24.44879 24.61446 24.77189 24.93184
25.08671

62 25.80032 25.82563 25.85309 25.87877 25.90909 25.94636 25.98993
26.03724

63 25.05716 25.09455 25.13114 25.17051 25.20739 25.24361 25.28337
25.32587

64 27.84075 28.04665 28.24191 28.44179 28.62167 28.80280 28.98991
29.18193

65 22.97127 23.03261 23.09335 23.15467 23.22810 23.30589 23.38905
23.45478

66 20.41435 20.48088 20.53630 20.58593 20.63716 20.69583 20.76738
20.84354

67 24.92825 24.82921 24.73249 24.65405 24.61017 24.59323 24.60131
24.61786

68 26.14012 26.20839 26.27577 26.34132 26.41410 26.48539 26.55047
26.61048

69 21.42402 21.49269 21.56186 21.64113 21.73307 21.82109 21.90907
21.99521

70 25.24259 25.28895 25.34534 25.38483 25.43099 25.48494 25.53608
25.60453

71 25.02616 25.06717 25.11891 25.18005 25.23576 25.30131 25.36390
25.42475

72 23.93367 23.98792 24.05428 24.11636 24.18421 24.24889 24.32500
24.40094

73 23.99349 24.06859 24.14395 24.22730 24.30849 24.39249 24.47797
24.56244

74 21.47000 21.52042 21.56541 21.61652 21.66950 21.72217 21.78149
21.84375

75 21.17416 21.19819 21.23877 21.28187 21.33048 21.38461 21.38489
21.39546

76 22.80459 22.84753 22.90881 22.97709 23.05076 23.12913 23.19851
23.27014

77 23.01622 23.01219 23.00373 23.01138 23.02365 23.04808 23.08169
23.12460

78 23.87519 23.95347 24.02490 24.09955 24.18044 24.26988 24.34796
24.41586

79 23.22325 23.37374 23.52496 23.66960 23.80513 23.93306 24.04084
24.14409

80 25.99537 26.02490 26.05337 26.07566 26.10413 26.13989 26.19210
26.24871

81 25.63281 25.69722 25.77402 25.84124 25.91334 25.99882 26.09548
26.19390

82 20.64642 20.62593 20.61725 20.62203 20.63797 20.66520 20.69815
20.74060

83 20.49719 20.57903 20.66926 20.76345 20.85661 20.94721 21.01366
21.07734

84 24.09265 24.19475 24.30065 24.40843 24.51378 24.61608 24.70879
24.78711

85 25.71062 25.73522 25.76909 25.78760 25.84621 25.88685 25.96694
26.08411

86 26.25085 26.31231 26.38027 26.45337 26.54485 26.65412 26.76096
26.86328

87 25.45771 25.53842 25.61811 25.71673 25.83036 25.94161 26.04805
26.15018

88 25.61943 25.65440 25.69556 25.73105 25.77075 25.80452 25.84628
25.89138

89 22.75759 22.82344 22.89494 22.96110 23.03603 23.10743 23.17743
23.25101

90 22.48151 22.54894 22.62295 22.70061 22.78450 22.86718 22.93991
23.00911

91 25.97150 26.07142 26.17154 26.27064 26.35048 26.44347 26.53386
26.61774

92 25.03312 25.03165 25.01606 24.99333 24.97532 24.96995 24.98548
25.02408

93 20.85751 20.89796 20.93270 20.96952 21.00601 21.04325 21.08762
21.13181

94 26.64841 26.78385 26.93106 27.07819 27.24093 27.40715 27.58718
27.78224

95 22.33416 22.34280 22.32529 22.28610 22.23183 22.17696 22.12870
22.08971

96 22.71199 22.78586 22.85881 22.94119 23.03472 23.11659 23.19187
23.27742

97 26.65572 26.83413 27.02469 27.21557 27.40334 27.57843 27.73497
27.88174

98 24.51208 24.45599 24.38295 24.30610 24.24907 24.21422 24.20921
24.20643

99 20.00568 20.05038 20.10266 20.15559 20.20878 20.26491 20.32028
20.38000

100 25.31612 25.29426 25.27586 25.27005 25.28771 25.31835 25.35780
25.41413

101 25.24546 25.37992 25.50984 25.65785 25.80689 25.96556 26.10938
26.24877

102 20.71191 20.73445 20.76178 20.79940 20.84460 20.89856 20.95402
21.01332

103 21.39278 21.39555 21.40775 21.41723 21.43646 21.47413 21.50622
21.54662

104 25.37987 25.45129 25.52624 25.59521 25.66955 25.74354 25.81026
25.86860

105 25.95745 25.91784 25.86401 25.83189 25.82294 25.83361 25.86464
25.90548

106 25.88519 25.98781 26.09424 26.18726 26.28181 26.37856 26.47301
26.57184

107 23.95554 24.07472 24.19368 24.30920 24.41917 24.51903 24.60659
24.68031

108 25.52933 25.50323 25.50643 25.51704 25.53988 25.56424 25.61423
25.67776

109 20.97571 20.99956 21.01822 21.03670 21.05489 21.07619 21.09783
21.12003

110 20.94862 20.97348 20.99899 21.04616 21.10198 21.16561 21.23388
21.31075

111 22.83756 22.96548 23.09928 23.24460 23.39285 23.53373 23.64981
23.76383

112 21.50514 21.61515 21.72258 21.81634 21.91005 22.00691 22.11027
22.20688

113 20.63152 20.67800 20.72976 20.77477 20.82456 20.88091 20.94695
21.01837

114 26.32343 26.41604 26.50236 26.60634 26.69914 26.79132 26.88889
26.98558

115 26.77802 26.96030 27.14187 27.32525 27.48536 27.63951 27.78486
27.93394

116 21.42490 21.48606 21.54433 21.61680 21.68749 21.75554 21.81767
21.89184

117 23.36001 23.48322 23.60584 23.71886 23.82652 23.92989 24.03661
24.14182

118 25.79848 25.90837 26.02117 26.11915 26.22286 26.32961 26.43387
26.53752

119 26.07245 26.22206 26.37687 26.53033 26.67402 26.80811 26.94028
27.05913

120 24.57371 24.52099 24.41854 24.30591 24.20170 24.11505 24.02066
23.93918

121 23.79353 23.79059 23.79410 23.80494 23.81547 23.84189 23.88370
23.93297

122 25.76374 25.70893 25.66753 25.64686 25.68660 25.73129 25.78081
25.81960

123 24.22001 24.30474 24.39779 24.47190 24.55772 24.64174 24.72833
24.80851

124 20.71624 20.75391 20.79259 20.82918 20.87000 20.92308 20.98645
21.05083

125 20.01802 20.05130 20.09014 20.13908 20.19545 20.25928 20.32560
20.39798

126 21.27006 21.28986 21.31720 21.34968 21.38736 21.44053 21.50213
21.57426

127 30.84639 31.04119 31.23113 31.41477 31.59122 31.76624 31.94707
32.13097

128 20.63693 20.63084 20.63165 20.63472 20.63549 20.64214 20.64776
20.65933

129 24.61928 24.69735 24.76790 24.84707 24.92677 25.00139 25.08457
25.17431

130 25.76481 25.87287 25.98254 26.10876 26.23626 26.36881 26.50441
26.63572

131 26.05001 26.12349 26.20156 26.28952 26.38163 26.46966 26.54919
26.64585

132 24.60781 24.65470 24.70176 24.75597 24.80855 24.86823 24.94007
25.02261

133 20.67278 20.67461 20.68006 20.69191 20.70413 20.72050 20.75920
20.79823

134 21.51588 21.61643 21.70705 21.79146 21.87817 21.96262 22.04579
22.13099

135 25.33276 25.40433 25.49028 25.57453 25.67179 25.77152 25.87428
25.97399

136 24.38626 24.51702 24.64511 24.78063 24.90626 25.02654 25.15218
25.26009

137 21.72510 21.75977 21.79347 21.83634 21.87969 21.91376 21.94951
21.98501

138 27.32420 27.51336 27.70460 27.90584 28.11214 28.31536 28.51126
28.69487

139 24.50784 24.59741 24.68749 24.78475 24.88972 24.99820 25.11160
25.22942

140 23.28480 23.43394 23.59245 23.73647 23.86733 23.99009 24.11004
24.22417

141 24.19453 24.27485 24.35741 24.44485 24.53223 24.61662 24.69241
24.77588

142 23.51614 23.54635 23.59906 23.66987 23.74694 23.83509 23.92300
24.01365

143 21.91127 21.97304 22.04148 22.10968 22.18426 22.25555 22.30886
22.36491

144 25.42163 25.45525 25.48839 25.53633 25.59576 25.66453 25.74525
25.83350

145 25.44172 25.52125 25.59756 25.67780 25.75557 25.82777 25.90605
25.99047

146 25.92082 26.04660 26.17938 26.32539 26.47035 26.62131 26.77866
26.94262

147 25.95368 26.06332 26.17688 26.29329 26.41204 26.54693 26.69291
26.84067

148 24.70036 24.66560 24.63574 24.62790 24.63848 24.63866 24.64353
24.65689

149 24.98536 24.98602 24.97425 24.96507 24.95205 24.95279 24.95298
24.97309

150 21.79264 21.78895 21.71451 21.71504 21.71962 21.73684 21.77367
21.82058

151 26.25930 26.35119 26.45641 26.57601 26.69849 26.81985 26.93852
27.06626

152 23.49037 23.57300 23.65405 23.73497 23.80912 23.88018 23.95697
24.02473

153 23.87487 23.95685 24.01646 24.08867 24.15437 24.23214 24.30362
24.38506

154 27.67714 27.80065 27.90823 28.03800 28.19742 28.36491 28.54905
28.73785

155 21.86141 21.92185 21.99450 22.06417 22.13677 22.23617 22.33400
22.42935

156 26.12018 26.22935 26.33868 26.45034 26.55977 26.66882 26.77904
26.88356

157 20.84855 20.90822 20.96130 21.01431 21.06393 21.12464 21.18605
21.25350

158 25.99561 25.95303 25.92375 25.90583 25.92565 25.95209 25.98264
25.98488

159 23.48498 23.62919 23.77534 23.90865 24.04069 24.18047 24.32030
24.44887

160 21.78860 21.80850 21.84373 21.87518 21.90497 21.91602 21.91706
21.90284

161 23.32999 23.40270 23.47382 23.54164 23.60396 23.65914 23.70100
23.73247

162 25.99551 26.01680 26.04675 26.08351 26.13178 26.19109 26.26112
26.30941

163 26.10641 26.14656 26.20079 26.26542 26.34704 26.42509 26.50649
26.58650

164 25.37952 25.51425 25.64945 25.79141 25.93356 26.06930 26.19822
26.31477

165 21.35827 21.39259 21.42431 21.44441 21.46899 21.49611 21.52228
21.54537

166 23.63539 23.69439 23.76762 23.85642 23.96304 24.09036 24.23022
24.39328

167 25.88464 25.96412 26.04306 26.12167 26.20999 26.30220 26.39609
26.50000

168 20.90149 20.95994 21.02658 21.09320 21.16420 21.23943 21.31520
21.38576

169 21.07525 21.12529 21.17918 21.23783 21.29703 21.36275 21.43225
21.49895

170 23.94219 24.01218 24.07298 24.13357 24.20795 24.30276 24.40073
24.50072

171 21.87637 21.91338 21.94854 21.98135 22.02255 22.07354 22.13207
22.20111

172 25.26597 25.31753 25.37889 25.43743 25.49521 25.56026 25.62147
25.68738

173 25.50033 25.54019 25.57968 25.61801 25.66158 25.69975 25.73992
25.77055

174 25.32346 25.41595 25.52016 25.62992 25.75749 25.87469 25.99952
26.11749

175 23.37324 23.45302 23.53399 23.61526 23.69346 23.77188 23.84441
23.91390

176 24.18024 24.08605 23.96471 23.84028 23.70978 23.59187 23.48205
23.39624

177 21.59534 21.61958 21.64031 21.65659 21.67487 21.71586 21.75849
21.80313

178 21.59724 21.74154 21.88441 22.03004 22.16708 22.28385 22.36538
22.43802

179 20.19698 20.25745 20.32359 20.39477 20.46321 20.53556 20.59645
20.60753

180 21.09815 21.11306 21.14536 21.18566 21.23926 21.28900 21.33483
21.38407

181 28.43514 28.60130 28.76827 28.94029 29.11615 29.28199 29.44018
29.60169

182 25.12136 25.12806 25.15276 25.18803 25.23361 25.28595 25.34881
25.42055

183 23.23761 23.34740 23.45644 23.55951 23.67153 23.79291 23.91893
24.05655

184 24.79153 24.91986 25.03051 25.14651 25.27038 25.39673 25.51746
25.62130

185 24.55385 24.53719 24.49877 24.45991 24.41998 24.37632 24.34956
24.35392

186 21.55733 21.59188 21.63840 21.69042 21.73546 21.78184 21.83446
21.88065

187 25.05866 25.04840 24.99754 24.93999 24.87676 24.82352 24.77336
24.73059

188 26.16562 26.26360 26.39207 26.51119 26.64237 26.76028 26.86474
26.97721

189 25.79325 25.90392 26.01879 26.12699 26.23783 26.34611 26.44777
26.55022

190 26.83609 26.95163 27.06838 27.17810 27.28376 27.39366 27.49846
27.60386

191 25.05527 25.15742 25.26958 25.36804 25.47642 25.58248 25.68818
25.78625

192 24.75026 24.73165 24.71118 24.69517 24.67727 24.68203 24.69876
24.72082

193 24.79143 24.92541 25.05856 25.19282 25.32325 25.45811 25.59565
25.72398

194 25.75528 25.87036 25.97218 26.08046 26.18272 26.29177 26.40105
26.50035

195 19.45212 19.51493 19.58757 19.66996 19.75854 19.84794 19.93580
20.02081

196 25.37683 25.48893 25.61249 25.73496 25.87428 26.01468 26.15144
26.28240

197 23.46544 23.51371 23.56154 23.61684 23.66973 23.72737 23.79152
23.85482

198 20.04096 20.07781 20.09502 20.09977 20.11009 20.12375 20.13349
20.15094

199 21.59010 21.58547 21.59029 21.58986 21.60362 21.62721 21.65496
21.68873

Y2000 Y2001 Y2002 Y2003 Y2004 Y2005 Y2006 Y2007

1 20.69521 20.62643 20.59848 20.58706 20.57759 20.58084 20.58749
20.60246

2 25.55835 25.66701 25.77167 25.87274 25.98136 26.08939 26.20867
26.32753

3 23.77659 23.86256 23.95294 24.05243 24.15957 24.27001 24.38270
24.48846

4 26.83179 26.92373 27.02525 27.12481 27.23107 27.32827 27.43588
27.53363

5 21.37480 21.43664 21.51765 21.59924 21.69218 21.80564 21.93881
22.08962

6 24.99158 25.05857 25.13039 25.20713 25.29898 25.39965 25.51382
25.64247

7 26.88103 26.96067 26.99882 27.04738 27.11001 27.18941 27.28179
27.38889

8 24.18045 24.26670 24.37698 24.50332 24.64178 24.81447 24.99160
25.17590

9 26.74486 26.84397 26.93858 27.03801 27.13871 27.24614 27.35267
27.45878

10 25.87471 25.93806 25.99583 26.06356 26.14360 26.21107 26.29374
26.38136

11 24.51287 24.57202 24.66021 24.77164 24.89376 25.06256 25.25706
25.45513

12 26.25748 26.38653 26.51184 26.62607 26.75612 26.88517 27.00715
27.12653

13 26.65409 26.80388 26.94923 27.09298 27.23908 27.38693 27.53868
27.68865

14 20.14774 20.16802 20.18621 20.20948 20.23957 20.27648 20.31554
20.35493

15 25.60292 25.68910 25.77615 25.87020 25.95660 26.06074 26.16874
26.27575

16 25.25472 25.32148 25.40160 25.48133 25.58449 25.70824 25.85820
26.01110

17 26.18388 26.24196 26.30602 26.37453 26.44661 26.51575 26.59522
26.67529

18 26.08213 26.19233 26.30847 26.43920 26.56389 26.68025 26.80065
26.90962

19 21.79710 21.87272 21.95309 22.02760 22.10390 22.17929 22.25322
22.33366

20 27.45476 27.55826 27.66492 27.76999 27.87082 27.98684 28.12057
28.26753

21 22.21076 22.26991 22.33607 22.40769 22.48194 22.55711 22.63300
22.72221

22 23.95185 24.01547 24.08033 24.14039 24.20067 24.26262 24.31851
24.37227

23 25.57757 25.71444 25.84310 25.97224 26.11931 26.25022 26.37229
26.49206

24 21.09464 21.19850 21.31605 21.43809 21.56543 21.69989 21.83982
21.98606

25 24.73196 24.84949 24.97064 25.09147 25.21990 25.34959 25.48902
25.63555

26 26.26016 26.41788 26.56046 26.66719 26.78915 26.91179 27.03094
27.16578

27 23.87813 23.90486 23.93406 23.97980 24.02261 24.06445 24.09869
24.13907

28 25.84258 25.89594 25.95657 26.03088 26.11251 26.20561 26.30869
26.42397

29 20.70895 20.75999 20.81927 20.88506 20.95357 21.02654 21.10561
21.18575

30 21.29665 21.30016 21.31762 21.33669 21.36172 21.38838 21.42011
21.45897

31 20.25863 20.31227 20.36407 20.42144 20.48485 20.55831 20.63655
20.72057

32 22.90632 22.98135 23.07282 23.16918 23.27218 23.37502 23.47444
23.57521

33 26.99336 27.06234 27.12542 27.18538 27.24205 27.29581 27.35018
27.40416

34 22.47423 22.59267 22.71017 22.83106 22.95363 23.07864 23.22111
23.36939

35 20.83702 20.86100 20.88060 20.88965 20.90453 20.92015 20.94058
20.96435

36 20.86887 20.91294 20.96196 21.02777 21.12698 21.22857 21.32338
21.40464

37 26.17741 26.26824 26.36532 26.46749 26.57109 26.67952 26.79366
26.90237

38 22.54068 22.57822 22.61654 22.65637 22.69719 22.74628 22.80042
22.86161

39 24.14347 24.23406 24.32036 24.40818 24.49940 24.59634 24.70577
24.82307

40 21.74088 21.76273 21.79129 21.82661 21.86940 21.91364 21.96340
22.01198

41 19.97498 19.89845 19.83696 19.80717 19.78927 19.78781 19.80180
19.82910

42 21.38374 21.42314 21.47048 21.51900 21.57437 21.64382 21.72486
21.79519

43 30.68088 30.92207 31.16078 31.41451 31.66918 31.92132 32.17190
32.42350

44 25.56878 25.67900 25.78377 25.88441 25.98928 26.10699 26.23096
26.35650

45 22.03598 22.09198 22.15328 22.21676 22.28061 22.34639 22.41761
22.48889

46 25.85519 25.93817 26.03011 26.12982 26.21837 26.30989 26.39597
26.49896

47 24.05065 24.16575 24.26055 24.39186 24.52858 24.65646 24.79302
24.93192

48 26.77099 26.84331 26.92450 26.99325 27.07204 27.15274 27.24326
27.32855

49 27.28216 27.34798 27.41303 27.48463 27.56048 27.63067 27.73361
27.81401

50 25.33594 25.42577 25.52596 25.62415 25.72962 25.82771 25.92875
26.03329

51 22.63424 22.70345 22.77671 22.85583 22.94165 23.04275 23.15419
23.26892

52 24.05267 24.12374 24.18375 24.24105 24.30642 24.37049 24.43348
24.50453

53 24.15264 24.26207 24.38454 24.51173 24.63408 24.76461 24.90856
25.05235

54 24.96302 25.02230 25.09470 25.16315 25.24706 25.33264 25.41453
25.49568

55 26.05777 26.15256 26.24082 26.32384 26.40268 26.48005 26.56054
26.64671

56 25.43048 25.55340 25.67399 25.78960 25.89710 26.00695 26.12564
26.24783

57 22.14823 22.37332 22.59892 22.81279 23.04308 23.25296 23.43077
23.60238

58 20.73423 20.76801 20.79514 20.81538 20.83535 20.85448 20.86087
20.86923

59 25.22421 25.33714 25.45733 25.58138 25.71923 25.85257 25.98743
26.13144

60 19.82768 19.86357 19.89855 19.92608 19.96905 20.02382 20.08834
20.16319

61 25.23879 25.39149 25.55150 25.71604 25.88463 26.05042 26.22081
26.37474

62 26.09098 26.15458 26.22336 26.29856 26.37982 26.46406 26.55016
26.64191

63 25.37416 25.42911 25.49014 25.54863 25.60759 25.66854 25.72756
25.79057

64 29.37214 29.56011 29.74904 29.93783 30.12372 30.30850 30.49157
30.67857

65 23.51540 23.57320 23.62414 23.68267 23.74528 23.81530 23.89335
23.98256

66 20.91996 21.00113 21.07306 21.15780 21.25230 21.34863 21.44274
21.54302

67 24.65540 24.71795 24.79837 24.90761 25.02260 25.15806 25.27708
25.41457

68 26.67425 26.72962 26.78618 26.84581 26.90287 26.96115 27.02184
27.09050

69 22.08191 22.16325 22.24690 22.32978 22.41644 22.51645 22.62040
22.73069

70 25.66926 25.74295 25.82012 25.90066 25.99356 26.07865 26.16494
26.25289

71 25.49719 25.56386 25.63414 25.70048 25.76241 25.83021 25.88646
25.94868

72 24.48022 24.55684 24.64323 24.73372 24.81219 24.90676 24.98739
25.08222

73 24.64744 24.72662 24.80671 24.88390 24.96091 25.04007 25.12426
25.20987

74 21.90431 21.96945 22.03964 22.11533 22.19452 22.27405 22.35562
22.43725

75 21.43209 21.44340 21.45472 21.47358 21.49230 21.51679 21.54966
21.59109

76 23.34875 23.42045 23.46826 23.50962 23.54778 23.58721 23.61695
23.64781

77 23.17348 23.22320 23.27578 23.32960 23.38565 23.44359 23.50879
23.58323

78 24.48024 24.54868 24.62025 24.68800 24.76042 24.84076 24.92453
25.01546

79 24.24734 24.34116 24.43015 24.51804 24.61484 24.72025 24.83090
24.94447

80 26.32296 26.40176 26.48809 26.57555 26.68557 26.78605 26.90203
27.00873

81 26.29702 26.39685 26.50299 26.61204 26.73403 26.85805 26.97796
27.09734

82 20.77932 20.81119 20.83562 20.85550 20.87218 20.88994 20.91145
20.93488

83 21.14825 21.22000 21.29583 21.37829 21.46416 21.55427 21.64688
21.74807

84 24.85189 24.90839 24.96062 24.99582 25.05111 25.11463 25.17429
25.24163

85 26.18983 26.31219 26.41797 26.45662 26.49992 26.53882 26.58597
26.64623

86 26.96904 27.07264 27.17342 27.26380 27.34373 27.41975 27.48572
27.57676

87 26.26250 26.37810 26.49152 26.59689 26.70230 26.81523 26.91824
27.02232

88 25.94303 25.99564 26.05786 26.11983 26.19245 26.26249 26.33693
26.40849

89 23.32343 23.40351 23.48137 23.56227 23.64944 23.73732 23.82337
23.91519

90 23.07719 23.13928 23.19359 23.24493 23.29598 23.34532 23.39421
23.44693

91 26.71033 26.80006 26.89672 26.97629 27.07908 27.17381 27.27590
27.37429

92 25.09305 25.19051 25.31124 25.44805 25.60121 25.76711 25.93951
26.11979

93 21.16970 21.20768 21.24814 21.28430 21.33211 21.38233 21.44531
21.51645

94 27.97350 28.15224 28.32844 28.49638 28.65407 28.80720 28.95385
29.09752

95 22.06108 22.03698 22.02024 22.00924 22.00605 22.00731 22.00708
22.01135

96 23.37520 23.46793 23.55274 23.64225 23.71901 23.78490 23.85106
23.92079

97 28.03291 28.16929 28.26425 28.38786 28.52341 28.67629 28.83975
29.00300

98 24.22082 24.25526 24.29772 24.35925 24.43839 24.51638 24.58982
24.66600

99 20.44315 20.50587 20.57241 20.64257 20.71752 20.79999 20.88963
20.98242

100 25.48263 25.56402 25.67228 25.78197 25.90648 26.04137 26.19151
26.32953

101 26.36601 26.48124 26.58461 26.69645 26.80757 26.90386 26.98947
27.09268

102 21.07902 21.15073 21.22586 21.31467 21.41338 21.51798 21.63691
21.76567

103 21.60139 21.65415 21.71408 21.72496 21.74375 21.76799 21.79850
21.84234

104 25.92907 25.99243 26.05284 26.12052 26.19720 26.27448 26.35506
26.44751

105 25.97347 26.06024 26.15035 26.25435 26.37283 26.49493 26.61939
26.74333

106 26.66440 26.75076 26.84210 26.93574 27.03119 27.12382 27.22776
27.33210

107 24.75673 24.82586 24.90383 24.99584 25.11858 25.24306 25.38320
25.54498

108 25.74675 25.79818 25.85252 25.92015 25.99986 26.07165 26.15740
26.25277

109 21.14569 21.17412 21.18056 21.19548 21.21640 21.24992 21.29165
21.34370

110 21.38712 21.45321 21.51781 21.58806 21.66330 21.73955 21.82693
21.92539

111 23.87947 23.98722 24.08880 24.19118 24.29169 24.39334 24.50300
24.61322

112 22.30609 22.39307 22.48262 22.57956 22.69181 22.79395 22.93190
23.07533

113 21.08027 21.15852 21.23538 21.32541 21.41081 21.50232 21.59780
21.69203

114 27.07791 27.16484 27.24103 27.31940 27.39609 27.46856 27.54120
27.60792

115 28.08491 28.23885 28.39540 28.55544 28.72246 28.88675 29.04784
29.21093

116 21.96901 22.04644 22.12388 22.19542 22.27490 22.35387 22.44672
22.53522

117 24.25019 24.36163 24.47135 24.58312 24.69464 24.80830 24.92287
25.03885

118 26.64478 26.74807 26.84663 26.94203 27.03794 27.13567 27.23219
27.32899

119 27.18218 27.30293 27.42871 27.54716 27.66177 27.77213 27.88686
27.99366

120 23.90064 23.86770 23.87107 23.89259 23.92992 23.99155 24.07066
24.14999

121 23.98707 24.05100 24.12177 24.20976 24.31712 24.43532 24.56507
24.71713

122 25.85950 25.91759 25.98394 26.07903 26.17555 26.25773 26.34725
26.44582

123 24.88582 24.96542 25.05147 25.13929 25.22994 25.31940 25.42322
25.52608

124 21.11392 21.19397 21.28235 21.37949 21.48161 21.59168 21.70539
21.81930

125 20.47997 20.57011 20.67094 20.78169 20.90676 21.04131 21.18272
21.32024

126 21.66432 21.75061 21.84144 21.94967 22.07364 22.20702 22.34933
22.49870

127 32.31834 32.50635 32.70215 32.89697 33.09517 33.29640 33.49282
33.69373

128 20.67479 20.69141 20.70203 20.71377 20.72315 20.73189 20.73895
20.74963

129 25.26476 25.35808 25.45318 25.53967 25.62767 25.72061 25.81805
25.91880

130 26.76995 26.88983 27.00248 27.11191 27.23803 27.35193 27.46039
27.58046

131 26.75492 26.87056 26.99480 27.11813 27.24742 27.38210 27.51091
27.64444

132 25.10603 25.18950 25.26476 25.33901 25.42519 25.50722 25.59272
25.68266

133 20.82732 20.85903 20.89746 20.94246 20.97408 21.02509 21.08073
21.14583

134 22.21424 22.29861 22.37732 22.47019 22.57170 22.68060 22.79538
22.91228

135 26.07561 26.17836 26.28499 26.39151 26.50614 26.61797 26.72222
26.83126

136 25.36880 25.48419 25.58856 25.68600 25.78828 25.89545 26.00377
26.12140

137 22.01724 22.04435 22.06815 22.09327 22.12042 22.15676 22.20030
22.24841

138 28.86910 29.04586 29.21880 29.39326 29.57591 29.76823 29.96297
30.16934

139 25.34018 25.44021 25.54370 25.64547 25.75525 25.86856 25.99121
26.12567

140 24.32653 24.42179 24.50827 24.59360 24.67095 24.75387 24.83114
24.92197

141 24.84526 24.92018 24.99871 25.08099 25.16125 25.24504 25.33655
25.43538

142 24.10617 24.18814 24.27281 24.35174 24.42612 24.50203 24.58439
24.67405

143 22.42190 22.46598 22.51297 22.56001 22.61532 22.67081 22.73129
22.80070

144 25.92540 26.01650 26.10348 26.18799 26.27893 26.37137 26.47001
26.57013

145 26.07041 26.14950 26.23559 26.31265 26.39127 26.46130 26.53228
26.60810

146 27.10872 27.27551 27.43545 27.59733 27.76338 27.92199 28.08172
28.22804

147 26.98686 27.12452 27.26179 27.40511 27.55011 27.69226 27.83362
27.98678

148 24.68514 24.73358 24.79496 24.87472 24.96144 25.06320 25.17666
25.28747

149 25.01720 25.08625 25.17367 25.28208 25.40880 25.54944 25.69557
25.85350

150 21.87056 21.91962 22.00366 22.09058 22.17715 22.26357 22.35369
22.45160

151 27.19905 27.32119 27.44162 27.56483 27.69350 27.81906 27.94909
28.08559

152 24.09073 24.13984 24.19099 24.25605 24.32437 24.40291 24.48682
24.56844

153 24.47418 24.57098 24.68569 24.80068 24.92831 25.05374 25.18827
25.31760

154 28.93492 29.13945 29.34069 29.53503 29.72547 29.90551 30.08890
30.26044

155 22.53154 22.64028 22.75203 22.86699 22.98085 23.10325 23.23616
23.37208

156 26.99168 27.09600 27.19191 27.30168 27.41224 27.52896 27.64713
27.76440

157 21.32190 21.38834 21.44909 21.51800 21.59394 21.67412 21.75457
21.84124

158 25.99052 26.02009 26.05982 26.12686 26.20059 26.26456 26.33689
26.42002

159 24.58040 24.70393 24.82301 24.93235 25.02781 25.14325 25.26795
25.41426

160 21.89919 21.91800 21.96438 22.02819 22.10557 22.19761 22.30192
22.41321

161 23.76281 23.77667 23.78492 23.78935 23.79608 23.80876 23.81831
23.83205

162 26.34440 26.38367 26.43238 26.48572 26.54207 26.62371 26.71742
26.82124

163 26.69247 26.78108 26.87825 26.96881 27.06755 27.16275 27.25763
27.35064

164 26.40337 26.47893 26.55288 26.63543 26.72525 26.82223 26.92452
27.03587

165 21.57201 21.59810 21.63510 21.67554 21.71384 21.77287 21.82666
21.89742

166 24.57778 24.78496 25.01756 25.27456 25.55277 25.85105 26.17266
26.51022

167 26.60724 26.71782 26.83500 26.95143 27.06646 27.17847 27.29197
27.39562

168 21.45652 21.51639 21.56997 21.62526 21.68151 21.74239 21.81124
21.88625

169 21.57897 21.66078 21.75247 21.84463 21.94340 22.04730 22.16048
22.28084

170 24.58296 24.67839 24.77476 24.88042 25.00262 25.12524 25.23747
25.36476

171 22.28343 22.37484 22.48246 22.58925 22.70309 22.81750 22.94034
23.05694

172 25.75589 25.82526 25.89779 25.97058 26.04705 26.12550 26.20980
26.29358

173 25.80709 25.85000 25.89402 25.93850 25.98248 26.02880 26.07963
26.13979

174 26.23028 26.32429 26.41778 26.50727 26.59230 26.67649 26.76554
26.84018

175 23.98341 24.03942 24.09281 24.14591 24.20489 24.26291 24.32540
24.38886

176 23.34496 23.32384 23.33256 23.36877 23.42971 23.50825 23.59211
23.68440

177 21.84710 21.89837 21.96421 22.03282 22.11099 22.19579 22.29067
22.38359

178 22.49964 22.54997 22.60467 22.66055 22.72091 22.78312 22.85569
22.93186

179 20.61151 20.61698 20.61505 20.60296 20.59168 20.57762 20.56050
20.56553

180 21.42564 21.46784 21.51224 21.56682 21.62273 21.68029 21.74056
21.80899

181 29.77377 29.94115 30.10416 30.25656 30.40434 30.54701 30.69518
30.84629

182 25.50427 25.59349 25.68500 25.79790 25.90978 26.02441 26.14762
26.27426

183 24.18309 24.30098 24.41337 24.53262 24.66164 24.77842 24.90897
25.03337

184 25.73719 25.82401 25.92331 26.03143 26.14951 26.28537 26.42238
26.56181

185 24.37988 24.42746 24.49745 24.58993 24.70728 24.83750 24.97361
25.11037

186 21.92922 21.98402 22.04069 22.09274 22.14330 22.18915 22.23996
22.29680

187 24.71955 24.73512 24.77167 24.83912 24.94095 25.05419 25.17695
25.30307

188 27.08488 27.17422 27.27616 27.39974 27.51332 27.61944 27.76261
27.90413

189 26.64648 26.74677 26.83783 26.92578 27.01620 27.10412 27.20432
27.29918

190 27.71039 27.80569 27.90479 28.00041 28.10039 28.19703 28.28959
28.37574

191 25.86898 25.93469 25.96627 26.00585 26.06073 26.13136 26.20624
26.29256

192 24.75326 24.79418 24.83998 24.88965 24.95455 25.03331 25.12717
25.22226

193 25.85208 25.96032 26.05661 26.16060 26.27087 26.38887 26.51376
26.64903

194 26.61021 26.71688 26.79210 26.85498 26.95162 27.05633 27.17698
27.30849

195 20.10343 20.18623 20.27145 20.36402 20.46585 20.57277 20.68655
20.80189

196 26.39074 26.45700 26.48925 26.51152 26.52924 26.54329 26.54449
26.55460

197 23.92467 23.99129 24.05692 24.12459 24.19204 24.25638 24.32120
24.37949

198 20.17261 20.20266 20.24298 20.29474 20.35966 20.43398 20.51422
20.59770

199 21.72652 21.76514 21.79645 21.82499 21.85806 21.89495 21.93371
21.97405

Y2008

1 20.62058

2 26.44657

3 24.59620

4 27.63048

5 22.25083

6 25.76602

7 27.50170

8 25.35542

9 27.56373

10 26.46741

11 25.65117

12 27.24594

13 27.83721

14 20.39742

15 26.38439

16 26.16443

17 26.75915

18 27.02255

19 22.41835

20 28.41894

21 22.82180

22 24.43335

23 26.61163

24 22.12984

25 25.78623

26 27.31079

27 24.18179

28 26.54286

29 21.27157

30 21.50291

31 20.80496

32 23.68173

33 27.45210

34 23.51522

35 20.99095

36 21.48569

37 27.01542

38 22.92176

39 24.94041

40 22.06131

41 19.86692

42 21.87134

43 32.67440

44 26.47897

45 22.56469

46 26.59629

47 25.06867

48 27.41899

49 27.90524

50 26.13287

51 23.38403

52 24.57270

53 25.19668

54 25.58841

55 26.73243

56 26.36751

57 23.76640

58 20.88509

59 26.26446

60 20.24700

61 26.53078

62 26.73339

63 25.85329

64 30.86752

65 24.07620

66 21.65029

67 25.54942

68 27.16509

69 22.84247

70 26.33786

71 26.01359

72 25.17988

73 25.29947

74 22.52449

75 21.64338

76 23.68465

77 23.66302

78 25.10872

79 25.05747

80 27.11568

81 27.20687

82 20.95956

83 21.85576

84 25.31003

85 26.71017

86 27.65325

87 27.13151

88 26.48020

89 24.00421

90 23.50004

91 27.47362

92 26.29078

93 21.59258

94 29.23840

95 22.01726

96 23.98950

97 29.17211

98 24.74743

99 21.07931

100 26.45693

101 27.20117

102 21.90157

103 21.89537

104 26.54164

105 26.86102

106 27.43404

107 25.71382

108 26.34473

109 21.40347

110 22.03468

111 24.73069

112 23.21991

113 21.78881

114 27.68361

115 29.37337

116 22.62295

117 25.15669

118 27.42468

119 28.10315

120 24.23690

121 24.88385

122 26.55412

123 25.63182

124 21.93536

125 21.44932

126 22.65008

127 33.89634

128 20.76344

129 26.01541

130 27.70558

131 27.76893

132 25.77291

133 21.21958

134 23.03322

135 26.93424

136 26.24109

137 22.29914

138 30.37757

139 26.26959

140 25.01506

141 25.54223

142 24.77041

143 22.87263

144 26.67380

145 26.68445

146 28.37804

147 28.13138

148 25.41069

149 26.01131

150 22.55453

151 28.22986

152 24.65176

153 25.44121

154 30.42475

155 23.51233

156 27.88432

157 21.92743

158 26.51495

159 25.56236

160 22.53139

161 23.83996

162 26.92717

163 27.43983

164 27.15988

165 21.96917

166 26.85538

167 27.49975

168 21.96671

169 22.40484

170 25.49887

171 23.16969

172 26.37629

173 26.20195

174 26.91969

175 24.44939

176 23.77966

177 22.47792

178 23.00803

179 20.59082

180 21.87875

181 30.99563

182 26.39669

183 25.15699

184 26.70371

185 25.24796

186 22.35833

187 25.42379

188 28.05359

189 27.39249

190 28.45698

191 26.39123

192 25.32054

193 26.78926

194 27.44500

195 20.91630

196 26.57750

197 24.44157

198 20.68321

199 22.02660

\>

\> \# View the first 6 rows

\> head(bmi, n = 6)

Country Y1980 Y1981 Y1982 Y1983 Y1984 Y1985

1 Afghanistan 21.48678 21.46552 21.45145 21.43822 21.42734 21.41222

2 Albania 25.22533 25.23981 25.25636 25.27176 25.27901 25.28669

3 Algeria 22.25703 22.34745 22.43647 22.52105 22.60633 22.69501

4 Andorra 25.66652 25.70868 25.74681 25.78250 25.81874 25.85236

5 Angola 20.94876 20.94371 20.93754 20.93187 20.93569 20.94857

6 Antigua and Barbuda 23.31424 23.39054 23.45883 23.53735 23.63584
23.73109

Y1986 Y1987 Y1988 Y1989 Y1990 Y1991 Y1992 Y1993

1 21.40132 21.37679 21.34018 21.29845 21.24818 21.20269 21.14238
21.06376

2 25.29451 25.30217 25.30450 25.31944 25.32357 25.28452 25.23077
25.21192

3 22.76979 22.84096 22.90644 22.97931 23.04600 23.11333 23.18776
23.25764

4 25.89089 25.93414 25.98477 26.04450 26.10936 26.17912 26.24017
26.30356

5 20.96030 20.98025 21.01375 21.05269 21.09007 21.12136 21.14987
21.13938

6 23.83449 23.93649 24.05364 24.16347 24.26782 24.36568 24.45644
24.54096

Y1994 Y1995 Y1996 Y1997 Y1998 Y1999 Y2000 Y2001

1 20.97987 20.91132 20.85155 20.81307 20.78591 20.75469 20.69521
20.62643

2 25.22115 25.25874 25.31097 25.33988 25.39116 25.46555 25.55835
25.66701

3 23.32273 23.39526 23.46811 23.54160 23.61592 23.69486 23.77659
23.86256

4 26.36793 26.43569 26.50769 26.58255 26.66337 26.75078 26.83179
26.92373

5 21.14186 21.16022 21.19076 21.22621 21.27082 21.31954 21.37480
21.43664

6 24.60945 24.66461 24.72544 24.78714 24.84936 24.91721 24.99158
25.05857

Y2002 Y2003 Y2004 Y2005 Y2006 Y2007 Y2008

1 20.59848 20.58706 20.57759 20.58084 20.58749 20.60246 20.62058

2 25.77167 25.87274 25.98136 26.08939 26.20867 26.32753 26.44657

3 23.95294 24.05243 24.15957 24.27001 24.38270 24.48846 24.59620

4 27.02525 27.12481 27.23107 27.32827 27.43588 27.53363 27.63048

5 21.51765 21.59924 21.69218 21.80564 21.93881 22.08962 22.25083

6 25.13039 25.20713 25.29898 25.39965 25.51382 25.64247 25.76602

\>

\> \# View the first 15 rows

\> head(bmi, n = 15)

Country Y1980 Y1981 Y1982 Y1983 Y1984 Y1985

1 Afghanistan 21.48678 21.46552 21.45145 21.43822 21.42734 21.41222

2 Albania 25.22533 25.23981 25.25636 25.27176 25.27901 25.28669

3 Algeria 22.25703 22.34745 22.43647 22.52105 22.60633 22.69501

4 Andorra 25.66652 25.70868 25.74681 25.78250 25.81874 25.85236

5 Angola 20.94876 20.94371 20.93754 20.93187 20.93569 20.94857

6 Antigua and Barbuda 23.31424 23.39054 23.45883 23.53735 23.63584
23.73109

7 Argentina 25.37913 25.44951 25.50242 25.55644 25.61271 25.66593

8 Armenia 23.82469 23.86401 23.91023 23.95649 24.00181 24.04083

9 Australia 24.92729 25.00216 25.07660 25.14938 25.22894 25.31849

10 Austria 24.84097 24.88110 24.93482 24.98118 25.02208 25.06015

11 Azerbaijan 24.49375 24.52584 24.56064 24.60150 24.64121 24.67566

12 Bahamas 24.21064 24.30814 24.42750 24.54415 24.66558 24.78408

13 Bahrain 23.97588 24.09045 24.20617 24.32335 24.43174 24.53684

14 Bangladesh 20.51918 20.47766 20.43741 20.40075 20.36524 20.32983

15 Barbados 24.36372 24.43455 24.49314 24.54713 24.59913 24.64998

Y1986 Y1987 Y1988 Y1989 Y1990 Y1991 Y1992 Y1993

1 21.40132 21.37679 21.34018 21.29845 21.24818 21.20269 21.14238
21.06376

2 25.29451 25.30217 25.30450 25.31944 25.32357 25.28452 25.23077
25.21192

3 22.76979 22.84096 22.90644 22.97931 23.04600 23.11333 23.18776
23.25764

4 25.89089 25.93414 25.98477 26.04450 26.10936 26.17912 26.24017
26.30356

5 20.96030 20.98025 21.01375 21.05269 21.09007 21.12136 21.14987
21.13938

6 23.83449 23.93649 24.05364 24.16347 24.26782 24.36568 24.45644
24.54096

7 25.72364 25.78529 25.84428 25.88510 25.92482 25.99177 26.07642
26.17288

8 24.08736 24.13334 24.17219 24.19556 24.20618 24.19790 24.12982
24.05854

9 25.41017 25.50528 25.60001 25.70050 25.80568 25.90295 26.00624
26.10586

10 25.10680 25.14747 25.19333 25.24928 25.30882 25.37186 25.43668
25.50507

11 24.71906 24.75799 24.78894 24.82277 24.83167 24.83972 24.81781
24.76250

12 24.90724 25.03166 25.14778 25.26173 25.35641 25.44039 25.51294
25.58479

13 24.63328 24.74914 24.86604 24.98644 25.11479 25.25103 25.40173
25.56146

14 20.29654 20.26401 20.23497 20.20736 20.18246 20.15921 20.14118
20.12952

15 24.71728 24.77976 24.84265 24.90790 24.96113 25.00859 25.05249
25.09414

Y1994 Y1995 Y1996 Y1997 Y1998 Y1999 Y2000 Y2001

1 20.97987 20.91132 20.85155 20.81307 20.78591 20.75469 20.69521
20.62643

2 25.22115 25.25874 25.31097 25.33988 25.39116 25.46555 25.55835
25.66701

3 23.32273 23.39526 23.46811 23.54160 23.61592 23.69486 23.77659
23.86256

4 26.36793 26.43569 26.50769 26.58255 26.66337 26.75078 26.83179
26.92373

5 21.14186 21.16022 21.19076 21.22621 21.27082 21.31954 21.37480
21.43664

6 24.60945 24.66461 24.72544 24.78714 24.84936 24.91721 24.99158
25.05857

7 26.27872 26.37522 26.47182 26.57778 26.68714 26.79005 26.88103
26.96067

8 24.02297 24.01570 24.02627 24.03885 24.07100 24.11699 24.18045
24.26670

9 26.20077 26.29241 26.38256 26.47351 26.56314 26.65506 26.74486
26.84397

10 25.56626 25.61814 25.66410 25.71737 25.75996 25.81773 25.87471
25.93806

11 24.69113 24.61946 24.55527 24.49745 24.47179 24.47842 24.51287
24.57202

12 25.65514 25.72418 25.79938 25.89374 25.99417 26.12080 26.25748
26.38653

13 25.71611 25.87566 26.03138 26.18600 26.34294 26.50245 26.65409
26.80388

14 20.11823 20.10770 20.10489 20.11304 20.12622 20.13361 20.14774
20.16802

15 25.14401 25.20411 25.26850 25.35236 25.42067 25.51681 25.60292
25.68910

Y2002 Y2003 Y2004 Y2005 Y2006 Y2007 Y2008

1 20.59848 20.58706 20.57759 20.58084 20.58749 20.60246 20.62058

2 25.77167 25.87274 25.98136 26.08939 26.20867 26.32753 26.44657

3 23.95294 24.05243 24.15957 24.27001 24.38270 24.48846 24.59620

4 27.02525 27.12481 27.23107 27.32827 27.43588 27.53363 27.63048

5 21.51765 21.59924 21.69218 21.80564 21.93881 22.08962 22.25083

6 25.13039 25.20713 25.29898 25.39965 25.51382 25.64247 25.76602

7 26.99882 27.04738 27.11001 27.18941 27.28179 27.38889 27.50170

8 24.37698 24.50332 24.64178 24.81447 24.99160 25.17590 25.35542

9 26.93858 27.03801 27.13871 27.24614 27.35267 27.45878 27.56373

10 25.99583 26.06356 26.14360 26.21107 26.29374 26.38136 26.46741

11 24.66021 24.77164 24.89376 25.06256 25.25706 25.45513 25.65117

12 26.51184 26.62607 26.75612 26.88517 27.00715 27.12653 27.24594

13 26.94923 27.09298 27.23908 27.38693 27.53868 27.68865 27.83721

14 20.18621 20.20948 20.23957 20.27648 20.31554 20.35493 20.39742

15 25.77615 25.87020 25.95660 26.06074 26.16874 26.27575 26.38439

\>

\> \# View the last 6 rows

\> tail(bmi, n = 6)

Country Y1980 Y1981 Y1982 Y1983 Y1984 Y1985

194 Venezuela 24.58052 24.69666 24.80082 24.89208 24.98440 25.07104

195 Vietnam 19.01394 19.03902 19.06804 19.09675 19.13046 19.16397

196 West Bank and Gaza 24.31624 24.40192 24.48713 24.57107 24.65582
24.74148

197 Yemen, Rep. 22.90384 22.96813 23.02669 23.07279 23.12566 23.16944

198 Zambia 19.66295 19.69512 19.72538 19.75420 19.78070 19.80335

199 Zimbabwe 21.46989 21.48867 21.50738 21.52936 21.53383 21.54341

Y1986 Y1987 Y1988 Y1989 Y1990 Y1991 Y1992 Y1993

194 25.15587 25.24624 25.35274 25.43322 25.52678 25.63444 25.75528
25.87036

195 19.19740 19.23481 19.27090 19.31105 19.35150 19.39625 19.45212
19.51493

196 24.82984 24.91615 25.00108 25.08593 25.17834 25.27187 25.37683
25.48893

197 23.20933 23.25043 23.29401 23.33879 23.38236 23.42152 23.46544
23.51371

198 19.82396 19.85065 19.88320 19.92451 19.96680 20.00746 20.04096
20.07781

199 21.54859 21.54590 21.55396 21.56903 21.58005 21.59694 21.59010
21.58547

Y1994 Y1995 Y1996 Y1997 Y1998 Y1999 Y2000 Y2001

194 25.97218 26.08046 26.18272 26.29177 26.40105 26.50035 26.61021
26.71688

195 19.58757 19.66996 19.75854 19.84794 19.93580 20.02081 20.10343
20.18623

196 25.61249 25.73496 25.87428 26.01468 26.15144 26.28240 26.39074
26.45700

197 23.56154 23.61684 23.66973 23.72737 23.79152 23.85482 23.92467
23.99129

198 20.09502 20.09977 20.11009 20.12375 20.13349 20.15094 20.17261
20.20266

199 21.59029 21.58986 21.60362 21.62721 21.65496 21.68873 21.72652
21.76514

Y2002 Y2003 Y2004 Y2005 Y2006 Y2007 Y2008

194 26.79210 26.85498 26.95162 27.05633 27.17698 27.30849 27.44500

195 20.27145 20.36402 20.46585 20.57277 20.68655 20.80189 20.91630

196 26.48925 26.51152 26.52924 26.54329 26.54449 26.55460 26.57750

197 24.05692 24.12459 24.19204 24.25638 24.32120 24.37949 24.44157

198 20.24298 20.29474 20.35966 20.43398 20.51422 20.59770 20.68321

199 21.79645 21.82499 21.85806 21.89495 21.93371 21.97405 22.02660

\>

\> \# View the last 10 rows

\> tail(bmi, n = 10)

Country Y1980 Y1981 Y1982 Y1983 Y1984 Y1985

190 United States 25.46406 25.57524 25.67883 25.78812 25.90690 26.02568

191 Uruguay 24.24001 24.31948 24.39260 24.44209 24.49525 24.54516

192 Uzbekistan 24.56500 24.60077 24.62187 24.64780 24.66890 24.69832

193 Vanuatu 23.20701 23.32990 23.46016 23.60431 23.75134 23.89466

194 Venezuela 24.58052 24.69666 24.80082 24.89208 24.98440 25.07104

195 Vietnam 19.01394 19.03902 19.06804 19.09675 19.13046 19.16397

196 West Bank and Gaza 24.31624 24.40192 24.48713 24.57107 24.65582
24.74148

197 Yemen, Rep. 22.90384 22.96813 23.02669 23.07279 23.12566 23.16944

198 Zambia 19.66295 19.69512 19.72538 19.75420 19.78070 19.80335

199 Zimbabwe 21.46989 21.48867 21.50738 21.52936 21.53383 21.54341

Y1986 Y1987 Y1988 Y1989 Y1990 Y1991 Y1992 Y1993

190 26.13740 26.25939 26.37687 26.49269 26.60827 26.71961 26.83609
26.95163

191 24.59804 24.67024 24.73972 24.80593 24.86952 24.95229 25.05527
25.15742

192 24.72305 24.74603 24.77115 24.78287 24.78404 24.77866 24.75026
24.73165

193 24.03171 24.15571 24.27529 24.39727 24.52964 24.66287 24.79143
24.92541

194 25.15587 25.24624 25.35274 25.43322 25.52678 25.63444 25.75528
25.87036

195 19.19740 19.23481 19.27090 19.31105 19.35150 19.39625 19.45212
19.51493

196 24.82984 24.91615 25.00108 25.08593 25.17834 25.27187 25.37683
25.48893

197 23.20933 23.25043 23.29401 23.33879 23.38236 23.42152 23.46544
23.51371

198 19.82396 19.85065 19.88320 19.92451 19.96680 20.00746 20.04096
20.07781

199 21.54859 21.54590 21.55396 21.56903 21.58005 21.59694 21.59010
21.58547

Y1994 Y1995 Y1996 Y1997 Y1998 Y1999 Y2000 Y2001

190 27.06838 27.17810 27.28376 27.39366 27.49846 27.60386 27.71039
27.80569

191 25.26958 25.36804 25.47642 25.58248 25.68818 25.78625 25.86898
25.93469

192 24.71118 24.69517 24.67727 24.68203 24.69876 24.72082 24.75326
24.79418

193 25.05856 25.19282 25.32325 25.45811 25.59565 25.72398 25.85208
25.96032

194 25.97218 26.08046 26.18272 26.29177 26.40105 26.50035 26.61021
26.71688

195 19.58757 19.66996 19.75854 19.84794 19.93580 20.02081 20.10343
20.18623

196 25.61249 25.73496 25.87428 26.01468 26.15144 26.28240 26.39074
26.45700

197 23.56154 23.61684 23.66973 23.72737 23.79152 23.85482 23.92467
23.99129

198 20.09502 20.09977 20.11009 20.12375 20.13349 20.15094 20.17261
20.20266

199 21.59029 21.58986 21.60362 21.62721 21.65496 21.68873 21.72652
21.76514

Y2002 Y2003 Y2004 Y2005 Y2006 Y2007 Y2008

190 27.90479 28.00041 28.10039 28.19703 28.28959 28.37574 28.45698

191 25.96627 26.00585 26.06073 26.13136 26.20624 26.29256 26.39123

192 24.83998 24.88965 24.95455 25.03331 25.12717 25.22226 25.32054

193 26.05661 26.16060 26.27087 26.38887 26.51376 26.64903 26.78926

194 26.79210 26.85498 26.95162 27.05633 27.17698 27.30849 27.44500

195 20.27145 20.36402 20.46585 20.57277 20.68655 20.80189 20.91630

196 26.48925 26.51152 26.52924 26.54329 26.54449 26.55460 26.57750

197 24.05692 24.12459 24.19204 24.25638 24.32120 24.37949 24.44157

198 20.24298 20.29474 20.35966 20.43398 20.51422 20.59770 20.68321

199 21.79645 21.82499 21.85806 21.89495 21.93371 21.97405 22.02660

\>

Good job! head() and tail() allow you to quickly see the top and bottom
of a dataset. They could also help to check if a dataset is sorted in a
particular way.

# Visualizing your data

100xp

There are many ways to visualize data. Since this is not a course about
data visualization, we will only touch on two types of plots that may be
useful for quickly identifying extreme or suspicious values in your
data: histograms and scatter plots.

A histogram, created with the hist() function, takes a vector (i.e.
column) of data, breaks it up into intervals, then plots as a vertical
bar the number of instances within each interval. A scatter plot,
created with the plot() function, takes two vectors (i.e. columns) of
data and plots them as a series of (x, y) coordinates on a
two-dimensional plane.

Let's look at a quick example of each.

## Instructions

For the bmi dataset:

- Use hist() to look at the distribution of average BMI across all
  countries in 2008

- Use plot() to see how each country's average BMI in 1980 (x-axis)
  compared with its BMI in 2008 (y-axis)

\# Histogram of BMIs from 2008

hist(bmi\$Y2008)

\# Scatter plot comparing BMIs from 1980 to those from 2008

plot(bmi\$Y1980, bmi\$Y2008)

![](media/image3.png)

![](media/image4.png)

Great Job! This concludes our first chapter. Continue to Chapter 2 to
learn about the principles of tidy data!

You have finished the chapter "Introduction and exploring raw data"!

**Principles of tidy data**

50xp

Which of the following is NOT a principle of tidy data?

**Possible Answers**

- ![](media/image2.wmf)Each observation forms a row, each variable forms
  a column, and each type of observational unit forms a table

- ![](media/image2.wmf)A variable contains all values measured on the
  same unit across attributes

- ![](media/image2.wmf)Each value belongs to a variable and an
  observation

- ![](media/image2.wmf)A dataset is a collection of values

That's correct!

**Common symptoms of messy data**

50xp

Based on what you know about the principles of tidy data, which of the
following is NOT a symptom of messy data?

**Possible Answers**

- ![](media/image2.wmf)Variables are stored in both rows and columns

- ![](media/image2.wmf)Column headers are values, not variable names

- ![](media/image2.wmf)A single observational unit is stored in multiple
  tables

- ![](media/image2.wmf)Multiple values are stored in one column

That's right! Multiple variables stored in one column is messy, but
there should be multiple values in each column.

**What kind of messy are the BMI data?**

50xp

Remember the bmi dataset from the previous chapter? We've loaded it for
you so can play around in the console.

Which symptom of messy data is exhibited by bmi?

**Possible Answers**

- ![](media/image2.wmf)Column headers are values, not variable names

- ![](media/image2.wmf)Multiple values are stored in one column

- ![](media/image2.wmf)Variables are stored in both rows and columns

- ![](media/image2.wmf)Multiple types of observational units are stored
  in the same table

- ![](media/image2.wmf)A single observational unit is stored in multiple
  tables

That's right! All of the year column names could be expressed as values
of a new variable called year.

# Gathering columns into key-value pairs

100xp

The most important function in tidyr is gather(). It should be used when
you have columns that are not variables and you want to collapse them
into key-value pairs.

The easiest way to visualize the effect of gather() is that it makes
wide datasets long. As you saw in the video, running the following
command on wide_df will make it long:

gather(wide_df, my_key, my_val, -col)

Experiment with this in the console before attempting the exercise.

## Instructions

- Apply the gather() function to bmi, saving the result to bmi_long.
  This will create two new columns:

  - year, containing as values what are currently column headers

  - bmi_val, the actual BMI values

- View the first 20 rows of bmi_long

\# Apply gather() to bmi and save the result as bmi_long

bmi_long \<- gather(bmi, year, bmi_val, -Country)

\# View the first 20 rows of the result

head(bmi_long, n = 20)

\> \# Apply gather() to bmi and save the result as bmi_long

\> bmi_long \<- gather(bmi, year, bmi_val, -Country)

\>

\> \# View the first 20 rows of the result

\> head(bmi_long, n = 20)

Country year bmi_val

1 Afghanistan Y1980 21.48678

2 Albania Y1980 25.22533

3 Algeria Y1980 22.25703

4 Andorra Y1980 25.66652

5 Angola Y1980 20.94876

6 Antigua and Barbuda Y1980 23.31424

7 Argentina Y1980 25.37913

8 Armenia Y1980 23.82469

9 Australia Y1980 24.92729

10 Austria Y1980 24.84097

11 Azerbaijan Y1980 24.49375

12 Bahamas Y1980 24.21064

13 Bahrain Y1980 23.97588

14 Bangladesh Y1980 20.51918

15 Barbados Y1980 24.36372

16 Belarus Y1980 24.90898

17 Belgium Y1980 25.09879

18 Belize Y1980 24.54345

19 Benin Y1980 20.80754

20 Bermuda Y1980 25.07881

\>

Well done! Notice how now, instead of being represented in the column
names, years are now all neatly represented in the year column. Try
checking dim(bmi_long) and dim(bmi) before moving on.

# Spreading key-value pairs into columns

100xp

The opposite of gather() is spread(), which takes key-values pairs and
spreads them across multiple columns. This is useful when values in a
column should actually be column names (i.e. variables). It can also
make data more compact and easier to read.

The easiest way to visualize the effect of spread() is that it makes
long datasets wide. As you saw in the video, running the following
command will make long_df wide:

spread(long_df, my_key, my_val)

Experiment with this in the console before attempting the exercise.

## Instructions

- Use spread() to reverse the operation that you performed in the last
  exercise with gather(). In other words, make bmi_long wide again,
  saving the result to bmi_wide

- View the head of bmi_wide

\# Apply spread() to bmi_long

bmi_wide \<- spread(bmi_long, year, bmi_val)

\# View the head of bmi_wide

head(bmi_wide)

\> head(bmi_long)

Country year bmi_val

1 Afghanistan Y1980 21.48678

2 Albania Y1980 25.22533

3 Algeria Y1980 22.25703

4 Andorra Y1980 25.66652

5 Angola Y1980 20.94876

6 Antigua and Barbuda Y1980 23.31424

\> \# Apply spread() to bmi_long

\> bmi_wide \<- spread(bmi_long, year, bmi_val)

\>

\> \# View the head of bmi_wide

\> head(bmi_wide)

Country Y1980 Y1981 Y1982 Y1983 Y1984 Y1985

1 Afghanistan 21.48678 21.46552 21.45145 21.43822 21.42734 21.41222

2 Albania 25.22533 25.23981 25.25636 25.27176 25.27901 25.28669

3 Algeria 22.25703 22.34745 22.43647 22.52105 22.60633 22.69501

4 Andorra 25.66652 25.70868 25.74681 25.78250 25.81874 25.85236

5 Angola 20.94876 20.94371 20.93754 20.93187 20.93569 20.94857

6 Antigua and Barbuda 23.31424 23.39054 23.45883 23.53735 23.63584
23.73109

Y1986 Y1987 Y1988 Y1989 Y1990 Y1991 Y1992 Y1993

1 21.40132 21.37679 21.34018 21.29845 21.24818 21.20269 21.14238
21.06376

2 25.29451 25.30217 25.30450 25.31944 25.32357 25.28452 25.23077
25.21192

3 22.76979 22.84096 22.90644 22.97931 23.04600 23.11333 23.18776
23.25764

4 25.89089 25.93414 25.98477 26.04450 26.10936 26.17912 26.24017
26.30356

5 20.96030 20.98025 21.01375 21.05269 21.09007 21.12136 21.14987
21.13938

6 23.83449 23.93649 24.05364 24.16347 24.26782 24.36568 24.45644
24.54096

Y1994 Y1995 Y1996 Y1997 Y1998 Y1999 Y2000 Y2001

1 20.97987 20.91132 20.85155 20.81307 20.78591 20.75469 20.69521
20.62643

2 25.22115 25.25874 25.31097 25.33988 25.39116 25.46555 25.55835
25.66701

3 23.32273 23.39526 23.46811 23.54160 23.61592 23.69486 23.77659
23.86256

4 26.36793 26.43569 26.50769 26.58255 26.66337 26.75078 26.83179
26.92373

5 21.14186 21.16022 21.19076 21.22621 21.27082 21.31954 21.37480
21.43664

6 24.60945 24.66461 24.72544 24.78714 24.84936 24.91721 24.99158
25.05857

Y2002 Y2003 Y2004 Y2005 Y2006 Y2007 Y2008

1 20.59848 20.58706 20.57759 20.58084 20.58749 20.60246 20.62058

2 25.77167 25.87274 25.98136 26.08939 26.20867 26.32753 26.44657

3 23.95294 24.05243 24.15957 24.27001 24.38270 24.48846 24.59620

4 27.02525 27.12481 27.23107 27.32827 27.43588 27.53363 27.63048

5 21.51765 21.59924 21.69218 21.80564 21.93881 22.08962 22.25083

6 25.13039 25.20713 25.29898 25.39965 25.51382 25.64247 25.76602

\>

Well done! Check the dimension of bmi_wide and bmi to verify that they
are indeed the same.

**Functions in tidyr**

50xp

Which of the following is NOT a function in the tidyr package?

**Possible Answers**

- ![](media/image2.wmf)gather()

- ![](media/image2.wmf)separate()

- ![](media/image2.wmf)spread()

- ![](media/image2.wmf)filter()

- ![](media/image2.wmf)unite()

That's right! filter() is a function in the dplyr package.

# Separating columns

100xp

The separate() function allows you to separate one column into multiple
columns. Unless you tell it otherwise, it will attempt to separate on
any character that is not a letter or number. You can also specify a
specific separator using the sep argument.

We've loaded the small dataset from the video called treatments into
your workspace. This dataset obeys the principles of tidy data, but we'd
like to split the treatment dates into two separate
columns: year and month. This can be accomplished with the following:

separate(treatments, year_mo, c("year", "month"))

Experiment with this in the console before attempting the exercise.

## Instructions

We've loaded a dataset called bmi_cc into your workspace that is a
slight variation of bmi_long, which you've already seen.
The Country_ISO column of bmi_cc has the name of each country as well
its two-letter ISO country code, separated by a forward slash.

- Apply the separate() function to bmi_cc

  - Separate Country_ISO into two columns: Countryand ISO

  - Be sure to specify the correct separator with the separgument

  - Save the result to a new object called bmi_cc_clean

- View the head of the result

\# Apply separate() to bmi_cc

bmi_cc_clean \<- separate(bmi_cc, col = Country_ISO, into = c("Country",
"ISO"), sep = "/")

\# Print the head of the result

head(bmi_cc_clean)

\> head(bmi_cc)

Country_ISO year bmi_val

1 Afghanistan/AF Y1980 21.48678

2 Albania/AL Y1980 25.22533

3 Algeria/DZ Y1980 22.25703

4 Andorra/AD Y1980 25.66652

5 Angola/AO Y1980 20.94876

6 Antigua and Barbuda/AG Y1980 23.31424

\> \# Apply separate() to bmi_cc

\> bmi_cc_clean \<- separate(bmi_cc, col = Country_ISO, into =
c("Country", "ISO"), sep = "/")

\>

\> \# Print the head of the result

\> head(bmi_cc_clean)

Country ISO year bmi_val

1 Afghanistan AF Y1980 21.48678

2 Albania AL Y1980 25.22533

3 Algeria DZ Y1980 22.25703

4 Andorra AD Y1980 25.66652

5 Angola AO Y1980 20.94876

6 Antigua and Barbuda AG Y1980 23.31424

\>

Excellent! It's good to be familiar with the separate function. In
practice, it's often used to break date-time values into their
individual pieces (day, month, year, etc.)

# Uniting columns

100xp

The opposite of separate() is unite(), which takes multiple columns and
pastes them together. By default, the contents of the columns will be
separated by underscores in the new column, but this behavior can be
altered via the sep argument.

We've loaded the treatments data into your workspace again, but this
time the year_mo column has been separated into year and month. The
original column can be recreated by putting year and month back
together:

unite(treatments, year_mo, year, month)

Experiment with this in the console before attempting the exercise.

## Instructions

In the last exercise, you separated the Country_ISO column of
the bmi_cc dataset into two columns (Country and ISO) and saved the
result to bmi_cc_clean. Now you're going to put the columns back
together!

- Apply the unite() function to bmi_cc_clean

  - Reunite the Country and ISO columns into a single column
    called Country_ISO

  - Separate each country name and code with a dash (-)

  - Save the result as bmi_cc

- View the head of the result

\# Apply unite() to bmi_cc_clean

bmi_cc \<- unite(bmi_cc_clean, Country_ISO, Country, ISO, sep = "-")

\# View the head of the result

head(bmi_cc)

\> \# Apply unite() to bmi_cc_clean

\> bmi_cc \<- unite(bmi_cc_clean, Country_ISO, Country, ISO, sep = "-")

\>

\> \# View the head of the result

\> head(bmi_cc)

Country_ISO year bmi_val

1 Afghanistan-AF Y1980 21.48678

2 Albania-AL Y1980 25.22533

3 Algeria-DZ Y1980 22.25703

4 Andorra-AD Y1980 25.66652

5 Angola-AO Y1980 20.94876

6 Antigua and Barbuda-AG Y1980 23.31424

\>

Well done! It's definitely useful to know how to combine columns

# Column headers are values, not variable names

100xp

You saw earlier in the chapter how we sometimes come across datasets
where column names are actually values of a variable (e.g. months of the
year). This is often the case when working with repeated measures data,
where measurements are taken on subjects of interest on multiple
occasions over time. The gather() function is helpful in these
situations.

## Instructions

- View the head of census.

- Gather the month columns, creating two new columns (monthand amount),
  saving the result to census2.

- Run the code given to arrange() the rows of census2 by
  the YEAR column.

- View the first 20 rows of the result.

\## tidyr and dplyr are already loaded for you

\# View the head of census

head(census)

\# Gather the month columns

census2 \<- gather(census, month, amount, -YEAR)

\# Arrange rows by YEAR using dplyr's arrange

census2 \<- arrange(census2, YEAR)

\# View first 20 rows of census2

head(census2, n = 20)

\> head(census)

YEAR JAN FEB MAR APR MAY JUN JUL AUG SEP OCT

1 1992 146913 147270 146831 148082 149015 149821 150809 151064 152595
153577

2 1993 157525 156292 154774 158996 160624 160171 162832 162491 163285
164711

3 1994 167504 169652 172775 173099 172340 174307 174801 177289 178776
180569

4 1995 182423 179472 180996 181702 183543 186088 185470 186814 187338
186546

5 1996 189167 192269 193993 194712 196210 196127 196229 196215 198843
200488

6 1997 202414 204273 204965 203372 201676 204666 207049 207643 208298
208064

NOV DEC

1 153605 155504

2 166593 168101

3 180695 181492

4 189052 190809

5 200200 201191

6 208982 209379

\> \## tidyr and dplyr are already loaded for you

\>

\> \# View the head of census

\> head(census)

YEAR JAN FEB MAR APR MAY JUN JUL AUG SEP OCT

1 1992 146913 147270 146831 148082 149015 149821 150809 151064 152595
153577

2 1993 157525 156292 154774 158996 160624 160171 162832 162491 163285
164711

3 1994 167504 169652 172775 173099 172340 174307 174801 177289 178776
180569

4 1995 182423 179472 180996 181702 183543 186088 185470 186814 187338
186546

5 1996 189167 192269 193993 194712 196210 196127 196229 196215 198843
200488

6 1997 202414 204273 204965 203372 201676 204666 207049 207643 208298
208064

NOV DEC

1 153605 155504

2 166593 168101

3 180695 181492

4 189052 190809

5 200200 201191

6 208982 209379

\>

\> \# Gather the month columns

\> census2 \<- gather(census, month, amount, -YEAR)

\>

\> \# Arrange rows by YEAR using dplyr's arrange

\> census2 \<- arrange(census2, YEAR)

\>

\> \# View first 20 rows of census2

\> head(census2, n = 20)

YEAR month amount

1 1992 JAN 146913

2 1992 FEB 147270

3 1992 MAR 146831

4 1992 APR 148082

5 1992 MAY 149015

6 1992 JUN 149821

7 1992 JUL 150809

8 1992 AUG 151064

9 1992 SEP 152595

10 1992 OCT 153577

11 1992 NOV 153605

12 1992 DEC 155504

13 1993 JAN 157525

14 1993 FEB 156292

15 1993 MAR 154774

16 1993 APR 158996

17 1993 MAY 160624

18 1993 JUN 160171

19 1993 JUL 162832

20 1993 AUG 162491

\>

Great job! Many datasets dealing with historical data appear in this
format with time expressed horizontally. Understanding how to tidy these
data is key for efficient data analysis.

# Variables are stored in both rows and columns

100xp

Sometimes you'll run into situations where variables are stored in both
rows and columns. To illustrate this, we've loaded the pets dataset from
the video, which tells us in a convoluted way how many birds, cats, and
dogs Jason, Lisa, and Terrence have. Print the pets dataset to see for
yourself.

Although it may not be immediately obvious, if we treat the values in
the type column as variables and create a separate column for each of
them, we can set things straight. To do this, we use
the spread() function. Run the following code to see for yourself:

spread(pets, type, num)

The result shows the exact same information in a much clearer way!
Notice that the spread() function took in three arguments. The first
argument takes the name of your messy dataset (pets), the second
argument takes the name of the column to spread into new columns (type),
and the third argument takes the column that contains the value with
which to fill in the newly spread out columns (num).

Now let's try this on a new messy dataset census_long. What information
does this tell us?

## Instructions

- View the first 50 rows of census_long

- Decide which column of census_long would be best to spread, and which
  column of census_long would be best to display in the newly spread out
  columns. Use the spread()function accordingly and save the result
  to census_long2

- View the first 20 rows of census_long2

\## tidyr is already loaded for you

\# View first 50 rows of census_long

head(census_long, n = 50)

\# Spread the type column

census_long2 \<- spread(census_long, type, amount)

\# View first 20 rows of census_long2

head(census_long2, n = 20)

\> \## tidyr is already loaded for you

\>

\> \# View first 50 rows of census_long

\> head(census_long, n = 50)

YEAR month type amount

1 1992 JAN MED 146913.0

2 1992 FEB MED 147270.0

3 1992 MAR MED 146831.0

4 1992 APR MED 148082.0

5 1992 MAY MED 149015.0

6 1992 JUN MED 149821.0

7 1992 JUL MED 150809.0

8 1992 AUG MED 151064.0

9 1992 SEP MED 152595.0

10 1992 OCT MED 153577.0

11 1992 NOV MED 153605.0

12 1992 DEC MED 155504.0

13 1992 JAN LOW 138283.1

14 1992 FEB LOW 139097.8

15 1992 MAR LOW 139707.8

16 1992 APR LOW 146174.1

17 1992 MAY LOW 144659.5

18 1992 JUN LOW 140761.8

19 1992 JUL LOW 145347.8

20 1992 AUG LOW 149368.9

21 1992 SEP LOW 145721.9

22 1992 OCT LOW 151195.6

23 1992 NOV LOW 150228.7

24 1992 DEC LOW 146701.6

25 1992 JAN HIGH 148180.5

26 1992 FEB HIGH 150315.3

27 1992 MAR HIGH 149089.4

28 1992 APR HIGH 157623.9

29 1992 MAY HIGH 155522.7

30 1992 JUN HIGH 158115.4

31 1992 JUL HIGH 160292.5

32 1992 AUG HIGH 152280.8

33 1992 SEP HIGH 154387.8

34 1992 OCT HIGH 157158.0

35 1992 NOV HIGH 158224.6

36 1992 DEC HIGH 162142.4

37 1993 JAN MED 157525.0

38 1993 FEB MED 156292.0

39 1993 MAR MED 154774.0

40 1993 APR MED 158996.0

41 1993 MAY MED 160624.0

42 1993 JUN MED 160171.0

43 1993 JUL MED 162832.0

44 1993 AUG MED 162491.0

45 1993 SEP MED 163285.0

46 1993 OCT MED 164711.0

47 1993 NOV MED 166593.0

48 1993 DEC MED 168101.0

49 1993 JAN LOW 148895.1

50 1993 FEB LOW 148119.8

\>

\> \# Spread the type column

\> census_long2 \<- spread(census_long, type, amount)

\>

\> \# View first 20 rows of census_long2

\> head(census_long2, n = 20)

YEAR month HIGH LOW MED

1 1992 APR 157623.9 146174.1 148082

2 1992 AUG 152280.8 149368.9 151064

3 1992 DEC 162142.4 146701.6 155504

4 1992 FEB 150315.3 139097.8 147270

5 1992 JAN 148180.5 138283.1 146913

6 1992 JUL 160292.5 145347.8 150809

7 1992 JUN 158115.4 140761.8 149821

8 1992 MAR 149089.4 139707.8 146831

9 1992 MAY 155522.7 144659.5 149015

10 1992 NOV 158224.6 150228.7 153605

11 1992 OCT 157158.0 151195.6 153577

12 1992 SEP 154387.8 145721.9 152595

13 1993 APR 168537.9 157088.1 158996

14 1993 AUG 163707.8 160795.9 162491

15 1993 DEC 174739.4 159298.6 168101

16 1993 FEB 159337.3 148119.8 156292

17 1993 JAN 158792.5 148895.1 157525

18 1993 JUL 172315.5 157370.8 162832

19 1993 JUN 168465.4 151111.8 160171

20 1993 MAR 157032.4 147650.8 154774

\>

# Multiple values are stored in one column

100xp

It's also fairly common that you will find two variables stored in a
single column of data. These variables may be joined by a separator like
a dash, underscore, space, or forward slash.

The separate() function comes in handy in these situations. To practice
using it, we have created a slight modification of last exercise's
result. Keep in mind that the into argument, which specifies the names
of the 2 new columns being formed, must be given as a character vector
(e.g. c("column1", "column2")).

## Instructions

- View the head of census_long3

- Use tidyr's separate() to split the yr_month column into two separate
  variables: year and month, saving the result to census_long4

- View the first 6 rows of the result

\## tidyr is already loaded for you

\# View the head of census_long3

head(census_long3)

\# Separate the yr_month column into two

census_long4 \<- separate(census_long3, yr_month, c("year", "month"),
sep="\_")

\# View the first 6 rows of the result

head(census_long4)

\> \## tidyr is already loaded for you

\>

\> \# View the head of census_long3

\> head(census_long3)

yr_month HIGH LOW MED

1 1992_APR 157623.9 146174.1 148082

2 1992_AUG 152280.8 149368.9 151064

3 1992_DEC 162142.4 146701.6 155504

4 1992_FEB 150315.3 139097.8 147270

5 1992_JAN 148180.5 138283.1 146913

6 1992_JUL 160292.5 145347.8 150809

\>

\> \# Separate the yr_month column into two

\> census_long4 \<- separate(census_long3, yr_month, c("year", "month"),
sep="\_")

\>

\> \# View the first 6 rows of the result

\> head(census_long4)

year month HIGH LOW MED

1 1992 APR 157623.9 146174.1 148082

2 1992 AUG 152280.8 149368.9 151064

3 1992 DEC 162142.4 146701.6 155504

4 1992 FEB 150315.3 139097.8 147270

5 1992 JAN 148180.5 138283.1 146913

6 1992 JUL 160292.5 145347.8 150809

\>

Great job! By now, you should have a good feel for what makes a dataset
tidy.

# Types of variables in R

100xp

As in other programming languages, R is capable of storing data in many
different formats, most of which you've probably seen by now.

Loosely speaking, the class() function tells you what type of object
you're working with. (There are subtle differences between
the class, type, and mode of an object, but these distinctions are
beyond the scope of this course.)

## Instructions

Change the object within each call of the class() function to make it
evaluate to the following (in order):

- character

- numeric

- integer

- factor

- logical

Add or remove quotes, add an L to numerics to make them integers and use
the factor() function when appropriate to accomplish this.

\# Make this evaluate to character

class("true")

\# Make this evaluate to numeric

class(8484.00)

\# Make this evaluate to integer

class(99L)

\# Make this evaluate to factor

class(factor("factor"))

\# Make this evaluate to logical

class(FALSE)

\> \# Make this evaluate to character

\> class("true")

\[1\] "character"

\>

\> \# Make this evaluate to numeric

\> class(8484.00)

\[1\] "numeric"

\>

\> \# Make this evaluate to integer

\> class(99L)

\[1\] "integer"

\>

\> \# Make this evaluate to factor

\> class(factor("factor"))

\[1\] "factor"

\>

\> \# Make this evaluate to logical

\> class(FALSE)

\[1\] "logical"

\>

Great job! It's essential to know how to examine your variable types and
convert them if necessary!

# Common type conversions

100xp

It is often necessary to change, or *coerce*, the way that variables in
a dataset are stored. This could be because of the way they were read
into R (with read.csv(), for example) or perhaps the function you are
using to analyze the data requires variables to be coded a certain way.

Only certain coercions are allowed, but the rules for what works are
generally pretty intuitive. For example, trying to convert a character
string to a number **gives an error**: as.numeric("some text").

There are a few less intuitive results. For example, under the hood, the
logical values TRUE and FALSE are coded as 1 and 0, respectively.
Therefore, as.logical(1) returns TRUE and as.numeric(TRUE)returns 1.

## Instructions

We've loaded a dataset called students into your workspace. These data
provide information on 395 students including their grades in three
classes (in the Grades column, separated by /).

- Use str() to preview students and see the class of each variable

- Coerce the following columns:

  - Grades to character

  - Medu to factor (categorical variable
    representing *mother's* education level)

  - Fedu to factor (categorical variable
    representing *father's* education level)

- Use str() again to see the changes to students

\# Preview students with str()

str(students)

\# Coerce Grades to character

students\$Grades \<- as.character(students\$Grades)

\# Coerce Medu to factor

students\$Medu \<- as.factor(students\$Medu)

\# Coerce Fedu to factor

students\$Fedu \<- as.factor(students\$Fedu)

\# Look at students once more with str()

str(students)

\> \# Preview students with str()

\> str(students)

'data.frame': 395 obs. of 31 variables:

\$ school : Factor w/ 2 levels "GP","MS": 1 1 1 1 1 1 1 1 1 1 ...

\$ sex : Factor w/ 2 levels "F","M": 1 1 1 1 1 2 2 1 2 2 ...

\$ age : int 18 17 15 15 16 16 16 17 15 15 ...

\$ address : Factor w/ 2 levels "R","U": 2 2 2 2 2 2 2 2 2 2 ...

\$ famsize : Factor w/ 2 levels "GT3","LE3": 1 1 2 1 1 2 2 1 2 1 ...

\$ Pstatus : Factor w/ 2 levels "A","T": 1 2 2 2 2 2 2 1 1 2 ...

\$ Medu : int 4 1 1 4 3 4 2 4 3 3 ...

\$ Fedu : int 4 1 1 2 3 3 2 4 2 4 ...

\$ Mjob : Factor w/ 5 levels "at_home","health",..: 1 1 1 2 3 4 3 3 4 3
...

\$ Fjob : Factor w/ 5 levels "at_home","health",..: 5 3 3 4 3 3 3 5 3 3
...

\$ reason : Factor w/ 4 levels "course","home",..: 1 1 3 2 2 4 2 2 2 2
...

\$ guardian : Factor w/ 3 levels "father","mother",..: 2 1 2 2 1 2 2 2 2
2 ...

\$ traveltime: int 2 1 1 1 1 1 1 2 1 1 ...

\$ studytime : int 2 2 2 3 2 2 2 2 2 2 ...

\$ failures : int 0 0 3 0 0 0 0 0 0 0 ...

\$ schoolsup : Factor w/ 2 levels "no","yes": 2 1 2 1 1 1 1 2 1 1 ...

\$ famsup : Factor w/ 2 levels "no","yes": 1 2 1 2 2 2 1 2 2 2 ...

\$ paid : Factor w/ 2 levels "no","yes": 1 1 2 2 2 2 1 1 2 2 ...

\$ activities: Factor w/ 2 levels "no","yes": 1 1 1 2 1 2 1 1 1 2 ...

\$ nursery : Factor w/ 2 levels "no","yes": 2 1 2 2 2 2 2 2 2 2 ...

\$ higher : Factor w/ 2 levels "no","yes": 2 2 2 2 2 2 2 2 2 2 ...

\$ internet : Factor w/ 2 levels "no","yes": 1 2 2 2 1 2 2 1 2 2 ...

\$ romantic : Factor w/ 2 levels "no","yes": 1 1 1 2 1 1 1 1 1 1 ...

\$ famrel : int 4 5 4 3 4 5 4 4 4 5 ...

\$ freetime : int 3 3 3 2 3 4 4 1 2 5 ...

\$ goout : int 4 3 2 2 2 2 4 4 2 1 ...

\$ Dalc : int 1 1 2 1 1 1 1 1 1 1 ...

\$ Walc : int 1 1 3 1 2 2 1 1 1 1 ...

\$ health : int 3 3 3 5 5 5 3 1 1 5 ...

\$ absences : int 6 4 10 2 4 10 0 6 0 0 ...

\$ Grades : Factor w/ 197 levels "10/0/0","10/10/0",..: 124 123 154 86
128 88 46 131 104 77 ...

\>

\> \# Coerce Grades to character

\> students\$Grades \<- as.character(students\$Grades)

\>

\> \# Coerce Medu to factor

\> students\$Medu \<- as.factor(students\$Medu)

\>

\> \# Coerce Fedu to factor

\> students\$Fedu \<- as.factor(students\$Fedu)

\>

\> \# Look at students once more with str()

\> str(students)

'data.frame': 395 obs. of 31 variables:

\$ school : Factor w/ 2 levels "GP","MS": 1 1 1 1 1 1 1 1 1 1 ...

\$ sex : Factor w/ 2 levels "F","M": 1 1 1 1 1 2 2 1 2 2 ...

\$ age : int 18 17 15 15 16 16 16 17 15 15 ...

\$ address : Factor w/ 2 levels "R","U": 2 2 2 2 2 2 2 2 2 2 ...

\$ famsize : Factor w/ 2 levels "GT3","LE3": 1 1 2 1 1 2 2 1 2 1 ...

\$ Pstatus : Factor w/ 2 levels "A","T": 1 2 2 2 2 2 2 1 1 2 ...

\$ Medu : Factor w/ 5 levels "0","1","2","3",..: 5 2 2 5 4 5 3 5 4 4 ...

\$ Fedu : Factor w/ 5 levels "0","1","2","3",..: 5 2 2 3 4 4 3 5 3 5 ...

\$ Mjob : Factor w/ 5 levels "at_home","health",..: 1 1 1 2 3 4 3 3 4 3
...

\$ Fjob : Factor w/ 5 levels "at_home","health",..: 5 3 3 4 3 3 3 5 3 3
...

\$ reason : Factor w/ 4 levels "course","home",..: 1 1 3 2 2 4 2 2 2 2
...

\$ guardian : Factor w/ 3 levels "father","mother",..: 2 1 2 2 1 2 2 2 2
2 ...

\$ traveltime: int 2 1 1 1 1 1 1 2 1 1 ...

\$ studytime : int 2 2 2 3 2 2 2 2 2 2 ...

\$ failures : int 0 0 3 0 0 0 0 0 0 0 ...

\$ schoolsup : Factor w/ 2 levels "no","yes": 2 1 2 1 1 1 1 2 1 1 ...

\$ famsup : Factor w/ 2 levels "no","yes": 1 2 1 2 2 2 1 2 2 2 ...

\$ paid : Factor w/ 2 levels "no","yes": 1 1 2 2 2 2 1 1 2 2 ...

\$ activities: Factor w/ 2 levels "no","yes": 1 1 1 2 1 2 1 1 1 2 ...

\$ nursery : Factor w/ 2 levels "no","yes": 2 1 2 2 2 2 2 2 2 2 ...

\$ higher : Factor w/ 2 levels "no","yes": 2 2 2 2 2 2 2 2 2 2 ...

\$ internet : Factor w/ 2 levels "no","yes": 1 2 2 2 1 2 2 1 2 2 ...

\$ romantic : Factor w/ 2 levels "no","yes": 1 1 1 2 1 1 1 1 1 1 ...

\$ famrel : int 4 5 4 3 4 5 4 4 4 5 ...

\$ freetime : int 3 3 3 2 3 4 4 1 2 5 ...

\$ goout : int 4 3 2 2 2 2 4 4 2 1 ...

\$ Dalc : int 1 1 2 1 1 1 1 1 1 1 ...

\$ Walc : int 1 1 3 1 2 2 1 1 1 1 ...

\$ health : int 3 3 3 5 5 5 3 1 1 5 ...

\$ absences : int 6 4 10 2 4 10 0 6 0 0 ...

\$ Grades : chr "5/6/6" "5/5/6" "7/8/10" "15/14/15" ...

\>

Good job! It's important to make sure that you know how to change
variable types in the event that you get some surprises when you first
import your data!

# Working with dates

100xp

Dates can be a challenge to work with in any programming language, but
thanks to the lubridate package, working with dates in R isn't so bad.
Since this course is about cleaning data, we only cover the most basic
functions from lubridate to help us standardize the format of dates and
times in our data.

As you saw in the video, these functions combine the
letters y, m, d, h, m, s, which stand for year, month, day, hour,
minute, and second, respectively. The order of the letters in the
function should match the order of the date/time you are attempting to
read in, although not all combinations are valid. Notice that the
functions are "smart" in that they are capable of parsing multiple
formats.

## Instructions

We have loaded a dataset called students2 into your
workspace. students2 is similar to students, except now instead of an
age for each student, we have a (hypothetical) date of birth in
the dobcolumn. There's another new column called nurse_visit, which
gives a timestamp for each student's most recent visit to the school
nurse.

- Preview students2 with str(). Notice that dob and nurse_visit are both
  stored as character

- Load the lubridate package

- Print "17 Sep 2015" as a date

- Print "July 15, 2012 12:56" as a date and time (note there are hours
  and minutes, but no seconds!)

- Coerce dob to a date (with no time)

- Coerce nurse_visit to a date and time

- Use str() to see the changes to students2

\# Preview students2 with str()

str(students2)

\# Load the lubridate package

library(lubridate)

\# Parse as date

dmy("17 Sep 2015")

\# Parse as date and time (with no seconds!)

mdy_hm("July 15, 2012 12:56")

\# Coerce dob to a date (with no time)

students2\$dob \<- ymd(students2\$dob)

\# Coerce nurse_visit to a date and time

students2\$nurse_visit \<- ymd_hms(students2\$nurse_visit)

\# Look at students2 once more with str()

str(students2)

\> head(students2)

X school sex dob address famsize Pstatus Medu Fedu Mjob Fjob

1 1 GP F 2000-06-05 U GT3 A 4 4 at_home teacher

2 2 GP F 1999-11-25 U GT3 T 1 1 at_home other

3 3 GP F 1998-02-02 U LE3 T 1 1 at_home other

4 4 GP F 1997-12-20 U GT3 T 4 2 health services

5 5 GP F 1998-10-04 U GT3 T 3 3 other other

6 6 GP M 1999-06-16 U LE3 T 4 3 services other

reason guardian traveltime studytime failures schoolsup famsup paid

1 course mother 2 2 0 yes no no

2 course father 1 2 0 no yes no

3 other mother 1 2 3 yes no yes

4 home mother 1 3 0 no yes yes

5 home father 1 2 0 no yes yes

6 reputation mother 1 2 0 no yes yes

activities nursery higher internet romantic famrel freetime goout Dalc
Walc

1 no yes yes no no 4 3 4 1 1

2 no no yes yes no 5 3 3 1 1

3 no yes yes yes no 4 3 2 2 3

4 yes yes yes yes yes 3 2 2 1 1

5 no yes yes no no 4 3 2 1 2

6 yes yes yes yes no 5 4 2 1 2

health nurse_visit absences Grades

1 3 2014-04-10 14:59:54 6 5/6/6

2 3 2015-03-12 14:59:54 4 5/5/6

3 3 2015-09-21 14:59:54 10 7/8/10

4 5 2015-09-03 14:59:54 2 15/14/15

5 5 2015-04-07 14:59:54 4 6/10/10

6 5 2013-11-15 14:59:54 10 15/15/15

\> \# Preview students2 with str()

\> str(students2)

'data.frame': 395 obs. of 33 variables:

\$ X : int 1 2 3 4 5 6 7 8 9 10 ...

\$ school : chr "GP" "GP" "GP" "GP" ...

\$ sex : chr "F" "F" "F" "F" ...

\$ dob : chr "2000-06-05" "1999-11-25" "1998-02-02" "1997-12-20" ...

\$ address : chr "U" "U" "U" "U" ...

\$ famsize : chr "GT3" "GT3" "LE3" "GT3" ...

\$ Pstatus : chr "A" "T" "T" "T" ...

\$ Medu : int 4 1 1 4 3 4 2 4 3 3 ...

\$ Fedu : int 4 1 1 2 3 3 2 4 2 4 ...

\$ Mjob : chr "at_home" "at_home" "at_home" "health" ...

\$ Fjob : chr "teacher" "other" "other" "services" ...

\$ reason : chr "course" "course" "other" "home" ...

\$ guardian : chr "mother" "father" "mother" "mother" ...

\$ traveltime : int 2 1 1 1 1 1 1 2 1 1 ...

\$ studytime : int 2 2 2 3 2 2 2 2 2 2 ...

\$ failures : int 0 0 3 0 0 0 0 0 0 0 ...

\$ schoolsup : chr "yes" "no" "yes" "no" ...

\$ famsup : chr "no" "yes" "no" "yes" ...

\$ paid : chr "no" "no" "yes" "yes" ...

\$ activities : chr "no" "no" "no" "yes" ...

\$ nursery : chr "yes" "no" "yes" "yes" ...

\$ higher : chr "yes" "yes" "yes" "yes" ...

\$ internet : chr "no" "yes" "yes" "yes" ...

\$ romantic : chr "no" "no" "no" "yes" ...

\$ famrel : int 4 5 4 3 4 5 4 4 4 5 ...

\$ freetime : int 3 3 3 2 3 4 4 1 2 5 ...

\$ goout : int 4 3 2 2 2 2 4 4 2 1 ...

\$ Dalc : int 1 1 2 1 1 1 1 1 1 1 ...

\$ Walc : int 1 1 3 1 2 2 1 1 1 1 ...

\$ health : int 3 3 3 5 5 5 3 1 1 5 ...

\$ nurse_visit: chr "2014-04-10 14:59:54" "2015-03-12 14:59:54"
"2015-09-21 14:59:54" "2015-09-03 14:59:54" ...

\$ absences : int 6 4 10 2 4 10 0 6 0 0 ...

\$ Grades : chr "5/6/6" "5/5/6" "7/8/10" "15/14/15" ...

\>

\> \# Load the lubridate package

\> library(lubridate)

Attaching package: 'lubridate'

The following object is masked from 'package:base':

date

\>

\> \# Parse as date

\> dmy("17 Sep 2015")

\[1\] "2015-09-17"

\>

\> \# Parse as date and time (with no seconds!)

\> mdy_hm("July 15, 2012 12:56")

\[1\] "2012-07-15 12:56:00 UTC"

\>

\> \# Coerce dob to a date (with no time)

\> students2\$dob \<- ymd(students2\$dob)

\>

\> \# Coerce nurse_visit to a date and time

\> students2\$nurse_visit \<- ymd_hms(students2\$nurse_visit)

\>

\> \# Look at students2 once more with str()

\> str(students2)

'data.frame': 395 obs. of 33 variables:

\$ X : int 1 2 3 4 5 6 7 8 9 10 ...

\$ school : chr "GP" "GP" "GP" "GP" ...

\$ sex : chr "F" "F" "F" "F" ...

\$ dob : Date, format: "2000-06-05" "1999-11-25" ...

\$ address : chr "U" "U" "U" "U" ...

\$ famsize : chr "GT3" "GT3" "LE3" "GT3" ...

\$ Pstatus : chr "A" "T" "T" "T" ...

\$ Medu : int 4 1 1 4 3 4 2 4 3 3 ...

\$ Fedu : int 4 1 1 2 3 3 2 4 2 4 ...

\$ Mjob : chr "at_home" "at_home" "at_home" "health" ...

\$ Fjob : chr "teacher" "other" "other" "services" ...

\$ reason : chr "course" "course" "other" "home" ...

\$ guardian : chr "mother" "father" "mother" "mother" ...

\$ traveltime : int 2 1 1 1 1 1 1 2 1 1 ...

\$ studytime : int 2 2 2 3 2 2 2 2 2 2 ...

\$ failures : int 0 0 3 0 0 0 0 0 0 0 ...

\$ schoolsup : chr "yes" "no" "yes" "no" ...

\$ famsup : chr "no" "yes" "no" "yes" ...

\$ paid : chr "no" "no" "yes" "yes" ...

\$ activities : chr "no" "no" "no" "yes" ...

\$ nursery : chr "yes" "no" "yes" "yes" ...

\$ higher : chr "yes" "yes" "yes" "yes" ...

\$ internet : chr "no" "yes" "yes" "yes" ...

\$ romantic : chr "no" "no" "no" "yes" ...

\$ famrel : int 4 5 4 3 4 5 4 4 4 5 ...

\$ freetime : int 3 3 3 2 3 4 4 1 2 5 ...

\$ goout : int 4 3 2 2 2 2 4 4 2 1 ...

\$ Dalc : int 1 1 2 1 1 1 1 1 1 1 ...

\$ Walc : int 1 1 3 1 2 2 1 1 1 1 ...

\$ health : int 3 3 3 5 5 5 3 1 1 5 ...

\$ nurse_visit: POSIXct, format: "2014-04-10 14:59:54" "2015-03-12
14:59:54" ...

\$ absences : int 6 4 10 2 4 10 0 6 0 0 ...

\$ Grades : chr "5/6/6" "5/5/6" "7/8/10" "15/14/15" ...

\>

Nice! As you can already tell, working with dates can be tricky, so this
is a useful skill set to have!

**Trimming and padding strings**

100xp

One common issue that comes up when cleaning data is the need to remove
leading and/or trailing white space. The str_trim() function from
stringr makes it easy to do this while leaving intact the part of the
string that you actually want.

\> str_trim(" this is a test ")

\[1\] "this is a test"

A similar issue is when you need to pad strings to make them a certain
number of characters wide. One example is if you had a bunch of employee
ID numbers, some of which begin with one or more zeros. When reading
these data in, you find that the leading zeros have been dropped
somewhere along the way (probably because the variable was thought to be
numeric and in that case, leading zeros would be unnecessary.)

\> str_pad("24493", width = 7, side = "left", pad = "0")

\[1\] "0024493"

## Instructions

- Load the stringr package

- Trim all leading and trailing white space from the first set of
  strings

- Pad the second set of strings with leading zeros such that all are 9
  characters in length

\# Load the stringr package

library(stringr)

\# Trim all leading and trailing whitespace

str_trim(c(" Filip ", "Nick ", " Jonathan"))

\# Pad these strings with leading zeros

str_pad(c("23485W", "8823453Q", "994Z"), width = 9, side = "left", pad =
"0")

\> \# Load the stringr package

\> library(stringr)

\>

\> \# Trim all leading and trailing whitespace

\> str_trim(c(" Filip ", "Nick ", " Jonathan"))

\[1\] "Filip" "Nick" "Jonathan"

\>

\> \# Pad these strings with leading zeros

\> str_pad(c("23485W", "8823453Q", "994Z"), width = 9, side = "left",
pad = "0")

\[1\] "00023485W" "08823453Q" "00000994Z"

\>

Nicely done! Examples like this are certainly handy in R. For example,
the str_pad() function is useful when importing a dataset with US zip
codes. Occasionally R will drop the leading 0 in a zipcode, thinking
it's numeric. Now that you know how to coerce variable types and pad
strings, this won't set you back!

# Upper and lower case

100xp

In addition to trimming and padding strings, you may need to adjust
their case from time to time. Making strings uppercase or lowercase is
very straightforward in (base) R thanks to toupper() and tolower(). Each
function takes exactly one argument: the character string (or
vector/column of strings) to be converted to the desired case.

## Instructions

There's a vector of state abbreviations called states in your workspace,
but there's a problem...it's all lowercase. It's more common for state
abbreviations to be all uppercase.

- Print states to the console

- Make states all uppercase and save the result to states_upper

- Make states_upper all lowercase again, but don't save the result

\# Print state abbreviations

print(states)

\# Make states all uppercase and save result to states_upper

states_upper \<- toupper(states)

\# Make states_upper all lowercase again

tolower(states_upper)

\> \# Print state abbreviations

\> print(states)

\[1\] "al" "ak" "az" "ar" "ca" "co" "ct" "de" "fl" "ga" "hi" "id" "il"
"in" "ia"

\[16\] "ks" "ky" "la" "me" "md" "ma" "mi" "mn" "ms" "mo" "mt" "ne" "nv"
"nh" "nj"

\[31\] "nm" "ny" "nc" "nd" "oh" "ok" "or" "pa" "ri" "sc" "sd" "tn" "tx"
"ut" "vt"

\[46\] "va" "wa" "wv" "wi" "wy"

\>

\> \# Make states all uppercase and save result to states_upper

\> states_upper \<- toupper(states)

\>

\> \# Make states_upper all lowercase again

\> tolower(states_upper)

\[1\] "al" "ak" "az" "ar" "ca" "co" "ct" "de" "fl" "ga" "hi" "id" "il"
"in" "ia"

\[16\] "ks" "ky" "la" "me" "md" "ma" "mi" "mn" "ms" "mo" "mt" "ne" "nv"
"nh" "nj"

\[31\] "nm" "ny" "nc" "nd" "oh" "ok" "or" "pa" "ri" "sc" "sd" "tn" "tx"
"ut" "vt"

\[46\] "va" "wa" "wv" "wi" "wy"

\>

# Finding and replacing strings

100xp

The stringr package provides two functions that are very useful for
finding and/or replacing strings: str_detect() and str_replace().

Like all functions in stringr, the first argument of each is the string
of interest. The second argument of each is the pattern of interest. In
the case of str_detect(), this is the pattern we are searching for. In
the case of str_replace(), this is the pattern we want to replace.
Finally, str_replace() has a third argument, which is the string to
replace with.

## Instructions

The students2 dataset from earlier in the chapter has been loaded for
you again.

- Look at the head() of students2 to remind yourself of how it looks

- Detect all dates of birth (dob) in 1997 using str_detect(). This
  should return a vector of TRUE and FALSE values.

- Replace all instances of "F" with "Female" in students2\$sex

- Replace all instances of "M" with "Male" in students2\$sex

- View the head() of students2 to see the result of these replacements

\## stringr has been loaded for you

\# Look at the head of students2

head(students2)

\# Detect all dates of birth (dob) in 1997

str_detect(students2\$dob, "1997")

\# In the sex column, replace "F" with "Female"...

students2\$sex \<- str_replace(students2\$sex, "F", "Female")

\# ...And "M" with "Male"

students2\$sex \<- str_replace(students2\$sex, "M", "Male")

\# View the head of students2

head(students2)

\> \## stringr has been loaded for you

\>

\> \# Look at the head of students2

\> head(students2)

X school sex dob address famsize Pstatus Medu Fedu Mjob Fjob

1 1 GP F 2000-06-05 U GT3 A 4 4 at_home teacher

2 2 GP F 1999-11-25 U GT3 T 1 1 at_home other

3 3 GP F 1998-02-02 U LE3 T 1 1 at_home other

4 4 GP F 1997-12-20 U GT3 T 4 2 health services

5 5 GP F 1998-10-04 U GT3 T 3 3 other other

6 6 GP M 1999-06-16 U LE3 T 4 3 services other

reason guardian traveltime studytime failures schoolsup famsup paid

1 course mother 2 2 0 yes no no

2 course father 1 2 0 no yes no

3 other mother 1 2 3 yes no yes

4 home mother 1 3 0 no yes yes

5 home father 1 2 0 no yes yes

6 reputation mother 1 2 0 no yes yes

activities nursery higher internet romantic famrel freetime goout Dalc
Walc

1 no yes yes no no 4 3 4 1 1

2 no no yes yes no 5 3 3 1 1

3 no yes yes yes no 4 3 2 2 3

4 yes yes yes yes yes 3 2 2 1 1

5 no yes yes no no 4 3 2 1 2

6 yes yes yes yes no 5 4 2 1 2

health nurse_visit absences Grades

1 3 2014-04-10 14:59:54 6 5/6/6

2 3 2015-03-12 14:59:54 4 5/5/6

3 3 2015-09-21 14:59:54 10 7/8/10

4 5 2015-09-03 14:59:54 2 15/14/15

5 5 2015-04-07 14:59:54 4 6/10/10

6 5 2013-11-15 14:59:54 10 15/15/15

\>

\> \# Detect all dates of birth (dob) in 1997

\> str_detect(students2\$dob, "1997")

\[1\] FALSE FALSE FALSE TRUE FALSE FALSE TRUE FALSE FALSE TRUE FALSE
FALSE

\[13\] FALSE TRUE FALSE FALSE TRUE FALSE FALSE FALSE FALSE FALSE TRUE
TRUE

\[25\] TRUE FALSE FALSE TRUE FALSE FALSE FALSE FALSE FALSE FALSE TRUE
FALSE

\[37\] TRUE FALSE FALSE FALSE FALSE TRUE TRUE FALSE FALSE FALSE TRUE
TRUE

\[49\] TRUE TRUE TRUE FALSE FALSE FALSE FALSE FALSE TRUE TRUE FALSE
FALSE

\[61\] FALSE FALSE FALSE FALSE FALSE FALSE FALSE TRUE FALSE FALSE TRUE
FALSE

\[73\] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE TRUE FALSE FALSE
TRUE

\[85\] FALSE FALSE FALSE TRUE FALSE FALSE TRUE TRUE FALSE TRUE FALSE
TRUE

\[97\] TRUE FALSE TRUE TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
FALSE

\[109\] FALSE FALSE FALSE FALSE FALSE TRUE FALSE TRUE FALSE FALSE FALSE
FALSE

\[121\] TRUE TRUE FALSE FALSE FALSE FALSE TRUE FALSE FALSE FALSE FALSE
TRUE

\[133\] FALSE FALSE FALSE FALSE TRUE FALSE FALSE FALSE TRUE FALSE FALSE
TRUE

\[145\] FALSE TRUE FALSE FALSE TRUE TRUE FALSE FALSE FALSE TRUE FALSE
FALSE

\[157\] FALSE FALSE FALSE FALSE FALSE FALSE TRUE FALSE TRUE TRUE TRUE
FALSE

\[169\] FALSE FALSE FALSE TRUE TRUE TRUE FALSE FALSE FALSE FALSE FALSE
FALSE

\[181\] TRUE FALSE FALSE FALSE FALSE FALSE TRUE FALSE TRUE TRUE TRUE
TRUE

\[193\] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
FALSE FALSE

\[205\] FALSE FALSE FALSE FALSE FALSE TRUE FALSE FALSE FALSE FALSE FALSE
FALSE

\[217\] FALSE TRUE FALSE TRUE FALSE FALSE FALSE FALSE FALSE TRUE TRUE
FALSE

\[229\] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE TRUE
FALSE

\[241\] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE TRUE FALSE
FALSE

\[253\] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
FALSE FALSE

\[265\] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
FALSE FALSE

\[277\] TRUE FALSE FALSE FALSE FALSE TRUE FALSE TRUE FALSE FALSE FALSE
FALSE

\[289\] FALSE FALSE FALSE FALSE FALSE TRUE FALSE FALSE FALSE TRUE FALSE
FALSE

\[301\] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
FALSE FALSE

\[313\] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
FALSE FALSE

\[325\] FALSE FALSE FALSE TRUE FALSE TRUE FALSE FALSE TRUE FALSE FALSE
FALSE

\[337\] FALSE FALSE FALSE TRUE FALSE FALSE TRUE FALSE FALSE TRUE FALSE
TRUE

\[349\] TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE TRUE FALSE FALSE
TRUE

\[361\] FALSE TRUE TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
FALSE

\[373\] FALSE TRUE TRUE TRUE FALSE FALSE FALSE FALSE TRUE TRUE TRUE TRUE

\[385\] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
FALSE

\>

\> \# In the sex column, replace "F" with "Female"...

\> students2\$sex \<- str_replace(students2\$sex, "F", "Female")

\>

\> \# ...And "M" with "Male"

\> students2\$sex \<- str_replace(students2\$sex, "M", "Male")

\>

\> \# View the head of students2

\> head(students2)

X school sex dob address famsize Pstatus Medu Fedu Mjob

1 1 GP Female 2000-06-05 U GT3 A 4 4 at_home

2 2 GP Female 1999-11-25 U GT3 T 1 1 at_home

3 3 GP Female 1998-02-02 U LE3 T 1 1 at_home

4 4 GP Female 1997-12-20 U GT3 T 4 2 health

5 5 GP Female 1998-10-04 U GT3 T 3 3 other

6 6 GP Male 1999-06-16 U LE3 T 4 3 services

Fjob reason guardian traveltime studytime failures schoolsup famsup

1 teacher course mother 2 2 0 yes no

2 other course father 1 2 0 no yes

3 other other mother 1 2 3 yes no

4 services home mother 1 3 0 no yes

5 other home father 1 2 0 no yes

6 other reputation mother 1 2 0 no yes

paid activities nursery higher internet romantic famrel freetime goout
Dalc

1 no no yes yes no no 4 3 4 1

2 no no no yes yes no 5 3 3 1

3 yes no yes yes yes no 4 3 2 2

4 yes yes yes yes yes yes 3 2 2 1

5 yes no yes yes no no 4 3 2 1

6 yes yes yes yes yes no 5 4 2 1

Walc health nurse_visit absences Grades

1 1 3 2014-04-10 14:59:54 6 5/6/6

2 1 3 2015-03-12 14:59:54 4 5/5/6

3 3 3 2015-09-21 14:59:54 10 7/8/10

4 1 5 2015-09-03 14:59:54 2 15/14/15

5 2 5 2015-04-07 14:59:54 4 6/10/10

6 2 5 2013-11-15 14:59:54 10 15/15/15

\>

Good job! Putting strings in the preferred format is essential for data
analysis!

**Types of missing and special values in R**

50xp

Which of the following is not a missing or special value in R?

**Possible Answers**

- ![](media/image2.wmf)NA

- ![](media/image2.wmf)NaN

- ![](media/image2.wmf)\#N/A

- ![](media/image2.wmf)Inf

Good job! \#N/A does not represent a missing or special value in an R
dataset.

# Finding missing values

100xp

As you've seen, missing values in R should be represented by NA, but
unfortunately you will not always be so lucky. Before you can deal with
missing values, you have to find them in the data.

If missing values are properly coded as NA, the is.na() function will
help you find them. Otherwise, if your dataset is too big to just look
at the whole thing, you may need to try searching for some of the usual
suspects like "", "#N/A", etc. You can also use
the summary() and table() functions to turn up unexpected values in your
data.

In this exercise, we've created a simple dataset called social_df that
has 3 pieces of information for each of four friends: - Name - Number of
friends on a popular social media platform - Current "status" on the
platform

## Instructions

- Call is.na() on social_df to spot all NA values.

- Wrap the above with the any() function to ask the question "Are
  there *any* NA values in my dataset?".

- View a summary() of the dataset to see how missing values are broken
  out.

- Use table to identify odd values of the status variable.

\# Call is.na() on the full social_df to spot all NAs

is.na(social_df)

\# Use the any() function to ask whether there are any NAs in the data

any(is.na(social_df))

\# View a summary() of the dataset

summary(social_df)

\# Call table() on the status column

table(social_df\$status)

\> \# Call is.na() on the full social_df to spot all NAs

\> is.na(social_df)

name n_friends status

\[1,\] FALSE FALSE FALSE

\[2,\] FALSE TRUE FALSE

\[3,\] FALSE FALSE FALSE

\[4,\] FALSE FALSE FALSE

\>

\> \# Use the any() function to ask whether there are any NAs in the
data

\> any(is.na(social_df))

\[1\] TRUE

\>

\> \# View a summary() of the dataset

\> summary(social_df)

name n_friends status

Alice:1 Min. : 43.0 :2

David:1 1st Qu.: 94.0 Going out! :1

Sarah:1 Median :145.0 Movie night...:1

Tom :1 Mean :144.0

3rd Qu.:194.5

Max. :244.0

NA's :1

\>

\> \# Call table() on the status column

\> table(social_df\$status)

Going out! Movie night...

2 1 1

\>

Nice! Scanning your dataset for NA values is essential before learning
how to remedy missing data problems.

# Dealing with missing values

100xp

Missing values can be a rather complex subject, but here we'll only look
at the simple case where you are simply interested in normalizing and/or
removing all missing values from your data. For more information on why
this is not always the best strategy, search online for "missing not at
random."

Looking at the social_df dataset again, we asked around a bit and
figured out what's causing the missing values that you saw in the last
exercise. Tom doesn't have a social media account on this particular
platform, which explains why his number of friends and current status
are missing (although coded in two different ways). Alice is on the
platform, but is a passive user and never sets her status, hence the
reason it's missing for her.

## Instructions

- Replace all empty strings (i.e. "") with NA in the statuscolumn
  of social_df.

- Print the updated version of social_df to confirm your changes.

- Use complete.cases() to return a vector containing TRUEand FALSE to
  see which rows have NO missing values.

- Use na.omit() to remove all rows with one or more missing values
  (without saving the result).

\## The stringr package is preloaded

\# Replace all empty strings in status with NA

social_df\$status\[social_df\$status == ""\] \<- "NA"

\# Print social_df to the console

print(social_df)

\# Use complete.cases() to see which rows have no missing values

complete.cases(social_df)

\# Use na.omit() to remove all rows with any missing values

na.omit(social_df)

\> \## The stringr package is preloaded

\>

\> \# Replace all empty strings in status with NA

\> social_df\$status\[social_df\$status == ""\] \<- "NA"

Warning message: invalid factor level, NA generated

\>

\> \# Print social_df to the console

\> print(social_df)

name n_friends status

1 Sarah 244 Going out!

2 Tom NA \<NA\>

3 David 145 Movie night...

4 Alice 43 \<NA\>

\>

\> \# Use complete.cases() to see which rows have no missing values

\> complete.cases(social_df)

\[1\] TRUE FALSE TRUE FALSE

\>

\> \# Use na.omit() to remove all rows with any missing values

\> na.omit(social_df)

name n_friends status

1 Sarah 244 Going out!

3 David 145 Movie night...

\>

Nice! Often times in data analyses, you'll want to get a feel for how
many complete observations you have. This can be helpful in determining
how you handle observations with missing data points.

**Identifying outliers and obvious errors**

50xp

Which two of the following are most useful for identifying outliers?

a. summary()

b. str()

c. hist()

d. outlier()

**Possible Answers**

- ![](media/image2.wmf)a and b

- ![](media/image5.wmf)a and c

- ![](media/image2.wmf)b and c

- ![](media/image2.wmf)b and d

- ![](media/image2.wmf)a and d

Good job! These two functions are very useful in getting information
about the distribution of values for a given variable!

# Dealing with outliers and obvious errors

100xp

When dealing with strange values in your data, you often must decide
whether they are just extreme or actually erroneous. Extreme values show
up all over the place, but you, the data analyst, must figure out when
they are plausible and when they are not.

We have loaded a dataset called students3, which is another slight
variation of the original students dataset. Two variables appear to have
suspicious values: age and absences. Let's explore these values further.

## Instructions

- Call summary() on the full students3 dataset to expose the concerning
  values of age and absences.

- View a histogram (using hist()) of the age variable.

- View a histogram of the absences variable.

- View another histogram of absences, but force values of zero to be
  bucketed to the right of zero on the x-axis with right =
  FALSE (see ?hist for more info).

\# Look at a summary() of students3

summary(students3)

\# View a histogram of the age variable

hist(students3\$age)

\# View a histogram of the absences variable

hist(students3\$absences)

\# View a histogram of absences, but force zeros to be bucketed to the
right of zero

hist(students3\$absences, right = FALSE)

\> \# Look at a summary() of students3

\> summary(students3)

school sex age address famsize Pstatus Medu

GP:349 F:208 Min. :15.00 R: 88 GT3:281 A: 41 Min. :0.000

MS: 46 M:187 1st Qu.:16.00 U:307 LE3:114 T:354 1st Qu.:2.000

Median :17.00 Median :3.000

Mean :16.75 Mean :2.749

3rd Qu.:18.00 3rd Qu.:4.000

Max. :38.00 Max. :4.000

Fedu Mjob Fjob reason guardian

Min. :0.000 at_home : 59 at_home : 20 course :145 father: 90

1st Qu.:2.000 health : 34 health : 18 home :109 mother:273

Median :2.000 other :141 other :217 other : 36 other : 32

Mean :2.522 services:103 services:111 reputation:105

3rd Qu.:3.000 teacher : 58 teacher : 29

Max. :4.000

traveltime studytime failures schoolsup famsup paid

Min. :1.000 Min. :1.000 Min. :0.0000 no :344 no :153 no :214

1st Qu.:1.000 1st Qu.:1.000 1st Qu.:0.0000 yes: 51 yes:242 yes:181

Median :1.000 Median :2.000 Median :0.0000

Mean :1.448 Mean :2.035 Mean :0.3342

3rd Qu.:2.000 3rd Qu.:2.000 3rd Qu.:0.0000

Max. :4.000 Max. :4.000 Max. :3.0000

activities nursery higher internet romantic famrel

no :194 no : 81 no : 20 no : 66 no :263 Min. :1.000

yes:201 yes:314 yes:375 yes:329 yes:132 1st Qu.:4.000

Median :4.000

Mean :3.944

3rd Qu.:5.000

Max. :5.000

freetime goout Dalc Walc

Min. :1.000 Min. :1.000 Min. :1.000 Min. :1.000

1st Qu.:3.000 1st Qu.:2.000 1st Qu.:1.000 1st Qu.:1.000

Median :3.000 Median :3.000 Median :1.000 Median :2.000

Mean :3.235 Mean :3.109 Mean :1.481 Mean :2.291

3rd Qu.:4.000 3rd Qu.:4.000 3rd Qu.:2.000 3rd Qu.:3.000

Max. :5.000 Max. :5.000 Max. :5.000 Max. :5.000

health absences Grades

Min. :1.000 Min. :-1.000 10/10/10: 9

1st Qu.:3.000 1st Qu.: 0.000 10/9/9 : 7

Median :4.000 Median : 4.000 11/11/11: 7

Mean :3.554 Mean : 5.691 16/15/15: 7

3rd Qu.:5.000 3rd Qu.: 8.000 8/9/10 : 7

Max. :5.000 Max. :75.000 11/11/10: 6

(Other) :352

\>

\> \# View a histogram of the age variable

\> hist(students3\$age)

\>

\> \# View a histogram of the absences variable

\> hist(students3\$absences)

\>

\> \# View a histogram of absences, but force zeros to be bucketed to
the right of zero

\> hist(students3\$absences, right = FALSE)

\>

![](media/image6.png)

![](media/image7.png)

![](media/image8.png)

Nice! As you can see, a simple histogram, displaying the distribution of
a variable's values across all the observations can be key to
identifying potential outliers as early as possible.

# Another look at strange values

100xp

Another useful way of looking at strange values is with boxplots. Simply
put, boxplots draw a box around the middle 50% of values for a given
variable, with a bolded horizontal line drawn at the median. Values that
fall far from the bulk of the data points (i.e. outliers) are denoted by
open circles. (If you're curious about the exact formula for determining
what is "far", check out ?hist.)

In this situation, we are concerned about three things:

1.  Since this dataset is about students and the only student above the
    age of 22 is 38 years old, we must wonder whether this is an error
    in the data or just an older student (perhaps returning to school
    after working for several years)

2.  There are four values of -1 for the absences variable, which is
    either a mistake or an intentional coding meant to say, for example,
    "this value is missing"

3.  There are several extreme values of absences in the positive
    direction, with a maximum value of 75 (which is over 18 times the
    median value of 4)

## Instructions

- View a boxplot() of the age variable from students3

- View a boxplot() of the absences variable from students3

\# View a boxplot of age

boxplot(students3\$age)

\# View a boxplot of absences

boxplot(students3\$absences)

\> \# View a boxplot of age

\> boxplot(students3\$age)

\>

\> \# View a boxplot of absences

\> boxplot(students3\$absences)

\>

![](media/image9.png)![](media/image10.png)

Great job! This is the end of Chapter 3. Advance to Chapter 4, where
you'll apply all of the skills you learned in Chapters 1-3 to a real
life messy dataset!

You have finished the chapter "Preparing data for analysis"!

# Get a feel for the data

100xp

Before diving into our data cleaning routine, we must first understand
the basic structure of the data. This involves looking at things like
the class() of the data object to make sure it's what we expect
(generally a data.frame) in addition to checking its dimensions
with dim() and the column names with names().

## Instructions

For the weather dataset, which is loaded in your workspace:

- Check that it's a data.frame using the function class()

- Look at the dimensions

- View the column names

\# Verify that weather is a data.frame

class(weather)

\# Check the dimensions

dim(weather)

\# View the column names

names(weather)

\> \# Verify that weather is a data.frame

\> class(weather)

\[1\] "data.frame"

\>

\> \# Check the dimensions

\> dim(weather)

\[1\] 286 35

\>

\> \# View the column names

\> names(weather)

\[1\] "X" "year" "month" "measure" "X1" "X2" "X3"

\[8\] "X4" "X5" "X6" "X7" "X8" "X9" "X10"

\[15\] "X11" "X12" "X13" "X14" "X15" "X16" "X17"

\[22\] "X18" "X19" "X20" "X21" "X22" "X23" "X24"

\[29\] "X25" "X26" "X27" "X28" "X29" "X30" "X31"

\>

# Summarize the data

100xp

Next up is to look at some summaries of the data. This is where
functions like str(), glimpse() from dplyr, and summary() come in handy.

## Instructions

- View the structure of weather using base R

- Load the dplyr package

- View the structure of weather, the dplyr way

- View a summary() of weather

\# View the structure of the data

str(weather)

\# Load dplyr package

library(dplyr)

\# Look at the structure using dplyr's glimpse()

glimpse(weather)

\# View a summary of the data

summary(weather)

\> \# View the structure of the data

\> str(weather)

'data.frame': 286 obs. of 35 variables:

\$ X : int 1 2 3 4 5 6 7 8 9 10 ...

\$ year : int 2014 2014 2014 2014 2014 2014 2014 2014 2014 2014 ...

\$ month : int 12 12 12 12 12 12 12 12 12 12 ...

\$ measure: chr "Max.TemperatureF" "Mean.TemperatureF"
"Min.TemperatureF" "Max.Dew.PointF" ...

\$ X1 : chr "64" "52" "39" "46" ...

\$ X2 : chr "42" "38" "33" "40" ...

\$ X3 : chr "51" "44" "37" "49" ...

\$ X4 : chr "43" "37" "30" "24" ...

\$ X5 : chr "42" "34" "26" "37" ...

\$ X6 : chr "45" "42" "38" "45" ...

\$ X7 : chr "38" "30" "21" "36" ...

\$ X8 : chr "29" "24" "18" "28" ...

\$ X9 : chr "49" "39" "29" "49" ...

\$ X10 : chr "48" "43" "38" "45" ...

\$ X11 : chr "39" "36" "32" "37" ...

\$ X12 : chr "39" "35" "31" "28" ...

\$ X13 : chr "42" "37" "32" "28" ...

\$ X14 : chr "45" "39" "33" "29" ...

\$ X15 : chr "42" "37" "32" "33" ...

\$ X16 : chr "44" "40" "35" "42" ...

\$ X17 : chr "49" "45" "41" "46" ...

\$ X18 : chr "44" "40" "36" "34" ...

\$ X19 : chr "37" "33" "29" "25" ...

\$ X20 : chr "36" "32" "27" "30" ...

\$ X21 : chr "36" "33" "30" "30" ...

\$ X22 : chr "44" "39" "33" "39" ...

\$ X23 : chr "47" "45" "42" "45" ...

\$ X24 : chr "46" "44" "41" "46" ...

\$ X25 : chr "59" "52" "44" "58" ...

\$ X26 : chr "50" "44" "37" "31" ...

\$ X27 : chr "52" "45" "38" "34" ...

\$ X28 : chr "52" "46" "40" "42" ...

\$ X29 : chr "41" "36" "30" "26" ...

\$ X30 : chr "30" "26" "22" "10" ...

\$ X31 : chr "30" "25" "20" "8" ...

\>

\> \# Load dplyr package

\> library(dplyr)

Attaching package: 'dplyr'

The following objects are masked from 'package:stats':

filter, lag

The following objects are masked from 'package:base':

intersect, setdiff, setequal, union

\>

\> \# Look at the structure using dplyr's glimpse()

\> glimpse(weather)

Observations: 286

Variables: 35

\$ X \<int\> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17,
...

\$ year \<int\> 2014, 2014, 2014, 2014, 2014, 2014, 2014, 2014, 2014,
2014,...

\$ month \<int\> 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12, 12,
12,...

\$ measure \<chr\> "Max.TemperatureF", "Mean.TemperatureF",
"Min.TemperatureF"...

\$ X1 \<chr\> "64", "52", "39", "46", "40", "26", "74", "63", "52",
"30.4...

\$ X2 \<chr\> "42", "38", "33", "40", "27", "17", "92", "72", "51",
"30.7...

\$ X3 \<chr\> "51", "44", "37", "49", "42", "24", "100", "79", "57",
"30....

\$ X4 \<chr\> "43", "37", "30", "24", "21", "13", "69", "54", "39",
"30.5...

\$ X5 \<chr\> "42", "34", "26", "37", "25", "12", "85", "66", "47",
"30.6...

\$ X6 \<chr\> "45", "42", "38", "45", "40", "36", "100", "93", "85",
"30....

\$ X7 \<chr\> "38", "30", "21", "36", "20", "-3", "92", "61", "29",
"30.6...

\$ X8 \<chr\> "29", "24", "18", "28", "16", "3", "92", "70", "47",
"30.77...

\$ X9 \<chr\> "49", "39", "29", "49", "41", "28", "100", "93", "86",
"30....

\$ X10 \<chr\> "48", "43", "38", "45", "39", "37", "100", "95", "89",
"29....

\$ X11 \<chr\> "39", "36", "32", "37", "31", "27", "92", "87", "82",
"29.8...

\$ X12 \<chr\> "39", "35", "31", "28", "27", "25", "85", "75", "64",
"29.8...

\$ X13 \<chr\> "42", "37", "32", "28", "26", "24", "75", "65", "55",
"29.8...

\$ X14 \<chr\> "45", "39", "33", "29", "27", "25", "82", "68", "53",
"29.9...

\$ X15 \<chr\> "42", "37", "32", "33", "29", "27", "89", "75", "60",
"30.1...

\$ X16 \<chr\> "44", "40", "35", "42", "36", "30", "96", "85", "73",
"30.1...

\$ X17 \<chr\> "49", "45", "41", "46", "41", "32", "100", "85", "70",
"29....

\$ X18 \<chr\> "44", "40", "36", "34", "30", "26", "89", "73", "57",
"29.8...

\$ X19 \<chr\> "37", "33", "29", "25", "22", "20", "69", "63", "56",
"30.1...

\$ X20 \<chr\> "36", "32", "27", "30", "24", "20", "89", "79", "69",
"30.3...

\$ X21 \<chr\> "36", "33", "30", "30", "27", "25", "85", "77", "69",
"30.3...

\$ X22 \<chr\> "44", "39", "33", "39", "34", "25", "89", "79", "69",
"30.4...

\$ X23 \<chr\> "47", "45", "42", "45", "42", "37", "100", "91", "82",
"30....

\$ X24 \<chr\> "46", "44", "41", "46", "44", "41", "100", "98", "96",
"30....

\$ X25 \<chr\> "59", "52", "44", "58", "43", "29", "100", "75", "49",
"29....

\$ X26 \<chr\> "50", "44", "37", "31", "29", "28", "70", "60", "49",
"30.1...

\$ X27 \<chr\> "52", "45", "38", "34", "31", "29", "70", "60", "50",
"30.2...

\$ X28 \<chr\> "52", "46", "40", "42", "35", "27", "76", "65", "53",
"29.9...

\$ X29 \<chr\> "41", "36", "30", "26", "20", "10", "64", "51", "37",
"30.2...

\$ X30 \<chr\> "30", "26", "22", "10", "4", "-6", "50", "38", "26",
"30.36...

\$ X31 \<chr\> "30", "25", "20", "8", "5", "1", "57", "44", "31",
"30.32",...

\>

\> \# View a summary of the data

\> summary(weather)

X year month measure

Min. : 1.00 Min. :2014 Min. : 1.000 Length:286

1st Qu.: 72.25 1st Qu.:2015 1st Qu.: 4.000 Class :character

Median :143.50 Median :2015 Median : 7.000 Mode :character

Mean :143.50 Mean :2015 Mean : 6.923

3rd Qu.:214.75 3rd Qu.:2015 3rd Qu.:10.000

Max. :286.00 Max. :2015 Max. :12.000

X1 X2 X3 X4

Length:286 Length:286 Length:286 Length:286

Class :character Class :character Class :character Class :character

Mode :character Mode :character Mode :character Mode :character

X5 X6 X7 X8

Length:286 Length:286 Length:286 Length:286

Class :character Class :character Class :character Class :character

Mode :character Mode :character Mode :character Mode :character

X9 X10 X11 X12

Length:286 Length:286 Length:286 Length:286

Class :character Class :character Class :character Class :character

Mode :character Mode :character Mode :character Mode :character

X13 X14 X15 X16

Length:286 Length:286 Length:286 Length:286

Class :character Class :character Class :character Class :character

Mode :character Mode :character Mode :character Mode :character

X17 X18 X19 X20

Length:286 Length:286 Length:286 Length:286

Class :character Class :character Class :character Class :character

Mode :character Mode :character Mode :character Mode :character

X21 X22 X23 X24

Length:286 Length:286 Length:286 Length:286

Class :character Class :character Class :character Class :character

Mode :character Mode :character Mode :character Mode :character

X25 X26 X27 X28

Length:286 Length:286 Length:286 Length:286

Class :character Class :character Class :character Class :character

Mode :character Mode :character Mode :character Mode :character

X29 X30 X31

Length:286 Length:286 Length:286

Class :character Class :character Class :character

Mode :character Mode :character Mode :character

\>

Nice! Now that we have a pretty good feel for how the table is
structured, we'll take a look at some real observations!

# Take a closer look

100xp

After understanding the structure of the data and looking at some brief
summaries, it often helps to preview the actual data. The
functions head()and tail() allow you to view the top and bottom rows of
the data, respectively. Recall you'll be shown 6 rows by default, but
you can alter this behavior with a second argument to the function.

## Instructions

For the weather data:

- View the first 6 rows

- View the first 15 rows

- View the last 6 rows

- View the last 10 rows

\# View first 6 rows

head(weather, n = 6)

\# View first 15 rows

head(weather, n = 15)

\# View the last 6 rows

tail(weather, n = 6)

\# View the last 10 rows

tail(weather, n = 10)

\> \# View first 6 rows

\> head(weather, n = 6)

X year month measure X1 X2 X3 X4 X5 X6 X7 X8 X9 X10 X11 X12 X13 X14

1 1 2014 12 Max.TemperatureF 64 42 51 43 42 45 38 29 49 48 39 39 42 45

2 2 2014 12 Mean.TemperatureF 52 38 44 37 34 42 30 24 39 43 36 35 37 39

3 3 2014 12 Min.TemperatureF 39 33 37 30 26 38 21 18 29 38 32 31 32 33

4 4 2014 12 Max.Dew.PointF 46 40 49 24 37 45 36 28 49 45 37 28 28 29

5 5 2014 12 MeanDew.PointF 40 27 42 21 25 40 20 16 41 39 31 27 26 27

6 6 2014 12 Min.DewpointF 26 17 24 13 12 36 -3 3 28 37 27 25 24 25

X15 X16 X17 X18 X19 X20 X21 X22 X23 X24 X25 X26 X27 X28 X29 X30 X31

1 42 44 49 44 37 36 36 44 47 46 59 50 52 52 41 30 30

2 37 40 45 40 33 32 33 39 45 44 52 44 45 46 36 26 25

3 32 35 41 36 29 27 30 33 42 41 44 37 38 40 30 22 20

4 33 42 46 34 25 30 30 39 45 46 58 31 34 42 26 10 8

5 29 36 41 30 22 24 27 34 42 44 43 29 31 35 20 4 5

6 27 30 32 26 20 20 25 25 37 41 29 28 29 27 10 -6 1

\>

\> \# View first 15 rows

\> head(weather, n = 15)

X year month measure X1 X2 X3 X4 X5 X6

1 1 2014 12 Max.TemperatureF 64 42 51 43 42 45

2 2 2014 12 Mean.TemperatureF 52 38 44 37 34 42

3 3 2014 12 Min.TemperatureF 39 33 37 30 26 38

4 4 2014 12 Max.Dew.PointF 46 40 49 24 37 45

5 5 2014 12 MeanDew.PointF 40 27 42 21 25 40

6 6 2014 12 Min.DewpointF 26 17 24 13 12 36

7 7 2014 12 Max.Humidity 74 92 100 69 85 100

8 8 2014 12 Mean.Humidity 63 72 79 54 66 93

9 9 2014 12 Min.Humidity 52 51 57 39 47 85

10 10 2014 12 Max.Sea.Level.PressureIn 30.45 30.71 30.4 30.56 30.68
30.42

11 11 2014 12 Mean.Sea.Level.PressureIn 30.13 30.59 30.07 30.33 30.59
30.24

12 12 2014 12 Min.Sea.Level.PressureIn 30.01 30.4 29.87 30.09 30.45
30.16

13 13 2014 12 Max.VisibilityMiles 10 10 10 10 10 10

14 14 2014 12 Mean.VisibilityMiles 10 8 5 10 10 4

15 15 2014 12 Min.VisibilityMiles 10 2 1 10 5 0

X7 X8 X9 X10 X11 X12 X13 X14 X15 X16 X17 X18

1 38 29 49 48 39 39 42 45 42 44 49 44

2 30 24 39 43 36 35 37 39 37 40 45 40

3 21 18 29 38 32 31 32 33 32 35 41 36

4 36 28 49 45 37 28 28 29 33 42 46 34

5 20 16 41 39 31 27 26 27 29 36 41 30

6 -3 3 28 37 27 25 24 25 27 30 32 26

7 92 92 100 100 92 85 75 82 89 96 100 89

8 61 70 93 95 87 75 65 68 75 85 85 73

9 29 47 86 89 82 64 55 53 60 73 70 57

10 30.69 30.77 30.51 29.58 29.81 29.88 29.86 29.91 30.15 30.17 29.91
29.87

11 30.46 30.67 30.04 29.5 29.61 29.85 29.82 29.83 30.05 30.09 29.75
29.78

12 30.24 30.51 29.49 29.43 29.44 29.81 29.78 29.78 29.91 29.92 29.69
29.71

13 10 10 10 10 10 10 10 10 10 10 10 10

14 10 8 2 3 7 10 10 10 10 9 6 10

15 5 2 1 1 1 7 10 10 10 5 1 10

X19 X20 X21 X22 X23 X24 X25 X26 X27 X28 X29 X30

1 37 36 36 44 47 46 59 50 52 52 41 30

2 33 32 33 39 45 44 52 44 45 46 36 26

3 29 27 30 33 42 41 44 37 38 40 30 22

4 25 30 30 39 45 46 58 31 34 42 26 10

5 22 24 27 34 42 44 43 29 31 35 20 4

6 20 20 25 25 37 41 29 28 29 27 10 -6

7 69 89 85 89 100 100 100 70 70 76 64 50

8 63 79 77 79 91 98 75 60 60 65 51 38

9 56 69 69 69 82 96 49 49 50 53 37 26

10 30.15 30.31 30.37 30.4 30.31 30.13 29.96 30.16 30.22 29.99 30.22
30.36

11 29.98 30.26 30.32 30.35 30.23 29.9 29.63 30.11 30.14 29.87 30.12
30.32

12 29.86 30.17 30.28 30.3 30.16 29.55 29.47 29.99 30.03 29.77 30 30.23

13 10 10 10 10 10 2 10 10 10 10 10 10

14 10 10 9 10 5 1 8 10 10 10 10 10

15 10 7 6 4 1 0 1 10 10 10 10 10

X31

1 30

2 25

3 20

4 8

5 5

6 1

7 57

8 44

9 31

10 30.32

11 30.25

12 30.13

13 10

14 10

15 10

\>

\> \# View the last 6 rows

\> tail(weather, n = 6)

X year month measure X1 X2 X3 X4 X5 X6 X7 X8

281 281 2015 12 Mean.Wind.SpeedMPH 6 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\>

282 282 2015 12 Max.Gust.SpeedMPH 17 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\>

283 283 2015 12 PrecipitationIn 0.14 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\>

284 284 2015 12 CloudCover 7 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\>

285 285 2015 12 Events Rain \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\>

286 286 2015 12 WindDirDegrees 109 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\>

X9 X10 X11 X12 X13 X14 X15 X16 X17 X18 X19 X20 X21 X22 X23

281 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

282 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

283 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

284 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

285 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

286 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

X24 X25 X26 X27 X28 X29 X30 X31

281 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

282 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

283 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

284 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

285 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

286 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

\>

\> \# View the last 10 rows

\> tail(weather, n = 10)

X year month measure X1 X2 X3 X4 X5 X6 X7 X8

277 277 2015 12 Max.VisibilityMiles 10 \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\>

278 278 2015 12 Mean.VisibilityMiles 8 \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\>

279 279 2015 12 Min.VisibilityMiles 1 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\>

280 280 2015 12 Max.Wind.SpeedMPH 15 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\>

281 281 2015 12 Mean.Wind.SpeedMPH 6 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\>

282 282 2015 12 Max.Gust.SpeedMPH 17 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\>

283 283 2015 12 PrecipitationIn 0.14 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\>

284 284 2015 12 CloudCover 7 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\>

285 285 2015 12 Events Rain \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\>

286 286 2015 12 WindDirDegrees 109 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\>

X9 X10 X11 X12 X13 X14 X15 X16 X17 X18 X19 X20 X21 X22 X23

277 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

278 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

279 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

280 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

281 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

282 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

283 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

284 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

285 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

286 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>
\<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

X24 X25 X26 X27 X28 X29 X30 X31

277 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

278 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

279 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

280 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

281 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

282 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

283 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

284 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

285 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

286 \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\> \<NA\>

\>

Well done! Not surprisingly, this dataset is pretty messy…for now :)

# Column names are values

100xp

The weather dataset suffers from one of the five most common symptoms of
messy data: column names are values. In particular, the column
names X1-X31 represent days of the month, which should really be values
of a new variable called day.

The tidyr package provides the gather() function for exactly this
scenario. To remind you of how it works, we've loaded a small dataset
called df in your workspace. Give the following a try in the console
before attempting the instructions below.

gather(df, time, val, t1:t3)

Notice that gather() allows you to select multiple columns to be
gathered by using the : operator.

## Instructions

- Load the tidyr package

- Call gather() on the weather data to gather columns X1-X31. The two
  columns created as a result should be called day and value. Save the
  result as weather2

- View the result with head()

\# Load the tidyr package

library(tidyr)

\# Gather the columns

weather2 \<- gather(weather, day, value, X1:X31, na.rm = TRUE)

\# View the head

head(weather2)

\> \# Load the tidyr package

\> library(tidyr)

\>

\> \# Gather the columns

\> weather2 \<- gather(weather, day, value, X1:X31, na.rm = TRUE)

\>

\> \# View the head

\> head(weather2)

X year month measure day value

1 1 2014 12 Max.TemperatureF X1 64

2 2 2014 12 Mean.TemperatureF X1 52

3 3 2014 12 Min.TemperatureF X1 39

4 4 2014 12 Max.Dew.PointF X1 46

5 5 2014 12 MeanDew.PointF X1 40

6 6 2014 12 Min.DewpointF X1 26

\>

Nice job! Good thing we took care of that issue.

# Values are variable names

100xp

Our data suffer from a second common symptom of messy data: values are
variable names. Specifically, values in the measure column should be
variables (i.e. column names) in our dataset.

The spread() function from tidyr is designed to help with this. To
remind you of how this function works, we've loaded another small
dataset called df2 (which is the result of applying gather() to the
original dffrom last exercise). Give the following a try before
attempting the instructions below.

spread(df2, time, val)

Note how the values of the time column now become column names.

## Instructions

- Using the code provided, remove the first column of weather2

- Spread the measure column of weather2 and save the result to weather3

- View the result with head()

\## The tidyr package is already loaded

\# First remove column of row names

weather2 \<- weather2\[, -1\]

\# Spread the data

weather3 \<- spread(weather2, measure, value)

\# View the head

head(weather3)

\> head(weather2)

X year month measure day value

1 1 2014 12 Max.TemperatureF X1 64

2 2 2014 12 Mean.TemperatureF X1 52

3 3 2014 12 Min.TemperatureF X1 39

4 4 2014 12 Max.Dew.PointF X1 46

5 5 2014 12 MeanDew.PointF X1 40

6 6 2014 12 Min.DewpointF X1 26

\> head(df)

1 function (x, df1, df2, ncp, log = FALSE)

2 {

3 if (missing(ncp))

4 .Call(C_df, x, df1, df2, log)

5 else .Call(C_dnf, x, df1, df2, ncp, log)

6 }

\> head(df2)

subject age time val

1 X 34 t1 0.6753014

2 Y 88 t1 0.3588532

3 Z 35 t1 0.3971684

4 X 34 t2 -0.7438284

5 Y 88 t2 0.9038673

6 Z 35 t2 0.7129142

\> spread(df2, time, val)

subject age t1 t2 t3

1 X 34 0.6753014 -0.7438284 0.2333987

2 Y 88 0.3588532 0.9038673 -0.5104356

3 Z 35 0.3971684 0.7129142 1.3817088

\> \## The tidyr package is already loaded

\>

\> \# First remove column of row names

\> weather2 \<- weather2\[, -1\]

\>

\> \# Spread the data

\> weather3 \<- spread(weather2, measure, value)

\>

\> \# View the head

\> head(weather3)

year month day CloudCover Events Max.Dew.PointF Max.Gust.SpeedMPH

1 2014 12 X1 6 Rain 46 29

2 2014 12 X2 7 Rain-Snow 40 29

3 2014 12 X3 8 Rain 49 38

4 2014 12 X4 3 24 33

5 2014 12 X5 5 Rain 37 26

6 2014 12 X6 8 Rain 45 25

Max.Humidity Max.Sea.Level.PressureIn Max.TemperatureF
Max.VisibilityMiles

1 74 30.45 64 10

2 92 30.71 42 10

3 100 30.4 51 10

4 69 30.56 43 10

5 85 30.68 42 10

6 100 30.42 45 10

Max.Wind.SpeedMPH Mean.Humidity Mean.Sea.Level.PressureIn
Mean.TemperatureF

1 22 63 30.13 52

2 24 72 30.59 38

3 29 79 30.07 44

4 25 54 30.33 37

5 22 66 30.59 34

6 22 93 30.24 42

Mean.VisibilityMiles Mean.Wind.SpeedMPH MeanDew.PointF Min.DewpointF

1 10 13 40 26

2 8 15 27 17

3 5 12 42 24

4 10 12 21 13

5 10 10 25 12

6 4 8 40 36

Min.Humidity Min.Sea.Level.PressureIn Min.TemperatureF
Min.VisibilityMiles

1 52 30.01 39 10

2 51 30.4 33 2

3 57 29.87 37 1

4 39 30.09 30 10

5 47 30.45 26 5

6 85 30.16 38 0

PrecipitationIn WindDirDegrees

1 0.01 268

2 0.10 62

3 0.44 254

4 0.00 292

5 0.11 61

6 1.09 313

\>

This dataset is looking much better already!

# Clean up dates

100xp

Now that the weather dataset adheres to tidy data principles, the next
step is to prepare it for analysis. We'll start by combining the year,
month, and day columns and recoding the resulting character column as a
date. We can use a combination of base R, stringr, and lubridate to
accomplish this task.

## Instructions

- Load the stringr and lubridate packages

- Use stringr's str_replace() to remove the Xs from the day column
  of weather3

- Create a new column called date. Use the unite()function from tidyr to
  paste together the year, month, and day columns in order, using - as a
  separator (see ?uniteif you need help)

- Coerce the date column using the appropriate function from lubridate

- Use the code provided (select()) to reorder columns, saving the result
  to weather5

- View the head of weather5

\## tidyr and dplyr are already loaded

\# Load the stringr and lubridate packages

library(stringr)

library(lubridate)

\# Remove X's from day column

weather3\$day \<- str_replace(weather3\$day, "X", "")

\# Unite the year, month, and day columns

weather4 \<- unite(weather3, date, year, month, day, sep = "-")

\# Convert date column to proper date format using lubridates's ymd()

weather4\$date \<- ymd(weather4\$date)

\# Rearrange columns using dplyr's select()

weather5 \<- select(weather4, date, Events, CloudCover:WindDirDegrees)

\# View the head of weather5

head(weather5)

\> \## tidyr and dplyr are already loaded

\>

\> \# Load the stringr and lubridate packages

\> library(stringr)

\> library(lubridate)

\>

\> \# Remove X's from day column

\> weather3\$day \<- str_replace(weather3\$day, "X", "")

\>

\> \# Unite the year, month, and day columns

\> weather4 \<- unite(weather3, date, year, month, day, sep = "-")

\>

\> \# Convert date column to proper date format using lubridates's ymd()

\> weather4\$date \<- ymd(weather4\$date)

\>

\> \# Rearrange columns using dplyr's select()

\> weather5 \<- select(weather4, date, Events,
CloudCover:WindDirDegrees)

\>

\> \# View the head of weather5

\> head(weather5)

date Events CloudCover Max.Dew.PointF Max.Gust.SpeedMPH Max.Humidity

1 2014-12-01 Rain 6 46 29 74

2 2014-12-02 Rain-Snow 7 40 29 92

3 2014-12-03 Rain 8 49 38 100

4 2014-12-04 3 24 33 69

5 2014-12-05 Rain 5 37 26 85

6 2014-12-06 Rain 8 45 25 100

Max.Sea.Level.PressureIn Max.TemperatureF Max.VisibilityMiles

1 30.45 64 10

2 30.71 42 10

3 30.4 51 10

4 30.56 43 10

5 30.68 42 10

6 30.42 45 10

Max.Wind.SpeedMPH Mean.Humidity Mean.Sea.Level.PressureIn
Mean.TemperatureF

1 22 63 30.13 52

2 24 72 30.59 38

3 29 79 30.07 44

4 25 54 30.33 37

5 22 66 30.59 34

6 22 93 30.24 42

Mean.VisibilityMiles Mean.Wind.SpeedMPH MeanDew.PointF Min.DewpointF

1 10 13 40 26

2 8 15 27 17

3 5 12 42 24

4 10 12 21 13

5 10 10 25 12

6 4 8 40 36

Min.Humidity Min.Sea.Level.PressureIn Min.TemperatureF
Min.VisibilityMiles

1 52 30.01 39 10

2 51 30.4 33 2

3 57 29.87 37 1

4 39 30.09 30 10

5 47 30.45 26 5

6 85 30.16 38 0

PrecipitationIn WindDirDegrees

1 0.01 268

2 0.10 62

3 0.44 254

4 0.00 292

5 0.11 61

6 1.09 313

\>

Great! You can see now that it's not too difficult to convert dates into
a different format.

# A closer look at column types

100xp

It's important for analysis that variables are coded appropriately. This
is not yet the case with our weather data. Recall that functions such
as as.numeric() and as.character() can be used to *coerce* variables
into different types.

It's important to keep in mind that coercions are not always successful,
particularly if there's some data in a column that you don't expect. For
example, the following will cause problems:

as.numeric(c(4, 6.44, "some string", 222))

If you run the code above in the console, you'll get a warning message
saying that R introduced an NA in the process of coercing to numeric.
This is because it doesn't know how to make a number out of a string
("some string"). Watch out for this in our weather data!

## Instructions

- Use str() to see how variables are stored in weather5

- View the first 20 rows of weather5. Keep an eye out for strange
  values!

- Try coercing the PrecipitationIn column of weather5 to numeric without
  saving the result

[  
](https://campus.datacamp.com/courses/cleaning-data-in-r/1829?ex=10)

\# View the structure of weather5

str(weather5)

\# Examine the first 20 rows of weather5. Are most of the characters
numeric?

head(weather5, n = 20)

\# See what happens if we try to convert PrecipitationIn to numeric

as.numeric(weather5\$PrecipitationIn)

\> str(weather5)

'data.frame': 366 obs. of 23 variables:

\$ date : POSIXct, format: "2014-12-01" "2014-12-02" ...

\$ Events : chr "Rain" "Rain-Snow" "Rain" "" ...

\$ CloudCover : chr "6" "7" "8" "3" ...

\$ Max.Dew.PointF : chr "46" "40" "49" "24" ...

\$ Max.Gust.SpeedMPH : chr "29" "29" "38" "33" ...

\$ Max.Humidity : chr "74" "92" "100" "69" ...

\$ Max.Sea.Level.PressureIn : chr "30.45" "30.71" "30.4" "30.56" ...

\$ Max.TemperatureF : chr "64" "42" "51" "43" ...

\$ Max.VisibilityMiles : chr "10" "10" "10" "10" ...

\$ Max.Wind.SpeedMPH : chr "22" "24" "29" "25" ...

\$ Mean.Humidity : chr "63" "72" "79" "54" ...

\$ Mean.Sea.Level.PressureIn: chr "30.13" "30.59" "30.07" "30.33" ...

\$ Mean.TemperatureF : chr "52" "38" "44" "37" ...

\$ Mean.VisibilityMiles : chr "10" "8" "5" "10" ...

\$ Mean.Wind.SpeedMPH : chr "13" "15" "12" "12" ...

\$ MeanDew.PointF : chr "40" "27" "42" "21" ...

\$ Min.DewpointF : chr "26" "17" "24" "13" ...

\$ Min.Humidity : chr "52" "51" "57" "39" ...

\$ Min.Sea.Level.PressureIn : chr "30.01" "30.4" "29.87" "30.09" ...

\$ Min.TemperatureF : chr "39" "33" "37" "30" ...

\$ Min.VisibilityMiles : chr "10" "2" "1" "10" ...

\$ PrecipitationIn : chr "0.01" "0.10" "0.44" "0.00" ...

\$ WindDirDegrees : chr "268" "62" "254" "292" ...

\> \# View the structure of weather5

\> str(weather5)

'data.frame': 366 obs. of 23 variables:

\$ date : POSIXct, format: "2014-12-01" "2014-12-02" ...

\$ Events : chr "Rain" "Rain-Snow" "Rain" "" ...

\$ CloudCover : chr "6" "7" "8" "3" ...

\$ Max.Dew.PointF : chr "46" "40" "49" "24" ...

\$ Max.Gust.SpeedMPH : chr "29" "29" "38" "33" ...

\$ Max.Humidity : chr "74" "92" "100" "69" ...

\$ Max.Sea.Level.PressureIn : chr "30.45" "30.71" "30.4" "30.56" ...

\$ Max.TemperatureF : chr "64" "42" "51" "43" ...

\$ Max.VisibilityMiles : chr "10" "10" "10" "10" ...

\$ Max.Wind.SpeedMPH : chr "22" "24" "29" "25" ...

\$ Mean.Humidity : chr "63" "72" "79" "54" ...

\$ Mean.Sea.Level.PressureIn: chr "30.13" "30.59" "30.07" "30.33" ...

\$ Mean.TemperatureF : chr "52" "38" "44" "37" ...

\$ Mean.VisibilityMiles : chr "10" "8" "5" "10" ...

\$ Mean.Wind.SpeedMPH : chr "13" "15" "12" "12" ...

\$ MeanDew.PointF : chr "40" "27" "42" "21" ...

\$ Min.DewpointF : chr "26" "17" "24" "13" ...

\$ Min.Humidity : chr "52" "51" "57" "39" ...

\$ Min.Sea.Level.PressureIn : chr "30.01" "30.4" "29.87" "30.09" ...

\$ Min.TemperatureF : chr "39" "33" "37" "30" ...

\$ Min.VisibilityMiles : chr "10" "2" "1" "10" ...

\$ PrecipitationIn : chr "0.01" "0.10" "0.44" "0.00" ...

\$ WindDirDegrees : chr "268" "62" "254" "292" ...

\>

\> \# Examine the first 20 rows of weather5. Are most of the characters
numeric?

\> head(weather5, n = 20)

date Events CloudCover Max.Dew.PointF Max.Gust.SpeedMPH

1 2014-12-01 Rain 6 46 29

2 2014-12-02 Rain-Snow 7 40 29

3 2014-12-03 Rain 8 49 38

4 2014-12-04 3 24 33

5 2014-12-05 Rain 5 37 26

6 2014-12-06 Rain 8 45 25

7 2014-12-07 Rain 6 36 32

8 2014-12-08 Snow 8 28 28

9 2014-12-09 Rain 8 49 52

10 2014-12-10 Rain 8 45 29

11 2014-12-11 Rain-Snow 8 37 28

12 2014-12-12 Snow 7 28 21

13 2014-12-13 5 28 23

14 2014-12-14 4 29 20

15 2014-12-15 2 33 21

16 2014-12-16 Rain 8 42 10

17 2014-12-17 Rain 8 46 26

18 2014-12-18 Rain 7 34 30

19 2014-12-19 4 25 23

20 2014-12-20 Snow 6 30 26

Max.Humidity Max.Sea.Level.PressureIn Max.TemperatureF
Max.VisibilityMiles

1 74 30.45 64 10

2 92 30.71 42 10

3 100 30.4 51 10

4 69 30.56 43 10

5 85 30.68 42 10

6 100 30.42 45 10

7 92 30.69 38 10

8 92 30.77 29 10

9 100 30.51 49 10

10 100 29.58 48 10

11 92 29.81 39 10

12 85 29.88 39 10

13 75 29.86 42 10

14 82 29.91 45 10

15 89 30.15 42 10

16 96 30.17 44 10

17 100 29.91 49 10

18 89 29.87 44 10

19 69 30.15 37 10

20 89 30.31 36 10

Max.Wind.SpeedMPH Mean.Humidity Mean.Sea.Level.PressureIn
Mean.TemperatureF

1 22 63 30.13 52

2 24 72 30.59 38

3 29 79 30.07 44

4 25 54 30.33 37

5 22 66 30.59 34

6 22 93 30.24 42

7 25 61 30.46 30

8 21 70 30.67 24

9 38 93 30.04 39

10 23 95 29.5 43

11 21 87 29.61 36

12 16 75 29.85 35

13 17 65 29.82 37

14 15 68 29.83 39

15 15 75 30.05 37

16 8 85 30.09 40

17 20 85 29.75 45

18 23 73 29.78 40

19 17 63 29.98 33

20 21 79 30.26 32

Mean.VisibilityMiles Mean.Wind.SpeedMPH MeanDew.PointF Min.DewpointF

1 10 13 40 26

2 8 15 27 17

3 5 12 42 24

4 10 12 21 13

5 10 10 25 12

6 4 8 40 36

7 10 15 20 -3

8 8 13 16 3

9 2 20 41 28

10 3 13 39 37

11 7 13 31 27

12 10 11 27 25

13 10 12 26 24

14 10 10 27 25

15 10 6 29 27

16 9 4 36 30

17 6 11 41 32

18 10 14 30 26

19 10 11 22 20

20 10 10 24 20

Min.Humidity Min.Sea.Level.PressureIn Min.TemperatureF
Min.VisibilityMiles

1 52 30.01 39 10

2 51 30.4 33 2

3 57 29.87 37 1

4 39 30.09 30 10

5 47 30.45 26 5

6 85 30.16 38 0

7 29 30.24 21 5

8 47 30.51 18 2

9 86 29.49 29 1

10 89 29.43 38 1

11 82 29.44 32 1

12 64 29.81 31 7

13 55 29.78 32 10

14 53 29.78 33 10

15 60 29.91 32 10

16 73 29.92 35 5

17 70 29.69 41 1

18 57 29.71 36 10

19 56 29.86 29 10

20 69 30.17 27 7

PrecipitationIn WindDirDegrees

1 0.01 268

2 0.10 62

3 0.44 254

4 0.00 292

5 0.11 61

6 1.09 313

7 0.13 350

8 0.03 354

9 2.90 38

10 0.28 357

11 0.02 230

12 T 286

13 T 298

14 0.00 306

15 0.00 324

16 T 79

17 0.43 311

18 0.01 281

19 0.00 305

20 T 350

\>

\> \# See what happens if we try to convert PrecipitationIn to numeric

\> as.numeric(weather5\$PrecipitationIn)

Warning message: NAs introduced by coercion

\[1\] 0.01 0.10 0.44 0.00 0.11 1.09 0.13 0.03 2.90 0.28 0.02 NA NA 0.00
0.00

\[16\] NA 0.43 0.01 0.00 NA NA 0.05 0.25 0.56 0.14 0.00 0.00 0.01 0.00
0.00

\[31\] 0.00 0.00 0.00 0.62 0.57 0.00 0.02 NA 0.00 0.01 0.00 0.00 0.20
0.00 NA

\[46\] 0.12 0.00 0.00 0.15 0.00 0.00 0.00 NA 0.00 0.71 0.00 0.10 0.95
0.01 NA

\[61\] 0.06 0.05 0.00 0.78 0.00 0.00 0.09 NA 0.07 0.37 0.88 0.05 0.01
0.03 0.00

\[76\] 0.23 0.39 0.00 0.02 0.01 0.06 0.00 0.17 0.11 0.00 NA 0.07 0.02
0.00 0.00

\[91\] 0.17 0.01 0.26 0.02 NA 0.00 0.00 NA 0.00 0.06 0.01 0.00 0.00 0.80
0.27

\[106\] 0.00 0.14 0.00 0.00 0.05 0.09 0.00 0.00 0.00 0.04 0.80 0.21 0.12
0.00 NA

\[121\] 0.00 0.00 0.00 0.03 0.39 0.00 0.00 0.03 0.26 0.09 0.09 0.00 0.00
0.00 0.01

\[136\] 0.00 0.00 0.06 0.00 0.00 0.61 0.54 NA 0.00 NA 0.00 0.00 0.10
0.07 0.00

\[151\] 0.00 0.00 0.00 0.00 0.00 0.02 0.00 0.00 0.00 0.00 0.00 0.00 0.02
0.00 0.00

\[166\] 0.00 NA 0.00 0.00 0.27 0.00 0.00 NA 0.00 0.00 NA 0.00 0.00 NA
0.00

\[181\] 0.00 0.91 0.38 0.74 0.00 0.00 NA 0.09 0.00 NA NA 0.00 0.00 0.00
NA

\[196\] 0.00 0.40 NA 0.00 0.00 0.00 0.04 1.72 0.00 0.01 0.00 0.00 NA
0.20 1.43

\[211\] NA 0.00 0.50 0.00 0.00 NA 0.00 0.00 0.02 NA 0.15 1.12 0.00 0.00
0.00

\[226\] 0.03 NA 0.00 NA 0.14 NA NA NA 0.00 0.00 0.01 0.00 NA 0.06 0.00

\[241\] 0.00 0.02 0.00 NA 0.00 0.00 0.49 0.00 0.00 0.00 0.00 0.00 0.00
0.83 0.00

\[256\] 0.00 0.00 0.08 0.00 0.00 0.14 0.00 0.00 0.63 NA 0.02 NA 0.00 NA
0.00

\[271\] 0.00 0.00 0.00 0.00 0.00 0.00 0.01 NA 0.00 0.00 0.00 0.20 0.00
0.17 0.66

\[286\] 0.01 0.38 0.00 0.00 0.00 0.00 0.00 0.00 NA 0.00 0.00 0.00 0.00
0.00 0.00

\[301\] 0.00 0.00 0.04 2.46 NA 0.08 0.01 0.00 0.00 0.00 0.00 0.00 0.34
0.00 0.00

\[316\] 0.00 0.12 0.00 0.00 NA NA NA 0.00 NA 0.07 NA 0.00 0.00 0.03 0.00

\[331\] 0.00 0.36 0.73 0.00 0.00 NA 0.00 0.00 0.00 0.00 0.00 0.00 0.00
0.00 0.07

\[346\] 0.54 0.04 0.01 0.00 0.00 0.00 0.00 0.00 NA 0.86 0.00 0.30 0.04
0.00 0.00

\[361\] 0.00 0.00 0.21 0.00 0.00 0.14

\>

Good! Scroll the output, notice the warning message. Go back to the
results of the head command if need be. What values in PrecipitationIn
would become NA if coerced to numbers? Why would they be in the dataset
to begin with?

# Column type conversions

100xp

As you saw in the last exercise, "T" was used to denote a *trace* amount
(i.e. too small to be accurately measured) of precipitation in
the PrecipitationIn column. In order to coerce this column to numeric,
you'll need to deal with this somehow. To keep things simple, we will
just replace "T" with the number zero.

## Instructions

- Use str_replace() from stringr to make the proper replacements in
  the PrecipitationIn column of weather5

- Run the call to mutate_each as-is to conveniently
  apply as.numeric() to all columns
  from CloudCover through WindDirDegrees (reading left to right in the
  data), saving the result to weather6

- View the structure of weather6 to confirm the coercions were
  successful

\## The dplyr and stringr packages are already loaded

\# Replace T with 0 (T = trace)

weather5\$PrecipitationIn \<- str_replace(weather5\$PrecipitationIn,
"T", 0)

\# Convert characters to numerics

weather6 \<- mutate_each(weather5, funs(as.numeric),
CloudCover:WindDirDegrees)

\# Look at result

str(weather6)

\> \## The dplyr and stringr packages are already loaded

\>

\> \# Replace T with 0 (T = trace)

\> weather5\$PrecipitationIn \<- str_replace(weather5\$PrecipitationIn,
"T", 0)

\>

\> \# Convert characters to numerics

\> weather6 \<- mutate_each(weather5, funs(as.numeric),
CloudCover:WindDirDegrees)

\>

\> \# Look at result

\> str(weather6)

'data.frame': 366 obs. of 23 variables:

\$ date : POSIXct, format: "2014-12-01" "2014-12-02" ...

\$ Events : chr "Rain" "Rain-Snow" "Rain" "" ...

\$ CloudCover : num 6 7 8 3 5 8 6 8 8 8 ...

\$ Max.Dew.PointF : num 46 40 49 24 37 45 36 28 49 45 ...

\$ Max.Gust.SpeedMPH : num 29 29 38 33 26 25 32 28 52 29 ...

\$ Max.Humidity : num 74 92 100 69 85 100 92 92 100 100 ...

\$ Max.Sea.Level.PressureIn : num 30.4 30.7 30.4 30.6 30.7 ...

\$ Max.TemperatureF : num 64 42 51 43 42 45 38 29 49 48 ...

\$ Max.VisibilityMiles : num 10 10 10 10 10 10 10 10 10 10 ...

\$ Max.Wind.SpeedMPH : num 22 24 29 25 22 22 25 21 38 23 ...

\$ Mean.Humidity : num 63 72 79 54 66 93 61 70 93 95 ...

\$ Mean.Sea.Level.PressureIn: num 30.1 30.6 30.1 30.3 30.6 ...

\$ Mean.TemperatureF : num 52 38 44 37 34 42 30 24 39 43 ...

\$ Mean.VisibilityMiles : num 10 8 5 10 10 4 10 8 2 3 ...

\$ Mean.Wind.SpeedMPH : num 13 15 12 12 10 8 15 13 20 13 ...

\$ MeanDew.PointF : num 40 27 42 21 25 40 20 16 41 39 ...

\$ Min.DewpointF : num 26 17 24 13 12 36 -3 3 28 37 ...

\$ Min.Humidity : num 52 51 57 39 47 85 29 47 86 89 ...

\$ Min.Sea.Level.PressureIn : num 30 30.4 29.9 30.1 30.4 ...

\$ Min.TemperatureF : num 39 33 37 30 26 38 21 18 29 38 ...

\$ Min.VisibilityMiles : num 10 2 1 10 5 0 5 2 1 1 ...

\$ PrecipitationIn : num 0.01 0.1 0.44 0 0.11 1.09 0.13 0.03 2.9 0.28
...

\$ WindDirDegrees : num 268 62 254 292 61 313 350 354 38 357 ...

\>

Great! It looks like our data are finally in the correct formats and
organized in a logical manner! Now that our data are in the right form,
we can begin the analysis.

# Find missing values

100xp

Before dealing with missing values in the data, it's important to find
them and figure out why they exist in the first place. If your dataset
is too big to look at all at once, like it is here, remember you can
use sum() and is.na() to quickly size up the situation by counting the
number of NAvalues.

The summary() function may also come in handy for identifying which
variables contain the missing values. Finally, the which() function is
useful for locating the missing values within a particular column.

## Instructions

- Use sum() and is.na() to count the number of NAvalues in weather6

- Look at a summary() of weather6 to figure out how the missings are
  distributed among the different variables

- Use which() to identify the indices (i.e. row numbers)
  where Max.Gust.SpeedMPH is NA and save the result
  to ind(for *indices*)

- Use ind to look at the full rows of weather6 for
  which Max.Gust.SpeedMPH is missing

\# Count missing values

sum(is.na(weather6))

\# Find missing values

summary(weather6)

\# Find indices of NAs in Max.Gust.SpeedMPH

ind \<- which(is.na(weather6\$Max.Gust.SpeedMPH))

\# Look at the full rows for records missing Max.Gust.SpeedMPH

weather6\[ind, \]

\> \# Count missing values

\> sum(is.na(weather6))

\[1\] 6

\>

\> \# Find missing values

\> summary(weather6)

date Events CloudCover

Min. :2014-12-01 00:00:00 Length:366 Min. :0.000

1st Qu.:2015-03-02 06:00:00 Class :character 1st Qu.:3.000

Median :2015-06-01 12:00:00 Mode :character Median :5.000

Mean :2015-06-01 12:00:00 Mean :4.708

3rd Qu.:2015-08-31 18:00:00 3rd Qu.:7.000

Max. :2015-12-01 00:00:00 Max. :8.000

Max.Dew.PointF Max.Gust.SpeedMPH Max.Humidity Max.Sea.Level.PressureIn

Min. :-6.00 Min. : 0.00 Min. : 39.00 Min. :29.58

1st Qu.:32.00 1st Qu.:21.00 1st Qu.: 73.25 1st Qu.:30.00

Median :47.50 Median :25.50 Median : 86.00 Median :30.14

Mean :45.48 Mean :26.99 Mean : 85.69 Mean :30.16

3rd Qu.:61.00 3rd Qu.:31.25 3rd Qu.: 93.00 3rd Qu.:30.31

Max. :75.00 Max. :94.00 Max. :1000.00 Max. :30.88

NA's :6

Max.TemperatureF Max.VisibilityMiles Max.Wind.SpeedMPH Mean.Humidity

Min. :18.00 Min. : 2.000 Min. : 8.00 Min. :28.00

1st Qu.:42.00 1st Qu.:10.000 1st Qu.:16.00 1st Qu.:56.00

Median :60.00 Median :10.000 Median :20.00 Median :66.00

Mean :58.93 Mean : 9.907 Mean :20.62 Mean :66.02

3rd Qu.:76.00 3rd Qu.:10.000 3rd Qu.:24.00 3rd Qu.:76.75

Max. :96.00 Max. :10.000 Max. :38.00 Max. :98.00

Mean.Sea.Level.PressureIn Mean.TemperatureF Mean.VisibilityMiles

Min. :29.49 Min. : 8.00 Min. :-1.000

1st Qu.:29.87 1st Qu.:36.25 1st Qu.: 8.000

Median :30.03 Median :53.50 Median :10.000

Mean :30.04 Mean :51.40 Mean : 8.861

3rd Qu.:30.19 3rd Qu.:68.00 3rd Qu.:10.000

Max. :30.77 Max. :84.00 Max. :10.000

Mean.Wind.SpeedMPH MeanDew.PointF Min.DewpointF Min.Humidity

Min. : 4.00 Min. :-11.00 Min. :-18.00 Min. :16.00

1st Qu.: 8.00 1st Qu.: 24.00 1st Qu.: 16.25 1st Qu.:35.00

Median :10.00 Median : 41.00 Median : 35.00 Median :46.00

Mean :10.68 Mean : 38.96 Mean : 32.25 Mean :48.31

3rd Qu.:13.00 3rd Qu.: 56.00 3rd Qu.: 51.00 3rd Qu.:60.00

Max. :22.00 Max. : 71.00 Max. : 68.00 Max. :96.00

Min.Sea.Level.PressureIn Min.TemperatureF Min.VisibilityMiles
PrecipitationIn

Min. :29.16 Min. :-3.00 Min. : 0.000 Min. :0.0000

1st Qu.:29.76 1st Qu.:30.00 1st Qu.: 2.000 1st Qu.:0.0000

Median :29.94 Median :46.00 Median :10.000 Median :0.0000

Mean :29.93 Mean :43.33 Mean : 6.716 Mean :0.1016

3rd Qu.:30.09 3rd Qu.:60.00 3rd Qu.:10.000 3rd Qu.:0.0400

Max. :30.64 Max. :74.00 Max. :10.000 Max. :2.9000

WindDirDegrees

Min. : 1.0

1st Qu.:113.0

Median :222.0

Mean :200.1

3rd Qu.:275.0

Max. :360.0

\>

\> \# Find indices of NAs in Max.Gust.SpeedMPH

\> ind \<- which(is.na(weather6\$Max.Gust.SpeedMPH))

\>

\> \# Look at the full rows for records missing Max.Gust.SpeedMPH

\> weather6\[ind, \]

date Events CloudCover Max.Dew.PointF Max.Gust.SpeedMPH Max.Humidity

169 2015-05-18 Fog 6 52 NA 100

185 2015-06-03 7 48 NA 93

251 2015-08-08 4 61 NA 87

275 2015-09-01 1 63 NA 78

316 2015-10-12 0 56 NA 89

338 2015-11-03 1 44 NA 82

Max.Sea.Level.PressureIn Max.TemperatureF Max.VisibilityMiles

169 30.30 58 10

185 30.31 56 10

251 30.02 76 10

275 30.06 79 10

316 29.86 76 10

338 30.25 73 10

Max.Wind.SpeedMPH Mean.Humidity Mean.Sea.Level.PressureIn
Mean.TemperatureF

169 16 79 30.23 54

185 14 82 30.24 52

251 14 68 29.99 69

275 15 65 30.02 74

316 15 65 29.80 64

338 16 57 30.13 60

Mean.VisibilityMiles Mean.Wind.SpeedMPH MeanDew.PointF Min.DewpointF

169 8 10 48 43

185 10 7 45 43

251 10 6 57 54

275 10 9 62 59

316 10 8 51 48

338 10 8 42 40

Min.Humidity Min.Sea.Level.PressureIn Min.TemperatureF
Min.VisibilityMiles

169 57 30.12 49 0

185 71 30.19 47 10

251 49 29.95 61 10

275 52 29.96 69 10

316 41 29.74 51 10

338 31 30.06 47 10

PrecipitationIn WindDirDegrees

169 0 72

185 0 90

251 0 45

275 0 54

316 0 199

338 0 281

\>

Good job! In this situation it's unclear why these values are missing
and there doesn't appear to be any obvious pattern to their missingness,
so we'll leave them alone for now.

# An obvious error

100xp

Besides missing values, we want to know if there are values in the data
that are too extreme or bizarre to be plausible. A great way to start
the search for these values is with summary().

Once implausible values are identified, they must be dealt with in an
intelligent and informed way. Sometimes the best way forward is obvious
and other times it may require some research and/or discussions with the
original collectors of the data.

## Instructions

- View a summary() of weather6

- Use which() to find the index of the erroneous element
  of weather6\$Max.Humidity, saving the result to ind

- Use ind to look at the full row of weather6 for that day

- You discover an extra zero was accidentally added to this value.
  Correct it in the data

\# Review distributions for all variables

summary(weather6)

\# Find row with Max.Humidity of 1000

ind \<- which(weather6\$Max.Humidity == 1000)

\# Look at the data for that day

weather6\[ind, \]

\# Change 1000 to 100

weather6\$Max.Humidity\[ind\] \<- 100

\> \# Review distributions for all variables

\> summary(weather6)

date Events CloudCover

Min. :2014-12-01 00:00:00 Length:366 Min. :0.000

1st Qu.:2015-03-02 06:00:00 Class :character 1st Qu.:3.000

Median :2015-06-01 12:00:00 Mode :character Median :5.000

Mean :2015-06-01 12:00:00 Mean :4.708

3rd Qu.:2015-08-31 18:00:00 3rd Qu.:7.000

Max. :2015-12-01 00:00:00 Max. :8.000

Max.Dew.PointF Max.Gust.SpeedMPH Max.Humidity Max.Sea.Level.PressureIn

Min. :-6.00 Min. : 0.00 Min. : 39.00 Min. :29.58

1st Qu.:32.00 1st Qu.:21.00 1st Qu.: 73.25 1st Qu.:30.00

Median :47.50 Median :25.50 Median : 86.00 Median :30.14

Mean :45.48 Mean :26.99 Mean : 85.69 Mean :30.16

3rd Qu.:61.00 3rd Qu.:31.25 3rd Qu.: 93.00 3rd Qu.:30.31

Max. :75.00 Max. :94.00 Max. :1000.00 Max. :30.88

NA's :6

Max.TemperatureF Max.VisibilityMiles Max.Wind.SpeedMPH Mean.Humidity

Min. :18.00 Min. : 2.000 Min. : 8.00 Min. :28.00

1st Qu.:42.00 1st Qu.:10.000 1st Qu.:16.00 1st Qu.:56.00

Median :60.00 Median :10.000 Median :20.00 Median :66.00

Mean :58.93 Mean : 9.907 Mean :20.62 Mean :66.02

3rd Qu.:76.00 3rd Qu.:10.000 3rd Qu.:24.00 3rd Qu.:76.75

Max. :96.00 Max. :10.000 Max. :38.00 Max. :98.00

Mean.Sea.Level.PressureIn Mean.TemperatureF Mean.VisibilityMiles

Min. :29.49 Min. : 8.00 Min. :-1.000

1st Qu.:29.87 1st Qu.:36.25 1st Qu.: 8.000

Median :30.03 Median :53.50 Median :10.000

Mean :30.04 Mean :51.40 Mean : 8.861

3rd Qu.:30.19 3rd Qu.:68.00 3rd Qu.:10.000

Max. :30.77 Max. :84.00 Max. :10.000

Mean.Wind.SpeedMPH MeanDew.PointF Min.DewpointF Min.Humidity

Min. : 4.00 Min. :-11.00 Min. :-18.00 Min. :16.00

1st Qu.: 8.00 1st Qu.: 24.00 1st Qu.: 16.25 1st Qu.:35.00

Median :10.00 Median : 41.00 Median : 35.00 Median :46.00

Mean :10.68 Mean : 38.96 Mean : 32.25 Mean :48.31

3rd Qu.:13.00 3rd Qu.: 56.00 3rd Qu.: 51.00 3rd Qu.:60.00

Max. :22.00 Max. : 71.00 Max. : 68.00 Max. :96.00

Min.Sea.Level.PressureIn Min.TemperatureF Min.VisibilityMiles
PrecipitationIn

Min. :29.16 Min. :-3.00 Min. : 0.000 Min. :0.0000

1st Qu.:29.76 1st Qu.:30.00 1st Qu.: 2.000 1st Qu.:0.0000

Median :29.94 Median :46.00 Median :10.000 Median :0.0000

Mean :29.93 Mean :43.33 Mean : 6.716 Mean :0.1016

3rd Qu.:30.09 3rd Qu.:60.00 3rd Qu.:10.000 3rd Qu.:0.0400

Max. :30.64 Max. :74.00 Max. :10.000 Max. :2.9000

WindDirDegrees

Min. : 1.0

1st Qu.:113.0

Median :222.0

Mean :200.1

3rd Qu.:275.0

Max. :360.0

\>

\> \# Find row with Max.Humidity of 1000

\> ind \<- which(weather6\$Max.Humidity == 1000)

\>

\> \# Look at the data for that day

\> weather6\[ind, \]

date Events CloudCover Max.Dew.PointF

142 2015-04-21 Fog-Rain-Thunderstorm 6 57

Max.Gust.SpeedMPH Max.Humidity Max.Sea.Level.PressureIn Max.TemperatureF

142 94 1000 29.75 65

Max.VisibilityMiles Max.Wind.SpeedMPH Mean.Humidity

142 10 20 71

Mean.Sea.Level.PressureIn Mean.TemperatureF Mean.VisibilityMiles

142 29.6 56 5

Mean.Wind.SpeedMPH MeanDew.PointF Min.DewpointF Min.Humidity

142 10 49 36 42

Min.Sea.Level.PressureIn Min.TemperatureF Min.VisibilityMiles

142 29.53 46 0

PrecipitationIn WindDirDegrees

142 0.54 184

\>

\> \# Change 1000 to 100

\> weather6\$Max.Humidity\[ind\] \<- 100

\>

Nice! Once you find obvious errors, it's not too hard to fix them if you
know which values they should take.

# Another obvious error

100xp

You've discovered and repaired one obvious error in the data, but it
appears that there's another. Sometimes you get lucky and can infer the
correct or intended value from the other data. For example, if you know
the minimum and maximum values of a particular metric on a given day...

## Instructions

- Use summary() to look at the value
  of *only* the Mean.VisibilityMiles variable of weather6

- Determine the element of the value that is clearly erroneous in this
  column, saving the result to ind

- Use ind to look at the full row of weather6 for this day

- Inspect the values of other variables for this day to determine the
  correct value of Mean.VisibilityMiles, then make the appropriate fix

\# Look at summary of Mean.VisibilityMiles

summary(weather6\$Mean.VisibilityMiles)

\# Get index of row with -1 value

ind \<- which(weather6\$Mean.VisibilityMiles == -1)

\# Look at full row

weather6\[ind,\]

\# Set Mean.VisibilityMiles to the appropriate value

weather6\$Mean.VisibilityMiles\[ind\] \<-
(weather6\$Min.VisibilityMiles + weather6\$Max.VisibilityMiles)/2

\> head(weather6)

date Events CloudCover Max.Dew.PointF Max.Gust.SpeedMPH Max.Humidity

1 2014-12-01 Rain 6 46 29 74

2 2014-12-02 Rain-Snow 7 40 29 92

3 2014-12-03 Rain 8 49 38 100

4 2014-12-04 3 24 33 69

5 2014-12-05 Rain 5 37 26 85

6 2014-12-06 Rain 8 45 25 100

Max.Sea.Level.PressureIn Max.TemperatureF Max.VisibilityMiles

1 30.45 64 10

2 30.71 42 10

3 30.40 51 10

4 30.56 43 10

5 30.68 42 10

6 30.42 45 10

Max.Wind.SpeedMPH Mean.Humidity Mean.Sea.Level.PressureIn
Mean.TemperatureF

1 22 63 30.13 52

2 24 72 30.59 38

3 29 79 30.07 44

4 25 54 30.33 37

5 22 66 30.59 34

6 22 93 30.24 42

Mean.VisibilityMiles Mean.Wind.SpeedMPH MeanDew.PointF Min.DewpointF

1 10 13 40 26

2 8 15 27 17

3 5 12 42 24

4 10 12 21 13

5 10 10 25 12

6 4 8 40 36

Min.Humidity Min.Sea.Level.PressureIn Min.TemperatureF
Min.VisibilityMiles

1 52 30.01 39 10

2 51 30.40 33 2

3 57 29.87 37 1

4 39 30.09 30 10

5 47 30.45 26 5

6 85 30.16 38 0

PrecipitationIn WindDirDegrees

1 0.01 268

2 0.10 62

3 0.44 254

4 0.00 292

5 0.11 61

6 1.09 313

\> \# Look at summary of Mean.VisibilityMiles

\> summary(weather6\$Mean.VisibilityMiles)

Min. 1st Qu. Median Mean 3rd Qu. Max.

-1.000 8.000 10.000 8.861 10.000 10.000

\>

\> \# Get index of row with -1 value

\> ind \<- which(weather6\$Mean.VisibilityMiles == -1)

\>

\> \# Look at full row

\> weather6\[ind,\]

date Events CloudCover Max.Dew.PointF Max.Gust.SpeedMPH Max.Humidity

200 2015-06-18 5 54 23 72

Max.Sea.Level.PressureIn Max.TemperatureF Max.VisibilityMiles

200 30.14 76 10

Max.Wind.SpeedMPH Mean.Humidity Mean.Sea.Level.PressureIn
Mean.TemperatureF

200 17 59 30.04 67

Mean.VisibilityMiles Mean.Wind.SpeedMPH MeanDew.PointF Min.DewpointF

200 -1 10 49 45

Min.Humidity Min.Sea.Level.PressureIn Min.TemperatureF
Min.VisibilityMiles

200 46 29.93 57 10

PrecipitationIn WindDirDegrees

200 0 189

\>

\> \# Set Mean.VisibilityMiles to the appropriate value

\> weather6\$Mean.VisibilityMiles\[ind\] \<-
(weather6\$Min.VisibilityMiles + weather6\$Max.VisibilityMiles)/2

Warning message: number of items to replace is not a multiple of
replacement length

\>

Well done! Your data are looking tidy. Just a quick sanity check left!

# Check other extreme values

100xp

In addition to dealing with obvious errors in the data, we want to see
if there are other extreme values. In addition to the
trusty summary() function, hist() is useful for quickly getting a feel
for how different variables are distributed.

## Instructions

- Check a summary() of weather6 one more time for extreme or unexpected
  values

- View a histogram for MeanDew.PointF

- Do the same for Min.TemperatureF

- And once more for Mean.TemperatureF to compare distributions

\# Review summary of full data once more

summary(weather6)

\# Look at histogram for MeanDew.PointF

hist(weather6\$MeanDew.PointF)

\# Look at histogram for Min.TemperatureF

hist(weather6\$Min.TemperatureF)

\# Compare to histogram for Mean.TemperatureF

hist(weather6\$Mean.TemperatureF)

\> \# Review summary of full data once more

\> summary(weather6)

date Events CloudCover

Min. :2014-12-01 00:00:00 Length:366 Min. :0.000

1st Qu.:2015-03-02 06:00:00 Class :character 1st Qu.:3.000

Median :2015-06-01 12:00:00 Mode :character Median :5.000

Mean :2015-06-01 12:00:00 Mean :4.708

3rd Qu.:2015-08-31 18:00:00 3rd Qu.:7.000

Max. :2015-12-01 00:00:00 Max. :8.000

Max.Dew.PointF Max.Gust.SpeedMPH Max.Humidity Max.Sea.Level.PressureIn

Min. :-6.00 Min. : 0.00 Min. : 39.00 Min. :29.58

1st Qu.:32.00 1st Qu.:21.00 1st Qu.: 73.25 1st Qu.:30.00

Median :47.50 Median :25.50 Median : 86.00 Median :30.14

Mean :45.48 Mean :26.99 Mean : 83.23 Mean :30.16

3rd Qu.:61.00 3rd Qu.:31.25 3rd Qu.: 93.00 3rd Qu.:30.31

Max. :75.00 Max. :94.00 Max. :100.00 Max. :30.88

NA's :6

Max.TemperatureF Max.VisibilityMiles Max.Wind.SpeedMPH Mean.Humidity

Min. :18.00 Min. : 2.000 Min. : 8.00 Min. :28.00

1st Qu.:42.00 1st Qu.:10.000 1st Qu.:16.00 1st Qu.:56.00

Median :60.00 Median :10.000 Median :20.00 Median :66.00

Mean :58.93 Mean : 9.907 Mean :20.62 Mean :66.02

3rd Qu.:76.00 3rd Qu.:10.000 3rd Qu.:24.00 3rd Qu.:76.75

Max. :96.00 Max. :10.000 Max. :38.00 Max. :98.00

Mean.Sea.Level.PressureIn Mean.TemperatureF Mean.VisibilityMiles

Min. :29.49 Min. : 8.00 Min. : 1.000

1st Qu.:29.87 1st Qu.:36.25 1st Qu.: 8.000

Median :30.03 Median :53.50 Median :10.000

Mean :30.04 Mean :51.40 Mean : 8.891

3rd Qu.:30.19 3rd Qu.:68.00 3rd Qu.:10.000

Max. :30.77 Max. :84.00 Max. :10.000

Mean.Wind.SpeedMPH MeanDew.PointF Min.DewpointF Min.Humidity

Min. : 4.00 Min. :-11.00 Min. :-18.00 Min. :16.00

1st Qu.: 8.00 1st Qu.: 24.00 1st Qu.: 16.25 1st Qu.:35.00

Median :10.00 Median : 41.00 Median : 35.00 Median :46.00

Mean :10.68 Mean : 38.96 Mean : 32.25 Mean :48.31

3rd Qu.:13.00 3rd Qu.: 56.00 3rd Qu.: 51.00 3rd Qu.:60.00

Max. :22.00 Max. : 71.00 Max. : 68.00 Max. :96.00

Min.Sea.Level.PressureIn Min.TemperatureF Min.VisibilityMiles
PrecipitationIn

Min. :29.16 Min. :-3.00 Min. : 0.000 Min. :0.0000

1st Qu.:29.76 1st Qu.:30.00 1st Qu.: 2.000 1st Qu.:0.0000

Median :29.94 Median :46.00 Median :10.000 Median :0.0000

Mean :29.93 Mean :43.33 Mean : 6.716 Mean :0.1016

3rd Qu.:30.09 3rd Qu.:60.00 3rd Qu.:10.000 3rd Qu.:0.0400

Max. :30.64 Max. :74.00 Max. :10.000 Max. :2.9000

WindDirDegrees

Min. : 1.0

1st Qu.:113.0

Median :222.0

Mean :200.1

3rd Qu.:275.0

Max. :360.0

\>

\> \# Look at histogram for MeanDew.PointF

\> hist(weather6\$MeanDew.PointF)

\>

\> \# Look at histogram for Min.TemperatureF

\> hist(weather6\$Min.TemperatureF)

\>

\> \# Compare to histogram for Mean.TemperatureF

\> hist(weather6\$Mean.TemperatureF)

\>

![](media/image11.png)

![](media/image12.png)

![](media/image13.png)

Great job! It looks like you have sufficiently tidied your data!

# Finishing touches

100xp

Before offically calling our weather data clean, we want to put a couple
of finishing touches on the data. These are a bit more subjective and
may not be necessary for analysis, but they will make the data easier
for others to interpret, which is generally a good thing.

There are a number of stylistic conventions in the R language. Depending
on who you ask, these conventions may vary. Because the period (.) has
special meaning in certain situations, we generally recommend using
underscores (\_) to separate words in variable names. We also prefer all
lowercase letters so that no one has to remember which letters are
uppercase or lowercase.

Finally, the events column (renamed to be all lowercase in the first
instruction) contains an empty string ("") for any day on which there
was no significant weather event such as rain, fog, a thunderstorm, etc.
However, if it's the first time you're seeing these data, it may not be
obvious that this is the case, so it's best for us to be explicit and
replace the empty strings with something more meaningful.

## Instructions

- We've created a vector of column names in your workspace
  called new_colnames, all of which obey the conventions described
  above. Clean up the column names of weather6 by
  assigning new_colnames to names(weather6)

- Replace all empty strings in the events column of weather6 with "None"

- One last time, print out the first 6 rows of the weather6 data frame
  to see the changes

\# Clean up column names

names(weather6) \<- new_colnames

\# Replace empty cells in events column

weather6\$events\[weather6\$events == ""\] \<- "None"

\# Print the first 6 rows of weather6

head(weather6, n = 6)

\> \# Clean up column names

\> names(weather6) \<- new_colnames

\>

\> \# Replace empty cells in events column

\> weather6\$events\[weather6\$events == ""\] \<- "None"

\>

\> \# Print the first 6 rows of weather6

\> head(weather6, n = 6)

date events cloud_cover max_dew_point_f max_gust_speed_mph

1 2014-12-01 Rain 6 46 29

2 2014-12-02 Rain-Snow 7 40 29

3 2014-12-03 Rain 8 49 38

4 2014-12-04 None 3 24 33

5 2014-12-05 Rain 5 37 26

6 2014-12-06 Rain 8 45 25

max_humidity max_sea_level_pressure_in max_temperature_f
max_visibility_miles

1 74 30.45 64 10

2 92 30.71 42 10

3 100 30.40 51 10

4 69 30.56 43 10

5 85 30.68 42 10

6 100 30.42 45 10

max_wind_speed_mph mean_humidity mean_sea_level_pressure_in

1 22 63 30.13

2 24 72 30.59

3 29 79 30.07

4 25 54 30.33

5 22 66 30.59

6 22 93 30.24

mean_temperature_f mean_visibility_miles mean_wind_speed_mph
mean_dew_point_f

1 52 10 13 40

2 38 8 15 27

3 44 5 12 42

4 37 10 12 21

5 34 10 10 25

6 42 4 8 40

min_dew_point_f min_humidity min_sea_level_pressure_in min_temperature_f

1 26 52 30.01 39

2 17 51 30.40 33

3 24 57 29.87 37

4 13 39 30.09 30

5 12 47 30.45 26

6 36 85 30.16 38

min_visibility_miles precipitation_in wind_dir_degrees

1 10 0.01 268

2 2 0.10 62

3 1 0.44 254

4 10 0.00 292

5 5 0.11 61

6 0 1.09 313

\>

Great job! Your data are now tidy and in an easy format for others to
examine!
