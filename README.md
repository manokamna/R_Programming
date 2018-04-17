    setwd("E:/GitHub/R")
    library(tidyverse)

    ## Warning: package 'tidyverse' was built under R version 3.3.3

    ## -- Attaching packages ------------------------------------------------------------ tidyverse 1.2.1 --

    ## v ggplot2 2.2.1     v purrr   0.2.4
    ## v tibble  1.3.4     v dplyr   0.7.4
    ## v tidyr   0.7.2     v stringr 1.2.0
    ## v readr   1.1.1     v forcats 0.2.0

    ## Warning: package 'ggplot2' was built under R version 3.3.3

    ## Warning: package 'tibble' was built under R version 3.3.3

    ## Warning: package 'tidyr' was built under R version 3.3.3

    ## Warning: package 'readr' was built under R version 3.3.3

    ## Warning: package 'purrr' was built under R version 3.3.3

    ## Warning: package 'dplyr' was built under R version 3.3.3

    ## Warning: package 'stringr' was built under R version 3.3.3

    ## Warning: package 'forcats' was built under R version 3.3.3

    ## -- Conflicts --------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

    attach(mpg)
    load("h4data")
    library("gridExtra")

    ## Warning: package 'gridExtra' was built under R version 3.3.3

    ## 
    ## Attaching package: 'gridExtra'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     combine

#### 1. Dataset mpg is available once you load the ggplot2 library. Recreate the R code necessary to generate the following graphs. Hint. for the last plot, use the aesthetic linetype=drv.

    # (a)
    g1=ggplot(data = mpg) +
    geom_point(mapping = aes(x = displ, y = hwy)) +
    geom_smooth(mapping = aes(x =displ, y = hwy), method="loess",se=FALSE)

    # (b)

    g2=ggplot(data = mpg ) +
    geom_point(mapping = aes(x =displ, y = hwy, color=drv))+
    geom_smooth(mapping = aes(x =displ, y = hwy, color=drv), method="loess",se=FALSE)

    # (c)

    g3=ggplot(data = mpg ) +
      geom_point(mapping = aes(x = displ, y = hwy, color=drv))+
      geom_smooth(mapping = aes(x = displ, y = hwy), method="loess",se=FALSE)

    # (d)

    g4=ggplot(data = mpg ) +
      geom_point(mapping = aes(x = displ, y = hwy,color=drv))+
      geom_smooth(mapping = aes(x = displ,y = hwy,linetype=drv), method="loess",se=FALSE)

    grid.arrange(g1,g2,g3,g4,nrow=2,ncol=2)

![](Assignment4_files/figure-markdown_strict/unnamed-chunk-5-1.png)

#### 2. This question involves a dataset which gives a record of every men's singles match played in Wim-bledon in 2015. Type in the following to load the data called wim. (File available on Moodle).

#### (a) Use mutate (from dplyr) to add a new variable which is the difference in heights of the winner and loser. Use ggplot to draw a histogram of the new variable.

    wim <- mutate(wim,htdiff=wim$winner_ht-wim$loser_ht)

    ## Warning: package 'bindrcpp' was built under R version 3.3.3

    wim$htdiff

    ##   [1]  10   5  NA  NA  NA  10 -13  NA  NA -15  NA  28   0  NA  -5  -5  NA
    ##  [18]  -5  -2  NA   3   0  NA -25  -2   3  NA  NA  NA  -5   8  11  NA  NA
    ##  [35]  20   3  NA  -4  16  -3  -5   0  NA  NA   7  NA   5   7   8   5   6
    ##  [52]  -8  NA -10  NA   0  10  NA  13  NA  NA  -2   8  13   3  NA  -2  13
    ##  [69]  23  18  NA  10  10  NA   0  NA   0 -18  NA   8  NA  15  12  11   0
    ##  [86]  28  NA   0   6 -16  10  -5  NA  NA  NA -13  -5  15  -8  -8  -5 -20
    ## [103]  -3  NA   3  -3  20   0  16 -10  NA  NA -15  18  20  NA   0 -18 -13
    ## [120]  NA -10   2  -3   2   3  -5   3

    ggplot(data=wim)+
      geom_histogram(mapping = aes(wim$htdiff),color="black",fill="lightblue",bins=30,na.rm=TRUE) 

![](Assignment4_files/figure-markdown_strict/unnamed-chunk-6-1.png)

#### (b) Construct a dataset with one row per player, recording also the number of wins, ranking points,height and country of the player.Do this in the following steps:

