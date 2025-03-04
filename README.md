
<!-- README.md is generated from README.Rmd. Please edit the README.Rmd file -->

# Lab report \#1

Follow the instructions posted at
<https://ds202-at-isu.github.io/labs.html> for the lab assignment. The
work is meant to be finished during the lab time, but you have time
until Monday evening to polish things.

Include your answers in this document (Rmd file). Make sure that it
knits properly (into the md file). Upload both the Rmd and the md file
to your repository.

All submissions to the github repo will be automatically uploaded for
grading once the due date is passed. Submit a link to your repository on
Canvas (only one submission per team) to signal to the instructors that
you are done with your submission.

### step 1 result:

(Jordyn)

``` r
library(classdata)

head(ames)
```

    ##    Parcel ID                       Address             Style
    ## 1 0903202160      1024 RIDGEWOOD AVE, AMES 1 1/2 Story Frame
    ## 2 0907428215 4503 TWAIN CIR UNIT 105, AMES     1 Story Frame
    ## 3 0909428070        2030 MCCARTHY RD, AMES     1 Story Frame
    ## 4 0923203160         3404 EMERALD DR, AMES     1 Story Frame
    ## 5 0520440010       4507 EVEREST  AVE, AMES              <NA>
    ## 6 0907275030       4512 HEMINGWAY DR, AMES     2 Story Frame
    ##                        Occupancy  Sale Date Sale Price Multi Sale YearBuilt
    ## 1 Single-Family / Owner Occupied 2022-08-12     181900       <NA>      1940
    ## 2                    Condominium 2022-08-04     127100       <NA>      2006
    ## 3 Single-Family / Owner Occupied 2022-08-15          0       <NA>      1951
    ## 4                      Townhouse 2022-08-09     245000       <NA>      1997
    ## 5                           <NA> 2022-08-03     449664       <NA>        NA
    ## 6 Single-Family / Owner Occupied 2022-08-16     368000       <NA>      1996
    ##   Acres TotalLivingArea (sf) Bedrooms FinishedBsmtArea (sf) LotArea(sf)  AC
    ## 1 0.109                 1030        2                    NA        4740 Yes
    ## 2 0.027                  771        1                    NA        1181 Yes
    ## 3 0.321                 1456        3                  1261       14000 Yes
    ## 4 0.103                 1289        4                   890        4500 Yes
    ## 5 0.287                   NA       NA                    NA       12493  No
    ## 6 0.494                 2223        4                    NA       21533 Yes
    ##   FirePlace              Neighborhood
    ## 1       Yes       (28) Res: Brookside
    ## 2        No    (55) Res: Dakota Ridge
    ## 3        No        (32) Res: Crawford
    ## 4        No        (31) Res: Mitchell
    ## 5        No (19) Res: North Ridge Hei
    ## 6       Yes   (37) Res: College Creek

The variables included in the data set are Parcel ID (Categorical),
Address (Categorical), Style (Categorical), Occupancy (Categorical),
Sale Date (Categorical), Sale Price (Quantitative), Multi Sale
(Categorical), Year Built (Categorical), Acres (Quantitative), Total
Living Area (Quantitative), Bedrooms (Quantitative), Finished Basement
Area (Quantitative), Lot Area (Quantitative), AC (Categorical),
Fireplace (Categorical), Neighborhood (Categorical). Each variable
represents a factor in the pricing of a home. We expect the ranges of
the large variables to be in the thousands.

### step 2 result:

(Ethan) A variable that could be of special interest for this data set
is Sale Price.

### step 3 result:

(Ashlynn and Eitan)

``` r
library(ggplot2)
ggplot(ames, aes(x = `Sale Price`)) + 
  geom_histogram(binwidth=100000) +
  ggtitle("binwidth = 1000")
```

![](README_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

``` r
# get the range of the variable sale price
range(ames$`Sale Price`, na.rm = T)
```

    ## [1]        0 20500000

The general pattern is that the higher the price of the house the less
houses there are. Oddities include insane outliers at certain prices.

### step 4 result:

Jordyn’s work:

I chose to compare the Lot Area against Sale Price to see if there were
any relationships between the two.

``` r
library(ggplot2)
ggplot(data = ames, aes(x = `LotArea(sf)`, y = `Sale Price`)) +
  geom_point() +
  geom_smooth(method = "lm", se = FALSE)
```

    ## `geom_smooth()` using formula = 'y ~ x'

    ## Warning: Removed 89 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).

    ## Warning: Removed 89 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

After plotting the data it is clear that there is really no relationship
between the two variables. The graph was linear, negative, and had no
correlation. There were several outliers, some in the y direction and
some in the x direction. The range of lot area is 0 sf to 1,028 sf. I
don’t think that this pattern really explains any odd findings in the
data, as there was no correlation.

Ashlynn’s work:

``` r
library(ggplot2)
ggplot(data = ames, aes(x = `TotalLivingArea (sf)`, y = `Sale Price`)) +
  geom_point(color = "skyblue", alpha = 0.7) +
  geom_smooth(method = "lm", se = TRUE, color = "blue") +
  scale_x_continuous(limits = c(0, 3000)) + 
  scale_y_continuous(limit = c(0, 1000000))
```

    ## `geom_smooth()` using formula = 'y ~ x'

    ## Warning: Removed 978 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).

    ## Warning: Removed 978 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
  labs(title = "Scatter Plot of Total Living Area vs Sale Price", 
       x = "Total Living Area (sf)", 
       y = "Sale Price") + 
  theme_minimal()
```

    ## NULL

After plotting, it is clear that there is a relationship between the two
variables. The graph has a positive correlation that indicates that as
the total living area increases the price of the house goes up. This is
seen by the regression line in blue. There are only a few outliers that
are seen which could be associated with the house having some value
either historic or being in an expensive area.

Eitan’s work:

``` r
# get the range of the variable Bedrooms
range(ames$Bedrooms, na.rm = T)
```

    ## [1]  0 10

Now we will plot our variable Bedrooms.

``` r
# the plot shows the distribution of homes and their bedroom count
ggplot(ames, aes(x=Bedrooms)) + 
  geom_histogram(binwidth = .5) + 
  scale_x_continuous(limits = c(0, 10))
```

    ## Warning: Removed 447 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_bar()`).

