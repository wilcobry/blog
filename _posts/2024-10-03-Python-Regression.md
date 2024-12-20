---
layout: post
title:  "Regression: The Python Way"
date:   2024-10-03
description: Expanding the limits of linear regression from the confines R code to explore the possibilites of regresssion and statistical analysis in Python. 
image: "/assets/img/Newphoto.jpg"
display_image: false  # change this to true to display the image below the banner 
---

<p class="intro"><span class="dropcap">A</span>s a dedicated R and Rstudio user, this post is an experiment in leaving the comfort of one's default language to understand how a linear regression analysis can be performed in Python. Being proficient in multiple statistical languages is a key skill for one's career, making the intitial struggle always worth it.</p>

### Why Learn Linear Regression? 
Linear regression is one of the most widely used techniques for predicting and modeling relationships between variables. Linear regression is not only restricted to the field of statistics but is widely used in finance, economics, and across the sciences due to the ease of interpreting results. Additionally, regression is not a difficult skill to master once you learn the important assumptions that are required! 

<figure>
  <img src="{{site.url}}/{{site.baseurl}}/assets/img/niceregressionphoto.jpg" alt="Figure" />
  <figcaption>
    <a href="https://www.linkedin.com/learning/sas-essential-training-2-regression-analysis-for-healthcare-research/basic-proc-logistic-output?u=2153100">Source</a>
  </figcaption>
</figure>

### R vs. Python
I think it is a rare occurance to come accross a data scientist who does not have a strong opinion regarding their favorite statistical language. So the question is, is R or Python better? The good news, that is up to you! But it is always good to be informed before you draw conclusions, so let's highlight a few key differences between the two languages to help you decide which path you would like to take when performing your own linear regression analysis. 

#### R
R is a language created for statistical analysis. Because of this, the language has an unmatched depth of libraries and functionalities to help you achieve the perfect statistical analysis. 

<figure>
  <img src="{{site.url}}/{{site.baseurl}}/assets/img/r.png" alt="" style="width:100px;"/>
  <figcaption>
    <a href="https://en.wikipedia.org/wiki/R_%28programming_language%29">Source</a>
  </figcaption>
</figure>

#### Python
Python, on the other hand, is the perfect multi-purpose tool. If R is the master, Python is the jack-of-all-trades. While statistical analysis may not be Python's default funcionality, the breadth of the program allows for seamless connections between multiple coding projects. 

<figure>
  <img src="{{site.url}}/{{site.baseurl}}/assets/img/python.png" alt="Python logo" style="width:100px;" />
  <figcaption>
    <a href="https://en.wikipedia.org/wiki/Python_%28programming_language%29">Source</a>
  </figcaption>
</figure>

### Python Packages for Linear Regression
1. 
`Numpy` is a package that is a very powerful scientific and mathematical tool. One of the main purposes of this library is to work with arrays. We can use arrays and the `np.linalg.inv()` function to calculate our beta coefficients of the regression. 

2. 
`Scikit-learn` is a widely used package great for machine learning. Because of this, this package is great for data analysis, specifically linear regression. The package provides straight forward functions that make regression simple and seamless. In `scikit-learn` we will first use numpy to create arrawy of our data and then use the `LinearRegression()` function to create a linear regression model. 

3. 
As the name suggests, `statsmodels` is a package devoted to statistical analysis. This package most closely follows the syntax and style of and R-code regression. Because of the similarity to R, this package offers various tools to check assumptions before running our linear regression model.


### Running a Regression
Without diving deep into the theory behind linear regression (we will save that for another post), we will focus on a simple linear regression model with only one independent variable. Now... let's actually code up our regression model in Python!

#### 1. Import Necessary Libraries
{%- highlight python -%}
import pandas as pd
import statsmodels.api as sm
{%- endhighlight -%}
`Pandas` will be used to pull in our data frame and `statmodels` is the package we will use to run our simple linear regression.
#### 2. Read in Dataset
{%- highlight python -%}
df = pd.read_csv('Data/Salary_dataset.csv')
df = df.drop(df.columns[0], axis=1)
print(df.head())
{%- endhighlight -%}
{% include kaggle_table.html %}
For our analysis, we will use a dataset from [kaggle](https://www.kaggle.com/datasets/abhishek14398/salary-dataset-simple-linear-regression) that provides the salary and years of experience for 29 different people. We are looking to analyze the relationship between these two variables in our analysis-- specifically, how years of experience effects one's salary. 
#### 3. Identify our Independent and Dependent Variable
{%- highlight python -%}
experience = df['YearsExperience']
salary = df['Salary']
experience = sm.add_constant(experience)
{%- endhighlight -%}
In this analysis, experience is our independent variable and salary is the dependent variable. A scatterplot shows us an initial relationship between our independent variable, years of experience, and our dependent variable, salary.
 
<img src="{{site.url}}/{{site.baseurl}}/assets/img/scatterplot.png"/>
#### 4. Run Regression Model
{%- highlight python -%}
model = sm.OLS(salary, experience)
results = model.fit()
{%- endhighlight -%}
The function `sm.OLS()` is using an ordinary least squares statistical model to run the regression model. OLS is a standard regression tool when dealing with simple linear regression.
#### 5. Interpret the results
{% include regression_string1.html %}

One of the most important parts of linear regression is being able to interpret the results of your model. As seen in just a few short steps, actually running a linear regression model is not all that difficult! The difficulty lies in being able to take the results of the analysis and actually draw data-driven conclusions. Two of the most important indicators to determine how years of experience is associated with salary will be our R-squared coefficient and our p-value. 
    
**R-squared** measures the proportion of variance in the dependent variable that can be explained by the independed variable. In this case, 95.7% of the variation in salary can be explained by years of experience.

Our **p-value** tells us probability of observing the data that we did or data more extreme, given that there is no association between our dependent and our independent variable. In this case, there is a probability of close to 0 that years of experience is not associated with salary, given the data we observed. 

### So what now?
In just a few short minutes we have gone through the process of learning simple linear regression in Python! This code will be easily applicable to any simple linear regression analysis you have, but as mentioned earlier, we did not dive into the ins and outs of checking assumptions and the process behind multi linear regression. As you learn regression theory and set up the correct analysis, this code will still be a very useful tool. 

Drop a comment below and let me know what you think of the code and if you have any questions. Happy coding!


    



