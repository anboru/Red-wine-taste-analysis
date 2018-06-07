RED WINES EXPLORATION by Anna Antonova
======================================

This report contains an analysis of a dataset of 1599 Portuguese Red wines based on their chemical characteristics and wine experts grades of these wines.

Univariate Plots Section
========================

    ## [1] 1599   13

    ## 'data.frame':    1599 obs. of  13 variables:
    ##  $ X                   : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ fixed.acidity       : num  7.4 7.8 7.8 11.2 7.4 7.4 7.9 7.3 7.8 7.5 ...
    ##  $ volatile.acidity    : num  0.7 0.88 0.76 0.28 0.7 0.66 0.6 0.65 0.58 0.5 ...
    ##  $ citric.acid         : num  0 0 0.04 0.56 0 0 0.06 0 0.02 0.36 ...
    ##  $ residual.sugar      : num  1.9 2.6 2.3 1.9 1.9 1.8 1.6 1.2 2 6.1 ...
    ##  $ chlorides           : num  0.076 0.098 0.092 0.075 0.076 0.075 0.069 0.065 0.073 0.071 ...
    ##  $ free.sulfur.dioxide : num  11 25 15 17 11 13 15 15 9 17 ...
    ##  $ total.sulfur.dioxide: num  34 67 54 60 34 40 59 21 18 102 ...
    ##  $ density             : num  0.998 0.997 0.997 0.998 0.998 ...
    ##  $ pH                  : num  3.51 3.2 3.26 3.16 3.51 3.51 3.3 3.39 3.36 3.35 ...
    ##  $ sulphates           : num  0.56 0.68 0.65 0.58 0.56 0.56 0.46 0.47 0.57 0.8 ...
    ##  $ alcohol             : num  9.4 9.8 9.8 9.8 9.4 9.4 9.4 10 9.5 10.5 ...
    ##  $ quality             : int  5 5 5 6 5 5 5 7 7 5 ...

I will change the name of first column with wines id from 'X' to 'wine.id'

    ##     wine.id       fixed.acidity   volatile.acidity  citric.acid   
    ##  Min.   :   1.0   Min.   : 4.60   Min.   :0.1200   Min.   :0.000  
    ##  1st Qu.: 400.5   1st Qu.: 7.10   1st Qu.:0.3900   1st Qu.:0.090  
    ##  Median : 800.0   Median : 7.90   Median :0.5200   Median :0.260  
    ##  Mean   : 800.0   Mean   : 8.32   Mean   :0.5278   Mean   :0.271  
    ##  3rd Qu.:1199.5   3rd Qu.: 9.20   3rd Qu.:0.6400   3rd Qu.:0.420  
    ##  Max.   :1599.0   Max.   :15.90   Max.   :1.5800   Max.   :1.000  
    ##  residual.sugar     chlorides       free.sulfur.dioxide
    ##  Min.   : 0.900   Min.   :0.01200   Min.   : 1.00      
    ##  1st Qu.: 1.900   1st Qu.:0.07000   1st Qu.: 7.00      
    ##  Median : 2.200   Median :0.07900   Median :14.00      
    ##  Mean   : 2.539   Mean   :0.08747   Mean   :15.87      
    ##  3rd Qu.: 2.600   3rd Qu.:0.09000   3rd Qu.:21.00      
    ##  Max.   :15.500   Max.   :0.61100   Max.   :72.00      
    ##  total.sulfur.dioxide    density             pH          sulphates     
    ##  Min.   :  6.00       Min.   :0.9901   Min.   :2.740   Min.   :0.3300  
    ##  1st Qu.: 22.00       1st Qu.:0.9956   1st Qu.:3.210   1st Qu.:0.5500  
    ##  Median : 38.00       Median :0.9968   Median :3.310   Median :0.6200  
    ##  Mean   : 46.47       Mean   :0.9967   Mean   :3.311   Mean   :0.6581  
    ##  3rd Qu.: 62.00       3rd Qu.:0.9978   3rd Qu.:3.400   3rd Qu.:0.7300  
    ##  Max.   :289.00       Max.   :1.0037   Max.   :4.010   Max.   :2.0000  
    ##     alcohol         quality     
    ##  Min.   : 8.40   Min.   :3.000  
    ##  1st Qu.: 9.50   1st Qu.:5.000  
    ##  Median :10.20   Median :6.000  
    ##  Mean   :10.42   Mean   :5.636  
    ##  3rd Qu.:11.10   3rd Qu.:6.000  
    ##  Max.   :14.90   Max.   :8.000

The dataset contains 1599 observations and 13 variables, 1 of them is numeric identifier of a wine.

Let's start with the dependent variable "quality"

![](redwines_project_files/figure-markdown_github/unnamed-chunk-4-1.png)

The distribution is almost normal, with a thinner left tail. The grades go from 3 to 8, and the most frequent grade is 5, the median grade being 6 and mean grade between 5 and 6.

I notice that grades are all integers between 3 and 8. So, I will convert the variable "quality" to a factor and assign the result to a new variable "quality\_factor". Now I can see how many wines got each grade.

    ##   3   4   5   6   7   8 
    ##  10  53 681 638 199  18

Grades 5 and 6 have almost the same number of occurencies, then comes the grade 7 with 199 occurencies. All together, grades 5,6 and 7 represent about 95% of observations. Grades 3, 4 and 8 have an insignificant number of occurencies. It will be interesting to look closer at the wines that got these more rare grades and see what is common to them, what makes a wine stand out as an excellent or on the contrary a clearily inferior wine.

