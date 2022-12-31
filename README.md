# Sentiment Analysis and Topic Modeling of Meta Quest 2 Product Reviews

<h3 align="center">
  Abstract
</h3>
<p>This study aims to analyze the sentiment and identify the main topics discussed in Meta Quest 2 product reviews scraped from the Argos website using Selenium. To achieve this goal, we first preprocessed the reviews by removing unwanted characters and applying text normalization techniques. Then, we applied sentiment analysis using a machine learning classifier to classify the reviews into positive, negative, and neutral categories. Finally, we used topic modeling to identify the main themes discussed in the reviews. The results of the sentiment analysis showed that a majority of the reviews were positive, while the topic modeling revealed that the main topics discussed included battery life, fun and overall satisfaction. the results are visualized using word clouds and line charts. The insights gained from this analysis can potentially be useful for understanding customer opinions and preferences, as well as identifying potential issues or areas for improvement in the product.
</p>



## 1.Introduction
<p> Virtual reality (VR) headsets have become increasingly popular in recent years, offering a new level of immersion and interactivity for gaming, entertainment, education and even socializing. As the VR industry continues to grow, it is important for companies to understand the sentiment and concerns of their customers in order to improve the user experience and stay competitive in the market [1]. With the emergence of the metaverse, a virtual world that is accessed through the internet and where people can interact with each other and virtual objects, it is even more crucial for businesses to understand the sentiment and topics being discussed by VR headset users. </p>
<p>
the Meta (Oculus) Quest 2 offers a good value for its price [2] and has a large selection of available content. By analyzing the sentiment and identifying the main topics discussed in reviews of the Meta Quest 2, businesses and developers can gain insights into customer opinions and preferences, as well as identify potential areas for improvement in the product. The Meta Quest 2's wide selection of content and versatility in terms of use make it an ideal subject for such analysis.
</p>

### 1.1.Context
<p>
Sentiment analysis (also known as opinion mining or emotion AI) is the use of natural language processing, text analysis, computational linguistics, and biometrics to systematically identify, extract, quantify, and study affective states and subjective information [3]. This allows us to understand the emotional tone and sentiment expressed in the text by classifying the text into positive or negative or neutral. which is why Sentiment analysis uses supervised machine learning approach.
</p>
<p>
Topic modeling is an unsupervised machine learning approach for identifying and extracting the most important themes or topics from a collection of texts. It is a crucial aspect of natural language processing (NLP) as it allows us to identify and analyze the most relevant information contained in a large corpus of text. By reducing the number of features (i.e., words) that we need to consider, we can focus our attention on the most meaningful and relevant content, rather than being overwhelmed by the sheer volume of data [4]. This enables us to more effectively analyze and understand the underlying themes and concepts contained in the texts.  
</p>



### 1.2.Aims and objectives
The main aim of this notebook, is to analyze the sentiment of the reviews and identify the main topics discussed in Meta Quest 2 product reviews scraped from the Argos website with the help of visualizations

#### 1.2.1.Methodology
- Scrape product reviews from the Argos website.
- Preprocess the data by cleaning and standardizing it for further analysis.
- Perform sentiment analysis on the reviews to determine the overall sentiment expressed in each review.
- Identify the main topics discussed in the reviews using topic modeling.
- Analyze the reviews for each identified topic to gain insights into the specific issues or aspects that are being discussed.
- Break down the sentiment analysis results by topic to understand how the sentiment varies across different topics.
- Extract relevant keywords from the reviews to further understand the specific aspects or features that are being discussed.
- Communicate the findings effectively through the use of visualization techniques such as bar charts and wordclouds.


#### 1.2.2.Asking the Questions that will guide us through our Analysis
- What are some common themes that emerge across the different topics? Are there any trends or patterns in customer sentiment that stand out?
- Is there a relationship between the sentiment of the reviews and the topics discussed?
- How can the insights gained from this analysis be used to improve the product or the customer experience?



### 1.3.Dataset
For the purpose of this project, I chose to utilize the Selenium web scraping library to obtain a dataset of reviews for the Meta Quest 2 virtual reality headset from the Argos website, a leading retailer in the United Kingdom. I chose to use Selenium library due to its ability to handle dynamic websites (website that generates content on the fly using server-side programming languages) which will be needed for scraping the reviews 

#### 1.3.1.Dataset:
- Source: Scraped from Argos website
- Size: 1310 records, 4 columns
- Variables:
  - `title`: Title of the product being reviewed
  - `reviews`: Text of the review
  - `location`: Location of the reviewer
  - `timestamp`: Date and time of the review submission
- Format: CSV flat file
- Scraping:
  - `reviews_list` and `timestamp` were first scraped from the Argos website.
  - `reviews_list` contains the title, review, and location for each review, in that order.
  - `timestamp` contains the datetime of the review.
  - Data was then stored in two lists (`reviews_list` and `timestamp`) locally using pickle.
- Preprocessing:
  - `reviews_list` and `timestamp` were merged into a dictionary.
  - The dataset was labeled.
  - The labeled dataset was then stored locally as a CSV file.
  - Minor formatting issues corrected.
  - Datetime formatting was applied to the `timestamp` column.
  - Text preprocessing was performed on the `title`, `reviews`, and `location` columns.
  
#### 1.3.2.Limitations
- We limited the data used in this study to reviews from the Argos website for a single VR headset. This means that the results may not be representative of the broader market for VR products or of other VR headsets. We must consider this limitation when interpreting the results of the study.
- The Argos website is only available in the United Kingdom. This means that the results of the analysis may not be representative of the broader market for VR products outside of the UK. Reviews on Argos may differ in terms of content, sentiment, and other characteristics from reviews on other websites or platforms in different regions or countries. Therefore, we must consider this when interpreting the results of the study, and be mindful of the potential for bias in the data due to the limited geographical scope.
- The results of the topic modeling may be influenced by the choice of modeling algorithm and the number of topics selected. Different choices may lead to slightly different results.




### 1.4.Ethical considerations 
- According to the website terms and conditions of Argos, scraping data for non-commercial purposes is permitted. This means that individuals or organizations may use web scraping techniques to extract data from the Argos website for research or personal use, as long as the data is not being used for commercial gain. [5]
- According to the website terms and condition of Argos, it is legal to use data that is publicly available, provided that it is used ethically and in accordance with the terms and conditions of the website. [5]  
- According to the information contained in the robots.txt file of the Argos website, it does not appear that scraping reviews is explicitly disallowed. [6]





### 1.5.Dependencies

The following code will create a text file called requirements.txt that lists all the dependencies needed for this notebook


```python
!pip freeze > requirements.txt
```

use ` pip install -r requirements.txt ` to install all the packages and versions listed in the requirements.txt


```python
# pip install -r requirements
```

## 2.Extracting Product Reviews from the Web with Selenium
<p>
 Web scraping is the process of extracting data from websites by using automated tools or programs. It is a useful technique for collecting large amounts of data from websites, especially when the data is not readily available for download. In this study, we used Selenium, a popular web automation tool, to scrape product reviews from the Argos website. </p>
<p>
Selenium is an open-source library that allows developers to write scripts in various programming languages to automate web browser interactions. It can simulate user actions such as clicking links, filling out forms, and navigating pages, and it can extract data from the web pages by using techniques such as web element selection, DOM parsing, and XPath queries. [7] </p>

<p> For our study, we use Selenium to navigate to the product page of Meta Quest 2 VR on the Argos website and retrieve the reviews, location of the reviewer, and timestamp of the review. We write code that uses the Selenium webdriver to open a web browser, navigate to the product page, and extract the data from the page elements. We also implement error handling and retry logic to ensure that the script can handle any issues that might arise during the scraping process, such as network errors or changes in the page structure. Here's the explanation in a procedural way
</p>    
<ol>
    <li>The Chrome web driver opens and navigates to the specified URL.</li>
    <li>The cookie consent prompt is clicked to accept cookies.</li>
    <li>The <code>reviews</code> button is clicked to navigate to the reviews section of the page.</li>
    <li>The code iterates through each page of reviews:
        <ol>
            <li>The code tries to locate the 'show more' button using the first specified XPATH. If the button is not found within the specified time, the TimeoutError exception is caught.</li>
            <li>If the TimeoutError exception is caught, the code tries to locate the 'show more' button using the second specified XPATH. If the button is not found within the specified time, the TimeoutError exception is caught and a message is printed.</li>
            <li>If the 'show more' button is found, it is clicked.</li>
        </ol>
        </li>
    <li>The reviews section of the page is located and stored in a variable.</li>
    <li>All <code>p</code> tags within the reviews section are found and stored in a list called <code>reviews.</code></li>
    <li>All <code>time</code> tags within the reviews section are found and stored in a list called <code>scraped_timestamps</code>.</li>
    <li>The code iterates through the "reviews" list and appends the text of each element to a new list called <code>reviews_list</code>.</li>
    <li>The code iterates through the ´scraped_timestamps´ list and appends the datetime attribute of each element to a new list called <code>timestamps</code>.</li>
    <li>The web driver browser closes.</li>
    <li>The <code>reviews_list</code> and <code>timestamps</code> lists are returned.</li>
</ol>

<code>note that it can take up to 5 to 10 minutes depending on max pages input has been selected to finish scraping.<code>


```python
# import selenium library and webdriver modules
import selenium
from selenium import webdriver

# import By class and Options class from selenium.webdriver.
# By is used to specify which elements on the page to locate,
# Options is used to set options for the Chrome web browser.
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.options import Options

# import NoSuchElementException from selenium.common.exceptions for error handling.
from selenium.common.exceptions import NoSuchElementException

# import WebDriverWait and expected_conditions from selenium.webdriver.support
# WebDriverWait is used to wait for elements to load on the page,
# expected_conditions is used to define conditions for waiting for elements to load on the page
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC


def scrape_reviews(url, maxPages):
    import time
    driver = webdriver.Chrome()
    driver.get(url)
    print(driver.title)

    # press cookies button
    cookie = driver.find_element(By.ID, 'consent_prompt_submit')
    cookie.click()

    # opens the review section
    reviewsBtn = driver.find_element(By.ID, 'reviews')
    reviewsBtn.click()
    
    currentPage = 1
    while currentPage <= maxPages:
        time.sleep(1)
        # stores the path of show more button
        btn_XPATH = '//*[@id="reviews-accordion-accordion-content-reviews-accordion"]/div/div/div/div[2]/div[2]/span[' + str(currentPage) + '1]/button'
        # print(btn_XPATH)

        # define the maximum amount of time to wait
        wait_time = 10

        # try to locate the show more button using the By XPATH
        try:
            showBtn = WebDriverWait(driver, wait_time).until(
                EC.presence_of_element_located((By.XPATH, btn_XPATH))
            )
            showBtn.click()
            currentPage += 1

        # if the show more button is not found using the By XPATH method, catch the TimeoutError exception
        except:
            # try to locate the show more button using the By CLASS_NAME method
            try:
                showBtn = WebDriverWait(driver, wait_time).until(
                    EC.presence_of_element_located((By.XPATH, '//button[@data-test="show-x-more-reviews-button"]'))
                )
                showBtn.click()
                currentPage += 1
            except TimeoutError:
                # the show button was not found using either strategy
                print("show button could not be located...")
                currentPage += 1


    # stores the reviews section
    reviews_section = driver.find_element(By.ID, 'reviews-accordion-accordion-content-reviews-accordion')  
    # stores all p tags of the reviews section
    reviews = reviews_section.find_elements(By.TAG_NAME, 'p')
    # stores all the scraped time
    scraped_timestamp = reviews_section.find_elements(By.TAG_NAME, 'time')
    
    # list to store the text of each review (title, review, location)
    reviews_list = []
    # iterates through the list of review elements
    for review in reviews:
        # stores the text of the reviews element to the list
        reviews_list.append(review.text)

    # list to store the datetime attributes of the scraped 'time' elements
    timestamps = []
    # iterates through the list of scraped 'time' elements
    for time in scraped_timestamp:
        # gets the datetime attribute of the time element 
        datetime = time.get_attribute("datetime")
        # stores datetime to the list
        timestamps.append(datetime)
        
    ## closes the browser
    driver.close()
    
    return reviews_list, timestamps

url = "https://www.argos.co.uk/product/9461987?clickSR=slp:term:meta%20quest%202:2:22:1"
reviews_list, timestamps = scrape_reviews(url=url, maxPages=130)

```

We save the lists to a local file because it allows us to use them for preprocessing to avoid errors and repetition. Scraping data from websites can be unreliable due to the possibility of changes in the structure of the website's Document Object Model. By saving the data locally, we can use it for preprocessing without the risk of it being affected by changes to the website. Additionally, saving the data locally allows us to access it more easily and avoid the need to scrape the website again, which can save time and resources.


```python
import pickle
```


```python
# Save the reviews_list and timestamps into a file
with open('data.pkl', 'wb') as f:
    pickle.dump((reviews_list, timestamps), f)
```


```python
# Load the reviews_list and timestamps from the file
with open('data.pkl', 'rb') as f:
    reviews_list, timestamps = pickle.load(f)
```

## 3.Data Preprocessing
<p>
The next step is Preprocessing the data. it can help to ensure that the data is clean, consistent, and ready for analysis, and can improve the accuracy and effectiveness of the sentiment analysis and topic modeling techniques.
</p>

### 3.1.Labeling the data
<p>
    
The first step in preprocessing the data is to use the Pandas library to label the data. This involves assigning appropriate names to the columns of the DataFrame. We will assign the names 'Title', 'Review', 'Location', and merge the timestamp list into the dataFrame as 'timestamp' to the columns of the DataFrame. This will help to clarify the meaning and purpose of each column, and will allow us to manipulate and analyze the data using these meaningful names. 
</p>


```python
import pandas as pd
import csv

def label_reviews(reviews_list):
    reviews_dict = {}
    for i in range(0, len(reviews_list), 3):
        title = reviews_list[i]
        review = reviews_list[i+1]
        location = reviews_list[i+2]
        reviews_dict[i] = {
            'title': title,
            'reviews': review,
            'location': location
    }
        
    return reviews_dict


def generate_df(reviews, timestamps):
    df = pd.DataFrame.from_dict(reviews, orient='index').reset_index(drop=True).drop(index=0)
    df = df[['title', 'reviews', 'location']]
    
    # We need to pad or truncate the timestamps list to match the length of the DataFrame
    
    # if length of timestamps is less than length of df:
    # pad timestamps with None values until length of timestamps is equal to length of df
    # else if length of timestamps is greater than length of df
    # truncate timestamps to length of df
    # add timestamps as a column to df with name 'timestamp' and return df
    if len(timestamps) < len(df):
        # Pad timestamps with None values to match the length of the index
        timestamps += [None] * (len(df) - len(timestamps))
    elif len(timestamps) > len(df):
        # Truncate timestamps to match the length of the index
        timestamps = timestamps[:len(df)]
    df.insert(loc=3, column='timestamp', value=timestamps)
    return df

reviews = label_reviews(reviews_list)
scraped_df = generate_df(reviews, timestamps)
scraped_df.head()

```

We save our labeled scraped_df DataFrame into a csv file `data.csv` since using a locally saved CSV file is more reliable and faster for further analysis. We also don't need to scrape the website again to get the dataset.


```python
scraped_df.to_csv('data.csv')
```

### Load CSV File
code to open the labeled dataset locally as a DataFrame


```python
import pandas as pd

# Set the maximum length of the string to display
pd.set_option('display.max_colwidth', None)

try:
    # Read the CSV file into a dataframe
    df = pd.read_csv('data.csv')
except Exception as e:
    print("Error opening file:", e)
    
df.isnull().sum()
```




    Unnamed: 0    0
    title         0
    reviews       0
    location      0
    timestamp     0
    dtype: int64




```python
# Drop column 'Unnamed: 0'
df.drop(columns=['Unnamed: 0'], inplace=True)
# Print the data type of each column
print(df.dtypes)
```

    title        object
    reviews      object
    location     object
    timestamp    object
    dtype: object
    


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1310 entries, 0 to 1309
    Data columns (total 4 columns):
     #   Column     Non-Null Count  Dtype 
    ---  ------     --------------  ----- 
     0   title      1310 non-null   object
     1   reviews    1310 non-null   object
     2   location   1310 non-null   object
     3   timestamp  1310 non-null   object
    dtypes: object(4)
    memory usage: 41.1+ KB
    

### 3.2.Preprocessing datetime
<p>
The next step in our data preprocessing process is to preprocess the timestamps data into a datetime object. This involves converting the timestamps from their current format, which is a string, into a datetime object, then into Year-Month-Day form so that can be easily manipulated and analyzed. 
</p>


