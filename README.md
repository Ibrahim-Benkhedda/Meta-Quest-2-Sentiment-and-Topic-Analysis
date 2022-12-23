# Sentiment Analysis and Topic Modeling of Meta Quest 2 Product Reviews
<b> Abstract: </b> </br>
This study aims to analyze the sentiment and identify the main topics discussed in Meta Quest 2 product reviews scraped from the Argos website. To achieve this goal, we first preprocessed the reviews by removing unwanted characters and applying text normalization techniques. Then, we applied sentiment analysis using a machine learning classifier to classify the reviews into positive, negative, and neutral categories. Finally, we used topic modeling to identify the main themes discussed in the reviews. The results of the sentiment analysis showed that a majority of the reviews were positive, while the topic modeling revealed that the main topics discussed included the product's features, gameplay, and overall satisfaction. We also visualized the results using word clouds and bar plots. This study provides valuable insights into the opinions and experiences of Meta Quest 2 customers and can help the manufacturer to improve the product.

</br>
<b> Introduction </b> </br>
Sentiment analysis and topic modelling are two important techniques in natural language processing (NLP) that have gained significant attention in recent years due to their potential applications in various fields such as marketing, customer service, and social media analysis. Sentiment analysis aims to identify the emotional state of the writer or speaker, while topic modelling is a method of uncovering the hidden structure of a large and complex text dataset by discovering the underlying topics and themes. </br>

In this study, we conducted sentiment analysis and topic modelling on product reviews of Meta Quest 2 VR, a virtual reality game for the PlayStation 4 console. The reviews were scraped from the Argos website using Selenium, a web automation tool. The data preprocessing steps included removing special characters, punctuations, and stop words, as well as tokenizing the reviews.

For sentiment analysis, we used the NLTK vader library, which is a pre-trained model that uses a lexicon of words and emojis to identify the sentiment of a text as positive, negative, or neutral. For topic modelling, we employed keyBERT, a transformer-based model trained on a large corpus of scientific articles and capable of extracting relevant keywords and themes from the text.

Visualization is an important aspect of any data analysis study as it helps to present the results in a clear and concise manner and facilitate understanding and interpretation of the findings. In our study, we used various types of visualizations to represent the results of the sentiment analysis and topic modelling.

Line charts: Line charts are a useful visualization tool for showing trends over time or for comparing multiple variables. In our study, we could use line charts to show the overall sentiment trend of the Meta Quest 2 VR reviews over time, or to compare the sentiment scores of positive, negative, and neutral reviews.

Word clouds: Word clouds are a popular visualization technique that represents the frequency of words in a text dataset by displaying them in different sizes according to their importance. In our study, we could use word clouds to represent the most frequent words in the positive, negative, and neutral reviews and understand the common themes and topics mentioned by the customers.

Bar plots: Bar plots are a type of chart that displays data using horizontal or vertical bars. In our study, we could use bar plots to show the distribution of sentiments among the Meta Quest 2 VR reviews, or to compare the sentiment scores of different groups of reviews based on various criteria such as product features or customer demographics.

By using these visualization techniques, we can effectively communicate the results of our analysis and draw meaningful conclusions about the sentiments and themes expressed by the Meta Quest 2 VR customers.

Overall, this study provides insights into the sentiments and themes expressed by the Meta Quest 2 VR customers, which can be useful for the game developers and marketers to understand the opinions and preferences of their target audience.

</br>
<b> Scraping the Web for Product Reviews: A Selenium-Based Approach </b>
</br>
Web scraping is the process of extracting data from websites by using automated tools or programs. It is a useful technique for collecting large amounts of data from websites, especially when the data is not readily available for download. In this study, we used Selenium, a popular web automation tool, to scrape product reviews from the Argos website.

Selenium is an open-source library that allows developers to write scripts in various programming languages such as Python, Java, and C# to automate web browser interactions. It can simulate user actions such as clicking links, filling out forms, and navigating pages, and it can extract data from the web pages by using techniques such as web element selection, DOM parsing, and XPath queries.

For our study, we used Selenium to navigate to the product page of Meta Quest 2 VR on the Argos website and retrieve the reviews, location of the reviewer, and timestamp of the review. We wrote a Python script that used the Selenium webdriver to open a web browser, navigate to the product page, and extract the data from the page elements. We also implemented error handling and retry logic to ensure that the script could handle any issues that might arise during the scraping process, such as network errors or changes in the page structure.

Overall, the web scraping process using Selenium allowed us to efficiently collect a large number of product reviews for our study, which would have been difficult or impossible to obtain manually. It also provided us with additional metadata such as the location and timestamp of the reviews, which could be useful for further analysis and insights.