I would also like to create a new grouped quality variable: quality\_grouped. It will be a factor with three levels: low quality (grades 3 and 4), average quality (grades 5 and 6) and good quality (grades 7 and 8). This grouped quality might be helpful later to better understand general trends or to explore the difference between the extremes.

There are 63 low quality wines, 1319 average wines and 217 good wines.

Now let's figure out the distribution of this new variable.

``` r
ggplot(redwines, aes(quality_grouped)) + geom_bar()
```

![](redwines_project_files/figure-markdown_github/unnamed-chunk-7-1.png)

Most wines are of average quality. There are less wines of low quality than wines of good quality.

Here is the exact count of wines per group:

``` r
summary(redwines$quality_grouped)
```

    ##     low average    good 
    ##      63    1319     217

Now let's figure out the dstribution of independent or input variables.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-9-1.png)

I notice that density and pH are distributed normally whereas other chemical caracteristics have eighter skewed distribution (positively for fixed acidity, total sulfur dioxide, free sufur dioxide, sulphates, alcohol, bimodal for volatile acidity). As for citric acid, the distribution does not seem to have a well defined shape, so I will take a closer look at it later. Residual sugar's and chlorides' distribution have a very small spread.

Now, let's take a look at measures of acidity: fixed, volatile and citric acid and pH. Fixed acidity is a measure of such acids as tartaric, malic, citric acids while volatile acidity measures among others acetic acid, the one that is found in vinegar and excess of it alters the wine's quality. All three types of acidity are measured as acids concentration in gram per litre. PH is negative logarithm to the base 10 of hydrogen ions concentration. That is why pH is normally distributed.

### Fixed acidity

![](redwines_project_files/figure-markdown_github/unnamed-chunk-10-1.png)

fixed acidity is positively skewed and varies between 4.6 and 15.9 g/l.

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    4.60    7.10    7.90    8.32    9.20   15.90

I decided to create a new categorical variable for measure of fixed acidity: fixed.acidity\_grouped. I will group data as follows: \* under 7 g/l - flat,
\* between 7 and 9 - low acidity,
\* between 9 and 11 - average acidity,
\* between 11 and 13 - higher acidity and
\* over 13 - very high acidity.

Upper limit in interval is always included and lower limit excluded. For example, low acidity &gt; 7 and &lt;= 9. I plan later to explore data by groups of acidity to see if there are different trends depending on acidity level.

    ##              flat       low acidity   average acidity    higher acidity 
    ##               362               796               306               115 
    ## very high acidity 
    ##                20

Let's look at this new variable distribution.

``` r
ggplot(redwines, aes(fixed.acidity_grouped)) + geom_bar()
```

![](redwines_project_files/figure-markdown_github/unnamed-chunk-13-1.png)

The distribution is positively skewed toward high acidity. Most wines have low acidity.

### Volatile acidity

![](redwines_project_files/figure-markdown_github/unnamed-chunk-14-1.png)

Volatile acidity is normally distributed, but is positively skewed. We can notice two modes: around 0.4 and 0.65.

### PH

![](redwines_project_files/figure-markdown_github/unnamed-chunk-15-1.png)

pH is normally distributed as it is calculated as a logarithm. It represents total acidity strengh.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-16-1.png)

For fixed acidity there are many outliers above 12 g/l.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-17-1.png)

For volatile acidity there are many ouitliers above 1 g/l. Both, fixed and volatile acidity have outliers. I wonder if such a high acidity might affect the quality in a negative way.

I decided to create a new variabe with groups by volatile acidity: \* under 0.2 g/l - 'very low volatile acidity', \* between 0.2 and 0.4 - 'low volatile acidity', \* between 0.4 and 0.8 average volatile acidity and \* above 0.8 - high volatile acidity.

I would like to explore later these groups to see if there are different trends.

    ## very low volatile acidity      low volatile acidity 
    ##                        17                       391 
    ##  average volatile acidity     high volatile acidity 
    ##                      1084                       107

Above you see number of wines per volatile acidity group.

Now let's look at this new variable distribution.

``` r
ggplot(redwines, aes(volatile.acidity_grouped)) + geom_bar()
```

![](redwines_project_files/figure-markdown_github/unnamed-chunk-19-1.png)

The distribution is negatively skewed. Most wines have average volatile acidity.

### Total acidity

What we actually taste is a total acidity, it is very difficult to distinguish which acidity we taste: volatile or fixed. That is why I will create a new variable "total.acidity" which equals the sum of volatile and fixed acidity. Let's look at its distribution

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   5.120   7.680   8.445   8.847   9.740  16.285

![](redwines_project_files/figure-markdown_github/unnamed-chunk-21-1.png)

![](redwines_project_files/figure-markdown_github/unnamed-chunk-22-1.png)

I transformed total acidity into logarthmical scale (base 10). Now the distribution loooks more normal.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-23-1.png)

Among wines of average quality the distribution of total acidity is normal: most of these average wines have the total acidity around 8, whereas low quality and high quality wines acidity is distributed more evenly between around 5 and 12 g/l. This is most probably related to the size of the samples (very few excellent and low quality wines, so there are not enough observations to see a normal distribution). But, let's look closer at excellent wines (grade 8).

![](redwines_project_files/figure-markdown_github/unnamed-chunk-24-1.png)

It is a uniform distribution with three modes. But again, the sample size is too small to draw conclusions.

Citric acidity is the one that gives the wine freshness and some interest. As we've seen earlier, the distribution shape is not well defined, so I will change the binwidth.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-25-1.png)