```python
from datetime import datetime
### https://docs.python.org/3/library/datetime.html#strftime-strptime-behavior ###

# convert the 'timestamp' column to datetime object
df['timestamp'] = df['timestamp'].apply(lambda x: datetime.strptime(x, "%Y-%m-%dT%H:%M:%S.%fZ"))

# Create a new column with the year, month, and day in the format "yyyy-mm-dd"
df['date'] = df['timestamp'].apply(lambda x: x.strftime("%Y-%m-%d"))

# remove the 'timestamp' column
df = df.drop(columns=['timestamp'])

# rename the 'date' column to 'timestamp'
df = df.rename(columns={'date': 'timestamp'})
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>reviews</th>
      <th>location</th>
      <th>timestamp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fast and Accurate Shopping</td>
      <td>I was very pleased with the stock accuracy, the help of the employees and the fast shopping.</td>
      <td>bg0139, 25 - 34, Ankara, turkey</td>
      <td>2022-12-22</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mr Donatas Barkus</td>
      <td>Good staff, my family very like</td>
      <td>Donatas, 35 - 44, London</td>
      <td>2022-12-21</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Great product</td>
      <td>My son enjoying it. Must have item for all age</td>
      <td>Nilu, 35 - 44, Droitwich</td>
      <td>2022-12-21</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Present for daughter</td>
      <td>I bought this for a Christmas present for my daughter very happy with the delivery ewas delivered with care.</td>
      <td>Mandy, 45 - 54, Prescot</td>
      <td>2022-12-14</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Meta Quest 2</td>
      <td>Excellent value for money. Happy customer would definitely recommend</td>
      <td>Racka, 45 - 54, Teesside</td>
      <td>2022-12-13</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1305</th>
      <td>Fun device, Abut not for everyone!</td>
      <td>Great fun for my son, but instantly gave my daughter and I motion sickness. It does say this in the blurb, but it affected the two of us quite badly. My son loves it though, so as long as you have plenty of space to move around I’m told it’s brilliant!</td>
      <td>Mathcornish, 45 - 54, West Sussex</td>
      <td>2021-09-22</td>
    </tr>
    <tr>
      <th>1306</th>
      <td>Great family fun</td>
      <td>My 8 year old autistic son loves to play with his occulus it gives him some sensory input and gives me some piece when hes playing lol. Occulus is also a great family adventure fun game from virtual reality car racing to shooting targets and many great brain training and competitive games it's a good choice for family fun times. ;,)</td>
      <td>Argosprobuyer, 25 - 34, Liverpool</td>
      <td>2021-09-22</td>
    </tr>
    <tr>
      <th>1307</th>
      <td>Not bad, not bad at all</td>
      <td>I bought this as I bought the Rift S... Turns out their last patch stopped the use of USB C adaptors... I had to buy a Quest 2. I am not disappointed. Very good non PC-VR kit. However, Oculus software is a bit rubbish.</td>
      <td>ahyman1990, 25 - 34, Manchester</td>
      <td>2021-09-21</td>
    </tr>
    <tr>
      <th>1308</th>
      <td>Worth it</td>
      <td>Have been waiting to get an Xbox series X. But after it’s taken so long I decided to try the world or VR without a Pc. Great for those into gaming and those who aren’t. My other half uses it for escape rooms. Downside is that streaming drops out often abs you can only export videos via Facebook which isn’t useful.</td>
      <td>Rob, 25 - 34, Chelmsford</td>
      <td>2021-09-21</td>
    </tr>
    <tr>
      <th>1309</th>
      <td>Great feature</td>
      <td>Is very nice game to play m very happy thank to argos</td>
      <td>Nauman, 25 - 34, London Walthamstow</td>
      <td>2021-09-21</td>
    </tr>
  </tbody>
</table>
<p>1310 rows × 4 columns</p>
</div>



### 3.4.Text preprocessing
the next step of our process is to clean and filter the noise from the text by using regular expressions and natural language processing tools (NLTK) to get accurate results in our analysis. 


```python
import re
import nltk

# Download the stopwords data from NLTK
nltk.download('stopwords')

# Download the wordnet data from NLTK
nltk.download('wordnet')

# downloads the "omw" data from NLTK
nltk.download('omw-1.4')

# import stop words from NLTK
from nltk.corpus import stopwords

# import word tokenizer from NLTK
from nltk.tokenize import word_tokenize

# import word Lemmatizer from NLTK
from nltk.stem import WordNetLemmatizer

# import a list of stop words in the English language from NLTK
stop_words = nltk.corpus.stopwords.words('english')
```

    [nltk_data] Downloading package stopwords to
    [nltk_data]     C:\Users\SHiFT\AppData\Roaming\nltk_data...
    [nltk_data]   Package stopwords is already up-to-date!
    [nltk_data] Downloading package wordnet to
    [nltk_data]     C:\Users\SHiFT\AppData\Roaming\nltk_data...
    [nltk_data]   Package wordnet is already up-to-date!
    [nltk_data] Downloading package omw-1.4 to
    [nltk_data]     C:\Users\SHiFT\AppData\Roaming\nltk_data...
    [nltk_data]   Package omw-1.4 is already up-to-date!
    

### 3.4.1.Preprocessing location
The next step in our data preprocessing process is to preprocess the location data in order to extract the city of each review. We can do this by using regular expressions (regex).


```python
def get_city_location(row):
    # access value of the row in location column and stores it in value variable
    value = row['location']
    complete_location = re.split(r",", value)
    try:
        #third element gives us the name of the city of the customer
        city_location = complete_location[2]
    except:
        # sets it to N/A 
        city_location = "N/A"
    
    return city_location

# apply the extract_city_location() function to each row of the dataframe in the location column
df['location'] = df.apply(get_city_location, axis=1)
```

### 3.4.1.1.Visaulize reviews count by city


```python
import matplotlib.pyplot as plt
#create a new df that contains all the cities that isnt N\A
filtered_df = df.loc[df['location'] != 'N/A']

# get the top cities by using counter then sorting the values and finally get only the first 5
top_cities = filtered_df['location'].value_counts().sort_values(ascending=False).head(5)

# Plot a bar chart of review counts by city
plt.bar(top_cities.index, top_cities)
plt.xlabel('City')
plt.ylabel('Number of Reviews')
# show the plot
plt.show()
```


    
![png](output_27_0.png)
    


London may have more robust infrastructure or support for VR technology, which could make it easier for consumers in these areas to use and review VR headset products

### 3.4.2.Preprocessing and cleaning text data for Sentiment Analysis and Topic Modelling
<p> 
    In order to get accurate results from sentiment analysis and topic modeling, we develop functions that filter and pre-process text by:
    <ul>
        <li> Implementing regular expressions to strip special characters and punctuation marks. </li>
        <li> Implementing NLTK for to remove stop words and perform tokenization and lemmatization on the remaining words.</li>
        <li> Concatenating the filtered and pre-processed words to create a cleaned version of the text.</li>           
    </ul>
<p>
    Lemmatization is the process of reducing a word to its base form. It  produce more accurate and meaningful forms of words than stemming. Hence, lemmatization is often preferred over stemming for tasks that require a high degree of accuracy or interpretability, which is needed in sentiment analysis and topic modeling.
</p>


```python
### https://stackoverflow.com/questions/18429143/strip-punctuation-with-regex-python ###

# function that removes special characters, punctuations, extra whitespace from text
def strip_special_characters(text):    
    # compile a regular expression pattern that matches one or more spaces
    pattern = re.compile('\s+')
    
    # removes any special characters and punctuations from text
    clean_text = re.sub(r'[^\w\s]',' ',text)
    
    # renoves any underscore from the text
    clean_text = re.sub(r'_',' ',clean_text)
    
    #removes exccess white space from the text
    clean_text = pattern.sub(' ', clean_text)
    
    #returns the text clean from special characters, punctuations, underscore and exccess white space
    return clean_text

# lowercase text
def get_lowercase(text):
    return [word.lower() for word in text]

# tokenize the reviews text 

### lab 5 ### 
### https://www.geeksforgeeks.org/removing-stop-words-nltk-python/ ###

def strip_stop_words(text):
    try:
        stop_words = set(stopwords.words('english'))
        cleaned = [word for word in text if word not in stop_words]
        return cleaned
    except:
        # return empty list
        return []
# Lemmatization is generally more accurate than stemming
# If the context in which the words are used is important, lemmatization may be a better choice
# preserve the original meaning of the words and improve the accuracy of the analysis


### https://www.geeksforgeeks.org/python-lemmatization-with-nltk/ ###


### if not all(isinstance(x, str) ###


def lemmatize_words(text):        
    try:
        lemmatizer = WordNetLemmatizer()
        cleaned = [lemmatizer.lemmatize(word) for word in text]
        return cleaned
    except:
        # return empty list
        return []
    
def concatenate_words(text):
    # checks if the input is a list or a string
    if isinstance(text, list):
        tokens = []
        for word in text:
            # Convert each word to a string and add it to the list of tokens
            tokens.append(str(word))
        # Concatenate the tokens with a space separator
        return ' '.join(tokens)
    # checks if the input is a string, return it as is
    if isinstance(text, str):       
        return text    
```

Apply the filtering to the DataFrame reviews column


```python
df['reviews'] = df['reviews'].apply(strip_special_characters)
df['reviews'] = df['reviews'].apply(word_tokenize)
df['reviews'] = df['reviews'].apply(get_lowercase)
df['reviews'] = df['reviews'].apply(strip_stop_words)
df['reviews'] = df['reviews'].apply(lemmatize_words)
df['reviews'] = df['reviews'].apply(concatenate_words)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>reviews</th>
      <th>location</th>
      <th>timestamp</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fast and Accurate Shopping</td>
      <td>pleased stock accuracy help employee fast shopping</td>
      <td>Ankara</td>
      <td>2022-12-22</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mr Donatas Barkus</td>
      <td>good staff family like</td>
      <td>London</td>
      <td>2022-12-21</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Great product</td>
      <td>son enjoying must item age</td>
      <td>Droitwich</td>
      <td>2022-12-21</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Present for daughter</td>
      <td>bought christmas present daughter happy delivery ewas delivered care</td>
      <td>Prescot</td>
      <td>2022-12-14</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Meta Quest 2</td>
      <td>excellent value money happy customer would definitely recommend</td>
      <td>Teesside</td>
      <td>2022-12-13</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1305</th>
      <td>Fun device, Abut not for everyone!</td>
      <td>great fun son instantly gave daughter motion sickness say blurb affected two u quite badly son love though long plenty space move around told brilliant</td>
      <td>West Sussex</td>
      <td>2021-09-22</td>
    </tr>
    <tr>
      <th>1306</th>
      <td>Great family fun</td>
      <td>8 year old autistic son love play occulus give sensory input give piece he playing lol occulus also great family adventure fun game virtual reality car racing shooting target many great brain training competitive game good choice family fun time</td>
      <td>Liverpool</td>
      <td>2021-09-22</td>
    </tr>
    <tr>
      <th>1307</th>
      <td>Not bad, not bad at all</td>
      <td>bought bought rift turn last patch stopped use usb c adaptor buy quest 2 disappointed good non pc vr kit however oculus software bit rubbish</td>
      <td>Manchester</td>
      <td>2021-09-21</td>
    </tr>
    <tr>
      <th>1308</th>
      <td>Worth it</td>
      <td>waiting get xbox series x taken long decided try world vr without pc great gaming half us escape room downside streaming drop often ab export video via facebook useful</td>
      <td>Chelmsford</td>
      <td>2021-09-21</td>
    </tr>
    <tr>
      <th>1309</th>
      <td>Great feature</td>
      <td>nice game play happy thank argo</td>
      <td>London Walthamstow</td>
      <td>2021-09-21</td>
    </tr>
  </tbody>
</table>
<p>1310 rows × 4 columns</p>
</div>



### 4.Sentiment Analysis
Sentiment analysis is the process of using computational methods to identify and classify opinions expressed in a text, with the aim of determining the writer's attitude towards a particular topic, product, or other subject. This process involves identifying and interpreting the emotions, opinions, or evaluations expressed in the text, and categorizing them as positive, negative, or neutral. [3] </br>
Heres the following steps on how I calculated the sentiments of each review by using 'Vader' pre-trained model from NLTK and calculating the composite score:
<ol>
  <li>The <code>classify_sentiment</code> function takes a list of tokens as input and concatenates them into a single string using the <code>concatenate_words</code> function.</li>
  <li>If the input is not a string, the function returns a dictionary with default values for the sentiment and the percentages of positive, negative, and neutral sentiments.</li>
  <li>The function then instantiates a <code>SentimentIntensityAnalyzer</code> object from the <code>nltk.sentiment.vader</code> library and uses it to calculate the sentiment scores for the input string.</li>
  <li>The <code>calculate_sentiment_percent</code> function is called to calculate the percentages of positive, negative, and neutral sentiments using the sentiment scores.</li>
  <li>If the compound score (a composite score that takes into account the positive, negative, and neutral scores) is greater than or equal to 0.05, the function returns a dictionary with the sentiment label "positive" and the calculated percentages.</li>
  <li>If the compound score is less than or equal to -0.05, the function returns a dictionary with the sentiment label "negative" and the calculated percentages.</li>
  <li>If the compound score is between -0.05 and 0.05 (inclusive), the function returns a dictionary with the sentiment label "neutral" and the calculated percentages.</li>
  <li>If any errors occur during the execution of the function, a dictionary with default values for the sentiment and the percentages is returned.</li>
</ol>


```python
### "Python Natural Language Processing" by Jacob Perkins (Chapter 3, "Sentiment Analysis") ###
# using sentiment analyzer
from nltk.sentiment.vader import SentimentIntensityAnalyzer

def calculate_sentiment_percent(sentiment):
    # validates if the the dictionary has the correct keys pos, neg and neu   
    keys = {'pos', 'neg', 'neu'}
    if not keys.issubset(sentiment.keys()):
        raise ValueError('must have the following three keys: "pos", "neg", "neu"')
        
    # Calculate the percentage of positive, negative, and neutral sentiments
    total = sum(sentiment.values())
    pos_percent = sentiment['pos'] / total * 100
    neg_percent = sentiment['neg'] / total * 100
    neu_percent = sentiment['neu'] / total * 100
    
    # returns the percentage of positive, negative, and neutral sentiments
    return pos_percent, neg_percent, neu_percent

def classify_sentiment(tokens):
    text = concatenate_words(tokens)
    # validates if the the input is a string
    if not isinstance(text, str):
        return {'sentiment': 'N\A', 'pos_percent': 0, 'neg_percent': 0, 'neu_percent': 0}

    try:
        sid = SentimentIntensityAnalyzer()
        sentiment = sid.polarity_scores(text)

        pos_percent, neg_percent, neu_percent = calculate_sentiment_percent(sentiment)

        if sentiment['compound'] >= 0.05:
            return {'sentiment': 'positive', 'pos_percent': pos_percent, 'neg_percent': neg_percent, 'neu_percent': neu_percent}
        elif sentiment['compound'] <= -0.05:
            return {'sentiment': 'negative', 'pos_percent': pos_percent, 'neg_percent': neg_percent, 'neu_percent': neu_percent}
        else:
            return {'sentiment': 'neutral', 'pos_percent': pos_percent, 'neg_percent': neg_percent, 'neu_percent': neu_percent}
    except:
        return {'sentiment': 'N\A', 'pos_percent': 0, 'neg_percent': 0, 'neu_percent': 0}
```


```python
pd.set_option('display.max_rows', 1000)

df['sentiment'] = df.apply(lambda row: classify_sentiment(row['reviews'])['sentiment'], axis=1)
```


```python
import matplotlib.pyplot as plt
# calculate the proportions of reviews per sentiment (positive, negative and neutral)
counts = df['sentiment'].value_counts().sort_values(ascending=False) / len(df)

# plot the counts as a bar plot
counts.plot(kind='bar')

# add label to the x axis
plt.xlabel('Sentiment')

# add label to the y axis
plt.ylabel('Proportion of Reviews')

# Show the plot
plt.show()
```


    
![png](output_36_0.png)
    


It appears that the vast majority of reviews for the Meta Quest 2 are positive. This suggests that most people who have used the product are satisfied with it and have had a positive experience. It is also worth noting that a small percentage of reviews were neutral or negative, which suggests that there may be some issues or areas for improvement with the product. To further understand the sentiment of the reviews, we will extract the themes present in these sentiment to identify any potential issues or areas for improvement of this product.

## 5.Topic Modelling using BERTopic
<p>
BERTopic is a topic modeling technique that leverages embedding models and c-TF-IDF to create dense clusters allowing for easily interpretable topics whilst keeping important words in the topic descriptions. BERTopic supports guided, (semi-) supervised, hierarchical, and dynamic topic modeling [8].
</p>


```python
#!pip install bertopic
from bertopic import BERTopic
from umap import UMAP
```


```python
# stores the 'reviews' column to a list of documents
docs = df.reviews

# creates an instance of the UMAP model with specified parameters:
#  - n_neighbors: the number of nearest neighbors used in the UMAP algorithm
#  - n_components: the number of dimensions to reduce the data to using UMAP
#  - min_dist: the minimum distance between points in the UMAP space
#  - metric: the distance metric used to calculate distances in the UMAP space
#  - random_state: the seed for the UMAP random number generator (default seed I used is 43)
umap_model = UMAP(n_neighbors=15, n_components=5, 
                  min_dist=0.0, metric='cosine', random_state=43)

# creates an instance of the BERT-based topic model, using the specified UMAP model as a dimensionality reduction method
topic_model = BERTopic(umap_model=umap_model)
# transforms the topic model on the list of documents, returning the identified topics and their probabilities
topics, probs = topic_model.fit_transform(docs)
```


