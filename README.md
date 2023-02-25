# Healthy High Protein Food!

This is a project for DSC 80 at UCSD

by Zhiming Liu (zhl109@ucsd.edu)

---

## Introduction

In this project, I took the recipe and rating datasets from the [food.com](food.com). 

The raw datasets are:
- Recipes data contains information about the recipes
- Interaction data contains information about the reviews and rating

I left merge the two datasets to get the average rating for each recipes as my final dataset to work on, in total there are 83781 rows and 13 columns


The interested column of my analysis will be mainly focusing on:
- Nutrition (which contains information of calories, fat, sugar, sodium, protein )
- Average rating (which contains the average rating ranging form 1-5)

other columns like:
- minutes (which contains the preparing time)
- n_steps(which contains number of steps)

will be used in some analysis



My interested question to investigate is: 
### Q: Does Heathy High Protein Food has a higher rating?
Heathy High Protein Food Definition: Calories protein ratio less than 10 :1

---

## Cleaning and EDA

### Data Cleaning
There are several operation I perfromed on this dataset which are:

- Seperating nutrition values into different columns
The nutrition columns are in the form of string that look like list, I sperate each of them into my dataframe.
In this way, I can get the value of protein and calories to generate another column of calories protein ratio that determine the healthy high protein food

- Filling 0 in the minutes column with np.nan

- Transfer tag, steps, and ingredients from a string of list to a list of string
Didn't help much to my analysis but did make the data look more tidier

- Replacing recipes with 0g of protein to 0.1 g of proteins
This prevent the appearance of NaN on calories protein ratio

- Adding a column called cal-pro-ratio
This stpes help me to get the my target data called calories protein ration which divide protein from calories

- Dropping certain column that is not useful
To make sure the data frame display nice

The dataframe after cleaning are shown below:
| name                                 |     id |   minutes |   contributor_id | submitted   |   n_steps |   n_ingredients |   avg_rating |   calories |   total_fat |   sugar |   sodium |   protein |   saturated_fat |   carbohydrates |   cal_pro_ratio |
|:-------------------------------------|-------:|----------:|-----------------:|:------------|----------:|----------------:|-------------:|-----------:|------------:|--------:|---------:|----------:|----------------:|----------------:|----------------:|
| 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27  |        10 |               9 |            4 |      138.4 |          10 |      50 |        3 |         3 |              19 |               6 |        46.1333  |
| 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11  |        12 |              11 |            5 |      595.1 |          46 |     211 |       22 |        13 |              51 |              26 |        45.7769  |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  |         6 |               9 |            5 |      194.8 |          20 |       6 |       32 |        22 |              36 |               3 |         8.85455 |
| millionaire pound cake               | 286009 |       120 |           461724 | 2008-02-12  |         7 |               7 |            5 |      878.3 |          63 |     326 |       13 |        20 |             123 |              39 |        43.915   |
| 2000 meatloaf                        | 475785 |        90 |          2202916 | 2012-03-06  |        17 |              13 |            5 |      267   |          30 |      12 |       12 |        29 |              48 |               2 |         9.2069  |





### Univariate Analysis

Plot: Distribution of Average Ratings for hhpf

<iframe src="assets/uni_plot.html" width=800 height=600 frameBorder=0></iframe>

The plot shows that the distribution of average rating for high protein food using a histogram. It seems like overall it's very high!


### Bivariate Analysis

Plot: Relationship between minutes and average rating (for minutes less than 120)

<iframe src="assets/bi_plot.html" width=800 height=600 frameBorder=0></iframe>

The plot shows that the relationship between minutes and average rating for minutes less than 120. It seems like most shorter time recipes have higher rating!


### Interesting Aggregates
| rating_above_3   |   False |    True |
|:-----------------|--------:|--------:|
| False            | 6.99545 | 6.91119 |
| True             | 7.02005 | 6.85427 |

It seems like the calories protein ratio for food that is 60min or less or not, and rating above 3 or not is quite close!


---


## Assesment of missingness

### NMAR Analysis
The description is not missing at random(NMAR) since if the description is too hard to describe or too easy to describe, the user just won't write it. Or it may be depend on the user's habbit. I would collect data about user's other's posts (whether the post have description missing or not) to confirm the idea.


### Missingness Dependency

#### For depend on
Using Permutation test to test whether the missingness of average rating depends on the number of steps

Column picked : name (added column that shows length of name)

<iframe src="assets/ns_dis_plot.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/ns_dis_False.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/stepemp_n.html" width=800 height=600 frameBorder=0></iframe>

 ** p_value=0.0, p-value <0.05 reject that the missingness of average rating does not depend on number of steps **


##### For not depend on (MCAR)
Using Permutation test to test whether the missingness of average rating depends on the length of the name

Column picked : name (added column that shows length of name)

<iframe src="assets/lenn_dis_plot.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/lenn_dis_plot_2.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/emp_lenn.html" width=800 height=600 frameBorder=0></iframe>

 ** p_value=0.267, p-value >0.05 fail to reject that missingness of avg_rating depends on lenghth of name **

---

### Hypothesis Testing
** Null Hypothesis ** : The average rating of healthy high protein food higher than others food is due to random chance

** Alternative Hypothesis ** : The average rating of healthy high protein food is higher than normal is not due to random chance

Choice of test statistics: The mean of average rating

Level of significance: 0.01

P-value: 0

Conclusion: Reject the null hypothesis that the average rating of healthy high protein food higher than others food is due to random chance.
















