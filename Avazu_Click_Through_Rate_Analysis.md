Advertisement Placement in Mobile Applications
================
Chase Baggett

Introduction
============

In 2015, Avazu, an online digital marketing company released 10 days of their data representing marketing compaigns within mobile platforms. It amounts to over 40 million ad views, and associated to that, a click through result of true or false. This data does not come from a conducted experiment, but from the real world, therefore is observational in nature. In addition to that, like the real world, the data is dirty.

It is made more complicated by data anonymization where category descriptions or even names have been hidden from the researchers for reasons of confidentiality. For instance, we are given a cagegorical banner position, but not where that position is, which means we cannot hypothesize from a position of knowledge about the similarity of any positions. We are also given categorical variables they believe are important, with no context. Despite this, it is a valuable insight into the world of online marketing, and the size and reach of the data provides interesting research opportunities.

To put it in context, companies pay to advertise within the platform, and have many options for advertising. The goal of advertising for many companies is to maximize click per view, or click-through-rate. Specifically for this exercise, I intend to try to understand the effect of advertisement position on the click-through rate, after adjustment for other variables.

Data
====

To create a dataset from the raw level clicks and views, I am recording the view and click count of advertiements over the 10 days. The data I am working with is raw web traffic over the 240 hours. Given I have assembled the data from raw clicks we could consider this data simulated, though it is drawn from the real world, I cannot be certain of many aspects of the design and am making some assumptions.

It is a crossed factoral observational data Every adertisement has an associated position that it was placed within the app. All factor levels are represented within each of the other factor levels randomly, though not all of the factor levels combinations were ever clicked. There is no nesting. It is an entirely random design. I am treating all variables as fixed becsause I have no need to generalize beyond the levels of the data. However, we a continuous variavble of importance, and therefore must test the slope to determine in an ANCOVA is needed.

There are a total of four variables in the data.

<table>
<colgroup>
<col width="9%" />
<col width="11%" />
<col width="7%" />
<col width="4%" />
<col width="67%" />
</colgroup>
<thead>
<tr class="header">
<th>Variable</th>
<th>Structure</th>
<th>Type</th>
<th>Lvls</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Clicks</td>
<td>Continuous</td>
<td>Response</td>
<td>NA</td>
<td>The nunber of times the advertisement was clicked.</td>
</tr>
<tr class="even">
<td>Views</td>
<td>Continuous</td>
<td>Fixed</td>
<td>NA</td>
<td>The number of times a given advertisement was viewed.</td>
</tr>
<tr class="odd">
<td>Position</td>
<td>Factor</td>
<td>Fixed</td>
<td>3</td>
<td>The position on the site of the advertisement.</td>
</tr>
<tr class="even">
<td>Unknown</td>
<td>Factor</td>
<td>Fixed</td>
<td>7</td>
<td>An unkown anonymized categorical variable.</td>
</tr>
</tbody>
</table>

Exploring the Data
==================

The purpose of an advertiser is to maximize the numbers of clicks per view, or stated differently, they are trying to increase the slope between Views and Clicks. This lends itself naturally to an ANCOVA model with Views as a continuous predictor. Our primarily point of concern is finding factors that increase the slope between clicks and views, or industry terms, the click-through-rate.

As we can see below, there are some very clear and identifiable linear trends in the data, where slope and intercept both change, suggesting an interaction term will be necessary. For Unknown, Avazu would not tell the researchers what it meant, yet chose to include it in the data anyway. It has been been made entirely anonymous, and we therefore cannot attribute any specific meaning to it. Position represents one of three locations to place an advertisement within the mobile app.

<img src="Avazu_Click_Through_Rate_Analysis_files/figure-markdown_github/unnamed-chunk-2-1.png" style="display: block; margin: auto;" />

Picking a Model
===============

Slopes Equal to Zero
--------------------

In order to know which kind of model to fit, we must first test the slope of Click to Views. If we establish the slope is zero, we can use an ANOVA model, but if the slope is non-zero, we must use an ANCOVA model.

For a function of *y* = *β*<sub>0</sub> + *β*<sub>1</sub>*V**i**e**w**s*:

