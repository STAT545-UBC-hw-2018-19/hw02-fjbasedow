hw02-gapminder exploration
================
Frederike Basedow
22 September 2018

### Load the data and packages

``` r
library(gapminder)
library(tidyverse)
library(knitr)
```

### Smell test the data

Explore the gapminder object:

1.  Is it a data.frame, a matrix, a vector, a list?

``` r
str(gapminder)
```

    ## Classes 'tbl_df', 'tbl' and 'data.frame':    1704 obs. of  6 variables:
    ##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
    ##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
    ##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
    ##  $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
    ##  $ gdpPercap: num  779 821 853 836 740 ...

``` r
typeof(gapminder)
```

    ## [1] "list"

1.  What is its class?

``` r
class(gapminder)
```

    ## [1] "tbl_df"     "tbl"        "data.frame"

1.  How many variables/columns?

``` r
n_var <- ncol(gapminder)
n_var
```

    ## [1] 6

Gapminder has 6 variables.

1.  How many rows/observations?

``` r
n_obs <- nrow(gapminder)
n_obs
```

    ## [1] 1704

Gapminder has 1704 observations.

1.  Can you get these facts about “extent” or “size” in more than one way? Can you imagine different functions being useful in different contexts?

You can get the number of variables and observations with the functions `ncol()` and `nrow()`, respectively as I did above, but you could also use the function `str()`, that includes the number of variable and observations in its output. `str` is useful if you just want to get an overview of what your data set looks like, `nrow` and `ncol` are useful if you want to use these number for further calculations.

1.  What data type is each variable?

``` r
sapply(gapminder, class)
```

    ##   country continent      year   lifeExp       pop gdpPercap 
    ##  "factor"  "factor" "integer" "numeric" "integer" "numeric"

### Explore individual variables

Pick at least one categorical variable and at least one quantitative variable to explore.

I will explore `year` as a categorical variable and `lifeExp` as a quanititative variable.

1.  What are possible values (or range, whichever is appropriate) of each variable?

``` r
range(gapminder$lifeExp)
```

    ## [1] 23.599 82.603

``` r
nlevels(gapminder$country)
```

    ## [1] 142

``` r
levels(gapminder$country)
```

    ##   [1] "Afghanistan"              "Albania"                 
    ##   [3] "Algeria"                  "Angola"                  
    ##   [5] "Argentina"                "Australia"               
    ##   [7] "Austria"                  "Bahrain"                 
    ##   [9] "Bangladesh"               "Belgium"                 
    ##  [11] "Benin"                    "Bolivia"                 
    ##  [13] "Bosnia and Herzegovina"   "Botswana"                
    ##  [15] "Brazil"                   "Bulgaria"                
    ##  [17] "Burkina Faso"             "Burundi"                 
    ##  [19] "Cambodia"                 "Cameroon"                
    ##  [21] "Canada"                   "Central African Republic"
    ##  [23] "Chad"                     "Chile"                   
    ##  [25] "China"                    "Colombia"                
    ##  [27] "Comoros"                  "Congo, Dem. Rep."        
    ##  [29] "Congo, Rep."              "Costa Rica"              
    ##  [31] "Cote d'Ivoire"            "Croatia"                 
    ##  [33] "Cuba"                     "Czech Republic"          
    ##  [35] "Denmark"                  "Djibouti"                
    ##  [37] "Dominican Republic"       "Ecuador"                 
    ##  [39] "Egypt"                    "El Salvador"             
    ##  [41] "Equatorial Guinea"        "Eritrea"                 
    ##  [43] "Ethiopia"                 "Finland"                 
    ##  [45] "France"                   "Gabon"                   
    ##  [47] "Gambia"                   "Germany"                 
    ##  [49] "Ghana"                    "Greece"                  
    ##  [51] "Guatemala"                "Guinea"                  
    ##  [53] "Guinea-Bissau"            "Haiti"                   
    ##  [55] "Honduras"                 "Hong Kong, China"        
    ##  [57] "Hungary"                  "Iceland"                 
    ##  [59] "India"                    "Indonesia"               
    ##  [61] "Iran"                     "Iraq"                    
    ##  [63] "Ireland"                  "Israel"                  
    ##  [65] "Italy"                    "Jamaica"                 
    ##  [67] "Japan"                    "Jordan"                  
    ##  [69] "Kenya"                    "Korea, Dem. Rep."        
    ##  [71] "Korea, Rep."              "Kuwait"                  
    ##  [73] "Lebanon"                  "Lesotho"                 
    ##  [75] "Liberia"                  "Libya"                   
    ##  [77] "Madagascar"               "Malawi"                  
    ##  [79] "Malaysia"                 "Mali"                    
    ##  [81] "Mauritania"               "Mauritius"               
    ##  [83] "Mexico"                   "Mongolia"                
    ##  [85] "Montenegro"               "Morocco"                 
    ##  [87] "Mozambique"               "Myanmar"                 
    ##  [89] "Namibia"                  "Nepal"                   
    ##  [91] "Netherlands"              "New Zealand"             
    ##  [93] "Nicaragua"                "Niger"                   
    ##  [95] "Nigeria"                  "Norway"                  
    ##  [97] "Oman"                     "Pakistan"                
    ##  [99] "Panama"                   "Paraguay"                
    ## [101] "Peru"                     "Philippines"             
    ## [103] "Poland"                   "Portugal"                
    ## [105] "Puerto Rico"              "Reunion"                 
    ## [107] "Romania"                  "Rwanda"                  
    ## [109] "Sao Tome and Principe"    "Saudi Arabia"            
    ## [111] "Senegal"                  "Serbia"                  
    ## [113] "Sierra Leone"             "Singapore"               
    ## [115] "Slovak Republic"          "Slovenia"                
    ## [117] "Somalia"                  "South Africa"            
    ## [119] "Spain"                    "Sri Lanka"               
    ## [121] "Sudan"                    "Swaziland"               
    ## [123] "Sweden"                   "Switzerland"             
    ## [125] "Syria"                    "Taiwan"                  
    ## [127] "Tanzania"                 "Thailand"                
    ## [129] "Togo"                     "Trinidad and Tobago"     
    ## [131] "Tunisia"                  "Turkey"                  
    ## [133] "Uganda"                   "United Kingdom"          
    ## [135] "United States"            "Uruguay"                 
    ## [137] "Venezuela"                "Vietnam"                 
    ## [139] "West Bank and Gaza"       "Yemen, Rep."             
    ## [141] "Zambia"                   "Zimbabwe"

