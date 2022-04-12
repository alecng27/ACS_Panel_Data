# Instructions

This readme describes the details of this project. Read it carefully and ask Prof. Lhost if you have any questions.

In this project you are exploring 2020 US Presidential Election results at the county level, together with county-level demographic data obtained from the 2019 ACS 5-Year via the tidycensus package. For the demographic variables, you will explore 4 categories of variables, with 2 specific variables in each category. Here are some possible categories (and variables in the category): race (e.g., % Black, % White), ethnicity (e.g., % Hispanic), birthplace (e.g., % native born, % foreign born), language (e.g., % with English as primary language, % with Spanish as primary language), economic (e.g., income, housing values, % in poverty), employment (e.g., % unemployed), education (e.g., % without high school degree, % with college or higher), age (e.g., % under 18, % under 40, % over 65), sex (e.g., % female), or others. You don't have to use these categories exactly. Explore the data and find others if you want. You can combine categories I listed, for example, combining Race and Ethnicity. But make sure your variables represent/measure four fairly distinct areas (so, don't just pick 8 variables from one area, e.g., % born in Estonia, % born in Latvia, % born in Lithuania, ...). 

How should you pick variables? Look at the data and pick what you think seems interesting. Once you get going with this, it's easy to select different variables and map them to see what looks like it has interesting variation and graph them to see what looks like it correlates with the election outcomes. 