We notice that citric acid distribution is descending. This is not surprising as citric acid is present naturally at very small concentration in grapes and adding citric acid is not allowed in Europe. That is why the higher the concentration the fewer observations we have. Surprisingly, the mode is 0 g/l: there are over 125 wines without citric acid at all. I will explore it more in detail later. There is another mode at around 0.49 g/l, about 70 wines have this concentration.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-26-1.png)

Here I notice a clear drop at around 0.5 g/l of citric acid. There a very few wines with a concentration of citric acid higher than 0.5 g/l.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-27-1.png)

There are very few outliers for citric acid.

Minimum value for citric acid concentration is 0. Let's verify how many obserations with 0 g/l of citric acid there are.

    ## [1] 132  18

There are 132 wines without citric acid.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-29-1.png)

Wines without citric acid at all did not get any 8 grade and have lesser percentage of grade 7, they also have a higher percentage of grades 3 and 4. Is citrtic acid presence necessary to make a wine outstanding? Does lack of citric acid contribute to the fact that a wine is perceived as a lower quality wine and under wich conditions? Can the lack of citric acid be compensated and how (what differs 7 grade wines with and without citric acid)?

![](redwines_project_files/figure-markdown_github/unnamed-chunk-30-1.png)

![](redwines_project_files/figure-markdown_github/unnamed-chunk-31-1.png)

I changed the binwidth for alcohol distribution. Now the distribution looks smoother. It is positively skewed and has a few upper outliers. Most of wines have alcohol content of 9.5%, but there are peaks at 9.75, 10, 10.5 and 11%. I am surprised to see that there are many wines with alcohol content under 9.5%.

Let's check alcohol data for outliers

    ##  75% 
    ## 13.5

Wines with more than 13.5% alcohol content are outliers. 75% here indicated that the value has been calculated from the 75% quantile.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-34-1.png)

Wines with high alcohol content in this sample did not obtain low grades like 3 or 4 at all. They got relatively more 8 grades than wines with normal alcohol content. Does higher alcohol content enhance wine taste? Of course, the size of high alcohol content' wines subset is too small which probably is the reason for absence of certain grades. Nevertheless, I will keep it in mind and explore the effect of alcohol content on wine quality.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-35-1.png)

We notice that as quality increases the distributions shift to the right. This means that the highr the alcohol content the higher the probability that this wine willl get a higher grade (7 or 8). We don't see the same pattern for lower grades: 3, 4, 5, 6. Let's look at the same distribution but by grouped quality (low, average and good).

![](redwines_project_files/figure-markdown_github/unnamed-chunk-36-1.png)

The probability here is measured by the surface of the area below the curve. Here the trend is clear: at very low alcohol content (below 9%) the probability that the wine will be of low quality is higher than to be of average quality, and almost 0 probability that this wine will be of good quality. This pattern is reversed at higher alcohol content (above 12%). For example, the wine with alcohol content above 12% has very high probabilty of being good, low probability of being average and very low - of being poor.

I would like to create a new variable grouping wines by alcohol content: low (under or equal to 10%), average (higher than 10% and lower than 12%) and high (higher than 12%).

Let's look at this new variable distribution.

``` r
ggplot(redwines, aes(alcohol_grouped)) + geom_bar()
```

![](redwines_project_files/figure-markdown_github/unnamed-chunk-38-1.png)

Here is the exact count of wines per group.

``` r
summary(redwines$alcohol_grouped)
```

    ## Very low alcohol      Low alcohol  Average alcohol     High alcohol 
    ##               37              710              711              141

The distribution look normal with two equal modes: around 700 wines with low alcohol, and 700 wines with average alcohol.

Now let's look at sulphur dioxide (SO2), total sulfur dioxide and sulphates

    ## [1] "free SO2"

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    1.00    7.00   14.00   15.87   21.00   72.00

    ## [1] "total SO2"

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    6.00   22.00   38.00   46.47   62.00  289.00

    ## [1] "potassium sulphates"

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##  0.3300  0.5500  0.6200  0.6581  0.7300  2.0000

![](redwines_project_files/figure-markdown_github/unnamed-chunk-41-1.png)

![](redwines_project_files/figure-markdown_github/unnamed-chunk-42-1.png)

Free sulfur dioxide is necessary to a wine to prevent oxidation and protect wine from bacteria. The distribution is positively skewed. After I transformed the x axis to a log10 axis I can see a less skewed distribution with mode around 6 mg/l. I notice a clear descending trend after concentration of about 15 mg/l.

Potassium sulphates are measured in g/l, their concentration is much higher than the concentration of sulfur dioxide.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-43-1.png)

![](redwines_project_files/figure-markdown_github/unnamed-chunk-44-1.png)

I removed the outliers ( &gt; 1 g/l ) to have a better idea of the distribution of the main data.

The distribution looks close to normal, slightly positively skewed.

Now, I will look at residual sugar. It might be an important factor in wine's taste. As seen earlier its distribution has a normal shape but a very small spread.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-45-1.png)

There are many outliers. I would like to consider separately subset without outilers. I will first determine the value above which data will be considered outliers. I will use 1.5 \* IQR.

    ##  75% 
    ## 3.65

Above 3.65 g/l of residual sugar the wine is considered outlier. 75% indicates that it was calculated from 75% quantile

I will plot residual sugar distribution for subset without outliers (sugar &lt;= 3.65 g/l)

![](redwines_project_files/figure-markdown_github/unnamed-chunk-47-1.png)

There are very few (about 2) wines with sugar less than 1 g/l. Most wines have sugar at around 2 g/l. The distrbution without outliers looks normal.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-48-1.png)