*H*<sub>0</sub> : *β*<sub>1</sub> = 0 vs *H*<sub>*a*</sub> : *β*<sub>1</sub> ≠ 0

As we can see below, with a near zero p-value, we reject the null hypothesis in favor the alternative that the slope is non-zero. This means we must use an ANCOVA model to account for the covariate.

<table>
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:right;">
Df
</th>
<th style="text-align:right;">
Sum.Sq
</th>
<th style="text-align:right;">
Mean.Sq
</th>
<th style="text-align:right;">
F.value
</th>
<th style="text-align:right;">
Pr..F.
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Views
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
9894694
</td>
<td style="text-align:right;">
9894694.31
</td>
<td style="text-align:right;">
363.2439
</td>
<td style="text-align:right;">
0
</td>
</tr>
<tr>
<td style="text-align:left;">
Residuals
</td>
<td style="text-align:right;">
2066
</td>
<td style="text-align:right;">
56277446
</td>
<td style="text-align:right;">
27239.81
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
</tr>
</tbody>
</table>
All Slopes Equal by Position
----------------------------

Now, we have established the slope is non-zero, but we have not established that the slopes are different. We must use this to decide to use an equal or different slopes model. For a function of *y* = *β*<sub>0</sub> + *β*<sub>1</sub>*V**i**e**w**s* + *β*<sub>2</sub>*P**o**s**i**t**i**o**n* + *β*<sub>3</sub>*V**i**e**w**s* \* *P**o**s**i**t**i**o**n*:

*H*<sub>0</sub> : *β*<sub>3</sub> = 0 vs *H*<sub>*a*</sub> : *β*<sub>3</sub> ≠ 0

As we can see below, with a near zero p-value, we reject the null hypothesis in favor the alternative that the slope are not equal, and therefore must use a different slopes model, because the interaction term is significant.

<table>
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:right;">
Df
</th>
<th style="text-align:right;">
Sum.Sq
</th>
<th style="text-align:right;">
Mean.Sq
</th>
<th style="text-align:right;">
F.value
</th>
<th style="text-align:right;">
Pr..F.
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Views
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
9894694.3
</td>
<td style="text-align:right;">
9894694.31
</td>
<td style="text-align:right;">
444.03969
</td>
<td style="text-align:right;">
0.0000000
</td>
</tr>
<tr>
<td style="text-align:left;">
Position
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
9821046.5
</td>
<td style="text-align:right;">
4910523.24
</td>
<td style="text-align:right;">
220.36731
</td>
<td style="text-align:right;">
0.0000000
</td>
</tr>
<tr>
<td style="text-align:left;">
Views:Position
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
508120.2
</td>
<td style="text-align:right;">
254060.08
</td>
<td style="text-align:right;">
11.40134
</td>
<td style="text-align:right;">
0.0000119
</td>
</tr>
<tr>
<td style="text-align:left;">
Residuals
</td>
<td style="text-align:right;">
2062
</td>
<td style="text-align:right;">
45948279.4
</td>
<td style="text-align:right;">
22283.36
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
</tr>
</tbody>
</table>
Unequal Slopes ANCOVA
=====================

I am using a generalized linear model of the following form to conduct the ANCOVA. Technically one of the factor levels will be "baked in" to the model, but I am including a beta for it here for statements on the hypothesis.