``` r
levels(as.factor(gapminder$year))
```

    ##  [1] "1952" "1957" "1962" "1967" "1972" "1977" "1982" "1987" "1992" "1997"
    ## [11] "2002" "2007"

1.  What values are typical? What’s the spread? What’s the distribution? Etc., tailored to the variable at hand.

lifeExp:

``` r
summary(gapminder$lifeExp)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   23.60   48.20   60.71   59.47   70.85   82.60

``` r
gapminder %>% 
  ggplot(aes(lifeExp)) + 
  geom_density()
```

![](hw02-gapminder_exploration_files/figure-markdown_github/unnamed-chunk-8-1.png)

``` r
gapminder %>% 
  ggplot(aes(year,lifeExp)) +
  geom_line(aes(group=country, colour=continent))
```

![](hw02-gapminder_exploration_files/figure-markdown_github/unnamed-chunk-8-2.png)

Feel free to use summary stats, tables, figures. We’re NOT expecting high production value (yet).

### Explore various plot types

Make a few plots, probably of the same variable you chose to characterize numerically. You can use the plot types we went over in class (cm006) to get an idea of what you’d like to make. Try to explore more than one plot type. Just as an example of what I mean:

1.  A scatterplot of two quantitative variables.

``` r
gapminder %>% 
  ggplot(aes(pop, lifeExp)) +
  geom_point() 
```

![](hw02-gapminder_exploration_files/figure-markdown_github/unnamed-chunk-9-1.png)

1.  A plot of one quantitative variable. Maybe a histogram or densityplot or frequency polygon.

``` r
gapminder %>% 
  ggplot(aes(gdpPercap)) +
  geom_density()
```

![](hw02-gapminder_exploration_files/figure-markdown_github/unnamed-chunk-10-1.png)

1.  A plot of one quantitative variable and one categorical. Maybe boxplots for several continents or countries.

``` r
gapminder %>% 
  ggplot(aes(continent, lifeExp)) +
  geom_violin() +
  geom_jitter(alpha=0.25)
```

![](hw02-gapminder_exploration_files/figure-markdown_github/unnamed-chunk-11-1.png)

You don’t have to use all the data in every plot! It’s fine to filter down to one country or small handful of countries.

``` r
gapminder %>% filter(continent == "Asia") %>% 
  ggplot(aes(country, lifeExp)) +
  geom_boxplot() +
  theme(axis.text.x = element_text(angle = 90, hjust = 1))
```

![](hw02-gapminder_exploration_files/figure-markdown_github/unnamed-chunk-12-1.png)

### Use filter(), select() and %&gt;%

1.  Use filter() to create data subsets that you want to plot. Practice piping together filter() and select(). Possibly even piping into ggplot().

``` r
gapminder %>% 
  select(continent, country, lifeExp, year) %>% 
  filter(year=="1952") %>% 
  ggplot(aes(continent, lifeExp)) +
  geom_violin() +
  geom_jitter()
```

![](hw02-gapminder_exploration_files/figure-markdown_github/unnamed-chunk-13-1.png)