From these plots we can conclude that wines in this sample with high sugar are more likely to get a low grade like 3 or 4. Both high and normal sugar wines might get a high grade such as 8 and wines with high sigar might have higher probability to get a 7 rather than a 6.

### Chlorides

Chlorides are salts and in larger amounts will give a wine salty taste. At some levels it probably goes unnoticed. Chlorides can also compensate for too high acidity. Later I will explore the combination of chlorides and acidity and its influence on wine quality.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-49-1.png)

There are a lot of outliers. I will draw a boxplot for chlorides &lt; 0.12 g/l

![](redwines_project_files/figure-markdown_github/unnamed-chunk-50-1.png)

50% of observations of chlorides content are below 0.08 g/l. The distribution has a small spread: lower quartile is at 0.07 and upper quartile is at 0.09 g/l. I wonder how many outliers are there?

    ##  75% 
    ## 0.12

    ##  25% 
    ## 0.04

Lower outlier limit is 0.04 g/l and upper outlier limit is 0.12 g/l

    ## [1] 100

    ## [1] 9

There are 100 upper outliers: wines with pretty high chlorides content. There are only 9 lower outlier. I wonder how total acidity is distributed among these wines?

![](redwines_project_files/figure-markdown_github/unnamed-chunk-54-1.png)

Compared to total acidity distribution of all wines this distribution is shifted to the right, the median is around 9., whereas the median of all wines acidity was at around 7.75. Is higher chlorides content related to higher acidity?

I would like to check if there are NA values in the dataset.

    ##                  wine.id            fixed.acidity         volatile.acidity 
    ##                        0                        0                        0 
    ##              citric.acid           residual.sugar                chlorides 
    ##                        0                        0                        0 
    ##      free.sulfur.dioxide     total.sulfur.dioxide                  density 
    ##                        0                        0                        0 
    ##                       pH                sulphates                  alcohol 
    ##                        0                        0                        0 
    ##                  quality           quality_factor          quality_grouped 
    ##                        0                        0                        0 
    ##    fixed.acidity_grouped volatile.acidity_grouped            total.acidity 
    ##                        0                        0                        0 
    ##          alcohol_grouped 
    ##                        0

Now, I would like to create a new data frame named "grouped\_data". I will group wines by alcohol content group and volatile acidity group and quality. I will then calculate median value for each predictor variable and each combination of alcohol group, volatile acidity group and quality. I will transform this data frame by gathering all predictor variables columns as values in a new column "predictor"

    ##          alcohol_grouped              volatile.acidity_grouped
    ##  Very low alcohol:104    very low volatile acidity: 65        
    ##  Low alcohol     :195    low volatile acidity     :208        
    ##  Average alcohol :234    average volatile acidity :247        
    ##  High alcohol    :182    high volatile acidity    :195        
    ##                                                               
    ##                                                               
    ##                                                               
    ##     quality      quality_factor            predictor       median       
    ##  Min.   :3.000   3: 52          alcohol         : 55   Min.   :  0.010  
    ##  1st Qu.:5.000   4:104          volatile.acidity: 55   1st Qu.:  0.635  
    ##  Median :6.000   5:182          fixed.acidity   : 55   Median :  3.250  
    ##  Mean   :5.618   6:182          total.acidity   : 55   Mean   :  9.200  
    ##  3rd Qu.:7.000   7:117          citric.acid     : 55   3rd Qu.:  9.500  
    ##  Max.   :8.000   8: 78          pH              : 55   Max.   :373.000  
    ##                                 (Other)         :385

Univariate Analysis
===================

### What is the structure of your dataset?

There are 1599 observations in the data set with 12 features, the 13th variable is numerical ID of each wine. The features are physicochemical properties (independent variables): acidity: volatile, fixed and citric, pH, residual sugars, alcohol, sulfur dioxide: free and total, sulphates, chlorides, density. The dependent variable is quality on the scale of 0 to 10. All variables are numeric, float type, except for quality which is numeric integer. Sulfur dioxode is measured in mg/l, density in g/dl, alcohol in %, other physicochemical properties in g/l. Quality is going from 0 to 10, from worst to best quality, 10 being the best wine.

Other observations:

1.  Most wines are of average quality with grades of 5 or 6

2.  Median quality grade is 6.

3.  The worst grade for this sample is 3 and the best is 8.

4.  Low (grades 3 or 4) and high (grade 8) quality wines represent only 5% of observations.

5.  There are no missing values in the data set.

6.  The only 0 values present in the data set are for citric acid content.

7.  Most wines have total acidity of around 8 g/l.

8.  There are a lot of outliers in fixed and volatile acidity observtions, as well as in residual sugar observations.

9.  Most of wines have total acidity at around 8 g/l, residual sugar at 2 g/l, free sulfur dioxide at around 6 mg/l, alcohol content at around 9.25%.

### What is/are the main feature(s) of interest in your dataset?

My first impression is that acidity and alcohol play an important role in general taste.

### What other features in the dataset do you think will help support your
investigation into your feature(s) of interest?

Chlorides and free sulfur dioxide might at certain levels affect the taste. Citric acid content seems to enhance the wine's taste. But the balance of different parameters is essential.

### Did you create any new variables from existing variables in the dataset?

Yes. I converted the variable "quality" into a factor and added this new variable to the data set. I also created a new variable "total acidity" adding "volatile" and "fixed" acidity. It is difficult to tell apart different types of acidity (except for citric acid), what we taste is total acidity. That is why I might explore the influence of total acidity on the general taste. I created categorical variabes by grouping wines by alcohol content, volatile acidity and fixed acidity. I would like to explore data by different groups.