The Type 3 Test of Fixed Effects is Below. The model has added significant terms for the Unknown category, as well as the interraction term.
<table>
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:right;">
SS
</th>
<th style="text-align:right;">
DF
</th>
<th style="text-align:right;">
F
</th>
<th style="text-align:right;">
P
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
(Intercept)
</td>
<td style="text-align:right;">
0.2412948
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.0002007
</td>
<td style="text-align:right;">
0.9886990
</td>
</tr>
<tr>
<td style="text-align:left;">
Views
</td>
<td style="text-align:right;">
6.3304147
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.0052647
</td>
<td style="text-align:right;">
0.9421649
</td>
</tr>
<tr>
<td style="text-align:left;">
Position
</td>
<td style="text-align:right;">
51800.4729386
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
21.5398731
</td>
<td style="text-align:right;">
0.0000000
</td>
</tr>
<tr>
<td style="text-align:left;">
Unknown
</td>
<td style="text-align:right;">
1205651.2732322
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
200.5354313
</td>
<td style="text-align:right;">
0.0000000
</td>
</tr>
<tr>
<td style="text-align:left;">
Views:Position
</td>
<td style="text-align:right;">
982152.5066556
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
408.4024562
</td>
<td style="text-align:right;">
0.0000000
</td>
</tr>
<tr>
<td style="text-align:left;">
Views:Unknown
</td>
<td style="text-align:right;">
4993376.0235274
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
830.5459770
</td>
<td style="text-align:right;">
0.0000000
</td>
</tr>
<tr>
<td style="text-align:left;">
Residuals
</td>
<td style="text-align:right;">
2467390.8211141
</td>
<td style="text-align:right;">
2052
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
</tr>
</tbody>
</table>
Hypothesis Tests
----------------

This model has Five Hypothesis Tests.

Test for Intercept
------------------

*H*<sub>0</sub> : *β*<sub>0</sub> = 0 vs *H*<sub>*a*</sub> : *β*<sub>0</sub> ≠ 0

Outcome: Reject the Null in Favor of the Alternative
<table>
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:right;">
SS
</th>
<th style="text-align:right;">
DF
</th>
<th style="text-align:right;">
F
</th>
<th style="text-align:right;">
P
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
(Intercept)
</td>
<td style="text-align:right;">
0.2412948
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.0002007
</td>
<td style="text-align:right;">
0.988699
</td>
</tr>
</tbody>
</table>
Test For Slope Across Factors
-----------------------------

*H*<sub>0</sub> : *β*<sub>1</sub> = 0

*H*<sub>*a*</sub> : *β*<sub>1</sub> ≠ 0

Outcome: Fail to Reject the Null. We could think of this as no slope between click and views in common across the factors. The interaction terms are significant so it stays in the model.
<table>
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:right;">
SS
</th>
<th style="text-align:right;">
DF
</th>
<th style="text-align:right;">
F
</th>
<th style="text-align:right;">
P
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Views
</td>
<td style="text-align:right;">
6.330415
</td>
<td style="text-align:right;">
1
</td>
<td style="text-align:right;">
0.0052647
</td>
<td style="text-align:right;">
0.9421649
</td>
</tr>
</tbody>
</table>
Test for Position Mean
----------------------

At Least One Inequality Satisfies rejection of the null

*H*<sub>0</sub> : *β*<sub>2</sub> = *β*<sub>3</sub> = *β*<sub>4</sub> vs *H*<sub>0</sub> : *β*<sub>2</sub> ≠ *β*<sub>3</sub> ≠ *β*<sub>4</sub>

Outcome: Reject the null in favor of the alternative.
<table>
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:right;">
SS
</th>
<th style="text-align:right;">
DF
</th>
<th style="text-align:right;">
F
</th>
<th style="text-align:right;">
P
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Position
</td>
<td style="text-align:right;">
51800.47
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
21.53987
</td>
<td style="text-align:right;">
0
</td>
</tr>
</tbody>
</table>
Test for Unknown Category Mean
------------------------------

At Least One Inequality Satisfies rejection of the null

*H*<sub>0</sub> : *β*<sub>5</sub> = *β*<sub>6</sub> = *β*<sub>7</sub> = *β*<sub>8</sub> = *β*<sub>9</sub> = *β*<sub>10</sub> = *β*<sub>11</sub> vs *H*<sub>*a*</sub> : *β*<sub>5</sub> ≠ *β*<sub>6</sub> ≠ *β*<sub>7</sub> ≠ *β*<sub>8</sub> ≠ *β*<sub>9</sub> ≠ *β*<sub>10</sub> ≠ *β*<sub>11</sub>

Outcome: Reject the null in favor of the alternative.
<table>
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:right;">
SS
</th>
<th style="text-align:right;">
DF
</th>
<th style="text-align:right;">
F
</th>
<th style="text-align:right;">
P
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Unknown
</td>
<td style="text-align:right;">
1205651
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
200.5354
</td>
<td style="text-align:right;">
0
</td>
</tr>
</tbody>
</table>
Test for Difference in Slope by Position
----------------------------------------