```python
# document, normalised count, -1 ignored
# get_topic_info method is a member function of the BERTopic to retrieve information about the identified topics.
topic_model.get_topic_info()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Topic</th>
      <th>Count</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-1</td>
      <td>130</td>
      <td>-1_product_fun_great_family</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>389</td>
      <td>0_vr_headset_game_oculus</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>358</td>
      <td>1_son_love_bought_christmas</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>157</td>
      <td>2_game_easy_bought_love</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3</td>
      <td>83</td>
      <td>3_ago_month_bought_happy</td>
    </tr>
    <tr>
      <th>5</th>
      <td>4</td>
      <td>73</td>
      <td>4_product_happy_excellent_item</td>
    </tr>
    <tr>
      <th>6</th>
      <td>5</td>
      <td>25</td>
      <td>5_family_fun_great_whole</td>
    </tr>
    <tr>
      <th>7</th>
      <td>6</td>
      <td>24</td>
      <td>6_argo_service_always_happy</td>
    </tr>
    <tr>
      <th>8</th>
      <td>7</td>
      <td>22</td>
      <td>7_battery_life_use_thing</td>
    </tr>
    <tr>
      <th>9</th>
      <td>8</td>
      <td>21</td>
      <td>8_world_fun_much_like</td>
    </tr>
    <tr>
      <th>10</th>
      <td>9</td>
      <td>16</td>
      <td>9_beat_saber_exercise_week</td>
    </tr>
    <tr>
      <th>11</th>
      <td>10</td>
      <td>12</td>
      <td>10_kit_piece_bit_amazing</td>
    </tr>
  </tbody>
</table>
</div>



The results show the top 12 topics identified by the model, along with the number of times each topic appears in the collection of documents. It is worth noting that according to BERTopic documentation [9], the "-1" topic is typically a noise term that should be ignored, as it is often used to represent documents that do not fit into any of the other identified topics. The remaining topics represent the main themes or topics present in the collection of documents.


```python
# add review topics to dataframe
df["topic"] = topics
```

### 5.1.Topic Insights
<p>
We will explore the results of our topic modeling by interpreting the representative documents for each identified topic.
For context, representative documents data that are selected from our dataset to represent the main topics or themes present in the dataset. They are chosen based on their high relevance to a particular topic and their ability to capture the main themes and ideas present in the dataset. We can gain insights into the content and focus of each topic. We will also consider any common patterns or issues that emerge across multiple topics.
</p>


```python
# print representative document of each topic 
for topic_num in range(11):
    print('topic #', topic_num)
    print(topic_model.representative_docs_[topic_num])
    print(' ')
```

    topic # 0
    ['bought christmas really happy product really robust experience using vr unlike really comfortable wear controller easy navigate', 'bought christmas gift oculus given u many laugh make feel different world', 'quest 2 3 week amazing piece kit fully immersive vr gaming brilliant graphic easy set oculus app joy whole family something experience understand']
     
    topic # 1
    ['got birthday', 'good daughter absolutely made', 'bought xmas living thanx']
     
    topic # 2
    ['excellent purchase come game price u would think would least 1 game free', 'partner bought 12 yr old 10 yr old love graphic excellent easy load pay game app depending game keep kid active moving around even adult loving', 'son love play online friend also one many game moment definitely future would recommend least 10ft square free space use lash move suddenly without remembering really reach hit wall furniture object house']
     
    topic # 3
    ['bought two month ago happy enjoy since', 'bought monts ago happy use', 'bought month ago happy']
     
    topic # 4
    ['happy product', 'product amazing', 'happy product far']
     
    topic # 5
    ['lot fun family', 'happy family great time playing together', 'fantastic fun family loved playing golf friend online']
     
    topic # 6
    ['best thing every plus argo way help', 'great buy went curry stock went argo stock made son happy thanks argo', 'bought argo 4 week ago amazing device well built easy setup use setup much fun']
     
    topic # 7
    ['bought partner love would recommend product side battery last two hour', 'downside short battery life approx 1 5 hour might positive stop playing eleven table tennis day', 'side u battery u dnt pc steam']
     
    topic # 8
    ['great game love', 'lad love lot good game', 'like another world great fun whole family']
     
    topic # 9
    ['combined beat saber prof lot fun surprisingly good workout time unit extremely clever aside short battery life really fault even much problem get one regret', 'thing great tethered anything game changing pun intended beat sabre best fun exercise year', 'bought month ago mainly using excercise apps motivating weight dropping 3 week see keeping excercise routine immersive unlike gym usualy given short keep wanting']
     
    topic # 10
    ['good kit someone send copy receipt email address plz', 'son extremely happy brill bit kit', 'amazing piece kit fence getting one go honestly amazing careful get motion sick']
     
    

The output is the the representative document of each topic from 0 to 10. We will try to make sense of each of the topic 

- #### Topic 0: <code>0_vr_headset_game_oculus</code>
The representative documents appear to discuss VR technology and the overall satisfaction with it. The reviewers generally seem to be satisfied with the VR headset and the technology, but there are some concerns about the cost of the games. The headset is described as being "great" and having a small range of games available, including fitness games. The headset is also described as being durable and having a reasonable price and quality, but the games are mentioned as being expensive. The reviewers also mention getting a lot of free entertainment, such as films and concerts, through the headset and using it in different places, such as while traveling or in a hotel. The VR technology is described as having progressed far and the headset is described as being subsidized by Facebook (Meta). it looks like that the reviewers are generally satisfied with the VR technology and the headset, but there are some concerns about the cost of the games. 

- #### Topic 1: <code>1_vr_headset_game_oculus</code>
The representative document appears to discuss the product that was bought for someone at Christmas period. The the person who received the product'son' loves the product. it looks like the product was well recieved as a gift.

- #### Topic 2: <code>2_game_easy_bought_love</code>
the representative documents are discussing the product and the overall satisfaction with it. The reviewers generally seem to be satisfied with the headset, but there are some concerns about the cost of the games. The headset is described as having plenty of free games and a good overall experience, and the purchase and delivery process is mentioned as being smooth. Some of the games are described as being "glorified tech demos" and the headset is mentioned as being used by the whole family. The headset is described as an "excellent piece of equipment" that is good for children to play with and is mentioned as being a good investment, although some of the popular games do cost money. The headset is mentioned as being cheaper than an Xbox or an X series, and the reviewers are overall happy with it.

- #### Topic 3:  <code>3_ago_month_bought_happy</code>
The representative documents are discussing the product, that it was recently purchased, and the reviewers bought it month ago and they are happy with it.

- #### Topic 4:  <code>4_product_happy_excellent_item</code>
The representative documents are disscussing the product. The first document states that the product works well and has not had any problems thus far. The second document uses strong, positive language to describe the product as "amazing." The third document also describes the product as "really excellent." All three documents suggest that the reviewers are satisfied with the product or service.

- #### Topic 5: <code>5_family_fun_great_whole</code>
The representative documents suggests that the first document mentions that the product is excellent and helps people stay active and fit. The second and third documents both mention that the product is enjoyable for the whole family, with the second document describing it as "great fun" and the third document mentioning that the reviewer's family had a "great time" using it together. All three documents suggest that the reviewers are satisfied with the product or service and that it is suitable for use with families and friends.


- #### Topic 6:<code> 6_argo_service_always_happy</code>
   The representative documents suggest that the reviewers are generally very satisfied with the product or service provided by "Argo," and they have positive experiences with it. It appears that they have had good experiences with the product in the past and are happy with it.
   
- #### Topic 7:<code> 7_battery_life_use_thing</code>
   The representative documents suggest that the main topic of discussion is the battery life and overall satisfaction with a product. It appears that the reviewers generally have positive opinions about the product, but there are some concerns about the battery life. The first document mentions that the product is highly regarded and that the reviewer is very fond of it, but wishes that it had a longer battery life. The second document mentions that the battery life is somewhat short and that there are issues with the remote, but the reviewer still thinks the product is generally good. It looks like reviewers are generally have positive feelings about the product, but there are some concerns about the battery life. 
   
- #### Topic 8: <code>8_world_fun_much_like</code>
The first document mentions that the product is like "another world" and is "great fun" for the whole family. This suggests that the product has a high level of immersion and is enjoyable to use with family members.
The second document mentions that the product is "fun" and that the reviewer has not "looked" or played anything else in the past week. This suggests that the product has been engaging and enjoyable to use over an extended period of time.
The third document mentions that the reviewer would "get one" because it is "much fun." This suggests that the reviewer enjoys the product and would consider purchasing it for themselves.
it looks like the reviewers find it enjoyable to use.


- #### Topic 9: <code>9_beat_saber_exercise_week</code>
    The first representative document describes the use of the product in combination with "beat saber" and mentions that it is a lot of fun and provides a good workout. However, it also mentions that the product has a short battery life, but this is not seen as a major problem. The reviewer expresses interest in purchasing the product and states that they do not regret doing so.

    The second representative document states that the product was purchased a month ago and has primarily been used for exercise apps. It mentions that the product has been effective in motivating the reviewer and has contributed to weight loss over the past three weeks. The document also describes the product as immersive and helpful for maintaining an exercise routine, unlike a traditional gym experience.

    The third representative document describes the product as being great and mentions that it is connected to something else. It is described as game-changing and the best and most fun exercise the reviewer has done in a year, with "beat sabre" being mentioned specifically.

    In summary, the representative documents suggest that the product or service is used for exercise and is enjoyable to use. The first and second documents mention its effectiveness in motivation and weight loss, and the third document describes it as fun and game-changing. The product's short battery life is mentioned in the first document, but it is not seen as a significant issue. All three documents indicate that the reviewers are satisfied with the product or service.


- #### Topic 10: <code>10_kit_piece_bit_amazing</code>
The representative documents express high levels of satisfaction with the product, which is described as an "amazing piece of kit" that is suitable for use by families. The second document describes the product as a "great bit of kit," and the third document mentions that the reviewer was very impressed with it and wishes they had more time in the day to use it. This documents suggest that the reviewers believe the product to be of high quality.





### 5.2.1.Breakdown sentiment by topic
<ol>
    <li>Create an empty dictionary called <code>topic_sentiment </code> </li>
  <li>Group the data in the <code>df</code> DataFrame by the "topic" column</li>
  <li>For each group of data in the "df" DataFrame:
    <ul>
      <li>Assign the "sentiment" column of the group to a variable called <code> df_ </code></li>
      <li>Calculate the percentage of each sentiment value in <code> df_ </code> and store the results in <code> topic_sentiment </code> with the group's "topic" as the key</li>
    </ul>
  </li>
  <li>Convert <code> topic_sentiment </code> to a DataFrame and display it</li>
</ol>


```python
# breakdown sentiment by topic
topic_sentiment = {}
for topic, df_ in df.groupby("topic"):
    topic_sentiment[topic] = df_["sentiment"].value_counts() / len(df_) * 100
pd.DataFrame(topic_sentiment)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>-1</th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>negative</th>
      <td>2.307692</td>
      <td>4.113111</td>
      <td>2.793296</td>
      <td>4.458599</td>
      <td>8.433735</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4.166667</td>
      <td>4.545455</td>
      <td>9.523810</td>
      <td>6.25</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>neutral</th>
      <td>9.230769</td>
      <td>2.313625</td>
      <td>8.379888</td>
      <td>0.636943</td>
      <td>3.614458</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>18.181818</td>
      <td>4.761905</td>
      <td>6.25</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>positive</th>
      <td>88.461538</td>
      <td>93.573265</td>
      <td>88.826816</td>
      <td>94.904459</td>
      <td>87.951807</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>95.833333</td>
      <td>77.272727</td>
      <td>85.714286</td>
      <td>87.50</td>
      <td>100.0</td>
    </tr>
  </tbody>
</table>
</div>



### 5.2.2.Visualize Sentiment per Topic


```python
import matplotlib.pyplot as plt

# get the values from the topic_sentiment dict and store them in separate lists
x_values = list(topic_sentiment.keys())
positive_values = []
neutral_values = []
negative_values = []

# iterates through the dictionary topic_sentiment
# extract the values for the keys "positive", "neutral", and "negative"
# for each key-value pair.
# If a key does not exist in the value, it appends 0 to the corresponding lists (pos, neg or neu lists above)
for key, value in topic_sentiment.items():
    if 'positive' in value:
        positive_values.append(value['positive'])
    else:
        positive_values.append(0)
    if 'neutral' in value:
        neutral_values.append(value['neutral'])
    else:
        neutral_values.append(0)
    if 'negative' in value:
        negative_values.append(value['negative'])
    else:
        negative_values.append(0)

# create the line chart
plt.plot(x_values, positive_values, label='Positive')
plt.plot(x_values, neutral_values, label='Neutral')
plt.plot(x_values, negative_values, label='Negative')

# ddd a title and axis labels
plt.title('Sentiment Analysis')
plt.xlabel('X-axis')
plt.ylabel('Sentiment Percentage')

# ddd a legend
plt.legend(loc='upper left')

# show the plot
plt.show()
```


    
![png](output_50_0.png)
    


it appears that there is a significant decline at topic 7 in the percentage of positive sentiment and an increase in neutral and negative sentiment. This suggests that there may be some issues with the battery life of the Meta Quest 2 that are causing dissatisfaction among users. The specific reasons for this decline in positive sentiment could be further explored.


```python
df[(df.topic == 7)]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>reviews</th>
      <th>location</th>
      <th>timestamp</th>
      <th>sentiment</th>
      <th>topic</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>48</th>
      <td>Incredible tech</td>
      <td>apprehensive buying thought might something use couple time put never use wrong use every day completely different way play game socialise careful though found certain game experience give motion sickness eye strain prolonged use also battery life terrible charging lot let thing put though really amazing bit kit</td>
      <td>Stoke-on-Trent</td>
      <td>2022-10-19</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>72</th>
      <td>Faulty controller</td>
      <td>one controller keep sticking</td>
      <td>N/A</td>
      <td>2022-09-27</td>
      <td>neutral</td>
      <td>7</td>
    </tr>
    <tr>
      <th>159</th>
      <td>Love it</td>
      <td>brilliant system bug still expected battery life bout 2hours advanced gaming purchase elite head strap additional battery pack really made white though due sweat turning greyish brown haha</td>
      <td>Sheffield</td>
      <td>2022-07-13</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>240</th>
      <td>Great quality</td>
      <td>bought son happy thing would suggest hand controller instead battery built battery charge otherwise absolutely fantastic</td>
      <td>Portslade</td>
      <td>2022-05-10</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>244</th>
      <td>Good</td>
      <td>side u battery u dnt pc steam</td>
      <td>Birmingham</td>
      <td>2022-05-04</td>
      <td>neutral</td>
      <td>7</td>
    </tr>
    <tr>
      <th>311</th>
      <td>Really cool</td>
      <td>small full power lightweight</td>
      <td>London</td>
      <td>2022-03-23</td>
      <td>neutral</td>
      <td>7</td>
    </tr>
    <tr>
      <th>328</th>
      <td>Amazing VR, good build quality</td>
      <td>downside short battery life approx 1 5 hour might positive stop playing eleven table tennis day</td>
      <td>N/A</td>
      <td>2022-03-16</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>450</th>
      <td>What i was expecting from it</td>
      <td>bought month two ago non stop thing thats negative battery life</td>
      <td>Sheffield</td>
      <td>2022-02-11</td>
      <td>negative</td>
      <td>7</td>
    </tr>
    <tr>
      <th>482</th>
      <td>It's almost great</td>
      <td>battery last long ok remote started going one way 2 week also need space play game overall great product</td>
      <td>N/A</td>
      <td>2022-02-08</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>583</th>
      <td>Amazing</td>
      <td>battery life bit rubbish amazing product</td>
      <td>N/A</td>
      <td>2022-01-19</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>602</th>
      <td>Great kids love it</td>
      <td>great item battery life seem la long maybe faulty battery</td>
      <td>Leicester</td>
      <td>2022-01-19</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>640</th>
      <td>Fantastic and value for money</td>
      <td>content purchase endless amount fun thing battery last long 2 hour overcome connecting long usb c power bank</td>
      <td>N/A</td>
      <td>2022-01-12</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>709</th>
      <td>Great fun</td>
      <td>brought christmas gift husband get great fun use load different thing complain much gaming get physical exercise well thing clear easy use</td>
      <td>Stonea</td>
      <td>2022-01-07</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>759</th>
      <td>VR for the future</td>
      <td>using since christmas amazing would strongly suggest try demo version game buying love game love quality love use plugged watch youtube netflix etc etc amazing battery last quite well option plug power pack playing official version great use pack standard usb c 90 deg adaptor specific wire comfortable wire work</td>
      <td>Wales</td>
      <td>2022-01-05</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>822</th>
      <td>Great features</td>
      <td>little bit heavy</td>
      <td>London</td>
      <td>2022-01-05</td>
      <td>neutral</td>
      <td>7</td>
    </tr>
    <tr>
      <th>837</th>
      <td>Amazing</td>
      <td>best thing bought fantastic family spent hour since got wish longer battery life need changing much addicted</td>
      <td>Liverpool</td>
      <td>2022-01-05</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>865</th>
      <td>Son very happy</td>
      <td>bought many christmas present son seems happy comment longevity use battery life easy always deal argo</td>
      <td>West Yorkshire</td>
      <td>2022-01-04</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>866</th>
      <td>Great fun</td>
      <td>bought partner love would recommend product side battery last two hour</td>
      <td>Ossett</td>
      <td>2022-01-04</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1101</th>
      <td>Good standalone vr experience</td>
      <td>need pc run well battery life good</td>
      <td>Chorley</td>
      <td>2021-12-08</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1118</th>
      <td>Love it</td>
      <td>bought 6th november playing took wacks controller sign damage anything love would recommend battery like last around 2 3 hour maybe depending game one small headset considering thats amazing</td>
      <td>South east</td>
      <td>2021-11-24</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1192</th>
      <td>Amazing gaming machine</td>
      <td>brilliant piece kit lot lot realise good actually use would suggest buying battery pack alongside battery best free game app store lot payed game also ranging 4 99 29 99</td>
      <td>Pontypridd</td>
      <td>2021-10-27</td>
      <td>positive</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1284</th>
      <td>Amazing product</td>
      <td>comfortable absolutely amazing pas time loved spending time friend game available battery life long ok use full battery life one ru anyway controller easy use button spaced apart right</td>
      <td>Scarborough</td>
      <td>2021-09-29</td>
      <td>positive</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>



We can see from these reviews of topic 7 that many of the reviewers mentioned that the battery life is a concern

### 5.3.1.Keyword Extraction using keyBERT
KeyBERT is a minimal and easy-to-use keyword extraction technique that leverages BERT embeddings to create keywords and keyphrases that are most similar to a document [10].

both BERTopic and keyBERT are based on the transformer architecture and are trained on large corpora of text data, making them effective at identifying the main topics and themes in a document, as well as extracting relevant keywords. However, BERTopic is specifically designed for topic modeling, while keyBERT is specifically designed for keyword extraction. Therefore, it may be a good idea to use BERTopic for topic modeling and keyBERT for keyword extraction, as they are both specialized tools that are well-suited for these tasks.


```python
# ! pip install keybert
from keybert import KeyBERT
from collections import Counter
```

#### 5.3.1.1.Extracting top keywords per topic


```python
def get_sorted_topic_keywords(topic_num):
    # initialize KeyBERT model
    kw_model = KeyBERT()
    # extract the keywords from the list of reviews for specific Topic number using the KeyBERT model 
    keywords = kw_model.extract_keywords(df[df.topic == topic_num]["reviews"].to_list())# keyphrase_ngram_range=(1))
    
    # sorted_keywords is a list of tuples where.
    # each tuple consists of a keyword and its frequency.
    # The list is sorted in descending order of frequency by applying the sorted function.
    # display only the 10 first.
    
    sorted_keywords = sorted(Counter([xx[0] for x in keywords for xx in x]).items(), key=lambda x: x[1], reverse=True)[:10]
    return sorted_keywords

