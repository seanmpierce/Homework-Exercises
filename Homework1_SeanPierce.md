# Homework 1

## Sean Pierce

**1)**  
So the year is 2008 and you’ve just finished your first Statistical
Learning assignment. While you learned a lot, it was pretty tough! You
decide to treat yourself for all your hard work by taking a trip to Las
Vegas. What’s the best month/day to go to minimize your delay, and which
airline should you fly?

Let’s explore the ABIA data set to answer these questions!

First let’s look at the carriers that depart from Austin heading for Las
Vegas.

    ## [1] "WN" "YV"

Carriers are Mesa airlines (YV) and Southwest Airlines (WN) There are
only two carries that fly to LAS in 2008 which should make our choice
simpler.

Let’s see which one is better:

The red line is the average delay for the year. Mesa is clearly lower,
but with less frequent flights.

    ## # A tibble: 2 × 4
    ## # Groups:   Year [1]
    ##    Year UniqueCarrier count avg_delay
    ##   <int> <chr>         <int>     <dbl>
    ## 1  2008 WN             1116     8.53 
    ## 2  2008 YV              115    -0.875

<img src="Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-6-1.png" style="display: block; margin: auto;" />

    ## Warning: Removed 3 rows containing non-finite values (stat_boxplot).

<img src="Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-6-2.png" style="display: block; margin: auto;" />

Flying with Mesa in January will give you the lowester average departure
delay.

Let’s go further and see the best day in January to fly with Mesa:

<img src="Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-8-1.png" style="display: block; margin: auto;" />
If you hate departure delays any day of the second week in January is
the best time to go.

**2)**

1.  

<!-- -->

    ## # A tibble: 10 × 3
    ## # Groups:   performer [10]
    ##    performer                              song                             count
    ##    <chr>                                  <chr>                            <int>
    ##  1 Imagine Dragons                        Radioactive                         87
    ##  2 AWOLNATION                             Sail                                79
    ##  3 Jason Mraz                             I'm Yours                           76
    ##  4 The Weeknd                             Blinding Lights                     76
    ##  5 LeAnn Rimes                            How Do I Live                       69
    ##  6 LMFAO Featuring Lauren Bennett & Goon… Party Rock Anthem                   68
    ##  7 OneRepublic                            Counting Stars                      68
    ##  8 Adele                                  Rolling In The Deep                 65
    ##  9 Jewel                                  Foolish Games/You Were Meant Fo…    65
    ## 10 Carrie Underwood                       Before He Cheats                    64

This plot shows us the most popular songs from 1959-2020 as defined as
the number of weeks spent on the Billboard 100. The total number of
weeks is contained in the count column. Imagine Dragons’s “Radioactive”
took the top spot for the most popular song with AWOLNATION’s “Sail” a
close second.  
These results are not surprising if you listened to the radio at all in
the past decade. Not my cup of tea, but who am I to judge? The only
surprisinng result is LeAnn Rimes’s “How Do I Live”, the title track
from the 1997 hit-film “Con Air” starring Nicholas Cage.

1.  Now we move on to musical diversity (number of unique songs that
    appeared on the Billboard 100 each year). How has it changed over
    time?

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-14-1.png)

There has been significant fluctuations in the diversity of music
overtime. We can see that the 1960s had the greatest diversity. The
trend in diversity fell to an all-time low in the 2000s (Thanks to Smash
Mouth’s “All-Star” in 1999. There’s no doubt that No Doubt is
responsible for this as well). The trend reversed in the early 2000s and
has recently peaked. C.

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-16-1.png)
This neat graph displays what can be thought of as the most popular
musicians of modern times. We define the popularity as the number of
songs they’ve written that spent ten weeks or longer on the Billboard. A
surprising result is the high amount of country music stars on this
list.

**3)**

Let’s take a look at historical data for the Olympics and try to glean
some interesting facts it. (A) what is the 95th percentile of height for
female competitors across all events? (B) Which women’s event had the
greatest variability in competitor’s heights across the entire history
of the Olympics? (C) How has the average age of male and female Olympic
swimmers changed over time?  
A. Note: Height reported in Centimeters.

    ##   quantile(height, prob = c(0.95))
    ## 1                              186

