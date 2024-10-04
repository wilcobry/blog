---
layout: post
title:  "Regression: The Python Way"
date:   2024-10-03
description: Expanding the limits of linear regression from the confines R code to explore the possibilites of regresssion and statistical analysis in Python. 
image: "/assets/img/regression1.jpg"
display_image: false  # change this to true to display the image below the banner 
---

<p class="intro"><span class="dropcap">A</span>s a dedicated R and Rstudio user, this post is an experiment in leaving the comfort of one's default language to understand how a linear regression analysis can be performed in Python. Being proficient in multiple statistical languages is a key skill for one's career, making the intitial struggle always worth it.</p>

### Why Learn Linear Regression? 
Linear regression is one of the most widely used techniques for predicting and modeling relationships between variables. Linear regression is not only restricted to the field of statistics but is widely used in finance, economics, and across the sciences due to the ease of interpreting results. Additionally, regression is not a difficult skill to master once you learn the important assumptions that are required! 

![Figure]({{site.url}}/{{site.baseurl}}/assets/img/niceregressionphoto.jpg)

### R vs. Python
I think it is a rare occurance to come accross a data scientist who does not have a strong opinion regarding their favorite statistical language. So the question is, is R or Python better? The good news, that is up to you! But it is always good to be informed before you draw conclusions, so let's highlight a few key differences between the two languages to help you decide which path you would like to take when performing your own linear regression analysis. 

#### R
R is a language created for statistical analysis. Because of this, the language has an unmatched depth of libraries and functionalities to help you achieve the perfect statistical analysis. 

#### Python
Python, on the other hand, is the perfect multi-purpose tool. If R is the master, Python is the jack-of-all-trades. While statistical analysis may not be Python's default funcionality, the breadth of the program allows for seamless connections between multiple coding projects. 


### Python Packages for Linear Regression
1.
`Numpy` is a package that is a very powerful scientific and mathematical tool. One of the main purposes of this library is to work with arrays. We can use arrays and the `np.linalg.inv()` function to calculate our beta coefficients of the regression. 

2. 
`Scikit-learn` is a widely used package great for machine learning. Because of this, this package is great for data analysis, specifically linear regression. The package provides straight forward functions that make regression simple and seamless. In `scikit-learn` we will first use numpy to create arrawy of our data and then use the `LinearRegression()` function to create a linear regression model. 

3.
As the name suggests, `statsmodels` is a package devoted to statistical analysis. This package most closely follows the syntax and style of and R-code regression. Because of the similarity to R, this package offers various tools to check assumptions before running our linear regression model.


### Running a Regression
Without diving deep into the theory behind linear regression (we will save that for another post), we will focus on a simple linear regression model with only one independent varialbe. Now... let's actually code up our regression model in Python!

1. Import Necessary Libraries
{%- highlight python -%}
import pandas as pd
import statsmodels.api as sm
{%- endhighlight -%}
`Pandas` will be used to pull in our data frame and `statmodels` is the package we will use to run our simple linear regression.

2. Read in Dataset
{%- highlight python -%}
df = pd.read_csv('Data/Salary_dataset.csv')
df = df.drop(df.columns[0], axis=1)
print(df.head())
{%- endhighlight -%}
For our analysis, we will use a dataset from kaggle that provides the salary and years of experience for 29 different people. We are looking to analyze the relationship between these two variables in our analysis-- specifically, how years of experience effects one's salary. 

3. Identify our Independent and Dependent Variable
{%- highlight python -%}
experience = df['YearsExperience']
salary = df['Salary']

experience = sm.add_constant(experience)
{%- endhighlight -%}
In this analysis, experience is our independent variable and salary is the dependent variable. 

4. Run Regression Model
{%- highlight python -%}
model = sm.OLS(salary, experience)
results = model.fit()
{%- endhighlight -%}
The function `sm.OLS()` is using an ordinary least squares statistical model to run the regression model. OLS is a standard regression tool when dealing with simple linear regression.

5. Interpret the results
{%- highlight python -%}
print(results.summary())
{%- endhighlight -%}
One of the most important parts of linear regression is being able to interpret the results of your model. As seen in just a few short steps, actually running a linear regression model is not all that difficult! The difficulty lies in being able to see the results of the analysis and actually draw data-driven conclusions. 