sorted_keywords_by_topic = {}

for topic_num in range(11):
     # extract and sort the keywords for the current topic number
    sorted_keywords = get_sorted_topic_keywords(topic_num)
    # store the sorted keywords to the dictionary using the topic number as the key for the dictionary
    sorted_keywords_by_topic[topic_num] = sorted_keywords

print(sorted_keywords_by_topic)
```

    {0: [('vr', 202), ('headset', 116), ('oculus', 103), ('quest', 57), ('pc', 47), ('bought', 45), ('game', 39), ('experience', 39), ('gaming', 31), ('virtual', 25)], 1: [('bought', 152), ('son', 131), ('love', 109), ('christmas', 87), ('birthday', 58), ('fun', 43), ('present', 42), ('family', 39), ('daughter', 33), ('kid', 32)], 2: [('game', 70), ('bought', 57), ('christmas', 25), ('set', 19), ('play', 18), ('gaming', 17), ('birthday', 14), ('free', 14), ('purchase', 14), ('son', 13)], 3: [('bought', 57), ('month', 31), ('ago', 29), ('happy', 18), ('week', 14), ('use', 8), ('fun', 7), ('worth', 7), ('game', 7), ('brought', 7)], 4: [('happy', 28), ('product', 27), ('great', 13), ('excellent', 12), ('purchase', 9), ('good', 9), ('fun', 8), ('item', 8), ('recommend', 7), ('bought', 7)], 5: [('family', 22), ('fun', 17), ('great', 7), ('good', 3), ('hour', 3), ('brilliant', 3), ('excellent', 3), ('loved', 3), ('amazing', 3), ('lot', 3)], 6: [('argo', 22), ('bought', 7), ('service', 6), ('happy', 6), ('stock', 3), ('buy', 2), ('son', 2), ('collection', 2), ('gift', 2), ('customer', 2)], 7: [('battery', 18), ('bought', 5), ('life', 5), ('controller', 4), ('use', 3), ('buying', 2), ('kit', 2), ('game', 2), ('gaming', 2), ('pc', 2)], 8: [('world', 10), ('fun', 8), ('game', 7), ('love', 3), ('like', 3), ('great', 3), ('fantastic', 3), ('playing', 2), ('feel', 2), ('new', 2)], 9: [('exercise', 8), ('saber', 7), ('bought', 4), ('play', 4), ('game', 3), ('apps', 2), ('free', 2), ('gym', 2), ('fun', 2), ('calorie', 2)], 10: [('kit', 11), ('piece', 7), ('bit', 3), ('great', 3), ('amazing', 3), ('bought', 2), ('fun', 2), ('brill', 1), ('son', 1), ('happy', 1)]}
    

we can see that sorted_keywords_by_topic is a dictionary of list of tuples

#### 5.3.1.2.Extracting top keywords from all reviews


```python
def get_all_sorted_keywords():
    docs = df.reviews
    kw_model = KeyBERT()
    keywords = kw_model.extract_keywords(docs)
    all_sorted_keywords = sorted(Counter([xx[0] for x in keywords for xx in x]).items(), key=lambda x: x[1], reverse=True)
    return all_sorted_keywords
all_sorted_keywords = get_all_sorted_keywords()
```

### 5.3.2.Keywords Frequency
Keyword frequency refers to the number of times a keyword appears in a text or document. This can be used as a measure of the importance or relevance of the keyword within the text. Higher keyword frequencies can indicate that a keyword is a key theme or topic in the text, while lower frequencies may indicate that it is less relavant.

The code consists of two functions:

get_keywords_frequencies: This function takes in a sorted list of tuples containing keywords and their corresponding frequencies. It returns two lists: one with the keywords and another with their frequencies.

generate_barh: This function takes in three arguments: a list of keywords, a list of frequencies, and an optional matplotlib axis object (ax). It creates a bar chart using the ax object and sets the tick labels for the y-axis. It also adds labels and a title to the plot. If a topic number (topic_num) is provided, it is included in the title. If no ax object is provided, it creates a new figure and axis object.


```python
def get_keywords_frequencies(sorted_keywords):
    # gets the first element of each tuple. (frequency)
    keywords = [keyword for keyword, frequency in sorted_keywords]
    
    # gets the the second element of each tuple. (keyword)
    frequencies = [frequency for keyword, frequency in sorted_keywords]
    return keywords, frequencies

keywords, frequencies = get_keywords_frequencies(sorted_keywords)
def generate_barh(keywords, frequencies, ax=None, topic_num=None):
    # checks if the keywords and frequencies have the same length
    if len(keywords) != len(frequencies):
        return 'keywords and frequencies are not the same len'

    # create a new figure and axis object if no ax object is provided
    if ax is None:
        fig, ax = plt.subplots()

    # create the bar chart using the ax object
    ax.barh(keywords, frequencies, color='#228b22')

    # set the tick labels for the y-axis
    ax.set_yticks(keywords, fontsize = 12)
    ax.set_yticklabels(keywords, fontsize = 12)

    # add labels and the title
    ax.set_ylabel('Keywords', fontsize=14)
    ax.set_xlabel('Frequency', fontsize=14)
    
    # checks if topic_num is provided, if yes, prints the topic num in the title, else not
    if topic_num is not None:
        ax.set_title(f'Keyword Frequencies for Topic #{topic_num}', fontsize=14)
    else:
        ax.set_title('Keyword Frequencies', fontsize=14)

keywords, frequencies = get_keywords_frequencies(get_sorted_topic_keywords(7))
# generate_barh(keywords, frequencies)
```

### 5.3.1.Visualization of Keyword Frequencies per Topic


```python
# Set the figure size
plt.figure(figsize=(20, 60))

# Loop over the range 0 to the length of the sorted_keywords_by_topic 
for topic in range(len(sorted_keywords_by_topic)):
    # Get the sorted topic keywords and frequencies
    keywords, frequencies = get_keywords_frequencies(get_sorted_topic_keywords(topic))

    # Create a subplot
    ax = plt.subplot(8, 2, topic + 1)
  
    # Call the generate_barh function and pass the ax object
    generate_barh(keywords, frequencies, ax, topic)

# Show the plot
plt.show()
```


    
![png](output_64_0.png)
    


From these results, we can gain more insight:

The Meta Quest 2 is generally well-liked by reviewers: The sentiment analysis indicated that 90% of the reviews were positive, and the keywords "happy", "great", "excellent", "good", and "fun" all appear in the keyword frequencies for various topics.

The Meta Quest 2 is often used by individuals and families: The keywords "family" and "son" appear in the top 10 keywords for topics 0, 1, 2, 5, and 6.

We can see that the Meta Quest 2 is often purchased as a gift: The keywords "christmas" and "birthday" appear in the keywords frequencies for topics 1, 2, and 5, indicating that the headset is often purchased as a gift for special occasions.

The Meta Quest 2 may have some additional features or accessories that are appreciated by reviewers: The keywords "set", "free", and "kit" all appear in the keywords for various topics. This could suggest that the VR headset may have some additional features or accessories that are appreciated by reviewers.

There may be concerns about the battery life of the Meta Quest 2. The results of the Keywords frequencies also support our previous insight from Topic insights chapter in topic 7 that there's a concern about battery life of the VR headset, as the top words in topic 7 include "battery" and "life," as well as other words related to battery performance, such as "use" and "controller." The high frequency of these words suggests that battery life is an important consideration for customers when evaluating the VR headset.

### 5.3.2.Visualization of All Keyword Frequencies with Word Cloud
Wordclouds are used to visualize the most common or important words in a text or set of texts. The size of the word in the wordcloud reflects its frequency or importance in the text.


```python
from wordcloud import WordCloud

keyword_frequencies = dict(all_sorted_keywords)

wordcloud = WordCloud(background_color='black', colormap='Blues', width=800, height=800)

wordcloud.generate_from_frequencies(keyword_frequencies)

# Generate the wordcloud from the keywords