![](README_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

The pattern shows us that most homes have between 2 and 4 bedrooms with
there obviously being outliers on either end.

To find the relationship that the number of bedrooms has to the main
variable of Sale Price I will plot a scatterplot.

``` r
# the plot shows the correlation between number of bedrooms as sale price
ggplot(ames, aes(x = Bedrooms, y = `Sale Price`)) + 
  geom_point(alpha = 0.5) +  
  geom_smooth(method = "lm", se = TRUE, color = "blue") + 
  scale_x_continuous(limits = c(0, 10)) + 
  scale_y_continuous(limit = c(0, 1000000))
```

    ## `geom_smooth()` using formula = 'y ~ x'

    ## Warning: Removed 817 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).

    ## Warning: Removed 817 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

``` r
  labs(title = "Relationship Between Number of Bedrooms and Sale Price",
       x = "Number of Bedrooms",
       y = "Sale Price ($)") +
  theme_minimal()
```

    ## NULL

The overall pattern of the plot after I removed crazy outliers shows the
trend we were expecting with a position correlation between sale price
and number of bedrooms. The oddities that we found in 3 which were the
outliers proved to influence the data as we expected if untouched.

Ethan’s work: I chose to compare Year Built against the special interest
variable of Sale Price. The range of this variable is from 1880 - 2022
(with on line showing 0 as a the year built indicating an error in
entering of the data) Below is the histogram plot of the variable
“YearBuilt”. The pattern shows the majority of the houses were built in
the late 1990’s and early 2000’s, but besides the one outlier at 0 the
data shows a bell curve that may be skewed left a bit.

``` r
library(classdata)
#the below code shows how I found the range of the variable "YearBuilt"
range(ames$YearBuilt, na.rm = T)
```

    ## [1]    0 2022

``` r
library(ggplot2)
#this code shows a histogram of the "YearBuilt" variable with a bandwidth of 5 to show the differences in years between the data. The x axis values were wide because there is one house at 0 due to incorrect entering of data, so a limit was added to the x axis to make the data more readable. 
ggplot(ames, aes(x=YearBuilt)) + geom_histogram(binwidth = 5) + scale_x_continuous(limits = c(1880,2022))
```

    ## Warning: Removed 448 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_bar()`).

![](README_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

After plotting just the “YearBuilt” variable, I plotted it against the
special variable of interest “SalePrice”. Below is the scatterplot of
the two variables. A limit was added to both of the axes in order to
make the plot readable in a sense. The y limit removed 1 outlier where
the “YearBuilt” variable was 0, and the x limit removed two sets of
outliers where the “SalePrice” was 20,000,000 and 14,000,000. From this
graph, you can identify somewhat of a positive correlation, but not a
strong one as data points are everywhere. An interesting oddity would be
at the y axis, where there are a bunch of points ranging from all years
where the “SalePrice” was 0. This plot still shows the oddities of the
main variable from step 3 as it shows points at 0 on the y axis, but it
does not show the outlier oddities that were removed from this graph to
make it readable. Overall, this plot has an unclear shape as points are
scattered all over, unclear pattern as there is no slope for the line of
best fit, weak strength as there is very little clustering between
points, and a very wide spread.

``` r
#this is code for the scatterplot shown below comparing the two variables "SalePrice" and "YearBuilt". A limit was added to both of the axes in order to make the plot readable in a sense.Geom_smooth adds a line of best fit, although it is has no slope. 
ggplot(ames, aes(x=`Sale Price`, y=YearBuilt)) + geom_point() + scale_y_continuous(limits = c(1880,2022)) + scale_x_continuous(limits = c(0,306000)) +  geom_smooth(method = "lm", se = FALSE)
```

    ## `geom_smooth()` using formula = 'y ~ x'

    ## Warning: Removed 1782 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).

    ## Warning: Removed 1782 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](README_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->