B. The event with the highest variability in women’s heights is Coxed
Fours Rowing. The Coxswain does not row, but is in charge of steering
the boat, and being small in stature reduces the drag. Those rowing
should be taller for increased power from greater arm length.
[Source](https://en.wikipedia.org/wiki/Coxswain_(rowing))

    ## # A tibble: 1 × 2
    ##   event                      height_variability
    ##   <chr>                                   <dbl>
    ## 1 Rowing Women's Coxed Fours               10.9

1.  

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-23-1.png)
This graph shows the average age of male and female Olympic swimmers
over time. In the Olympics early years there was greater variability of
the average age. We can see the average age bottoms out and then slowly
rises year over year to the present day. Note: Women competed for the
first time in the 1900 Olympic games in Paris;
[Source](https://olympics.com/ioc/faq/history-and-origin-of-the-games/when-did-women-first-compete-in-the-olympic-games)

**4)**

Now we will explore the data set sclass.csv which details the many
characteristics of several S-class Mercedes trims. We want to focus on
the 350, and 65 AMG trims and create a predictive model of price using
mileage. To accomplish this we will be using utilizing K-nearest
neighbors and K-folds. We generate our model on a training data set (80%
of data) and then, using the remaining 20% of the data, test the the
accuracy of our predictive line by the root mean squared error. We then
plot the lowest RMSE predictive line against our data set to show what a
reasonable, but not necessarily optimal model looks like.

First, let’s create our training and testing sets for both trims.

    split_350 = initial_split(s350, prop=0.8)
    train_350 = training(split_350)
    test_350 = testing(split_350)

    split_65 = initial_split(s65, prop=0.8)
    train_65 = training(split_65)
    test_65 = testing(split_65)

Next, we’ll perform K-nearest neighbors for various & increasing values
of K. We’ll also plot each one to get a feel for how the bias and
variance progresses with K. Let’s start with the 350 S-class.

    ## [1] 13562.98

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-26-1.png)

    ## [1] 11384.46

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-27-1.png)

    ## [1] 9652.011

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-27-2.png)

    ## [1] 9523.361

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-28-1.png)

    ## [1] 9646.581

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-28-2.png)

    ## [1] 9718.347

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-28-3.png)

    ## [1] 9749.745

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-28-4.png)

    ## [1] 10171.6

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-28-5.png)

Now let’s use a K-folds approach and graph the RMSEs of different K
values.

The different K values we will be testing are:

    ##  [1]   2   4   6   8  10  15  20  25  30  35  40  45  50  65  76  80  90 100 125
    ## [20] 150 175 200 250 300

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-32-1.png)
From this plot of the RMSEs it appears that the optimal value of K is
around 18. The corresponding RMSE with K=18:

    ## [1] 10040.92

Let’s plot this and see if we like our choice:

    ## [1] 9493.096

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-35-1.png)
This looks great for the overall trend, but maybe doesn’t capture enough
variance in the data. Overall though, this seems like an effective
predictive model.

**65 AMG sclass**

    ## [1] 23513.06

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-36-1.png)

    ## [1] 21268.78

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-37-1.png)

    ## [1] 18624.81

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-37-2.png)

    ## [1] 17029.53

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-37-3.png)

    ## [1] 16502.54

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-37-4.png)

    ## [1] 16865.62

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-37-5.png)

    ## [1] 16585.25

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-37-6.png)

    ## [1] 20524.32

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-37-7.png)

Now let’s use a K-folds approach and graph the RMSEs of different K
values, using the same K grid we used for the 350 s-class.

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-39-1.png)

From this plot it appears that the optimal value of k is around 10

Let’s plot this and see if we agree that this is the optimal K value:

    ## [1] 18624.81

![](Homework1_SeanPierce_files/figure-markdown_strict/unnamed-chunk-41-1.png)

It seems that the 65 AMG predictive model has a lower average RMSE than
the 350.  
The 350 s-class has a higher optimal value of K.This is most likely true
because the observations are more concentrated. There is less variance
in price for a given mileage.