#### (i) Construct a dataset w\_wim, by using select on wim, with variables name= winner\_name, points=winner\_rank\_points, ht= winner\_ht, ioc= winner\_ioc.

    w_wim <- select(wim,name=winner_name,points=winner_rank_points,ht=winner_ht,ioc=winner_ioc)
    w_wim

    ## # A tibble: 127 x 4
    ##                     name points    ht   ioc
    ##                    <chr>  <int> <int> <chr>
    ##  1        Novak Djokovic  13845   188   SRB
    ##  2       Jarkko Nieminen    564   185   FIN
    ##  3 Pierre Hugues Herbert    353    NA   FRA
    ##  4         Bernard Tomic   1355   193   AUS
    ##  5        Leonardo Mayer   1605   188   ARG
    ##  6     Marcel Granollers    715   190   ESP
    ##  7          Marsel Ilhan    647   190   TUR
    ##  8        Kevin Anderson   2090   203   RSA
    ##  9           Marin Cilic   3540   198   CRO
    ## 10     Ricardas Berankis    577   175   LTU
    ## # ... with 117 more rows

#### (ii) Repeat the above step to create l\_wim, a dataset with the names of players who lost a match, their points, height and country.

    l_wim <- select(wim,name=loser_name,points=loser_rank_points,ht=loser_ht,ioc=loser_ioc)
    l_wim

    ## # A tibble: 127 x 4
    ##                     name points    ht   ioc
    ##                    <chr>  <int> <int> <chr>
    ##  1 Philipp Kohlschreiber   1195   178   GER
    ##  2        Lleyton Hewitt    465   180   AUS
    ##  3           Hyeon Chung    671    NA   KOR
    ##  4    Jan Lennard Struff    478    NA   GER
    ##  5    Thanasi Kokkinakis    723    NA   AUS
    ##  6      Janko Tipsarevic     76   180   SRB
    ##  7        Jerzy Janowicz    975   203   POL
    ##  8         Lucas Pouille    539    NA   FRA
    ##  9         Hiroki Moriya    294    NA   JPN
    ## 10 Andreas Haider Maurer    857   190   AUT
    ## # ... with 117 more rows

#### (iii) Use mutate to add a variable wins to w\_wim, with value 1. Use mutate to add a variable wins to l\_wim, with value 0.

    w_wim <- mutate(w_wim,wins=1)
    w_wim

    ## # A tibble: 127 x 5
    ##                     name points    ht   ioc  wins
    ##                    <chr>  <int> <int> <chr> <dbl>
    ##  1        Novak Djokovic  13845   188   SRB     1
    ##  2       Jarkko Nieminen    564   185   FIN     1
    ##  3 Pierre Hugues Herbert    353    NA   FRA     1
    ##  4         Bernard Tomic   1355   193   AUS     1
    ##  5        Leonardo Mayer   1605   188   ARG     1
    ##  6     Marcel Granollers    715   190   ESP     1
    ##  7          Marsel Ilhan    647   190   TUR     1
    ##  8        Kevin Anderson   2090   203   RSA     1
    ##  9           Marin Cilic   3540   198   CRO     1
    ## 10     Ricardas Berankis    577   175   LTU     1
    ## # ... with 117 more rows

    l_wim <- mutate(l_wim,wins=0)
    l_wim

    ## # A tibble: 127 x 5
    ##                     name points    ht   ioc  wins
    ##                    <chr>  <int> <int> <chr> <dbl>
    ##  1 Philipp Kohlschreiber   1195   178   GER     0
    ##  2        Lleyton Hewitt    465   180   AUS     0
    ##  3           Hyeon Chung    671    NA   KOR     0
    ##  4    Jan Lennard Struff    478    NA   GER     0
    ##  5    Thanasi Kokkinakis    723    NA   AUS     0
    ##  6      Janko Tipsarevic     76   180   SRB     0
    ##  7        Jerzy Janowicz    975   203   POL     0
    ##  8         Lucas Pouille    539    NA   FRA     0
    ##  9         Hiroki Moriya    294    NA   JPN     0
    ## 10 Andreas Haider Maurer    857   190   AUT     0
    ## # ... with 117 more rows

#### (iv) Use rbind to stick w\_wim and l\_wim together. Call the result wl\_wim.

    wl_wim <- rbind(w_wim,l_wim)
    wl_wim

    ## # A tibble: 254 x 5
    ##                     name points    ht   ioc  wins
    ##  *                 <chr>  <int> <int> <chr> <dbl>
    ##  1        Novak Djokovic  13845   188   SRB     1
    ##  2       Jarkko Nieminen    564   185   FIN     1
    ##  3 Pierre Hugues Herbert    353    NA   FRA     1
    ##  4         Bernard Tomic   1355   193   AUS     1
    ##  5        Leonardo Mayer   1605   188   ARG     1
    ##  6     Marcel Granollers    715   190   ESP     1
    ##  7          Marsel Ilhan    647   190   TUR     1
    ##  8        Kevin Anderson   2090   203   RSA     1
    ##  9           Marin Cilic   3540   198   CRO     1
    ## 10     Ricardas Berankis    577   175   LTU     1
    ## # ... with 244 more rows