### Of the features you investigated, were there any unusual distributions?
Did you perform any operations on the data to tidy, adjust, or change the form
of the data? If so, why did you do this?

I decided to organize data in a new data frame grouping them by alcohol content, volatile acidity and quality and calculating median value for each variable. I then gathered the data to use variables names as values in column "predictor". I plan using this data frame for plots in multivariate section.

The unusual distributions were citric acid content observations. I used density plot to show general descending trend and a drop at 5 g/l. I also log transformed the free sulfur dioxide distribution as it was clearily positively skewed. As a result I got a more normal distribution

Bivariate Plots Section
=======================

![](redwines_project_files/figure-markdown_github/unnamed-chunk-59-1.png)

From the scatterplot matrix above we can see that there is no very strong correlation between any of input variables and quality. The strongest correlation we have is between alcohol and quality: 0.476 which is meaningful, but small. Then there is a meaningful negative correlation between volatile acidity and quality (-0.391), though it is still small. There is correlation between some input variables. For example, citric acid and fixed acid, negative correlation between citric and volatile acid. Density is correlated with 4 other input variables and pH - with 3 other variables.

I excluded free.sulfur dioxide from the table as the correlation cofficient is very low. Here it is:

    ## [1] -0.05065606

Let's start with relationship between alcohol and quality.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-61-1.png)

From this plot we see that median alcohol content per quality grade is generally increasing with grade. Only grade 5 wines have their median lower than grade 3 and 4 wines. These wines have also most upper outliers.

Let's represent these data in a different way.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-62-1.png)

Here I added noise and smoothed data to see a general tendancy. The relationship is not exactly linear but we can see that quality increases as alohol content increases. The variance is higher in the middle of the graph between values 10 and 11 of alcohol content. It is lower at low alcohol content (below 9), the variance is the lowest at higher alcohol content (above 13).

![](redwines_project_files/figure-markdown_github/unnamed-chunk-63-1.png)

Here I decided to plot grades on x-axis and alcohol content in % on y-axis. I added some noise to better see the general tendancy. I also added some summary lines over raw data. Red line connects the dots representing mean alcohol content for wines grouped by grade. Blue line - median, dashed lines - lower (10%) and upper (90%) qunatile. We notice that there is a positive relationship between alcohol content and grade.Although, we notice that median and mean alcohol content for wines of grade 5 is lower than for wines of grade 4. Is it related to unsufficient number of observations for lower grade wines? We notice that there are a lot of wines with alcohol content at around 9.5% and getting grade 5. Clearly, wines with high alcohol above 13% content got higher grades: 6, 7 or 8.

    ## 
    ## Calls:
    ## m1: lm(formula = quality ~ alcohol, data = redwines)
    ## 
    ## ================================
    ##   (Intercept)         1.875***  
    ##                      (0.175)    
    ##   alcohol             0.361***  
    ##                      (0.017)    
    ## --------------------------------
    ##   R-squared           0.227     
    ##   adj. R-squared      0.226     
    ##   sigma               0.710     
    ##   F                 468.267     
    ##   p                   0.000     
    ##   Log-likelihood  -1721.057     
    ##   Deviance          805.870     
    ##   AIC              3448.114     
    ##   BIC              3464.245     
    ##   N                1599         
    ## ================================

Here I tried to create a model with only one predictor: alcohol content. The model explaines about 22.7% on the data.

Next variable with a meningful correlation: volatile acidity.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-65-1.png)

On the left plot we see horizontal lines (as grades are integers) and we can notice a shift in data set from higher grade to lower grade. On the right plot I added noise and some transparency. We can see the descending tendency. Most of observations are in the middle (grade 5 and 6: no surprise here). The lower the grade the more on the right are our observations.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-66-1.png)

Here I decided to use factor variable quality\_factor to represent how observations are distributed for each grade. It confirms our initial assumption that there is a negative relationship between volatile acidity and quality. The higher is the grade the lower is its median, as well as whiskers ends. Except for medians for 7 and 8 grade - they are the same.

Only exception: lower whiskey end of 8 grade wines is higher than 7 grade wines. May be this is simply due to unsufficient number of observations.

Another observation: there are only upper outliers and grades 5 and 6 have most of them. The higher the grade the smaller is volatile acidity spread for the central 50% of data.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-67-1.png)

The dsitribution of data points seems similar for best and worst wines (graded 3 and 8). There are more observations and a bigger spread for average quality wines. This is certainly related to the number of observations. Here we see that there is no relationship between residual sugar and quality despite what I assumed in Univariate analysis section. This is also confirmed by the correlation coefficient of only 0.0137. I notice though that most grade 3, 4 and 8 wines do not have high residual sugar above 6 g/l.

### Quality and sulphates

![](redwines_project_files/figure-markdown_github/unnamed-chunk-68-1.png)

![](redwines_project_files/figure-markdown_github/unnamed-chunk-69-1.png)

There is a positive relationship between sulphates content and wine quality. On the upper graph I showed all the data whereas on the lower graph I removed the top 5% of observations. On the second graph we can see an ascending tendency. On the first graph we also observe a descendning or flat pattern starting at around 0.9 g/l f sulphates. We need more data to confirm this descending pattern starting at cerain level of sulphates, but it seems possible as with any ingredients of taste too much of any ingredient will hurt the general perception.

### Citric acid and quality

![](redwines_project_files/figure-markdown_github/unnamed-chunk-70-1.png)

