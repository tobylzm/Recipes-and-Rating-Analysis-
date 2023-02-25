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

The dataframe after cleaning are shown below:
|    | name                                 |     id |   minutes |   contributor_id | submitted   | tags                                                                                                                                                                                                                                                                                               | nutrition                                     |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | description                                                                                                                                                                                                                                                                                                                                                                       | ingredients                                                                                                                                                                                                                             |   n_ingredients |   avg_rating |   calories |   total_fat |   sugar |   sodium |   protein |   saturated_fat |   carbohydrates |   cal_pro_ratio |\n|---:|:-------------------------------------|-------:|----------:|-----------------:|:------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------|----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|-------------:|-----------:|------------:|--------:|---------:|----------:|----------------:|----------------:|----------------:|\n|  0 | 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27  | [\'60-minutes-or-less\', \'time-to-make\', \'course\', \'main-ingredient\', \'preparation\', \'for-large-groups\', \'desserts\', \'lunch\', \'snacks\', \'cookies-and-brownies\', \'chocolate\', \'bar-cookies\', \'brownies\', \'number-of-servings\']                                                                        | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]      |        10 | [\'heat the oven to 350f and arrange the rack in the middle\', \'line an 8-by-8-inch glass baking dish with aluminum foil\', \'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted\', \'remove from heat and let cool to room temperature\', \'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated\', \'add cooled chocolate and mix until uniform in color\', \'add flour and stir until just incorporated\', \'transfer batter to the prepared baking dish\', \'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes\', \'remove from the oven and cool completely before cutting\']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you\'ll ever make.....sereiously! there\'s no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they\'re pure heaven!                                                                                                              | [\'bittersweet chocolate\', \'unsalted butter\', \'eggs\', \'granulated sugar\', \'unsweetened cocoa powder\', \'vanilla extract\', \'brewed espresso\', \'kosher salt\', \'all-purpose flour\']                                                          |               9 |            4 |      138.4 |          10 |      50 |        3 |         3 |              19 |               6 |        46.1333  |\n|  1 | 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11  | [\'60-minutes-or-less\', \'time-to-make\', \'cuisine\', \'preparation\', \'north-american\', \'for-large-groups\', \'canadian\', \'british-columbian\', \'number-of-servings\']                                                                                                                                      | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0]  |        12 | [\'pre-heat oven the 350 degrees f\', \'in a mixing bowl , sift together the flours and baking powder\', \'set aside\', \'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy\', \'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined\', \'add in the flour mixture to the wet ingredients and blend until combined\', \'scrape down the sides of the bowl and add the chocolate chips\', \'mix until combined\', \'scrape down the sides to the bowl again\', \'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking\', \'bake for 10 - 15 minutes or until golden brown on the outside and soft & chewy in the center\', \'serve hot and enjoy !\']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don\'t have margarine or don\'t like it, then just use butter (softened) instead.                                                                                                                                            | [\'white sugar\', \'brown sugar\', \'salt\', \'margarine\', \'eggs\', \'vanilla\', \'water\', \'all-purpose flour\', \'whole wheat flour\', \'baking soda\', \'chocolate chips\']                                                                             |              11 |            5 |      595.1 |          46 |     211 |       22 |        13 |              51 |              26 |        45.7769  |\n|  2 | 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | [\'60-minutes-or-less\', \'time-to-make\', \'course\', \'main-ingredient\', \'preparation\', \'side-dishes\', \'vegetables\', \'easy\', \'beginner-cook\', \'broccoli\']                                                                                                                                               | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]     |         6 | [\'preheat oven to 350 degrees\', \'spray a 2 quart baking dish with cooking spray , set aside\', \'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce\', \'pour into baking dish , sprinkle remaining cheese over top\', \'bake for 25 minutes or until cheese is lightly browned\', \'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes\']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don\'t think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell\'s soup. but i think mine is better since i don\'t like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | [\'frozen broccoli cuts\', \'cream of chicken soup\', \'sharp cheddar cheese\', \'garlic powder\', \'ground black pepper\', \'salt\', \'milk\', \'soy sauce\', \'french-fried onions\']                                                                   |               9 |            5 |      194.8 |          20 |       6 |       32 |        22 |              36 |               3 |         8.85455 |\n|  6 | millionaire pound cake               | 286009 |       120 |           461724 | 2008-02-12  | [\'time-to-make\', \'course\', \'cuisine\', \'preparation\', \'occasion\', \'north-american\', \'desserts\', \'american\', \'southern-united-states\', \'dinner-party\', \'holiday-event\', \'cakes\', \'dietary\', \'christmas\', \'thanksgiving\', \'low-sodium\', \'low-in-something\', \'taste-mood\', \'sweet\', \'4-hours-or-less\'] | [878.3, 63.0, 326.0, 13.0, 20.0, 123.0, 39.0] |         7 | [\'freheat the oven to 300 degrees\', \'grease a 10-inch tube pan with butter , dust the bottom and sides with flour , and set aside\', \'in a large mixing bowl , cream the butter and sugar with an electric mixer and add the eggs one at a time , beating after each addition\', \'alternately add the flour and milk , stirring till the batter is smooth\', \'add the two extracts and stir till well blended\', \'scrape the batter into the prepared pan and bake till a cake tester or knife blade inserted in the center comes out clean , about 1 1 / 2 hours\', \'cool the cake in the pan on a rack for 5 minutes , then turn it out on the rack to cool completely\']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | why a millionaire pound cake?  because it\'s super rich!  this scrumptious cake is the pride of an elderly belle from jackson, mississippi.  the recipe comes from "the glory of southern cooking" by james villas.                                                                                                                                                                | [\'butter\', \'sugar\', \'eggs\', \'all-purpose flour\', \'whole milk\', \'pure vanilla extract\', \'almond extract\']                                                                                                                                |               7 |            5 |      878.3 |          63 |     326 |       13 |        20 |             123 |              39 |        43.915   |\n|  7 | 2000 meatloaf                        | 475785 |        90 |          2202916 | 2012-03-06  | [\'time-to-make\', \'course\', \'main-ingredient\', \'preparation\', \'main-dish\', \'potatoes\', \'vegetables\', \'4-hours-or-less\', \'meatloaf\', \'simply-potatoes2\']                                                                                                                                             | [267.0, 30.0, 12.0, 12.0, 29.0, 48.0, 2.0]    |        17 | [\'pan fry bacon , and set aside on a paper towel to absorb excess grease\', \'mince yellow onion , red bell pepper , and add to your mixing bowl\', \'chop garlic and set aside\', \'put 1tbsp olive oil into a saut pan , along with chopped garlic , teaspoons white pepper and a pinch of kosher salt\', \'bring to a medium heat to sweat your garlic\', \'preheat oven to 350f\', \'coarsely chop your baby spinach add to your heated pan , stir frequently for approximately 5 min to wilt\', \'add your spinach to the mixing bowl\', \'chop your now cooled bacon , and add it to the mixing bowl\', \'add your meatloaf mix to the bowl , with one egg and mix till thoroughly combined\', \'add your goat cheese , one egg , 1 / 8 tsp white pepper and 1 / 8 tsp of kosher salt and mix till thoroughly combined\', \'transfer to a 9x5 meatloaf pan , and cook for 60 min or until the internal temperature is at least 160f\', \'let stand for 5min\', \'melt 1tbsp unsalted butter into a frying pan , and cook up to three eggs at a time\', \'crack each egg into a separate dish , in order to prevent egg shells from reaching the pan , then add salt and pepper to taste\', \'wait until the egg whites are firm looking , but slightly runny on top before flipping your eggs\', \'after flipping , wait 10~20 seconds before removing each egg and placing it over your slices of meatloaf\'] | ready, set, cook! special edition contest entry: a mediterranean flavor inspired meatloaf dish. featuring: simply potatoes - shredded hash browns, egg, bacon, spinach, red bell pepper, and goat cheese.                                                                                                                                                                         | [\'meatloaf mixture\', \'unsmoked bacon\', \'goat cheese\', \'unsalted butter\', \'eggs\', \'baby spinach\', \'yellow onion\', \'red bell pepper\', \'simply potatoes shredded hash browns\', \'fresh garlic\', \'kosher salt\', \'white pepper\', \'olive oil\'] |              13 |            5 |      267   |          30 |      12 |       12 |        29 |              48 |               2 |         9.2069  |



### Univariate Analysis

Plot: Distribution of Average Ratings for hhpf
<iframe src="assets/uni_plot_one.html" width=800 height=600 frameBorder=0></iframe>
The plot shows that the distribution of average rating for high protein food using a histogram. It seems like overall it's very high!


### Bivariate Analysis

Plot: Relationship between minutes and average rating (for minutes less than 120)
<iframe src="assets/bi_plot_one.html" width=800 height=600 frameBorder=0></iframe>
The plot shows that the relationship between minutes and average rating for minutes less than 120. It seems like most shorter time recipes have higher rating!


### Interesting Aggregates
| rating_above_3   |   False |    True |\n|:-----------------|--------:|--------:|\n| False            | 6.99545 | 6.91119 |\n| True             | 7.02005 | 6.85427 |

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



### Hypothesis Testing
** Null Hypothesis ** : The average rating of healthy high protein food higher than others food is due to random chance
** Alternative Hypothesis ** : The average rating of healthy high protein food is higher than normal is not due to random chance

Choice of test statistics: The mean of average rating

Level of significance: 0.01

P-value: 0

Conclusion: Reject the null hypothesis that the average rating of healthy high protein food higher than others food is due to random chance.
