# Display the wordcloud
plt.figure(figsize=(6, 6))
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis("off")
plt.show()
```


    
![png](output_67_0.png)
    


We can see fron the Wordcloud that the Meta Quest 2 VR headset is a popular choice for gift giving, as the words "bought", "Christmas", "birthday", and "present" all appear prominently. This suggests that the headset is a well-liked and widely-appreciated gift. Additionally, the words "fun", "amazing", "love"and "quality" suggest that the headset is enjoyable to use and well-made. The word "family" also appears, indicating that the headset is enjoyed by multiple people in a household. Overall, the wordcloud suggests that the Meta Quest 2 VR headset is a well-received and widely-used product, particularly as a gift.

### 5.4.Topics over Time
topics over time is a visual representation of the prevalence of  topics in a dataset over a period of time.

<code> note that you need to run this code on jupyter notebook to see the plot </code>


```python
topics_over_time = topic_model.topics_over_time(docs, df['timestamp'])
topic_model.visualize_topics_over_time(topics_over_time)
```


<div>                            <div id="452e784c-90dc-4825-a117-29bb01d851af" class="plotly-graph-div" style="height:450px; width:1250px;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("452e784c-90dc-4825-a117-29bb01d851af")) {                    Plotly.newPlot(                        "452e784c-90dc-4825-a117-29bb01d851af",                        [{"hoverinfo":"text","hovertext":["<b>Topic 0</b><br>Words: patch, taken, export, pc, adaptor","<b>Topic 0</b><br>Words: pc, long, vr, system, headset","<b>Topic 0</b><br>Words: headset, vr, apps, people, quest","<b>Topic 0</b><br>Words: pc, vr, suffered, win, game","<b>Topic 0</b><br>Words: thought, head, world, set, vr","<b>Topic 0</b><br>Words: starting, interested, loving, product, reality","<b>Topic 0</b><br>Words: 64g, blowing, step, second, future","<b>Topic 0</b><br>Words: spec, explore, world, apps, connect","<b>Topic 0</b><br>Words: travelogue, fantasy, startrek, transported, holodeck","<b>Topic 0</b><br>Words: using, quest, advice, vr, close","<b>Topic 0</b><br>Words: putt, virtual, workout, video, vr","<b>Topic 0</b><br>Words: make, gather, gaming, ps4, immerse","<b>Topic 0</b><br>Words: hour, yhis, tbh, couldnt, tell","<b>Topic 0</b><br>Words: asd, hurt, 30th, definitely, september","<b>Topic 0</b><br>Words: good, headset, facebook, bit, set","<b>Topic 0</b><br>Words: headset, directly, vr, airlink, play","<b>Topic 0</b><br>Words: purpose, vr, life, headset, game","<b>Topic 0</b><br>Words: performance, issue, near, mile, ahead","<b>Topic 0</b><br>Words: rift, former, vrcover, nicer, brainer","<b>Topic 0</b><br>Words: game, vr, experience, big, wanted","<b>Topic 0</b><br>Words: decent, playing, must, game, one","<b>Topic 0</b><br>Words: iv, activity, sport, found, enjoying","<b>Topic 0</b><br>Words: headset, vr, extend, strap, make","<b>Topic 0</b><br>Words: quest, vr, headset, sure, problem","<b>Topic 0</b><br>Words: graphic, brilliant, best, happy, headset","<b>Topic 0</b><br>Words: never, put, fantastic, kid, vr","<b>Topic 0</b><br>Words: vr, wire, starting, play, playstation","<b>Topic 0</b><br>Words: entry, gaming, vr, point, price","<b>Topic 0</b><br>Words: pc, oomph, gaming, headset, hilarious","<b>Topic 0</b><br>Words: vr, experience, quest, headset, game","<b>Topic 0</b><br>Words: vr, head, oculus, quite, different","<b>Topic 0</b><br>Words: vr, would, another, one, quest","<b>Topic 0</b><br>Words: quest, oculus, vr, box, headset","<b>Topic 0</b><br>Words: vr, device, usb, need, tracker","<b>Topic 0</b><br>Words: within, men, 35, female, cinematic","<b>Topic 0</b><br>Words: content, vr, refund, le, hour","<b>Topic 0</b><br>Words: vr, headset, even, like, oculus","<b>Topic 0</b><br>Words: vr, oculus, headset, game, one","<b>Topic 0</b><br>Words: vr, oculus, bit, game, headset","<b>Topic 0</b><br>Words: usage, disorientating, restriction, promptly, arrived","<b>Topic 0</b><br>Words: awesome, link, work, oculus, vr","<b>Topic 0</b><br>Words: wired, vr, headset, strap, battery","<b>Topic 0</b><br>Words: play, game, vr, experience, oculus","<b>Topic 0</b><br>Words: filled, portable, lightweight, boyfriend, fit","<b>Topic 0</b><br>Words: vrs, evening, busy, every, keep","<b>Topic 0</b><br>Words: roam, disappointment, desk, free, bit","<b>Topic 0</b><br>Words: device, headset, progressed, rival, subsidising","<b>Topic 0</b><br>Words: vr, quest, headset, game, oculus","<b>Topic 0</b><br>Words: cost, put, implication, graphic, default","<b>Topic 0</b><br>Words: equipement, superb, wife, market, piece","<b>Topic 0</b><br>Words: headset, drone, vr, headphone, speaker","<b>Topic 0</b><br>Words: vr, headset, ring, quest, resolution","<b>Topic 0</b><br>Words: vr, game, freeing, stage, event","<b>Topic 0</b><br>Words: system, always, time, oculus, great","<b>Topic 0</b><br>Words: oculus, amazing, love, vr, headset","<b>Topic 0</b><br>Words: fine, vr, removed, tos, rated","<b>Topic 0</b><br>Words: headset, vr, pc, say, fact","<b>Topic 0</b><br>Words: tonne, lab, extenders, guardian, safe","<b>Topic 0</b><br>Words: one, everything, heartedly, go, vr","<b>Topic 0</b><br>Words: vr, week, stand, headset, alone","<b>Topic 0</b><br>Words: game, headset, quest, even, vr","<b>Topic 0</b><br>Words: fit, glass, assumed, swap, impossible","<b>Topic 0</b><br>Words: quest, vr, help, head, headset","<b>Topic 0</b><br>Words: top, added, 3d, cinema, movie","<b>Topic 0</b><br>Words: device, since, designed, 15, strap","<b>Topic 0</b><br>Words: fixed, peice, bug, would, waiting","<b>Topic 0</b><br>Words: sou, oculus, quest, happy, vr","<b>Topic 0</b><br>Words: adjustment, band, halo, sceptical, kept","<b>Topic 0</b><br>Words: sticker, bank, using, headset, run","<b>Topic 0</b><br>Words: generation, gamer, play, oculus, different","<b>Topic 0</b><br>Words: real, powrbank, solved, wanderlust, world","<b>Topic 0</b><br>Words: tried, uncle, linked, boxing, decided","<b>Topic 0</b><br>Words: headset, oculus, vr, best, strap","<b>Topic 0</b><br>Words: interact, catch, sit, card, together","<b>Topic 0</b><br>Words: want, vr, necessary, better, pc","<b>Topic 0</b><br>Words: system, use, work, opposed, fancy","<b>Topic 0</b><br>Words: collected, local, online, store, product","<b>Topic 0</b><br>Words: wire, look, around, noting, didnt","<b>Topic 0</b><br>Words: build, market, value, way, long","<b>Topic 0</b><br>Words: realistic, overall, head, new, brilliant","<b>Topic 0</b><br>Words: demanding, work, laptop, used, also","<b>Topic 0</b><br>Words: thrilled, 15, gift, old, year","<b>Topic 0</b><br>Words: le, headset, screen, positioning, eyepiece","<b>Topic 0</b><br>Words: 15, film, said, place, vr","<b>Topic 0</b><br>Words: going, headset, covered, hotspot, serial","<b>Topic 0</b><br>Words: helpful, friendly, staff, recommended, think","<b>Topic 0</b><br>Words: good, availability, linking, miss, mode","<b>Topic 0</b><br>Words: accurate, camera, positioned, creating, struggled","<b>Topic 0</b><br>Words: headset, provided, game, vr, need","<b>Topic 0</b><br>Words: pc, vr, prior, oculus, single","<b>Topic 0</b><br>Words: also, check, game, better, extra","<b>Topic 0</b><br>Words: rift, pointless, device, quest, spinning","<b>Topic 0</b><br>Words: fantastici, grandson, brought, month, oculus","<b>Topic 0</b><br>Words: oculus, overpriced, play, quality, game","<b>Topic 0</b><br>Words: size, tube, change, literally, technology","<b>Topic 0</b><br>Words: wear, oculus, quest, make, sure","<b>Topic 0</b><br>Words: smallest, vr, surprised, opinion, selection","<b>Topic 0</b><br>Words: either, game, reasonable, demo, straight","<b>Topic 0</b><br>Words: prepared, seamless, functionality, need, regularly","<b>Topic 0</b><br>Words: intrigued, blow, sure, glad, away","<b>Topic 0</b><br>Words: interface, stock, amvr, facial, comfortable","<b>Topic 0</b><br>Words: retired, superior, dandling, exclusive, evil","<b>Topic 0</b><br>Words: accept, none, vision, higher, afford","<b>Topic 0</b><br>Words: vive, say, quest, vr, headset","<b>Topic 0</b><br>Words: headset, vr, get, lens, setup","<b>Topic 0</b><br>Words: get, around, bump, appreciate, fantastic","<b>Topic 0</b><br>Words: clear, use, though, test, firefox","<b>Topic 0</b><br>Words: fascinating, advise, hilarious, wrong, strange","<b>Topic 0</b><br>Words: movement, reality, graphic, life, battery","<b>Topic 0</b><br>Words: grid, step, equipment, option, room","<b>Topic 0</b><br>Words: research, weird, knocking, minor, port","<b>Topic 0</b><br>Words: mountain, feel, many, brink, munich","<b>Topic 0</b><br>Words: vrpc, effort, managed, hike, headstrap","<b>Topic 0</b><br>Words: terrible, tho, first, life, time","<b>Topic 0</b><br>Words: pc, title, standard, vr, available","<b>Topic 0</b><br>Words: get, front, workout, technology, video","<b>Topic 0</b><br>Words: impressive, apps, spoilt, experiencing, quest","<b>Topic 0</b><br>Words: variety, gaming, epic, medium, environment","<b>Topic 0</b><br>Words: standalone, display, pc, vr, choice","<b>Topic 0</b><br>Words: pain, eye, put, alright, hardship","<b>Topic 0</b><br>Words: headset, learn, prime, amazon, quest","<b>Topic 0</b><br>Words: enthusiast, throughly, little, kit, vr","<b>Topic 0</b><br>Words: index, vr, pc, steam, able","<b>Topic 0</b><br>Words: bcs, nausea, stay, ok, effect","<b>Topic 0</b><br>Words: sometimes, try, enjoying, oculus, much","<b>Topic 0</b><br>Words: pc, handle, task, processing, need","<b>Topic 0</b><br>Words: vr, introduce, launch, interacting, demonstrate","<b>Topic 0</b><br>Words: range, thought, clue, waited, rather","<b>Topic 0</b><br>Words: entertainment, vidoes, style, degree, realised","<b>Topic 0</b><br>Words: since, gotten, device, regular, aware","<b>Topic 0</b><br>Words: awkward, elastic, adjust, meta, incredible","<b>Topic 0</b><br>Words: truest, exceptional, investment, pricey, fault","<b>Topic 0</b><br>Words: although, better, orientation, adequate, hybrid","<b>Topic 0</b><br>Words: quality, good, headset, vr, game","<b>Topic 0</b><br>Words: code, put, thought, account, love","<b>Topic 0</b><br>Words: monitor, whilst, impressed, headset, one"],"marker":{"color":"#E69F00"},"mode":"lines","name":"0_vr_headset_game_oculus","x":["2021-09-21T00:00:00","2021-09-22T00:00:00","2021-09-23T00:00:00","2021-09-29T00:00:00","2021-10-02T00:00:00","2021-10-05T00:00:00","2021-10-06T00:00:00","2021-10-09T00:00:00","2021-10-12T00:00:00","2021-10-13T00:00:00","2021-10-19T00:00:00","2021-10-20T00:00:00","2021-10-21T00:00:00","2021-10-26T00:00:00","2021-10-27T00:00:00","2021-11-03T00:00:00","2021-11-10T00:00:00","2021-11-13T00:00:00","2021-11-16T00:00:00","2021-11-17T00:00:00","2021-11-18T00:00:00","2021-11-23T00:00:00","2021-11-24T00:00:00","2021-12-08T00:00:00","2021-12-09T00:00:00","2021-12-10T00:00:00","2021-12-12T00:00:00","2021-12-13T00:00:00","2021-12-14T00:00:00","2021-12-15T00:00:00","2021-12-16T00:00:00","2021-12-21T00:00:00","2021-12-22T00:00:00","2021-12-23T00:00:00","2021-12-26T00:00:00","2021-12-29T00:00:00","2022-01-04T00:00:00","2022-01-05T00:00:00","2022-01-06T00:00:00","2022-01-07T00:00:00","2022-01-09T00:00:00","2022-01-11T00:00:00","2022-01-12T00:00:00","2022-01-13T00:00:00","2022-01-14T00:00:00","2022-01-15T00:00:00","2022-01-18T00:00:00","2022-01-19T00:00:00","2022-01-20T00:00:00","2022-01-21T00:00:00","2022-01-25T00:00:00","2022-01-26T00:00:00","2022-01-27T00:00:00","2022-01-29T00:00:00","2022-01-30T00:00:00","2022-02-01T00:00:00","2022-02-02T00:00:00","2022-02-06T00:00:00","2022-02-08T00:00:00","2022-02-09T00:00:00","2022-02-10T00:00:00","2022-02-22T00:00:00","2022-02-23T00:00:00","2022-02-24T00:00:00","2022-02-27T00:00:00","2022-02-28T00:00:00","2022-03-01T00:00:00","2022-03-02T00:00:00","2022-03-08T00:00:00","2022-03-09T00:00:00","2022-03-11T00:00:00","2022-03-15T00:00:00","2022-03-16T00:00:00","2022-03-20T00:00:00","2022-03-22T00:00:00","2022-03-23T00:00:00","2022-03-30T00:00:00","2022-03-31T00:00:00","2022-04-06T00:00:00","2022-04-07T00:00:00","2022-04-12T00:00:00","2022-04-13T00:00:00","2022-04-14T00:00:00","2022-04-20T00:00:00","2022-04-21T00:00:00","2022-04-26T00:00:00","2022-04-27T00:00:00","2022-05-01T00:00:00","2022-05-04T00:00:00","2022-05-05T00:00:00","2022-05-10T00:00:00","2022-05-11T00:00:00","2022-05-12T00:00:00","2022-05-18T00:00:00","2022-05-24T00:00:00","2022-05-25T00:00:00","2022-06-01T00:00:00","2022-06-08T00:00:00","2022-06-10T00:00:00","2022-06-15T00:00:00","2022-06-17T00:00:00","2022-06-22T00:00:00","2022-06-28T00:00:00","2022-06-29T00:00:00","2022-07-06T00:00:00","2022-07-19T00:00:00","2022-07-20T00:00:00","2022-07-26T00:00:00","2022-07-27T00:00:00","2022-08-03T00:00:00","2022-08-04T00:00:00","2022-08-16T00:00:00","2022-08-18T00:00:00","2022-08-24T00:00:00","2022-08-31T00:00:00","2022-09-02T00:00:00","2022-09-14T00:00:00","2022-09-15T00:00:00","2022-09-18T00:00:00","2022-09-21T00:00:00","2022-09-25T00:00:00","2022-09-27T00:00:00","2022-09-28T00:00:00","2022-09-30T00:00:00","2022-10-05T00:00:00","2022-10-12T00:00:00","2022-10-19T00:00:00","2022-10-25T00:00:00","2022-10-26T00:00:00","2022-10-28T00:00:00","2022-11-05T00:00:00","2022-11-08T00:00:00","2022-11-09T00:00:00","2022-11-22T00:00:00","2022-12-07T00:00:00","2022-12-13T00:00:00"],"y":[2,4,1,6,1,2,1,1,1,6,1,3,1,3,4,3,4,1,1,6,2,2,7,6,1,1,3,1,3,23,3,3,6,2,1,3,9,33,6,2,1,6,9,1,1,1,4,15,3,1,7,6,4,1,1,3,7,1,4,8,3,3,12,1,1,1,1,2,2,3,2,1,8,1,1,2,1,2,2,1,1,1,1,1,2,1,2,1,3,1,1,2,1,4,2,3,2,2,1,1,1,1,1,2,3,3,3,1,1,1,1,1,1,1,3,1,3,1,1,2,5,1,1,1,1,1,1,1,1,1,1,1,1,1,2,1],"type":"scatter"},{"hoverinfo":"text","hovertext":["<b>Topic 1</b><br>Words: son, love, instantly, affected, blurb","<b>Topic 1</b><br>Words: teenage, pleased, present, son, love","<b>Topic 1</b><br>Words: birthday, son, bought, endless, moon","<b>Topic 1</b><br>Words: 13th, birthday, son, love, bought","<b>Topic 1</b><br>Words: grandchild, never, brought, month, ago","<b>Topic 1</b><br>Words: autism, trek, love, holodeck, wife","<b>Topic 1</b><br>Words: percent, 100, bought, daughter, last","<b>Topic 1</b><br>Words: buzzing, old, year, spot, great","<b>Topic 1</b><br>Words: asked, christmas, brand, ready, opened","<b>Topic 1</b><br>Words: birthday, involved, nephew, love, everyday","<b>Topic 1</b><br>Words: today, moon, made, grandson, birthday","<b>Topic 1</b><br>Words: saved, learning, equipment, daughter, piece","<b>Topic 1</b><br>Words: bouth, thebest, old, son, year","<b>Topic 1</b><br>Words: 11th, active, highly, last, getting","<b>Topic 1</b><br>Words: sept, done, perfect, gift, birthday","<b>Topic 1</b><br>Words: school, ggghbbnnnnhhgfdtstdyd, hc, son, love","<b>Topic 1</b><br>Words: love, son, day, prestine, bought","<b>Topic 1</b><br>Words: 12, age, present, absolutely, son","<b>Topic 1</b><br>Words: havnt, tested, yet, xmas, away","<b>Topic 1</b><br>Words: 12yr, said, ever, old, present","<b>Topic 1</b><br>Words: whole, kid, family, fun, bought","<b>Topic 1</b><br>Words: expecting, son, review, xmas, think","<b>Topic 1</b><br>Words: gift, birthday, teenager, boyfriend, excited","<b>Topic 1</b><br>Words: got, love, husband, thought, find","<b>Topic 1</b><br>Words: said, never, daughter, ever, thing","<b>Topic 1</b><br>Words: early, love, great, gift, kid","<b>Topic 1</b><br>Words: son, october, ine, love, surprising","<b>Topic 1</b><br>Words: love, bought, son, kid, child","<b>Topic 1</b><br>Words: son, christmas, love, family, brought","<b>Topic 1</b><br>Words: brought, awsome, understand, grandson, xmas","<b>Topic 1</b><br>Words: stepson, sort, realistic, brilliant, love","<b>Topic 1</b><br>Words: kid, 11yr, christmas, hope, whenever","<b>Topic 1</b><br>Words: christmas, love, bought, gift, son","<b>Topic 1</b><br>Words: gran, turn, whole, kid, got","<b>Topic 1</b><br>Words: christmas, son, love, brought, bought","<b>Topic 1</b><br>Words: yr, 11, son, love, bought","<b>Topic 1</b><br>Words: pre, teen, offer, said, thought","<b>Topic 1</b><br>Words: star, xmas, present, absolutely, son","<b>Topic 1</b><br>Words: christmas, son, love, bought, present","<b>Topic 1</b><br>Words: son, christmas, bought, love, present","<b>Topic 1</b><br>Words: bought, christmas, son, present, raving","<b>Topic 1</b><br>Words: love, playing, fun, yo, anf","<b>Topic 1</b><br>Words: christmas, gift, bought, observer, purchaser","<b>Topic 1</b><br>Words: christmas, son, bought, love, loved","<b>Topic 1</b><br>Words: christmas, present, kid, love, day","<b>Topic 1</b><br>Words: amazingly, ton, touch, realistic, keep","<b>Topic 1</b><br>Words: enjoyed, present, christmas, really, son","<b>Topic 1</b><br>Words: husband, love, christmas, bought, kid","<b>Topic 1</b><br>Words: bought, son, christmas, love, one","<b>Topic 1</b><br>Words: stoped, money, christmas, playing, son","<b>Topic 1</b><br>Words: money, christmas, boy, brought, well","<b>Topic 1</b><br>Words: birthday, thank, son, participated, also","<b>Topic 1</b><br>Words: entertaining, adult, kid, good, son","<b>Topic 1</b><br>Words: granddaughter, family, fun, love, bought","<b>Topic 1</b><br>Words: present, rest, yr, thrilled, loved","<b>Topic 1</b><br>Words: bough, he, son, saved, love","<b>Topic 1</b><br>Words: apparently, mum, purchased, ever, birthday","<b>Topic 1</b><br>Words: sevice, 11th, enjoying, daughter, whole","<b>Topic 1</b><br>Words: son, love, discarded, grandma, army","<b>Topic 1</b><br>Words: happy, bought, love, son, absolutely","<b>Topic 1</b><br>Words: 16th, kid, certainly, nephew, love","<b>Topic 1</b><br>Words: 15yr, son, simple, excellent, say","<b>Topic 1</b><br>Words: grandson, south, youngest, love, brother","<b>Topic 1</b><br>Words: fun, bought, adult, son, tech","<b>Topic 1</b><br>Words: work, well, really, son, love","<b>Topic 1</b><br>Words: grandson, 10, gift, birthday, grafic","<b>Topic 1</b><br>Words: presentfor, enjoys, nephew, recently, grandson","<b>Topic 1</b><br>Words: grandson, absolutely, love, bought, son","<b>Topic 1</b><br>Words: person, stream, stopped, partner, able","<b>Topic 1</b><br>Words: birthday, 17th, brought, packaging, thrilled","<b>Topic 1</b><br>Words: brithday, really, got, thing, son","<b>Topic 1</b><br>Words: 13, think, old, year, also","<b>Topic 1</b><br>Words: saved, decided, boy, adult, loved","<b>Topic 1</b><br>Words: sweat, visit, enjoyable, film, place","<b>Topic 1</b><br>Words: 13th, birthday, son, love, bought","<b>Topic 1</b><br>Words: son, trailing, youngest, parent, love","<b>Topic 1</b><br>Words: nonstop, 11th, entertainment, ever, brought","<b>Topic 1</b><br>Words: everywhere, 100, 12, take, son","<b>Topic 1</b><br>Words: daughter, naught, laughter, birthday, son","<b>Topic 1</b><br>Words: extremely, birthday, happy, product, son","<b>Topic 1</b><br>Words: daughter, love, son, bought, christmas","<b>Topic 1</b><br>Words: granddaughter, love, bought, son, christmas","<b>Topic 1</b><br>Words: academic, helped, regarding, son, enjoying","<b>Topic 1</b><br>Words: busy, amazed, seems, tried, keep","<b>Topic 1</b><br>Words: birthday, stress, exchange, bought, faulty","<b>Topic 1</b><br>Words: grandchild, using, fantastic, month, ago","<b>Topic 1</b><br>Words: son, therefore, birthday, mum, yes","<b>Topic 1</b><br>Words: 14th, spent, birthday, son, family","<b>Topic 1</b><br>Words: love, 12th, funny, son, grandson","<b>Topic 1</b><br>Words: boy, 10, ever, say, old","<b>Topic 1</b><br>Words: grandson, love, son, bought, christmas","<b>Topic 1</b><br>Words: arm, leg, forget, moving, played","<b>Topic 1</b><br>Words: unbelievable, granddaughter, rate, may, love","<b>Topic 1</b><br>Words: load, rhine, 9th, son, autistic","<b>Topic 1</b><br>Words: ups, grown, market, kid, best","<b>Topic 1</b><br>Words: chance, interested, husband, daughter, son","<b>Topic 1</b><br>Words: lad, enjoying, go, birthday, brilliant","<b>Topic 1</b><br>Words: absolutely, son, love, bought, christmas","<b>Topic 1</b><br>Words: son, bought, love, christmas, birthday","<b>Topic 1</b><br>Words: done, full, could, thing, best","<b>Topic 1</b><br>Words: admit, must, son, love, bought","<b>Topic 1</b><br>Words: amazed, cant, son, technology, recommended","<b>Topic 1</b><br>Words: open, yet, daughter, christmas, bought","<b>Topic 1</b><br>Words: love, son, birthday, bought, git","<b>Topic 1</b><br>Words: dementia, sufferer, logopenic, rare, beneficial","<b>Topic 1</b><br>Words: brill, grandchild, least, santa, enjoying","<b>Topic 1</b><br>Words: school, autistic, mine, soon, home","<b>Topic 1</b><br>Words: kid, life, like, love, son","<b>Topic 1</b><br>Words: fantastic, son, fun, great, love","<b>Topic 1</b><br>Words: brought, birthday, got, thing, absolutely","<b>Topic 1</b><br>Words: grandson, advised, question, hapoy, answer","<b>Topic 1</b><br>Words: know, anything, grandson, xmas, present","<b>Topic 1</b><br>Words: daughter, birthday, love, bought, son","<b>Topic 1</b><br>Words: birthday, got, family, son, fun","<b>Topic 1</b><br>Words: look, xmas, kid, present, amazing","<b>Topic 1</b><br>Words: 10th, moon, present, birthday, son","<b>Topic 1</b><br>Words: 12th, ideal, birthday, present, make","<b>Topic 1</b><br>Words: dearer, say, 100, two, come","<b>Topic 1</b><br>Words: review, xmas, kid, honest, undo","<b>Topic 1</b><br>Words: opened, yet, grandson, xmas, bought","<b>Topic 1</b><br>Words: wee, ex, soo, love, brother","<b>Topic 1</b><br>Words: ewas, delivered, care, delivery, daughter","<b>Topic 1</b><br>Words: enjoying, must, age, item, son"],"marker":{"color":"#56B4E9"},"mode":"lines","name":"1_son_love_bought_christmas","x":["2021-09-22T00:00:00","2021-09-28T00:00:00","2021-09-29T00:00:00","2021-10-01T00:00:00","2021-10-05T00:00:00","2021-10-06T00:00:00","2021-10-12T00:00:00","2021-10-13T00:00:00","2021-10-19T00:00:00","2021-10-20T00:00:00","2021-10-21T00:00:00","2021-10-22T00:00:00","2021-10-26T00:00:00","2021-10-27T00:00:00","2021-10-29T00:00:00","2021-11-02T00:00:00","2021-11-03T00:00:00","2021-11-04T00:00:00","2021-11-09T00:00:00","2021-11-10T00:00:00","2021-11-17T00:00:00","2021-11-18T00:00:00","2021-11-24T00:00:00","2021-12-08T00:00:00","2021-12-09T00:00:00","2021-12-12T00:00:00","2021-12-13T00:00:00","2021-12-14T00:00:00","2021-12-15T00:00:00","2021-12-16T00:00:00","2021-12-18T00:00:00","2021-12-21T00:00:00","2021-12-22T00:00:00","2021-12-23T00:00:00","2021-12-29T00:00:00","2021-12-30T00:00:00","2021-12-31T00:00:00","2022-01-02T00:00:00","2022-01-04T00:00:00","2022-01-05T00:00:00","2022-01-06T00:00:00","2022-01-07T00:00:00","2022-01-08T00:00:00","2022-01-11T00:00:00","2022-01-12T00:00:00","2022-01-14T00:00:00","2022-01-15T00:00:00","2022-01-18T00:00:00","2022-01-19T00:00:00","2022-01-21T00:00:00","2022-01-25T00:00:00","2022-01-26T00:00:00","2022-01-27T00:00:00","2022-02-01T00:00:00","2022-02-02T00:00:00","2022-02-08T00:00:00","2022-02-09T00:00:00","2022-02-10T00:00:00","2022-02-22T00:00:00","2022-02-23T00:00:00","2022-03-01T00:00:00","2022-03-02T00:00:00","2022-03-08T00:00:00","2022-03-09T00:00:00","2022-03-10T00:00:00","2022-03-15T00:00:00","2022-03-16T00:00:00","2022-03-17T00:00:00","2022-03-21T00:00:00","2022-03-22T00:00:00","2022-03-23T00:00:00","2022-03-24T00:00:00","2022-03-30T00:00:00","2022-04-01T00:00:00","2022-04-05T00:00:00","2022-04-06T00:00:00","2022-04-07T00:00:00","2022-04-12T00:00:00","2022-04-13T00:00:00","2022-04-26T00:00:00","2022-05-03T00:00:00","2022-05-04T00:00:00","2022-05-12T00:00:00","2022-05-17T00:00:00","2022-05-18T00:00:00","2022-05-24T00:00:00","2022-05-25T00:00:00","2022-05-31T00:00:00","2022-06-01T00:00:00","2022-06-08T00:00:00","2022-06-14T00:00:00","2022-06-15T00:00:00","2022-06-16T00:00:00","2022-06-28T00:00:00","2022-06-30T00:00:00","2022-07-06T00:00:00","2022-07-12T00:00:00","2022-07-13T00:00:00","2022-07-19T00:00:00","2022-07-20T00:00:00","2022-07-26T00:00:00","2022-08-03T00:00:00","2022-09-21T00:00:00","2022-09-25T00:00:00","2022-09-27T00:00:00","2022-09-28T00:00:00","2022-09-29T00:00:00","2022-10-04T00:00:00","2022-10-06T00:00:00","2022-10-11T00:00:00","2022-10-18T00:00:00","2022-10-26T00:00:00","2022-11-02T00:00:00","2022-11-07T00:00:00","2022-11-08T00:00:00","2022-11-09T00:00:00","2022-11-15T00:00:00","2022-11-16T00:00:00","2022-11-23T00:00:00","2022-12-06T00:00:00","2022-12-07T00:00:00","2022-12-14T00:00:00","2022-12-21T00:00:00"],"y":[3,1,3,1,1,3,2,4,2,3,1,1,4,1,1,4,4,1,1,1,1,2,4,3,1,2,2,10,10,3,1,3,12,1,16,2,1,1,23,38,7,4,3,11,4,1,1,6,8,1,1,2,1,1,2,3,1,1,5,5,3,2,4,3,1,4,3,1,1,3,1,1,2,1,1,4,1,2,4,1,1,1,2,1,3,1,4,1,2,1,1,2,2,2,1,1,1,1,1,1,1,2,1,7,1,3,1,1,1,1,4,1,1,1,1,1,1,1,2,1,4,1,1],"type":"scatter"},{"hoverinfo":"text","hovertext":["<b>Topic 2</b><br>Words: occulus, give, training, sensory, input","<b>Topic 2</b><br>Words: 24, forgets, password, lock, annoying","<b>Topic 2</b><br>Words: teen, otherwise, expected, brilliant, life","<b>Topic 2</b><br>Words: travel, past, entertained, 360, video","<b>Topic 2</b><br>Words: game, therapy, whim, relaxing, easy","<b>Topic 2</b><br>Words: reliable, set, easy, seems, purchasing","<b>Topic 2</b><br>Words: enjoyable, effect, equipment, piece, gaming","<b>Topic 2</b><br>Words: ab, seen, decided, one, wait","<b>Topic 2</b><br>Words: glorified, believed, pricy, horror, cracking","<b>Topic 2</b><br>Words: charge, calming, gaming, chair, addition","<b>Topic 2</b><br>Words: connects, seem, kid, thing, like","<b>Topic 2</b><br>Words: load, recommended, highly, free, experience","<b>Topic 2</b><br>Words: easy, 4all, restricted, 2use, challenge","<b>Topic 2</b><br>Words: whole, sometime, ive, thinking, played","<b>Topic 2</b><br>Words: happening, adapter, upto, shame, linked","<b>Topic 2</b><br>Words: disappoint, yes, game, aswell, addictive","<b>Topic 2</b><br>Words: leap, share, forward, problem, connected","<b>Topic 2</b><br>Words: involved, casting, including, boyfriend, laptop","<b>Topic 2</b><br>Words: surreal, enjoyed, account, facebook, daughter","<b>Topic 2</b><br>Words: loved, take, grate, electronic, evan","<b>Topic 2</b><br>Words: yr, game, adult, old, crappy","<b>Topic 2</b><br>Words: easy, christmas, set, tutorial, follow","<b>Topic 2</b><br>Words: happier, 12, available, great, could","<b>Topic 2</b><br>Words: xmas, bought, 32, daughter, year","<b>Topic 2</b><br>Words: game, got, wow, love, free","<b>Topic 2</b><br>Words: game, son, easy, christmas, love","<b>Topic 2</b><br>Words: age, game, younger, 16, suitable","<b>Topic 2</b><br>Words: holiday, download, see, game, grandson","<b>Topic 2</b><br>Words: enjoy, bought, one, set, easy","<b>Topic 2</b><br>Words: game, free, time, kid, play","<b>Topic 2</b><br>Words: immortal, vader, played, got, brilliant","<b>Topic 2</b><br>Words: game, hubby, love, daughter, eldest","<b>Topic 2</b><br>Words: game, buy, completely, plenty, bought","<b>Topic 2</b><br>Words: every, penny, state, eve, year","<b>Topic 2</b><br>Words: game, daughter, handy, got, birthday","<b>Topic 2</b><br>Words: us, console, game, purchased, function","<b>Topic 2</b><br>Words: game, old, year, selling, floor","<b>Topic 2</b><br>Words: read, game, amazing, 13, son","<b>Topic 2</b><br>Words: electrical, set, unreal, easy, number","<b>Topic 2</b><br>Words: request, tweaking, blocking, profile, bit","<b>Topic 2</b><br>Words: 14yr, poor, bored, unless, selection","<b>Topic 2</b><br>Words: crazy, laptop, different, world, need","<b>Topic 2</b><br>Words: pestered, apart, others, pay, game","<b>Topic 2</b><br>Words: game, stacked, response, tutorial, heard","<b>Topic 2</b><br>Words: chair, rather, sitting, fit, help","<b>Topic 2</b><br>Words: choice, partner, fit, everything, exercise","<b>Topic 2</b><br>Words: line, choose, load, product, amazing","<b>Topic 2</b><br>Words: cousin, wary, group, admit, gamer","<b>Topic 2</b><br>Words: wait, realistic, graphic, make, absolutely","<b>Topic 2</b><br>Words: sofa, sitting, good, content, game","<b>Topic 2</b><br>Words: graphic, easy, use, son, love","<b>Topic 2</b><br>Words: daddy, office, gift, whenever, sport","<b>Topic 2</b><br>Words: account, facebook, using, set, birthday","<b>Topic 2</b><br>Words: console, immersive, game, responsive, old","<b>Topic 2</b><br>Words: could, possibly, costly, opened, 13","<b>Topic 2</b><br>Words: worked, thrilled, soon, expensive, since","<b>Topic 2</b><br>Words: came, whatsoever, scuff, reseted, factory","<b>Topic 2</b><br>Words: free, definitely, reach, remembering, square","<b>Topic 2</b><br>Words: limit, lose, lol, admit, touch","<b>Topic 2</b><br>Words: case, pricey, move, fun, place","<b>Topic 2</b><br>Words: load, set, easy, fun, game","<b>Topic 2</b><br>Words: 2nd, debating, considering, purchasing, value","<b>Topic 2</b><br>Words: nope, laid, follow, suffer, seemed","<b>Topic 2</b><br>Words: free, game, love, piece, son","<b>Topic 2</b><br>Words: driving, lorry, onto, pick, straight","<b>Topic 2</b><br>Words: account, facebook, need, 12yr, onto","<b>Topic 2</b><br>Words: gamer, recommend, would, son, love","<b>Topic 2</b><br>Words: 14yr, reasonably, priced, totally, immersive","<b>Topic 2</b><br>Words: live, concert, simply, offer, husband","<b>Topic 2</b><br>Words: option, amerce, regulate, emotion, limited","<b>Topic 2</b><br>Words: education, whatever, whether, movie, expensive","<b>Topic 2</b><br>Words: occupied, little, item, keep, gaming","<b>Topic 2</b><br>Words: overwhelmed, awsome, 10th, boy, graphic","<b>Topic 2</b><br>Words: 3weeks, easy, play, enjoy, purchase","<b>Topic 2</b><br>Words: sound, effect, look, far, free","<b>Topic 2</b><br>Words: start, set, easy, charged, using"],"marker":{"color":"#009E73"},"mode":"lines","name":"2_game_easy_bought_love","x":["2021-09-22T00:00:00","2021-09-28T00:00:00","2021-09-29T00:00:00","2021-10-06T00:00:00","2021-10-12T00:00:00","2021-10-13T00:00:00","2021-10-14T00:00:00","2021-10-16T00:00:00","2021-10-20T00:00:00","2021-10-26T00:00:00","2021-11-03T00:00:00","2021-11-16T00:00:00","2021-11-24T00:00:00","2021-12-07T00:00:00","2021-12-12T00:00:00","2021-12-15T00:00:00","2021-12-21T00:00:00","2021-12-22T00:00:00","2021-12-26T00:00:00","2021-12-27T00:00:00","2021-12-29T00:00:00","2021-12-30T00:00:00","2021-12-31T00:00:00","2022-01-01T00:00:00","2022-01-04T00:00:00","2022-01-05T00:00:00","2022-01-06T00:00:00","2022-01-08T00:00:00","2022-01-11T00:00:00","2022-01-12T00:00:00","2022-01-15T00:00:00","2022-01-18T00:00:00","2022-01-19T00:00:00","2022-01-25T00:00:00","2022-01-26T00:00:00","2022-02-01T00:00:00","2022-02-02T00:00:00","2022-02-08T00:00:00","2022-02-09T00:00:00","2022-02-22T00:00:00","2022-02-24T00:00:00","2022-02-25T00:00:00","2022-03-01T00:00:00","2022-03-02T00:00:00","2022-03-04T00:00:00","2022-03-08T00:00:00","2022-03-15T00:00:00","2022-03-16T00:00:00","2022-03-23T00:00:00","2022-04-12T00:00:00","2022-04-13T00:00:00","2022-04-20T00:00:00","2022-04-27T00:00:00","2022-05-04T00:00:00","2022-05-17T00:00:00","2022-05-25T00:00:00","2022-06-08T00:00:00","2022-06-15T00:00:00","2022-06-21T00:00:00","2022-06-22T00:00:00","2022-06-29T00:00:00","2022-07-12T00:00:00","2022-07-28T00:00:00","2022-08-03T00:00:00","2022-08-09T00:00:00","2022-08-10T00:00:00","2022-09-25T00:00:00","2022-09-27T00:00:00","2022-10-18T00:00:00","2022-10-19T00:00:00","2022-10-26T00:00:00","2022-11-02T00:00:00","2022-11-04T00:00:00","2022-11-15T00:00:00","2022-12-06T00:00:00","2022-12-07T00:00:00"],"y":[2,1,1,1,4,2,1,1,3,2,1,1,2,1,1,2,1,2,1,1,2,2,1,2,10,21,3,1,3,5,1,3,7,3,4,4,3,2,3,1,1,1,1,2,1,1,1,2,1,1,1,1,1,4,1,1,1,2,1,2,1,1,1,3,1,1,1,1,1,1,1,1,1,1,1,1],"type":"scatter"},{"hoverinfo":"text","hovertext":["<b>Topic 3</b><br>Words: 100, ago, month, put, since","<b>Topic 3</b><br>Words: rope, learning, impressive, ago, tech","<b>Topic 3</b><br>Words: last, month, brilliant, bought, ago","<b>Topic 3</b><br>Words: month, ago, ever, thing, best","<b>Topic 3</b><br>Words: xxx, recently, back, enjoying, bought","<b>Topic 3</b><br>Words: knew, trust, recommendation, earlier, easier","<b>Topic 3</b><br>Words: 10am, shop, satisfied, search, closest","<b>Topic 3</b><br>Words: forgotten, draw, ago, expecting, everyday","<b>Topic 3</b><br>Words: boyfriend, im, ago, month, bought","<b>Topic 3</b><br>Words: ago, stop, month, item, since","<b>Topic 3</b><br>Words: looked, mate, due, saying, back","<b>Topic 3</b><br>Words: superb, stopped, try, item, price","<b>Topic 3</b><br>Words: month, ago, happy, bought, week","<b>Topic 3</b><br>Words: month, bought, recently, regret, ago","<b>Topic 3</b><br>Words: soo, bought, recently, ago, month","<b>Topic 3</b><br>Words: 3week, brill, regret, xbox, ago","<b>Topic 3</b><br>Words: month, ago, brought, happy, bought","<b>Topic 3</b><br>Words: insane, visuals, crazy, boyfriend, regret","<b>Topic 3</b><br>Words: month, ago, bought, unprecedented, confidence","<b>Topic 3</b><br>Words: week, ago, fantastic, absolutely, bought","<b>Topic 3</b><br>Words: month, last, definitely, worth, money","<b>Topic 3</b><br>Words: ago, month, ever, whole, thing","<b>Topic 3</b><br>Words: ago, month, bought, put, week","<b>Topic 3</b><br>Words: complaint, ago, le, month, stopped","<b>Topic 3</b><br>Words: recommended, month, ago, would, bought","<b>Topic 3</b><br>Words: depression, pulled, incredible, ago, week","<b>Topic 3</b><br>Words: header, ago, month, week, brought","<b>Topic 3</b><br>Words: changed, keeping, entertained, looking, mind","<b>Topic 3</b><br>Words: girl, ago, month, put, excellent","<b>Topic 3</b><br>Words: trust, bored, never, buying, brilliant","<b>Topic 3</b><br>Words: exchange, thr, developed, burn, bought","<b>Topic 3</b><br>Words: month, ago, happy, bought, week","<b>Topic 3</b><br>Words: idiot, thi, guide, tube, grip","<b>Topic 3</b><br>Words: month, ago, happy, bought, week","<b>Topic 3</b><br>Words: update, series, better, got, much","<b>Topic 3</b><br>Words: besides, ago, penny, expected, everything","<b>Topic 3</b><br>Words: happy, ago, honestly, week, item","<b>Topic 3</b><br>Words: ago, month, linked, bought, impressive","<b>Topic 3</b><br>Words: broke, already, week, happy, ago","<b>Topic 3</b><br>Words: right, ago, month, service, bought","<b>Topic 3</b><br>Words: earlier, wish, couple, week, brought","<b>Topic 3</b><br>Words: advance, gladly, waiting, others, month","<b>Topic 3</b><br>Words: regret, option, feel, need, much","<b>Topic 3</b><br>Words: young, recently, excellent, old, bought","<b>Topic 3</b><br>Words: week, ago, absolutely, bought, love","<b>Topic 3</b><br>Words: date, later, early, considering, glad","<b>Topic 3</b><br>Words: irritation, eye, ago, month, amazing","<b>Topic 3</b><br>Words: ago, exciting, month, bought, two","<b>Topic 3</b><br>Words: ago, monts, bought, little, quite","<b>Topic 3</b><br>Words: penny, ago, month, already, every","<b>Topic 3</b><br>Words: working, item, ago, month, happy","<b>Topic 3</b><br>Words: satisfied, month, ago, product, bought","<b>Topic 3</b><br>Words: week, ago, happy, really, bought","<b>Topic 3</b><br>Words: ago, month, worth, well, lot"],"marker":{"color":"#F0E442"},"mode":"lines","name":"3_ago_month_bought_happy","x":["2021-09-25T00:00:00","2021-09-28T00:00:00","2021-10-05T00:00:00","2021-10-06T00:00:00","2021-10-13T00:00:00","2021-10-20T00:00:00","2021-10-26T00:00:00","2021-10-27T00:00:00","2021-11-10T00:00:00","2021-11-24T00:00:00","2021-12-07T00:00:00","2021-12-08T00:00:00","2021-12-14T00:00:00","2021-12-15T00:00:00","2021-12-21T00:00:00","2021-12-22T00:00:00","2021-12-30T00:00:00","2022-01-04T00:00:00","2022-01-05T00:00:00","2022-01-11T00:00:00","2022-01-12T00:00:00","2022-01-18T00:00:00","2022-01-19T00:00:00","2022-01-25T00:00:00","2022-02-02T00:00:00","2022-02-08T00:00:00","2022-02-09T00:00:00","2022-02-11T00:00:00","2022-02-22T00:00:00","2022-03-02T00:00:00","2022-03-08T00:00:00","2022-03-10T00:00:00","2022-03-23T00:00:00","2022-03-30T00:00:00","2022-04-06T00:00:00","2022-04-13T00:00:00","2022-04-20T00:00:00","2022-04-27T00:00:00","2022-05-03T00:00:00","2022-05-10T00:00:00","2022-05-18T00:00:00","2022-06-08T00:00:00","2022-06-29T00:00:00","2022-07-13T00:00:00","2022-07-20T00:00:00","2022-07-23T00:00:00","2022-07-25T00:00:00","2022-08-10T00:00:00","2022-08-31T00:00:00","2022-09-07T00:00:00","2022-09-14T00:00:00","2022-09-28T00:00:00","2022-11-02T00:00:00","2022-11-16T00:00:00"],"y":[1,1,1,1,2,2,1,1,2,2,1,1,1,3,3,2,1,2,5,1,1,1,7,2,1,2,2,1,1,1,2,1,2,1,1,1,2,2,1,1,1,1,1,1,1,1,1,2,2,1,1,1,1,1],"type":"scatter"},{"hoverinfo":"text","hovertext":["<b>Topic 4</b><br>Words: happy, product, excellent, item, good","<b>Topic 4</b><br>Words: excellent, product, really, happy, item","<b>Topic 4</b><br>Words: im, thank, excellent, product, happy","<b>Topic 4</b><br>Words: happy, product, fantastic, item, fun","<b>Topic 4</b><br>Words: money, well, worth, product, happy","<b>Topic 4</b><br>Words: product, happy, bought, excellent, item","<b>Topic 4</b><br>Words: service, product, great, happy, excellent","<b>Topic 4</b><br>Words: pleased, purchase, recommend, would, product","<b>Topic 4</b><br>Words: lovely, boxed, excellent, happy, item","<b>Topic 4</b><br>Words: setup, happy, lot, good, easy","<b>Topic 4</b><br>Words: happy, product, purchase, rely, defo","<b>Topic 4</b><br>Words: thank, good, product, happy, excellent","<b>Topic 4</b><br>Words: excellent, equipment, glad, great, quality","<b>Topic 4</b><br>Words: highly, purchase, recommend, great, product","<b>Topic 4</b><br>Words: product, 21, nov, happy, excellent","<b>Topic 4</b><br>Words: product, excellent, happy, son, love","<b>Topic 4</b><br>Words: glad, lot, fun, bought, product","<b>Topic 4</b><br>Words: purchase, happy, product, excellent, item","<b>Topic 4</b><br>Words: delighted, product, happy, lot, using","<b>Topic 4</b><br>Words: product, contacting, contact, luck, excellent","<b>Topic 4</b><br>Words: simply, happy, purchase, ever, buy","<b>Topic 4</b><br>Words: item, product, brilliant, buy, easy","<b>Topic 4</b><br>Words: perch, recommending, strongly, product, happy","<b>Topic 4</b><br>Words: product, happy, modern, thanks, upgrading","<b>Topic 4</b><br>Words: product, happy, enjoyed, everything, definitely","<b>Topic 4</b><br>Words: superb, product, get, happy, excellent","<b>Topic 4</b><br>Words: proudly, good, product, happy, excellent","<b>Topic 4</b><br>Words: product, happy, lot, fun, excellent","<b>Topic 4</b><br>Words: sick, item, long, make, great","<b>Topic 4</b><br>Words: item, happy, product, excellent, good","<b>Topic 4</b><br>Words: good, price, product, happy, excellent","<b>Topic 4</b><br>Words: content, item, free, good, great","<b>Topic 4</b><br>Words: thanks, quiet, product, keep, money","<b>Topic 4</b><br>Words: device, happy, product, excellent, item","<b>Topic 4</b><br>Words: easy, good, use, product, happy","<b>Topic 4</b><br>Words: indeed, pleased, fantastic, buy, product","<b>Topic 4</b><br>Words: really, excellent, pleased, product, happy","<b>Topic 4</b><br>Words: item, purchase, happy, product, excellent","<b>Topic 4</b><br>Words: excellent, woth, quality, customer, product","<b>Topic 4</b><br>Words: happy, glad, comfortable, highly, purchased","<b>Topic 4</b><br>Words: excellent, product, month, ago, good","<b>Topic 4</b><br>Words: convenient, product, happy, purchase, quality","<b>Topic 4</b><br>Words: regret, product, great, happy, excellent","<b>Topic 4</b><br>Words: fit, product, keep, definitely, fantastic","<b>Topic 4</b><br>Words: pleased, product, happy, excellent, item","<b>Topic 4</b><br>Words: customer, excellent, happy, value, definitely"],"marker":{"color":"#D55E00"},"mode":"lines","name":"4_product_happy_excellent_item","x":["2021-09-22T00:00:00","2021-10-05T00:00:00","2021-10-19T00:00:00","2021-10-20T00:00:00","2021-10-28T00:00:00","2021-11-10T00:00:00","2021-11-25T00:00:00","2021-12-07T00:00:00","2021-12-08T00:00:00","2021-12-14T00:00:00","2021-12-15T00:00:00","2021-12-21T00:00:00","2021-12-22T00:00:00","2021-12-29T00:00:00","2022-01-04T00:00:00","2022-01-05T00:00:00","2022-01-09T00:00:00","2022-01-12T00:00:00","2022-01-18T00:00:00","2022-01-19T00:00:00","2022-02-01T00:00:00","2022-02-02T00:00:00","2022-02-09T00:00:00","2022-02-22T00:00:00","2022-02-23T00:00:00","2022-03-01T00:00:00","2022-03-09T00:00:00","2022-03-23T00:00:00","2022-03-30T00:00:00","2022-03-31T00:00:00","2022-04-12T00:00:00","2022-04-20T00:00:00","2022-04-21T00:00:00","2022-04-27T00:00:00","2022-05-13T00:00:00","2022-06-15T00:00:00","2022-06-29T00:00:00","2022-07-13T00:00:00","2022-07-19T00:00:00","2022-07-27T00:00:00","2022-09-01T00:00:00","2022-09-25T00:00:00","2022-10-07T00:00:00","2022-10-19T00:00:00","2022-10-25T00:00:00","2022-12-13T00:00:00"],"y":[1,1,2,6,1,1,1,1,2,2,5,1,3,1,4,2,1,1,2,3,1,2,1,2,2,1,1,1,1,1,1,1,1,1,1,1,1,1,2,2,1,2,1,1,1,1],"type":"scatter"},{"hoverinfo":"text","hovertext":["<b>Topic 5</b><br>Words: entire, perfect, family, fun, great","<b>Topic 5</b><br>Words: together, family, playing, time, happy","<b>Topic 5</b><br>Words: wont, regret, family, fun, amazing","<b>Topic 5</b><br>Words: family, fun, brought, hour, happy","<b>Topic 5</b><br>Words: family, fun, golf, loved, online","<b>Topic 5</b><br>Words: family, lot, fun, great, whole","<b>Topic 5</b><br>Words: family, member, active, fitness, loved","<b>Topic 5</b><br>Words: family, work, lot, fun, great","<b>Topic 5</b><br>Words: family, definitely, brilliant, fun, great","<b>Topic 5</b><br>Words: whip, l9ves, pistol, family, competitive","<b>Topic 5</b><br>Words: family, seeing, learning, fun, enjoying","<b>Topic 5</b><br>Words: ref, family, fun, hour, recommend","<b>Topic 5</b><br>Words: round, family, great, people, fun","<b>Topic 5</b><br>Words: family, omg, purchsed, fun, amazing","<b>Topic 5</b><br>Words: family, fun, great, whole, loved","<b>Topic 5</b><br>Words: family, excellent, fun, whole, go","<b>Topic 5</b><br>Words: fun, good, loved, family, great","<b>Topic 5</b><br>Words: entertainment, excellent, family, fun, great","<b>Topic 5</b><br>Words: family, brilliant, fun, hour, play","<b>Topic 5</b><br>Words: family, whole, fun, great, loved","<b>Topic 5</b><br>Words: staff, family, like, good, fun"],"marker":{"color":"#0072B2"},"mode":"lines","name":"5_family_fun_great_whole","x":["2021-09-29T00:00:00","2021-10-26T00:00:00","2021-12-15T00:00:00","2021-12-29T00:00:00","2021-12-31T00:00:00","2022-01-04T00:00:00","2022-01-05T00:00:00","2022-01-07T00:00:00","2022-01-11T00:00:00","2022-01-12T00:00:00","2022-01-13T00:00:00","2022-01-15T00:00:00","2022-01-19T00:00:00","2022-02-23T00:00:00","2022-03-15T00:00:00","2022-09-25T00:00:00","2022-09-28T00:00:00","2022-10-12T00:00:00","2022-10-25T00:00:00","2022-11-22T00:00:00","2022-12-21T00:00:00"],"y":[1,1,1,1,2,1,2,1,1,1,1,1,2,2,1,1,1,1,1,1,1],"type":"scatter"},{"hoverinfo":"text","hovertext":["<b>Topic 6</b><br>Words: nice, thank, argo, happy, play","<b>Topic 6</b><br>Words: argo, day, em, tastic, failure","<b>Topic 6</b><br>Words: ordered, argo, needed, find, happy","<b>Topic 6</b><br>Words: always, reliable, pickup, argo, quick","<b>Topic 6</b><br>Words: rescue, struggled, argo, anywhere, stock","<b>Topic 6</b><br>Words: argo, setup, built, plus, help","<b>Topic 6</b><br>Words: job, team, argo, im, item","<b>Topic 6</b><br>Words: argo, usual, ace, collection, text","<b>Topic 6</b><br>Words: argo, loved, guest, dad, everyday","<b>Topic 6</b><br>Words: argo, collection, service, customer, gave","<b>Topic 6</b><br>Words: porcoase, argo, happy, service, always","<b>Topic 6</b><br>Words: argo, else, anyone, day, service","<b>Topic 6</b><br>Words: argo, wait, back, new, sud","<b>Topic 6</b><br>Words: basis, argo, giving, daily, quick","<b>Topic 6</b><br>Words: argo, always, wonderment, created, providing","<b>Topic 6</b><br>Words: argo, service, always, partner, ago","<b>Topic 6</b><br>Words: argo, stock, went, curry, thanks","<b>Topic 6</b><br>Words: berryden, aberdeen, argo, class, service","<b>Topic 6</b><br>Words: argo, checked, hassle, availability, closest"],"marker":{"color":"#CC79A7"},"mode":"lines","name":"6_argo_service_always_happy","x":["2021-09-21T00:00:00","2021-10-20T00:00:00","2021-10-27T00:00:00","2021-11-16T00:00:00","2021-12-08T00:00:00","2021-12-15T00:00:00","2021-12-22T00:00:00","2022-01-04T00:00:00","2022-01-05T00:00:00","2022-01-06T00:00:00","2022-01-19T00:00:00","2022-01-26T00:00:00","2022-02-09T00:00:00","2022-06-01T00:00:00","2022-06-22T00:00:00","2022-07-08T00:00:00","2022-07-26T00:00:00","2022-11-09T00:00:00","2022-11-16T00:00:00"],"y":[1,1,1,1,1,2,1,2,2,1,1,3,1,1,1,1,1,1,1],"type":"scatter"},{"hoverinfo":"text","hovertext":["<b>Topic 7</b><br>Words: battery, life, ru, spaced, use","<b>Topic 7</b><br>Words: 99, battery, lot, 29, ranging","<b>Topic 7</b><br>Words: wacks, november, sign, 6th, battery","<b>Topic 7</b><br>Words: run, battery, life, well, need","<b>Topic 7</b><br>Words: battery, longevity, comment, deal, side","<b>Topic 7</b><br>Words: battery, pack, etc, version, wire","<b>Topic 7</b><br>Words: thing, physical, complain, use, get","<b>Topic 7</b><br>Words: long, overcome, bank, endless, amount","<b>Topic 7</b><br>Words: battery, life, la, seem, rubbish","<b>Topic 7</b><br>Words: remote, ok, started, battery, going","<b>Topic 7</b><br>Words: thats, non, negative, stop, two","<b>Topic 7</b><br>Words: positive, eleven, approx, table, tennis","<b>Topic 7</b><br>Words: small, lightweight, power, full, battery","<b>Topic 7</b><br>Words: dnt, side, steam, battery, pc","<b>Topic 7</b><br>Words: battery, suggest, instead, hand, otherwise","<b>Topic 7</b><br>Words: battery, greyish, bout, 2hours, brown","<b>Topic 7</b><br>Words: sticking, controller, keep, one, battery","<b>Topic 7</b><br>Words: use, battery, though, put, certain"],"marker":{"color":"#E69F00"},"mode":"lines","name":"7_battery_life_use_thing","x":["2021-09-29T00:00:00","2021-10-27T00:00:00","2021-11-24T00:00:00","2021-12-08T00:00:00","2022-01-04T00:00:00","2022-01-05T00:00:00","2022-01-07T00:00:00","2022-01-12T00:00:00","2022-01-19T00:00:00","2022-02-08T00:00:00","2022-02-11T00:00:00","2022-03-16T00:00:00","2022-03-23T00:00:00","2022-05-04T00:00:00","2022-05-10T00:00:00","2022-07-13T00:00:00","2022-09-27T00:00:00","2022-10-19T00:00:00"],"y":[1,1,1,1,2,3,1,1,2,1,1,1,1,1,1,1,1,1],"type":"scatter"},{"hoverinfo":"text","hovertext":["<b>Topic 8</b><br>Words: else, played, anything, look, week","<b>Topic 8</b><br>Words: lad, lot, good, love, game","<b>Topic 8</b><br>Words: crazy, world, away, way, get","<b>Topic 8</b><br>Words: world, fantastic, fun, much, like","<b>Topic 8</b><br>Words: much, get, fun, one, world","<b>Topic 8</b><br>Words: world, new, whole, amazing, fun","<b>Topic 8</b><br>Words: sick, feel, everyone, make, world","<b>Topic 8</b><br>Words: mesmerising, absolutly, endless, fun, penny","<b>Topic 8</b><br>Words: bye, inside, world, big, item","<b>Topic 8</b><br>Words: detailed, fantastically, track, world, exploring","<b>Topic 8</b><br>Words: different, world, funny, someone, look","<b>Topic 8</b><br>Words: enjoyed, fantastic, really, game, world","<b>Topic 8</b><br>Words: real, awesome, like, life, game","<b>Topic 8</b><br>Words: world, another, whole, like, fun","<b>Topic 8</b><br>Words: worst, world, game, fun, much","<b>Topic 8</b><br>Words: fingertip, world, new, whole, fun","<b>Topic 8</b><br>Words: queasy, feeling, side, however, lot","<b>Topic 8</b><br>Words: im, stood, lounge, world, forget","<b>Topic 8</b><br>Words: owned, ever, much, brought, thing"],"marker":{"color":"#56B4E9"},"mode":"lines","name":"8_world_fun_much_like","x":["2021-09-22T00:00:00","2021-10-20T00:00:00","2021-11-02T00:00:00","2021-11-03T00:00:00","2021-11-16T00:00:00","2021-12-15T00:00:00","2021-12-22T00:00:00","2022-01-04T00:00:00","2022-01-20T00:00:00","2022-01-30T00:00:00","2022-02-23T00:00:00","2022-03-01T00:00:00","2022-03-02T00:00:00","2022-03-08T00:00:00","2022-04-20T00:00:00","2022-05-18T00:00:00","2022-07-13T00:00:00","2022-09-28T00:00:00","2022-12-13T00:00:00"],"y":[2,1,1,1,1,1,1,2,1,1,1,1,1,1,1,1,1,1,1],"type":"scatter"},{"hoverinfo":"text","hovertext":["<b>Topic 9</b><br>Words: kg, gym, lose, lost, weight","<b>Topic 9</b><br>Words: 23, saber, beat, favourite, remember","<b>Topic 9</b><br>Words: saber, beat, exercise, every, week","<b>Topic 9</b><br>Words: medium, night, saber, beat, compared","<b>Topic 9</b><br>Words: house, fight, motivational, thrill, ibs","<b>Topic 9</b><br>Words: joint, heard, pressure, forehead, three","<b>Topic 9</b><br>Words: prof, saber, beat, combined, clever","<b>Topic 9</b><br>Words: alls, meditation, relax, day, calorie","<b>Topic 9</b><br>Words: pun, intended, tethered, changing, sabre","<b>Topic 9</b><br>Words: way, pas, favourite, saber, beat","<b>Topic 9</b><br>Words: excercise, usualy, dropping, motivating, routine","<b>Topic 9</b><br>Words: exercise, app, free, even, brought","<b>Topic 9</b><br>Words: hate, exercising, saber, beat, favourite","<b>Topic 9</b><br>Words: saber, beat, good, cinema, movie"],"marker":{"color":"#009E73"},"mode":"lines","name":"9_beat_saber_exercise_week","x":["2021-11-16T00:00:00","2021-12-21T00:00:00","2022-01-04T00:00:00","2022-01-05T00:00:00","2022-01-12T00:00:00","2022-01-13T00:00:00","2022-01-19T00:00:00","2022-01-25T00:00:00","2022-01-26T00:00:00","2022-02-23T00:00:00","2022-05-17T00:00:00","2022-07-13T00:00:00","2022-08-16T00:00:00","2022-08-20T00:00:00"],"y":[1,1,3,1,1,1,1,1,1,1,1,1,1,1],"type":"scatter"},{"hoverinfo":"text","hovertext":["<b>Topic 10</b><br>Words: kit, piece, excellent, hour, fun","<b>Topic 10</b><br>Words: kit, piece, brilliant, bit, amazing","<b>Topic 10</b><br>Words: kit, great, bit, fun, piece","<b>Topic 10</b><br>Words: kit, address, receipt, copy, email","<b>Topic 10</b><br>Words: kit, away, piece, pick, blown","<b>Topic 10</b><br>Words: kit, piece, amazing, bit, away","<b>Topic 10</b><br>Words: kit, bit, family, great, piece","<b>Topic 10</b><br>Words: kit, fence, piece, careful, amazing","<b>Topic 10</b><br>Words: kit, bit, guru, blow, separately","<b>Topic 10</b><br>Words: kit, piece, impressed, day, well","<b>Topic 10</b><br>Words: piece, equipment, feature, quality, good","<b>Topic 10</b><br>Words: brill, kit, extremely, bit, happy"],"marker":{"color":"#F0E442"},"mode":"lines","name":"10_kit_piece_bit_amazing","x":["2021-09-28T00:00:00","2021-10-13T00:00:00","2021-10-19T00:00:00","2021-11-16T00:00:00","2021-11-23T00:00:00","2021-12-29T00:00:00","2022-01-04T00:00:00","2022-01-05T00:00:00","2022-01-12T00:00:00","2022-01-26T00:00:00","2022-02-09T00:00:00","2022-05-24T00:00:00"],"y":[1,1,1,1,1,1,1,1,1,1,1,1],"type":"scatter"}],                        {"template":{"data":{"barpolar":[{"marker":{"line":{"color":"white","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"bar":[{"error_x":{"color":"rgb(36,36,36)"},"error_y":{"color":"rgb(36,36,36)"},"marker":{"line":{"color":"white","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"carpet":[{"aaxis":{"endlinecolor":"rgb(36,36,36)","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"rgb(36,36,36)"},"baxis":{"endlinecolor":"rgb(36,36,36)","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"rgb(36,36,36)"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"},"type":"choropleth"}],"contourcarpet":[{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"},"type":"contourcarpet"}],"contour":[{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"},"colorscale":[[0.0,"#440154"],[0.1111111111111111,"#482878"],[0.2222222222222222,"#3e4989"],[0.3333333333333333,"#31688e"],[0.4444444444444444,"#26828e"],[0.5555555555555556,"#1f9e89"],[0.6666666666666666,"#35b779"],[0.7777777777777778,"#6ece58"],[0.8888888888888888,"#b5de2b"],[1.0,"#fde725"]],"type":"contour"}],"heatmapgl":[{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"},"colorscale":[[0.0,"#440154"],[0.1111111111111111,"#482878"],[0.2222222222222222,"#3e4989"],[0.3333333333333333,"#31688e"],[0.4444444444444444,"#26828e"],[0.5555555555555556,"#1f9e89"],[0.6666666666666666,"#35b779"],[0.7777777777777778,"#6ece58"],[0.8888888888888888,"#b5de2b"],[1.0,"#fde725"]],"type":"heatmapgl"}],"heatmap":[{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"},"colorscale":[[0.0,"#440154"],[0.1111111111111111,"#482878"],[0.2222222222222222,"#3e4989"],[0.3333333333333333,"#31688e"],[0.4444444444444444,"#26828e"],[0.5555555555555556,"#1f9e89"],[0.6666666666666666,"#35b779"],[0.7777777777777778,"#6ece58"],[0.8888888888888888,"#b5de2b"],[1.0,"#fde725"]],"type":"heatmap"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"},"colorscale":[[0.0,"#440154"],[0.1111111111111111,"#482878"],[0.2222222222222222,"#3e4989"],[0.3333333333333333,"#31688e"],[0.4444444444444444,"#26828e"],[0.5555555555555556,"#1f9e89"],[0.6666666666666666,"#35b779"],[0.7777777777777778,"#6ece58"],[0.8888888888888888,"#b5de2b"],[1.0,"#fde725"]],"type":"histogram2dcontour"}],"histogram2d":[{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"},"colorscale":[[0.0,"#440154"],[0.1111111111111111,"#482878"],[0.2222222222222222,"#3e4989"],[0.3333333333333333,"#31688e"],[0.4444444444444444,"#26828e"],[0.5555555555555556,"#1f9e89"],[0.6666666666666666,"#35b779"],[0.7777777777777778,"#6ece58"],[0.8888888888888888,"#b5de2b"],[1.0,"#fde725"]],"type":"histogram2d"}],"histogram":[{"marker":{"line":{"color":"white","width":0.6}},"type":"histogram"}],"mesh3d":[{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"}},"marker":{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"}},"type":"scattermapbox"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"}},"type":"scatterpolargl"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"}},"type":"scatterpolar"}],"scatter":[{"fillpattern":{"fillmode":"overlay","size":10,"solidity":0.2},"type":"scatter"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"},"colorscale":[[0.0,"#440154"],[0.1111111111111111,"#482878"],[0.2222222222222222,"#3e4989"],[0.3333333333333333,"#31688e"],[0.4444444444444444,"#26828e"],[0.5555555555555556,"#1f9e89"],[0.6666666666666666,"#35b779"],[0.7777777777777778,"#6ece58"],[0.8888888888888888,"#b5de2b"],[1.0,"#fde725"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"rgb(237,237,237)"},"line":{"color":"white"}},"header":{"fill":{"color":"rgb(217,217,217)"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":1,"tickcolor":"rgb(36,36,36)","ticks":"outside"}},"colorscale":{"diverging":[[0.0,"rgb(103,0,31)"],[0.1,"rgb(178,24,43)"],[0.2,"rgb(214,96,77)"],[0.3,"rgb(244,165,130)"],[0.4,"rgb(253,219,199)"],[0.5,"rgb(247,247,247)"],[0.6,"rgb(209,229,240)"],[0.7,"rgb(146,197,222)"],[0.8,"rgb(67,147,195)"],[0.9,"rgb(33,102,172)"],[1.0,"rgb(5,48,97)"]],"sequential":[[0.0,"#440154"],[0.1111111111111111,"#482878"],[0.2222222222222222,"#3e4989"],[0.3333333333333333,"#31688e"],[0.4444444444444444,"#26828e"],[0.5555555555555556,"#1f9e89"],[0.6666666666666666,"#35b779"],[0.7777777777777778,"#6ece58"],[0.8888888888888888,"#b5de2b"],[1.0,"#fde725"]],"sequentialminus":[[0.0,"#440154"],[0.1111111111111111,"#482878"],[0.2222222222222222,"#3e4989"],[0.3333333333333333,"#31688e"],[0.4444444444444444,"#26828e"],[0.5555555555555556,"#1f9e89"],[0.6666666666666666,"#35b779"],[0.7777777777777778,"#6ece58"],[0.8888888888888888,"#b5de2b"],[1.0,"#fde725"]]},"colorway":["#1F77B4","#FF7F0E","#2CA02C","#D62728","#9467BD","#8C564B","#E377C2","#7F7F7F","#BCBD22","#17BECF"],"font":{"color":"rgb(36,36,36)"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"white","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"white","polar":{"angularaxis":{"gridcolor":"rgb(232,232,232)","linecolor":"rgb(36,36,36)","showgrid":false,"showline":true,"ticks":"outside"},"bgcolor":"white","radialaxis":{"gridcolor":"rgb(232,232,232)","linecolor":"rgb(36,36,36)","showgrid":false,"showline":true,"ticks":"outside"}},"scene":{"xaxis":{"backgroundcolor":"white","gridcolor":"rgb(232,232,232)","gridwidth":2,"linecolor":"rgb(36,36,36)","showbackground":true,"showgrid":false,"showline":true,"ticks":"outside","zeroline":false,"zerolinecolor":"rgb(36,36,36)"},"yaxis":{"backgroundcolor":"white","gridcolor":"rgb(232,232,232)","gridwidth":2,"linecolor":"rgb(36,36,36)","showbackground":true,"showgrid":false,"showline":true,"ticks":"outside","zeroline":false,"zerolinecolor":"rgb(36,36,36)"},"zaxis":{"backgroundcolor":"white","gridcolor":"rgb(232,232,232)","gridwidth":2,"linecolor":"rgb(36,36,36)","showbackground":true,"showgrid":false,"showline":true,"ticks":"outside","zeroline":false,"zerolinecolor":"rgb(36,36,36)"}},"shapedefaults":{"fillcolor":"black","line":{"width":0},"opacity":0.3},"ternary":{"aaxis":{"gridcolor":"rgb(232,232,232)","linecolor":"rgb(36,36,36)","showgrid":false,"showline":true,"ticks":"outside"},"baxis":{"gridcolor":"rgb(232,232,232)","linecolor":"rgb(36,36,36)","showgrid":false,"showline":true,"ticks":"outside"},"bgcolor":"white","caxis":{"gridcolor":"rgb(232,232,232)","linecolor":"rgb(36,36,36)","showgrid":false,"showline":true,"ticks":"outside"}},"title":{"x":0.05},"xaxis":{"automargin":true,"gridcolor":"rgb(232,232,232)","linecolor":"rgb(36,36,36)","showgrid":false,"showline":true,"ticks":"outside","title":{"standoff":15},"zeroline":false,"zerolinecolor":"rgb(36,36,36)"},"yaxis":{"automargin":true,"gridcolor":"rgb(232,232,232)","linecolor":"rgb(36,36,36)","showgrid":false,"showline":true,"ticks":"outside","title":{"standoff":15},"zeroline":false,"zerolinecolor":"rgb(36,36,36)"}}},"xaxis":{"showgrid":true},"yaxis":{"showgrid":true,"title":{"text":"Frequency"}},"title":{"font":{"size":22,"color":"Black"},"text":"<b>Topics over Time","y":0.95,"x":0.4,"xanchor":"center","yanchor":"top"},"hoverlabel":{"font":{"size":16,"family":"Rockwell"},"bgcolor":"white"},"width":1250,"height":450,"legend":{"title":{"text":"<b>Global Topic Representation"}}},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('452e784c-90dc-4825-a117-29bb01d851af');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


<code>We saved the topics over time as an image in case the BERTopic visualization of topics overtime doesn't work, as it is an interactive plot. This way, we can still view and analyze the trends in the topics over time even if the interactive plot is not functioning properly. </code>


```python
from IPython.display import display
from PIL import Image