It is difficult to see any tendency on the scatterplot, even with added noise and transparency, whereas we can observe a clear ascending tendency on the right plot if we consider medians for each grade. The correlation coefficient is not high enough (0.223), nevertheless it seems that there is a certain relationship between citric acid content and quality. For example, all the 8 grade wines contain some amount of citric acid, whereas some of other grade wines do not contain citric acid. This is also what we have seen in Univariate analysis section.

It is worth noticing that for the first time we see lower outliers for 7 grade wines. So far, we have only observed upper ouitliers. Possible explanation is that citric acid is found in small quantities in grapes and adding it in the process of wine makinng is not allowed in Europe.

I wanted to check again the fixed acidity even though the correlation coefficient is very small. I still coud not believe that acidity does not affect taste.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-71-1.png)

But here we see that there is an ascending trend when we consider only 80% middle observations (the right plot), eliminating lower and top 10%. Is it possible that a combination of fixed acidity and another property (for example, residual sugar or alcohol) influences the taste? I will verify this in Multivariate analysis section.

### Relationship between input variables

### Density and fixed acidity

![](redwines_project_files/figure-markdown_github/unnamed-chunk-72-1.png)

Here we see an ascending trend. The higher the fixed acidity, the higher the density. This is related to the higher density of acids dissolved in water compare to the rest of the liquid in wine. The correlation coefficient is moderate: 0.668.

In general, we notice that density has meaningful correlation with several other variables: alcohol (descending: -0.4962), citric acid (ascending: 0.365), residual sugar (ascending: 0.355), and pH (descending: -0.3425).

### Fixed acidity and pH

A few words about two different measures of acidity: pH is a measure of the acid strength. It is based on logarithmical scale. As an example, pH of 3 means 10 times stronger acidity than pH of 4. Fixed acidity measures different acids content in g per liter. Each particular acid has its own pH, but we don't know how much of each acid we have in our fixed acidity measure.

So, the pH is cerainly negatively related to fixed acidity, but it is not a clear linear relationship. pH can be the same or even lower for a higher fixed acidity, but the higher the increase in fixed acidity the higher will be the decrease in pH.

Let's see on a graph:

![](redwines_project_files/figure-markdown_github/unnamed-chunk-73-1.png)

Here the relationship is of a negatively powered function. No surprise - taking into account the definition of pH.

### Citric acid and volatile acidity

Whereas positive relationship between citric acid and fixed acidity is not surprising (correlation coeff: 0.672) - citric acid is one of fixed acids - negative relationship between citric and volatile acids is not that evident. Correlation corefficient is moderately high though: -0.552

![](redwines_project_files/figure-markdown_github/unnamed-chunk-74-1.png)

Here the descending trend is clear. The more the citric acid content the lower the volatile acidity. I wonder if this explains the influence of citric acid on quality. May be, it is not citric acid itself that influences wine quality, but a lower volatile acidity that is somehow explained by higher citric acid content. In that case, I should not include citric acid in my model as then, there will be a relationship between two input variables.

Bivariate Analysis
==================

### Talk about some of the relationships you observed in this part of the
investigation. How did the feature(s) of interest vary with other features
in the dataset?

1.  I explored the relationship between the dependent variable: wine quality or grade and several input variables describing wine physcochemical properties. Based on my exploration, I see that alcohol influences the most the wine quality. The relationship is positive: for most of observations, higher alcohol content corresponds to a higher quality.

2.  Second comes volatile acidity that is negatively related to wine quality. The most common among volatile acids in wine is acetic acid the one present in vinegar. The higher the volatile acidity the lower the wine quality as it will give the wine a vinegar taste.

3.  Sulphates - surprisingly, and citric acid - as expected, have some positive influence on wine quality (at least, for our sample). Although, the correlation coefficient is not meaningful (0.251 for sulphates and 0.226 for citric acid). I based my conclusion on a slight positive trend on sulphates/quality scatterplot, as well as on citric acid boxplots per grade: medians are clearily increasing as the grade increases.

### Did you observe any interesting relationships between the other features
(not the main feature(s) of interest)?

1.  Density is related to several variables, which is not surprising as density of certain chemicals might be typically higher or lower than others chemicals. For example if we would explore the relationship between density and quality we would find a correlation, but the real reason for that is that alcohol density is typically lower than other chemicals dissolved in wine and that is alcohol that explains wine quality.

2.  Fixed acidity and pH relationship is worth to be mentioned. Those are two different measures of acidity that are negatively related and do not have a linear relationship. I will be interested in fixed acidity rather than pH. This is confirmed by very low correlation coefficient of pH and quality: -0.0577. Also a very low correlaation coefficient between total acidity and quality. So, I won't consider total acidity as predictor.

3.  One important conlusion though is that citric acid and volatile acidity are negatively related. As citric acid itself does not have a meaningful correlation coefficient with wine quality, while volatile acidity does, I should probaby eliminate citric acid from my input variables and keep only volatile acidity.

### What was the strongest relationship you found?

> The strongest relationship is between alcohol content and quality. Although, as high volatile acidity can significantly reduce wine's grade it will be interesting to explore the three variables together in the next section.

Multivariate Plots Section
==========================

![](redwines_project_files/figure-markdown_github/unnamed-chunk-75-1.png)

On this plot we see how the combination of alcohol and volatile acidity is realted to wine quality. As wine grade increases the variance of alcohol content increases and volatile acidity variance decreases.

For grade 3 wines volatile acidity varies betweeen 0.4 and 1.6 but alcohol content varies only between 8 and 11%, whereas for grade 8 wines volatile acidity varies between 0.2 and 0.8 and alcohol content varies between 10 and 14%.

