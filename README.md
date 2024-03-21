# Recipe-Data-Exploration

This project is for DSC80 at UCSD. 
by Amelia Lei and Kyra Deng

---

## Introduction

The world of cooking has taken a change as people start to take on fast-paced lifestyles. Thus, people tend to resort to eating out which may take a toll on one's health. To encourage people to cook more, we analyzed recipes based on their preparation times and nutrition to see what types of recipes people ejoy more. Since we know that many people don't have a lot of time on their hands, we will do our investigation on recipes that take 30 minutes or under to complete. 

The first dataset we are given contains information for 83782 recipes, and comes from food.com. It contains 10 columns, with the descriptions below. 

<img src="recipes_description.jpeg" >


The second dataset we are given contains people's ratings on the recipes and also comes from food.com. It contains 5 columns, and has 731,927 total reviews. 

## Data Cleaning and Exploratory Data Analysis

Before conducting any analysis, we first merged the two datasets together to have one cohesive dataset to work with. The two dataframes have one column in common; the "id" and "recipe_id" columns. We merge on those columns and drop the "recipe_id" column. 
In the new merged dataframe, we noticed that there were ratings of 0s for some recipes, and replaced those with np.NaN because the 0 was not a true reflection of the ratings for those recipes. In this dataframe, there were repeated recipes since some recipes had multiple ratings, so we got a series of average ratings per each unique recipe and added that back to the dataframe. This dataframe is named 'final'.
We split up the values in the 'nutrition' column to individual columns named: 'calories (#)', 'total fat (PDV)', 'sugar (PDV)', 'sodium (PDV)', 'protein (PDV)', 'saturated fat (PDV)',  and 'carbohydrates (PDV)', with all the values in those columns being ints and we drop the 'nutrition' column. After checking the types of the values in the columns, we notice that the 'tags', 'steps' and 'ingredient' columns contains strings that are formatted like lists, so we changed the strings into actual lists with the commas in the original string representing the different elements within each list. We changed the 'submitted' and 'date' column from an object to a datetime data type. 
Lastly, since we want to work with quick recipes, or recipes that are 30 minutes or shorter, so we filter for those recipes only and recipes with less than 1000 calories so we can focus on a more specific dataset.


## Assessment of Missingness 
### NMAR Analysis

One column in the dataset wth missing values that may be NMAR is the  description column. The missingness may be due to the user thinking their recipe does not need a description because it is straightfoward enough. Another reasons may be ebcause the user does not have enough time to write a description on top of writing the rest of the recipe so they leave it out as it's not necesssary.

### Missingness Dependancy 

Another column whose missingness we decided to investigate was the reviews column. While running our permutation tests to see if the distributions of the other columns remained the same when reviews was missing was when it was not, we found that the missigness of reviews does not depend on name but does depend on total fat. 

#### 1. Reviews and Name

Null Hypothesis: The distribution of the name is the same when reviews is missing and when it's not missing.

Alternative Hypothesis: The distribution of name is different when reviews is missing and when it's not missing.

Test Statistic: Since name is a categorical variable, we use total variation distance as our test statistic

We reassigned the name column with a shuffled version of names. 





## Hypothesis Testing
Null Hypothesis: There is no correlation between average recipe rating and the amount of sodium in each individual recipe. 

Alternate Hypothesis: There is significant correlation between average recipe rating and the amount of sodium in each individual recipe. 


Test statistic: absolute value of Pearson's R
We chose the absolute value of Pearson's R because we want to see how strong of a correlation there is between the average recipe rating and the amount of soduium in each recipe. We take the absolute value because we want to see if there is any relationship between the two columns, not if there is a negative or positive relationship present. 

We end up with an R value of 0.006323716062416152, and a p-value of 0.045529470241813606. With significance level alpha=0.05, we fail to reject the null in favor of the alternate, where there is a correlation between the average recipe rating and the amount of sodium in each individual recipe. 

## Framing a Prediction Problem
We want to predict the rating for a reicpe based on its features. To do this, we will be performing a multi-class classification as we are predicting whether the recipe will a 0 star, 1 star, 2 star, 3 star, 4 star, or 5 star recipe. 
Our response variable is the rating of the recipe. We chose this because rating represents the likeability of the recipe which is aligned with the goals of our prediction problem and our data exploration. 
We will only use features of the dataset that are available at the time of our prediction. These are features that are known before someone has tried the recipe such as the number of ingredients, number of steps, nutrition facts (calories, sodium, carbohydrates, etc.), and description. We will not use review in our model training as that is that information that we would know before a user has tried the recipe. 
The metric we chose was F1-score as opposed to accuracy because when looking at our dataset, there is an imbalance between the number of recipes that have a 4 or 5 star rating compared to recipes that receive a 1 or 2 star rating. Therefore, if we were to use accuracy as our metric, a model that predicts that every recipe was 5 star could recieve high accuracy score, but it would be less useful than if we were to use the F1-score


## Baseline Model
For our baseline model, we used a RandomForestClassifier. The quantitative variables we used were the recipe's nutrition facts: calories, total fat, sugar, sodium, protein, saturated fat, carbohydrates. For the quantitative variables, we used the StandardScaler to make all the values standardized. At this stage, we do not think our model is good yet because its very basic. Every recipe consists of many features such as the amount of time it takes to prepare and the ingredients that are needed which can be helpful in predicting rating, but we are only looking at the nutrition facts.   


## Final Model


## Fairness Analysis