#### (v) Use group\_by on wl\_wim, to group it by name.

    wl_wim_group <- group_by(wl_wim,name)
    wl_wim_group

    ## # A tibble: 254 x 5
    ## # Groups:   name [128]
    ##                     name points    ht   ioc  wins
    ##  *                 <chr>  <int> <int> <chr> <dbl>
    ##  1        Novak Djokovic  13845   188   SRB     1
    ##  2       Jarkko Nieminen    564   185   FIN     1
    ##  3 Pierre Hugues Herbert    353    NA   FRA     1
    ##  4         Bernard Tomic   1355   193   AUS     1
    ##  5        Leonardo Mayer   1605   188   ARG     1
    ##  6     Marcel Granollers    715   190   ESP     1
    ##  7          Marsel Ilhan    647   190   TUR     1
    ##  8        Kevin Anderson   2090   203   RSA     1
    ##  9           Marin Cilic   3540   198   CRO     1
    ## 10     Ricardas Berankis    577   175   LTU     1
    ## # ... with 244 more rows

#### (vi) summarise the result of the previous step, with wins=sum(wins), points=points\[1\], ht=ht\[1\], ioc=ioc\[1\]

    resultsummary <-summarise(wl_wim_group,wins=sum(wins),points=points[1],ht=ht[1],ioc=ioc[1])

    resultsummary

    ## # A tibble: 128 x 5
    ##                     name  wins points    ht   ioc
    ##                    <chr> <dbl>  <int> <int> <chr>
    ##  1      Adrian Mannarino     1   1188   183   FRA
    ##  2          Albert Ramos     1    758   188   ESP
    ##  3       Alejandro Falla     0    423   185   COL
    ##  4  Aleksandr Nedovyesov     0    457    NA   KAZ
    ##  5      Alexander Zverev     1    689    NA   GER
    ##  6   Alexandr Dolgopolov     1    740   180   UKR
    ##  7          Aljaz Bedene     1    688   181   GBR
    ##  8 Andreas Haider Maurer     0    857   190   AUT
    ##  9         Andreas Seppi     2   1280   190   ITA
    ## 10           Andy Murray     5   7450   190   GBR
    ## # ... with 118 more rows

### (c) Calculate the average height for all players in the tournament. Use ggplot to plot player points versus number of wins.

    height=mean(resultsummary$ht,na.rm=TRUE)
    height

    ## [1] 186.65

    ggplot(data = resultsummary) +
      geom_point(mapping = aes(x = resultsummary$wins, y = resultsummary$points))

![](Assignment4_files/figure-markdown_strict/unnamed-chunk-13-1.png)

#### (d) Using the dataset by\_player, write code to find the names of the tournament winner and the losing finalist. If you did not manage to correctly construct the dataset by\_player, do this some other way.

    Tournament_winner <- sort(tapply(wl_wim_group$wins,wl_wim_group$name,sum),decreasing = TRUE)[1:2]
    Tournament_winner

    ## Novak Djokovic  Roger Federer 
    ##              7              6

    # Tournament Winner is Novak Djokovic and the losing finalist is Roger Federer

#### (e) Calculate the number of wins per country. How many matches were won by Spanish (ESP) players?

    country_by <- group_by(wl_wim,ioc)
    country_by

    ## # A tibble: 254 x 5
    ## # Groups:   ioc [43]
    ##                     name points    ht   ioc  wins
    ##  *                 <chr>  <int> <int> <chr> <dbl>
    ##  1        Novak Djokovic  13845   188   SRB     1
    ##  2       Jarkko Nieminen    564   185   FIN     1
    ##  3 Pierre Hugues Herbert    353    NA   FRA     1
    ##  4         Bernard Tomic   1355   193   AUS     1
    ##  5        Leonardo Mayer   1605   188   ARG     1
    ##  6     Marcel Granollers    715   190   ESP     1
    ##  7          Marsel Ilhan    647   190   TUR     1
    ##  8        Kevin Anderson   2090   203   RSA     1
    ##  9           Marin Cilic   3540   198   CRO     1
    ## 10     Ricardas Berankis    577   175   LTU     1
    ## # ... with 244 more rows

    X <- summarise(country_by,wins=sum(wins))

    wonmatches <- filter(X,ioc=='ESP')
    wonmatches

    ## # A tibble: 1 x 2
    ##     ioc  wins
    ##   <chr> <dbl>
    ## 1   ESP    11

#### (f) Draw a barplot showing the number of wins for the top 10 countries, preferrably in decreasing order by wins.

    topcountry <- head(X[order(X$wins,decreasing = TRUE),],10)
    topcountry$ioc <- factor(topcountry$ioc,levels = topcountry$ioc)
    ggplot(topcountry, aes(x=ioc,y=wins)) + geom_bar(stat="identity",fill=1:10)

![](Assignment4_files/figure-markdown_strict/unnamed-chunk-16-1.png)