Also, most of 5 grade wines have alcohol content between 9 and 10.5%, whereas 6 grade wines - between 9 and 12%.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-76-1.png)

![](redwines_project_files/figure-markdown_github/unnamed-chunk-77-1.png)

On the upper plot I represented all wines, colored by their grouped quality: low, average and good.

On the lower plot I represented only average wines colored by grade: 6 and 7.

On both graphs we see that points are positioned along a diagonal, better wines being on the upper right side and worse wines being on the lower left side. This shows that if fixed acidity is high enough it can compensate lower alcohol and assure the wine a good grade. If fixed acidity is low, a higher alcohol content is needed for a wine to be of better quality. Fixed acidity reinforces alcohol effect on quality.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-78-1.png)

This plot gives me a general idea of data within different combinations of alcohol and volatile acidity. For example, there are no wines with very low volatile acidity and very low alcohol. I am interested in extreme cases. A wine with high alcohol content and low volatile acidity should be of good quality. We see on the graph that among these wines there are many 6 and 7 grades, a few 8 and 5. What differs wines in this category making them better or worse?

![](redwines_project_files/figure-markdown_github/unnamed-chunk-79-1.png)

Here we see median values for each quality and each predictor variable. What might have contributed to the lowest grade of 5? Chlorides, total sulfur dioxide and residual sugar are are very high. In this case citric acid is very high and fixed acidity too.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-80-1.png)

Here most of wines should be of lower quality, nevertheless, there is even a 6 grade wine. What differs them? Citric acid seems to have a clear increase. 6 grade wine has much more citric acid than other wines. Chlorides are decreasing. Residual sugar increases as grade increases.

It seems that depending on other parameters chlorides, residual sugar and total sulfur dioxide might influence positively or negatively the quality.

Let's explore the relationship between residual sugar and fixed acidity

![](redwines_project_files/figure-markdown_github/unnamed-chunk-81-1.png)

Here it seems that for higher sugar (&gt; 3 g/l) poor wines tend to have lower fixed acidity.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-82-1.png)

Despite my expectation I can not see a relationship between residual sugar and fixed acidity and its influence on quality. I notice though that average wines have more wines with high residual sugar than poor or good wines.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-83-1.png)

No matter what is alcohol content, the concentration of sulphates of 0.7 g/l and higher increases the probability to get a good wine rather than an average or poor wine.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-84-1.png)

Same situation here: only for very high acidity wines sulphates content does not play a role.

![](redwines_project_files/figure-markdown_github/unnamed-chunk-85-1.png)

Here at very low volatile acidity the probability to get a good wine is much higher starting only at around 1.1 g/l of sulphates. At very low volatile acidity the sulphates content has to be higher to influence the quality.

For the next graph I created a new data frame with wines grouped by alcohol and quality and median values per predictor variable. Below are a few lines from this new data frame.

    ## # A tibble: 10 x 4
    ## # Groups:   alcohol_grouped [4]
    ##     alcohol_grouped quality_grouped   predictor median
    ##               <ord>           <ord>      <fctr>  <dbl>
    ##  1      Low alcohol             low citric.acid  0.195
    ##  2      Low alcohol         average citric.acid  0.220
    ##  3      Low alcohol            good citric.acid  0.400
    ##  4  Average alcohol             low citric.acid  0.055
    ##  5  Average alcohol         average citric.acid  0.270
    ##  6  Average alcohol            good citric.acid  0.410
    ##  7     High alcohol             low citric.acid  0.150
    ##  8     High alcohol         average citric.acid  0.260
    ##  9     High alcohol            good citric.acid  0.390
    ## 10 Very low alcohol             low   sulphates  0.535

![](redwines_project_files/figure-markdown_github/unnamed-chunk-87-1.png)

Here are median values for each predictor variable and wine quality. A wine quality gets better as: 1. Chlorides content increases for wines with high alcohol content and decreases slightly for other wines. Chlorides content is in general lower in wines with high alcohol content. 2. Citric acid and sulphates content increases 3. Fixed acidity increases, but is in general lower in wines with high alcohol content 4. Total sulfur dioxide decreases in wines with high alcohol content and is very high for poor wines with high alcohol content. Although, there is only one or two low quality wines with high alcohol, so it might be a coincidence.

Now I am ready to create my model.

I will take the following variables as predictors: alcohol, volatile acidity, fixed acidity, sulphates and totall sulphur dioxide

    ## 
    ## Calls:
    ## m1: lm(formula = quality ~ alcohol + volatile.acidity, data = redwines)
    ## m2: lm(formula = quality ~ alcohol + volatile.acidity + fixed.acidity, 
    ##     data = redwines)
    ## m3: lm(formula = quality ~ alcohol + volatile.acidity + sulphates, 
    ##     data = redwines)
    ## m4: lm(formula = quality ~ alcohol + volatile.acidity + sulphates + 
    ##     total.sulfur.dioxide, data = redwines)
    ## 
    ## ================================================================================
    ##                              m1            m2            m3            m4       
    ## --------------------------------------------------------------------------------
    ##   (Intercept)               3.095***      2.674***      2.611***      2.826***  
    ##                            (0.184)       (0.218)       (0.196)       (0.201)    
    ##   alcohol                   0.314***      0.321***      0.309***      0.295***  
    ##                            (0.016)       (0.016)       (0.016)       (0.016)    
    ##   volatile.acidity         -1.384***     -1.286***     -1.221***     -1.199***  
    ##                            (0.095)       (0.099)       (0.097)       (0.097)    
    ##   fixed.acidity                           0.036***                              
    ##                                          (0.010)                                
    ##   sulphates                                             0.679***      0.712***  
    ##                                                        (0.101)       (0.101)    
    ##   total.sulfur.dioxide                                               -0.002***  
    ##                                                                      (0.001)    
    ## --------------------------------------------------------------------------------
    ##   R-squared                 0.317         0.322         0.336         0.344     
    ##   adj. R-squared            0.316         0.321         0.335         0.342     
    ##   sigma                     0.668         0.665         0.659         0.655     
    ##   F                       370.379       253.055       268.912       208.768     
    ##   p                         0.000         0.000         0.000         0.000     
    ##   Log-likelihood        -1621.814     -1615.379     -1599.384     -1589.835     
    ##   Deviance                711.796       706.090       692.105       683.887     
    ##   AIC                    3251.628      3240.758      3208.768      3191.669     
    ##   BIC                    3273.136      3267.643      3235.654      3223.932     
    ##   N                      1599          1599          1599          1599         
    ## ================================================================================