At Least One Inequality Satisfies rejection of the null

*H*<sub>0</sub> : *β*<sub>12</sub> = *β*<sub>13</sub> = *β*<sub>14</sub> vs *H*<sub>0</sub> : *β*<sub>12</sub> ≠ *β*<sub>13</sub> ≠ *β*<sub>14</sub>

Outcome: Reject the null in favor of the alternative.

<table>
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:right;">
SS
</th>
<th style="text-align:right;">
DF
</th>
<th style="text-align:right;">
F
</th>
<th style="text-align:right;">
P
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Views:Position
</td>
<td style="text-align:right;">
982152.5
</td>
<td style="text-align:right;">
2
</td>
<td style="text-align:right;">
408.4025
</td>
<td style="text-align:right;">
0
</td>
</tr>
</tbody>
</table>
Test for Difference in Slope by Unknown Category
------------------------------------------------

At Least One Inequality Satisfies rejection of the null

*H*<sub>0</sub> : *β*<sub>15</sub> = *β*<sub>16</sub> = *β*<sub>17</sub> = *β*<sub>18</sub> = *β*<sub>19</sub> = *β*<sub>20</sub> = *β*<sub>21</sub> vs *H*<sub>*a*</sub> : *β*<sub>15</sub> ≠ *β*<sub>16</sub> ≠ *β*<sub>17</sub> ≠ *β*<sub>18</sub> ≠ *β*<sub>19</sub> ≠ *β*<sub>20</sub> ≠ *β*<sub>21</sub>

Outcome: Reject the null in favor of the alternative.

<table>
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:right;">
SS
</th>
<th style="text-align:right;">
DF
</th>
<th style="text-align:right;">
F
</th>
<th style="text-align:right;">
P
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Views:Unknown
</td>
<td style="text-align:right;">
4993376
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
830.546
</td>
<td style="text-align:right;">
0
</td>
</tr>
</tbody>
</table>
Mean Comparisons
================

Position
--------

Because I have a covariate and my primary area of interest in the interaction between views and clicks, I am doing a Tukey means comparison at 3 points along the values. As Views increases they each start to separate into their own groups. At high numbers of views we can establish a signficiant difference between all 3 positions, with banner position 0 having the highest mean. The middle View amount represents the mean for the data.

![](Avazu_Click_Through_Rate_Analysis_files/figure-markdown_github/unnamed-chunk-12-1.png)

Conclusion
==========

We've established that clicks do increase with views, and that position as well as our unknown category both effect the mean as well as the slope between click and views. Considering the unknown category as a fixed and unchangeable variable, we can provide guidance to advertisers that banner position 0 has a significantly higher click-through-rate as compared to banner position 1 and 2. Knowing the most beneficial advertisement within a mobile application could provide considerible value to advertisers.

Appendix
========

Location of the Raw Data: <https://www.kaggle.com/c/avazu-ctr-prediction> Full Code and Aggregated Data on Github: <https://github.com/cbagg/avazu_click_through>

The entire project was performed in R.

The entire document is reproducible via the R code and included data on github, provided the right packages are installed on the machine.

Notes
-----

I conducted my study only on app category 07d7df22 and banner\_position 0,1,2, taking the others out of the study because they were so rare it created missing data in the comnbinations. Over 35 milllion clicks remained. I aggredated those clicks into a dataset with 2,068 records, once for each application. Because it is click log data I could have reobserved the data at the app, site, or other levels, and chose to observe it at the application level because that seemed most logical to me. I consider this data more akin to a video feed-- there are many things I could have observed from it because it is extremely granular.

I could not test the interaction term between Views,Unknown and Position because some combinations had only a click of zero.

Table for Tukey Means
---------------------

``` r
knitr::kable(data.frame(pos_means_letters), row.names = F)
```

