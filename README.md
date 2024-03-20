# Recipe-Data-Exploration

This project is for DSC80 at UCSD. 
by Amelia Lei and Kyra Deng

---

## Introduction

The world of cooking has taken a change as people start to take on fast-paced lifestyles. Thus, people resort to quicker at-home-recipes, or eating out, both which may take a toll on one's health. To see if people truly suffer from unhealthy meals, we investigate the correlation between sodium levels in a recipe to quick and easy recipes, recipes that take 30 minutes or under to complete. 

The first dataset we are given contains information for 83782 recipes, and comes from food.com. It contains 10 columns, with the descriptions below. 

The second dataset we are given contains people's ratings on the recipes and also comes from food.com. It contains 5 columns, and has 731,927 total reviews. 

## Data Cleaning and Exploratory Data Analysis

Before conducting any analysis, we first merged the two datasets together to have one cohesive dataset to work with. The two dataframes have one column in common; the "id" and "recipe_id" columns. We merge on those columns and drop the "recipe_id" column. 