Multivariate Analysis
=====================

### Talk about some of the relationships you observed in this part of the
investigation. Were there features that strengthened each other in
terms of looking at your feature(s) of interest?

Fixed acidity strengthens alcohol effect on quality. This is particularly true for good and low quality wines, not for average wines. A wine with lower alcohol content needs higher fixed acidity to be of good quality. And vice versa: a wine with higher alcohol content can have a lower fixed acidity and still get a good grade.

### Were there any interesting or surprising interactions between features?

I noticed that some predictor variable influence quality only within certain groups of wines: for example, chlorides seem to positively influence quality only in high alcohol wines.

### OPTIONAL: Did you create any models with your dataset? Discuss
the strengths and limitations of your model.

Yes, I created a regression model with quality as output variable and following input variables: alcohol, volatile acidity, fixed acidity, sulphates and total sulfur dioxide. My model explains only 34.4% of data. I did not tranform data on a different scale as seemed to not have any influence on the model. The model is based on a pretty small sample and very low proportion of poor and good wines, this is why this model is limited and should be rebuilt based on a better sample and more variables.

Final Plots and Summary
=======================

### Plot One

![](redwines_project_files/figure-markdown_github/unnamed-chunk-89-1.png)

### Description One

In this plot I used grouped wine quality: low (grade 3 and 4), average (grade 3 and 4) and good (grade 7 and 8). The higher the alcohol content, the higher the probability for a wine to be of good quality. If alcohol content is higher than 10.5% the probability for it to be of good quality is higher than to be of low or average quality. If a wine in this sample has less than 9% alcohol content, probability for it to be of low quality is higher than the probability to be of average quality, and the probability for it to be of good quality is almost 0.

### Plot Two

![](redwines_project_files/figure-markdown_github/unnamed-chunk-90-1.png)

### Description Two

Median volatile acidity is decreasing as wine quality increases. Volatile acidity variance is the smallest for best quality wines (grade 8). Median volatile acidity of two best quality groups of wines (grade 7 and 8) is the same. Minimum volatile acidity of grade 8 wines is higher than minimum volatile acidity of grade 7 wines. This means that at some level of volatile acidity (around 0.20 - 0.25 g/l) further decrease in volatile acidity does not improve wine quality.

### Plot Three

![](redwines_project_files/figure-markdown_github/unnamed-chunk-91-1.png)

### Description Three

On this plot we see that good quality wines are mostly in the upper right part of the cluster, whereas low quality wines are mostly in the lower left part of the cluster. The higher the fixed acidity of a wine the lower minimum alcohol content is needed for the wine to be good. The lower the alcohol content the higher minimum fixed acidity is needed for a wine to be good. Fixed acidity reinforces the effect of alcohol content on quality.

Reflection
==========

In this project I explored the effect of several physicochemical properties of red wine on its quality. I used a sample of 1599 observations with 11 variables representing physicochemical properties of red wine. Here are my conclusions:

1.  The strongest effect on quality is produced by alcohol content. The higher the alcohol content in a wine the higher the probability for this wine to be of a higher quality.

2.  The second strongest effect is produced by volatile acidity. This time, the effect is negative. The higher the volatile acidity, the lower the probability for a wine to be of higher quality.

3.  Fixed acidity reinforces the effect of alcohol on wine quality. This means that a wine with lower alcohol content but higher fixed acidity has chance to get the same grade as another wine with higher alcohol content and lower fixed acidity.

4.  There is some slight positive relationship between sulphates and quality.

5.  Citric acid affects wine quality, but as it is part of fixed acids and its effect is already taken into account when fixed acids are considered.

6.  The effect of other variables can be different depending on the alcohol content. For example, chlorides play positive role only at high alcohol content.

**Challenges of this project**

The sample size is not big enough and also, the proportion of low and good quality wines is too small, so it is sometimes difficult to make conclusions with only a few wines as comparison.

Also, not all important wine ingredients were measured for this sample. For example, tannins or flavonoids.

I was able to create a model explaining only 0.35% of data.

**Surprises**

I was surprised to see that residual sugar does not have an effect on taste. I noticed though that at too high amounts residual sugar decreases wine quality. I also expected that acidity would have a stronger effect on quality.

**Future insights**

It would be interesting to look at a sample with equal amount of low, average and high quality wines. More detailed grades could be useful too: for example, grades with 0.5 scale. I would like to explore more the relationship between acidity and residual sugar or acidity and chlorides.