Note that when you first look at the list of available variables (from running `v19 <- load_variables(2019, "acs5", cache = TRUE)`), it will likely be confusing. Often the data is available with numerator and denominator, from which you can calculate percentages. For example,  row 1 says "Estimate!!Total" and row 2 says "Estimate!!Total:!!Male". To calculate percent male, you'd divide Estimate!!Total:!!Male by Estimate!!Total. If instead you wanted percent female, you'd go down to row 26 where it says "Estimate!!Total:!!Female" and use that as the denominator. The next row you see "Estimate!!Total" is the denominator of the next set of estimates (row 50 starts Sex by Age for White alone...the first 49 rows were all for Sex by Age for all races). You might want to use look at the pre-prepared tables on the [Census Bureau website](https://data.census.gov/cedsci/) to compare what you get with what they report to make sure you're getting the data you intend to get. 

For regressions and scatter plots, make sure all percentages are expressed from 0 to 100, not from 0 to 1. That way a 1 unit increase is a 1 percentage point increase (e.g., from 43% to 44%), not a 100% increase (e.g., from 0.43 to 1.43).

For this project, display all of your code in your HTML output (i.e., the `echo=TRUE` code chunk option), as well as the other things you're asked to display below. For the other two projects (PP and RP), you will not display your code in your output, but for this project you should. 



## Due date

**Due: Monday, February 15 by 11:59pm Central/Appleton time**

Because you are working in GitHub, you do not need to do anything to submit your CP. I'll just look at your repo (the GitHub Pages HTML output and your code) after this deadline. The date/time of your last commit will be considered the submission date/time, so make sure not to make any changes after the deadline. Late projects will be penalized 5% per day.



# Here are the details of what should go in each file:

There are placeholders in the files, but make sure to read the complete instructions here.


## index.Rmd

`index.Rmd` provides the terms of the project, asks you to acknowledge all help received, and asks you to reaffirm the LU Honor Code. Your work will not be accepted without this. 



## 01-Data.Rmd

This bookdown project uses the `new_session: false` option, meaning bookdown combines all your RMD files into a single RMD file before knitting. That means that later RMD files can use R objects created in earlier RMD files. This means you can create your data in the first file (01-Data.Rmd) and then use it in later RMD files. So, that's what you should do. Specifically, in this file (01-Data.Rmd) you should download and prepare 2 datasets:

**Dataset 1:**

The first dataset is for use in making the maps. You'll want to use the "Map Examples" R Project posted in Moodle. You can use my code for the GIS data used to make the maps, as well as the election data. You need to download 8 other variables from the 2019 5-year ACS (not county population, the variable I downloaded in the "Map Examples") and join/merge them to the dataset. You can drop Alaska and Hawaii as I did for the maps in Map Examples (and also make sure not to include Puerto Rico). 

**Dataset 2:**

The second dataset is for use with the scatter plots and regressions. The `ms_simplify` step that simplifies the GIS data seems to drop more counties than should be dropped. So just repeat the same process of downloading the county-level data from tidycensus, just with `geometry = FALSE`, and merge your census data with the the election data in the same way you did for the mapping data. You'll need to drop Alaska and Puerto Rico (but you can keep Hawaii). There's several ways to do this (I added a note in Map Examples about how you can create the 2-character state FIPS (stFIPS) by separating the 5-character GEOID, or you can do it with your joins), just make sure you have the right number of counties when you're finished (how do you know if you have the right number? Look at the data...most people don't know how many counties there are, so you have to look at the data to make sure you're doing what you mean to be doing)

**Summary Statistics:**
At the bottom of this file ("01-Data.Rmd""), display summary statistics for the election results (display pctGOP and totalVotes) and your 8 ACS variables. Use your second dataset (the one you use for the scatter plots and regressions). Make sure you have the correct number of observations for each variable and nothing looks strange. Use a stargazer table for this as shown in the BP chapter "14-ch3-MLR.Rmd". If you find that the average age in a county is 4 or -17, that should stand out to you as wrong. You always want to look at summary statistics to help catch errors (some errors won't show up in summary statistics). It's also important in empirical work to share summary statistics for readers/your audience. 



## 02-ElectionMap.Rmd

Display a map of the election results. Choose the color pallet that you believe best displays the data. Look at the examples I gave you in "Map Examples".




## 03-Category1.Rmd

In a sentence or two, describe this category and the two variables that are part of the category. We need to know what variables you're including (and for the purposes of grading you, I need to know that the variables you work with are actually what you think they are...if you, for example, say you're working with median household income and you're actually working with the margin of error for the percentage of people born in Armenia, it will negatively affect your grade.). These sentences should be in your own words. Don't just copy directly from documentation. But obviously some phrases will obviously be the same (e.g., don't try to put "Median Family Income" into your own words...that's just what it's called). 

### Category 1 variable 1

Map of category 1 variable 1

Scatter Plot of category 1 variable 1 with SLR regression line

SLR regression of category 1 variable 1 (x) and pctGOP (y) with output displayed via Pander as demonstrated in BP "13-ch2-SLR.Rmd"

Make sure that the map uses a color pallet (and scale or categories) that does a good job of showing the data. Make sure everything is labeled clearly and correctly. You don't need to describe the map, scatter plot, or regression. However, make sure that you could if I asked you to (e.g., if I meet with your group and ask anyone in your group to explain it, you should be able to).  

### Category 1 variable 2

Same as for category 1 variable 1, except for the second variable from this category. Note that this bookdown project uses the option `split_by: section`, which means each chapter section (that's the two ##) will be saved in a separate HTML file. This means each HTML file will only have 1 map in it, making each HTML file smaller, which typically works better with Git/GitHub. 




## 04-Category2.Rmd

Same as "03-Category1.RMD" except for category 2


## 05-Category3.Rmd

Same as "03-Category1.RMD" except for category 3



## 06-Category4.Rmd

Same as "03-Category1.RMD" except for category 4



## 07-Regressions.Rmd

Run 4 MLR regressions and display the results in a stargazer table (just like in BP chapter "14-ch3-MLR.Rmd"). Model 1 should have "variable 1" from each of the 4 categories. Model 2 should have "variable 2" from each of the 4 categories. (So keep this in mind when you choose which is variable 1 and which is variable 2 in the categories.) Models 3 and 4 can be any combination of variables you'd like to include. Try to choose models that have interesting results. 

In a few sentences, explain why we should most likely not interpret any of the results as causal (i.e., we shouldn't interpret a particular coefficient as representing how the percent voting GOP in a county is caused by an increase in that explanatory variable). 

Beyond those few sentences, you do not need to write anything else. You do not need to interpret the coefficients or explain the results. You'll focus on explaining results in the remaining two projects. For this project, I only want you to write an answer 
