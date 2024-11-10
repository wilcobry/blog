---
layout: post
title:  "House Hunters: Webscraping Edition"
date:   2024-11-03
description: Buying a house is no easy task! With hundreds of houses available, it becomes difficult to sift through all the many options. But with just a few lines of code we can turn overwhelming pages of data into a clean, curated data set of housing information!
image: "/assets/img/house_pic.png"
display_image: false  # change this to true to display the image below the banner 
---

<p class="intro"><span class="dropcap">W</span>hen I get bored, online shopping is a common hobby -- and house shopping has become a recent favorite. My husband and I want to buy a house once we graduate so we like to look at the options that are available in the region. The problem: about 95% of the houses we scroll through are way out of our budget or not what we are looking for. As an aspiring data scientist, the obvious solution to any problem is code! This post will dive into scraping and cleaning housing data to better understand the housing market in the region.</p>

## Goals of the Webscraper
As a first-time prospective home buyer, one of the biggest questions we have is knowing if the house is really worth what it says it is. Luckily, with the webscraper we are going to build, we will be able to create a data frame that filters to houses in our price range and calculate the average square footage and common features of the houses in this range.

## Building the Webscraper
Extracting data from websites can be done in multiple ways, such as APIs and Python packages such as `BeautifulSoup`. In any case, it is very important to extract the data in a way that is ethical and follows the guidelines of the website. For the purpose of this project, I found that redfin.com was the easiest and most accessible website to collect data. 

### Steps to Collect Data
1. **Identify best method to extract your data**. In the case of Redfin, I first looked at the options to use an API but the APIs available did not have the data I was looking for. Because of this, I decided to use the `Selenium` package in Python to scrape the Redfin website using a web driver. The robots.txt file specified that county housing data was available to scrape. 

2. **Identify the container with the housing data**. As seen below, Redfin's website has a section of the website that contains a list of all the houses, this section is called a *container*. When webscraping in `Selenium`, you first need to identify the container where all of your data is located. Within this larger container, Redfin also uses containers to group each listing together. Identifying these containers sets us up to easily locate all the data we want to scrape from Redfin.

<figure>
  <img src="{{site.url}}/{{site.baseurl}}/assets/img/house_screenshot.jpg" alt="Figure" style="width:400px;"/>
  <figcaption>
    <a href="https://www.redfin.com/county/2918/UT/Utah-County">Source</a>
  </figcaption>
</figure>

3. **Identify the elements that will be extracted**. Within each container, there are elements associated with the information that we want to extract about each home. In fact, for this dataset all the elements we need to extract fall under the *bp-Homecard__Stats* class. Navigate to this class in your inspector and you will easily find the elements you are looking for! In my analysis, I wanted price, beds and baths, square footage, and the address.

4. 