# Read the image file into memory using the Image class
image = Image.open("assets/topics-over-time.png")

# Display the image
display(image)
```


    
![png](output_72_0.png)
    


We can see that there was a significant increase in the number of reviews discussing VR technology and the Meta Quest 2 headset (topic 0) and the product being purchased as a gift, particularly for Christmas (topic 1) in the period from December 2021 to February 2022. This could suggest that the VR headset was a popular gift during the holiday season and that there was an overall increase in interest in the product during this time. The other topics also experienced a peak in this time period, but not to the same extent as topics 0 and 1, suggesting that they may not have been as central to the conversations around the product during this time.

### 6.External Validation
Incorporating independent findings into our conclusions is essential for ensuring the validity and credibility of our study. By consulting external evidence, we can validate our own conclusions and provide additional support for their validity. Additionally, considering multiple perspectives and professional respectable sources can help us to better understand the concerns of the product.

According to PCMag [20], battery life is one of the main issues for standalone VR headsets, including the Meta Quest 2. CNET [21] reports that the headset has a battery life of two to three hours, which may not be sufficient for longer play sessions. Techspot [22] lists the short battery life as a con of the headset, stating that it only lasts for two to three hours. Mashable [23] also notes that the battery life of the Meta Quest 2 VR headset could be longer. These findings from independent tech industry sources [20, 21, 22, 23] suggest that battery life may be a concern for users of the Meta Quest 2 VR headset.

## 7.Conclusion
Our analysis of customer reviews of the Meta Quest 2 VR headset revealed that battery life was a common concern among users. Upon conducting sentiment analysis on this topic, we observed a decline in positive sentiments and an increase in neutral and negative sentiments in the topic about battery. This trend suggests that the battery lifespan of the Meta Quest 2 VR headset may be perceived as short by users. To further confirm our findings, we consulted multiple well-respected tech industry sources, including PCMag [20], CNET [21], Techspot [22], and Mashable [23], which all identified battery life as a common drawback of the Meta Quest 2 VR headset. 

<p> In summary, our study suggests that the battery lifespan of the Meta Quest 2 VR headset is a potential area for improvement. as supported by both our analysis on the customer reviews and independent sources </p>

## 8.Future Work
<ul>
    <li> Explore other neural models for keyword extraction and compare their performance to the KeyBERT model </li>
    <li> Investigate the effectiveness of the extracted keywords for applications such as text summarization </li>
    <li> Apply Time-series Analysis to see the relationship between sentiment over time </li>
</ul> 


# 9.References and Resources
### 9.1.Report

#### References
- Dr.Sean 

#### General
- [1] Sentiment analysis: Why it's necessary and how it improves CX from https://www.techtarget.com/searchcustomerexperience/tip/Sentiment-analysis-Why-its-necessary-and-how-it-improves-CX 
- [2] Meta Quest 2 Good price for value from https://arstechnica.com/gaming/2022/07/despite-100-price-increase-meta-quest-2-still-offers-historically-cheap-vr/
- [3] Sentiment Analysis definition from https://en.wikipedia.org/wiki/Sentiment_analysis
- [4] Topic modelling definition from https://en.wikipedia.org/wiki/Topic_model
- [7] Selenium definition from https://www.guru99.com/introduction-to-selenium.html
- [8] BERTopic definition from  https://spacy.io/universe/project/bertopic
- [9] BERTopic topic outlier https://maartengr.github.io/BERTopic/faq.html
- [10] KeyBERT about from https://maartengr.github.io/KeyBERT/

####  Ethical considerations 
- [5] Argos terms and conditions from https://www.argos.co.uk/help/terms-and-conditions/
- [6] Argos robots.txt from https://www.argos.co.uk/robots.txt

#### Conclusion

- [20] PCMag Oculus Quest 2 review from https://www.pcmag.com/reviews/oculus-quest-2 </br>
- [21] CNET Oculus Quest 2 review from https://www.cnet.com/tech/gaming/facebook-oculus-quest-2-vr-review-one-of-my-favorite-game-consoles/ </br>
- [22] Techspot Oculus Quest 2 review from https://www.techspot.com/products/audio-video/oculus-quest-2.224801/ </br>
- [23] Mashable Oculus Quest 2 review from https://mashable.com/review/oculus-quest-2-review </br>

### 9.2.Code
#### General
- [9] Lambda function with pandas DataFrame from : www.geeksforgeeks.org/applying-lambda-functions-to-pandas-dataframe/

#### Web Scraping 
- Dr.Sean Lab
- [11] Selenium waits from https://selenium-python.readthedocs.io/waits.html
- [12] Using lambda function with Pandas DataFrames from https://pandas.pydata.org/pandas-docs/stable/user_guide/apply.html
- [13] Worked examples of lambda function from https://sparkbyexamples.com/pandas/pandas-apply-with-lambda-examples/

#### Data and Text Preprocessing 
- [6] Converting string to datetime format and object inspired from https://docs.python.org/3/library/datetime.html#strftime-strptime-behavior
- [6] Removing special charactres and punctuations code inspired from https://stackoverflow.com/questions/18429143/strip-punctuation-with-regex-python 
- Dr.Sean Lab 5 
- [6] Removing stop words inspired from https://www.geeksforgeeks.org/removing-stop-words-nltk-python/
- [6] Lemmatizing using NLTK from https://www.geeksforgeeks.org/python-lemmatization-with-nltk/

#### Sentiment Analysis
- Sentiment analysis refrence from "Python Natural Language Processing" by Jacob Perkins (Chapter 3, "Sentiment Analysis")
- [14] Sentiment Analysis using Vader from https://www.nltk.org/api/nltk.sentiment.vader.html </br>
- [14] Sentiment Analysis calculatuing compound score from https://github.com/cjhutto/vaderSentiment#about-the-scoring

#### Topic Modelling
- Topic Modelling with BERT from https://towardsdatascience.com/topic-modeling-with-bert-779f7db187e6
- Dinensionality reduction from https://en.wikipedia.org/wiki/Dimensionality_reduction
- [10] BERTopic from https://spacy.io/universe/project/bertopic
- [10] BERTopic, Getting the same results https://maartengr.github.io/BERTopic/faq.html#why-are-the-results-not-consistent-between-runs
- [10] BERTopic, Calculate topics probability from https://maartengr.github.io/BERTopic/faq.html#how-do-i-calculate-the-probabilities-of-all-topics-in-a-document

#### Visualization
- BERTopic Visualization from https://maartengr.github.io/BERTopic/getting_started/visualization/visualization.html
