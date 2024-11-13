---
layout: post
title:  "House Hunters: Webscraping Edition"
date:   2024-11-03
description: Buying a house is no easy task! With hundreds of houses available, it becomes difficult to sift through all the many options. But with just a few lines of code we can turn overwhelming pages of data into a clean, curated data set of housing information!
image: "/assets/img/househeader.png"
display_image: false  # change this to true to display the image below the banner 
---

<p class="intro"><span class="dropcap">W</span>hen I get bored, online shopping is a common hobby, and house shopping has become a recent favorite. My husband and I want to buy a house once we graduate so we like to look at the options that are available in the region. The problem: about 95% of the houses we scroll through are way out of our budget or not what we are looking for. As an aspiring data scientist, the obvious solution to any problem is code! This post will dive into scraping and cleaning housing data to better understand the housing market in the region.</p>

## Goals of the Webscraper
As a first-time prospective home buyer, one of the biggest questions we have is knowing if the house is really worth what it says it is. Luckily, with the webscraper we are going to build, we will be able to create a data frame that filters to houses in our price range and calculate the average square footage and common features of the houses in this range.

## Building the Webscraper
Extracting data from websites can be done in multiple ways, such as APIs and Python packages such as `BeautifulSoup`. In any case, it is very important to extract the data in a way that is ethical and follows the guidelines of the website. For the purpose of this project, I found that [Redfin](https://www.redfin.com/county/2918/UT/Utah-County) was the easiest and most accessible website to collect data. 

### Steps to Collect Data
1. **Identify best method to extract your data**. In the case of Redfin, I first looked at the options to use an API but the APIs available did not have the data I was looking for. Because of this, I decided to use the `Selenium` package in Python to scrape the Redfin website using a web driver. The robots.txt file specified that county housing data was available to scrape for non-commercial use. 

2. **Identify the container with the housing data**. As seen below, Redfin's website has a section of the website that contains a list of all the houses, this section is called a *container*. When webscraping in `Selenium`, you first need to identify the container where all of your data is located. Within this larger container, Redfin also uses containers to group each listing together. Identifying these containers sets us up to easily locate all the data we want to scrape from Redfin.

    <figure>
    <img src="{{site.url}}/{{site.baseurl}}/assets/img/house_screenshot.jpg" alt="Figure" style="width:600px;"/>
    <figcaption>
        <a href="https://www.redfin.com/county/2918/UT/Utah-County">Source</a>
    </figcaption>
    </figure>

3. **Identify the elements that will be extracted**. Within each container, there are elements associated with the information that we want to extract about each home. In fact, for this dataset all the elements we need to extract fall under the *bp-Homecard__Stats* class. Navigate to this class in your inspector and you will easily find the elements you are looking for! In my analysis, I wanted price, beds and baths, square footage, and the address.

4. **Use a for loop to extract elements from every container and page.** Once we have identified the elements we want to extract, if we don't use a for loop, our code will only scrape the first element it finds. Instead, we need code that will extract elements from each container. Additionally, Redfin's data is stored on multiple pages, so we need to add code that will allow our web driver to access each page and scrape the data. Below is code for a for loop that can be used to scrape the data. This data can be appended to lists and then made into a data frame. For access to my entire code, click [here](https://github.com/wilcobry/Post_2_data).
{%- highlight python -%}
prices = []
current_page = 1
pagination = driver.find_element(By.CLASS_NAME, 'PageNumbers')
last_page = pagination.find_elements(By.CLASS_NAME, 'ButtonLabel')[-1].text
while current_page <= int(last_page):
    container = driver.find_element(By.CLASS_NAME, 'HomeCardsContainer')
    all_homes = container.find_elements(By.CLASS_NAME, 'HomeCardContainer')
    for home in all_homes:
        try:
            price = home.find_element(By.CLASS_NAME, 'bp-Homecard__Price--value').text
        except:
            price = None
        prices.append(price)
    try:
        next_button = driver.find_element(By.CSS_SELECTOR, '.PageArrow__direction--next')
        next_button.click()
        current_page += 1
        time.sleep(2)
    except:
        pass
{%- endhighlight -%}

Once our data has been scraped and read into a dataframe, it is important to clean your data. 
In the dataframe I created from Redfin, I removed NA values in the `Price` column and used 
regular expressions to extract float values from `Price`, `Sq_Footage`, `Beds`, and `Baths`, 
and to extract the city and zipcode from the `Address` column. For more information regarding regular expresssions, click [here](https://www.regular-expressions.info).
{% include small_table.html %}

### Analyzing the Data
 Now that our data is clean and ready to go, it is time to go house hunting! I first wanted to understand how median home prices compared between the different cities in Utah County to get an idea of where affordable homes are located. 
 <img src="{{site.url}}/{{site.baseurl}}/assets/img/medianhouse.png"/>
* From the barplot we can clearly see that median home prices in Alpine and Woodland Hills are significanly more expensive than other cities. For our budget, this graph tells us that we should focus our house search in Vineyard and can afford up to about Pleasant Grove.

Next, to get an idea of the square footage of houses in our price range, I filtered the data down to prices below $400,000 and created a dot plot of home price by the square footage. 
 <img src="{{site.url}}/{{site.baseurl}}/assets/img/regression_plot2.png"/>
* From our plot it looks like, in general, as square footage increases, prices increase as well-- which definitely makes sense. Within our budget, this graph tells us that that most houses are going to be between 1000 and 2000 square feet. 

### Closing Time
After scraping Redfin and making a few plots, we now have a much better idea of where we should narrow our house search and what we can afford! Webscraping can be a little intimidating at first, but with a little bit of practice, the options become endless! This tutorial can be applied to your own personal house hunt or really any shopping experience (as long as you are ethically scraping of course). Can't decide what to get your family for Christmas? Scrape your favorite website and find the products in your price range! Drop in the comments what you are going to do with your new-found webscraping power. Happy coding!