<table>
<thead>
<tr>
<th style="text-align:left;">
Position
</th>
<th style="text-align:right;">
Views
</th>
<th style="text-align:right;">
lsmean
</th>
<th style="text-align:right;">
SE
</th>
<th style="text-align:right;">
df
</th>
<th style="text-align:right;">
lower.CL
</th>
<th style="text-align:right;">
upper.CL
</th>
<th style="text-align:left;">
.group
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
2
</td>
<td style="text-align:right;">
5000.00
</td>
<td style="text-align:right;">
-568.1410
</td>
<td style="text-align:right;">
330.2460
</td>
<td style="text-align:right;">
2052
</td>
<td style="text-align:right;">
-1482.4092
</td>
<td style="text-align:right;">
346.1273
</td>
<td style="text-align:left;">
a
</td>
</tr>
<tr>
<td style="text-align:left;">
1
</td>
<td style="text-align:right;">
5000.00
</td>
<td style="text-align:right;">
206.1607
</td>
<td style="text-align:right;">
306.1976
</td>
<td style="text-align:right;">
2052
</td>
<td style="text-align:right;">
-641.5309
</td>
<td style="text-align:right;">
1053.8524
</td>
<td style="text-align:left;">
b
</td>
</tr>
<tr>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
5000.00
</td>
<td style="text-align:right;">
221.9675
</td>
<td style="text-align:right;">
306.1820
</td>
<td style="text-align:right;">
2052
</td>
<td style="text-align:right;">
-625.6809
</td>
<td style="text-align:right;">
1069.6160
</td>
<td style="text-align:left;">
c
</td>
</tr>
<tr>
<td style="text-align:left;">
2
</td>
<td style="text-align:right;">
12652.61
</td>
<td style="text-align:right;">
-1469.2586
</td>
<td style="text-align:right;">
837.0145
</td>
<td style="text-align:right;">
2052
</td>
<td style="text-align:right;">
-3786.4883
</td>
<td style="text-align:right;">
847.9710
</td>
<td style="text-align:left;">
a
</td>
</tr>
<tr>
<td style="text-align:left;">
1
</td>
<td style="text-align:right;">
12652.61
</td>
<td style="text-align:right;">
465.9629
</td>
<td style="text-align:right;">
775.5229
</td>
<td style="text-align:right;">
2052
</td>
<td style="text-align:right;">
-1681.0306
</td>
<td style="text-align:right;">
2612.9565
</td>
<td style="text-align:left;">
b
</td>
</tr>
<tr>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
12652.61
</td>
<td style="text-align:right;">
499.6191
</td>
<td style="text-align:right;">
775.5167
</td>
<td style="text-align:right;">
2052
</td>
<td style="text-align:right;">
-1647.3572
</td>
<td style="text-align:right;">
2646.5954
</td>
<td style="text-align:left;">
c
</td>
</tr>
<tr>
<td style="text-align:left;">
2
</td>
<td style="text-align:right;">
50000.00
</td>
<td style="text-align:right;">
-5867.0250
</td>
<td style="text-align:right;">
3310.2433
</td>
<td style="text-align:right;">
2052
</td>
<td style="text-align:right;">
-15031.2557
</td>
<td style="text-align:right;">
3297.2056
</td>
<td style="text-align:left;">
a
</td>
</tr>
<tr>
<td style="text-align:left;">
1
</td>
<td style="text-align:right;">
50000.00
</td>
<td style="text-align:right;">
1733.8878
</td>
<td style="text-align:right;">
3066.0297
</td>
<td style="text-align:right;">
2052
</td>
<td style="text-align:right;">
-6754.2506
</td>
<td style="text-align:right;">
10222.0262
</td>
<td style="text-align:left;">
b
</td>
</tr>
<tr>
<td style="text-align:left;">
0
</td>
<td style="text-align:right;">
50000.00
</td>
<td style="text-align:right;">
1854.6550
</td>
<td style="text-align:right;">
3066.0451
</td>
<td style="text-align:right;">
2052
</td>
<td style="text-align:right;">
-6633.5260
</td>
<td style="text-align:right;">
10342.8361
</td>
<td style="text-align:left;">
c
</td>
</tr>
</tbody>
</table>
