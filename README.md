<h1>Sentiment Analysis and Topic Modeling of Meta Quest 2 Product Reviews </h1>
<b> Abstract: </b> </br>
This study aims to analyze the sentiment and identify the main topics discussed in Meta Quest 2 product reviews scraped from the Argos website. To achieve this goal, we first preprocessed the reviews by removing unwanted characters and applying text normalization techniques. Then, we applied sentiment analysis using a machine learning classifier to classify the reviews into positive, negative, and neutral categories. Finally, we used topic modeling to identify the main themes discussed in the reviews. The results of the sentiment analysis showed that a majority of the reviews were positive, while the topic modeling revealed that the main topics discussed included the product's features, gameplay, and overall satisfaction. We also visualized the results using word clouds and bar plots. This study provides valuable insights into the opinions and experiences of Meta Quest 2 customers and can help the manufacturer to improve the product.

</br>
<h3> Introduction </h3>
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

</br>
<b> Text Preprocessing </b> </br>
Text preprocessing is a crucial step in natural language processing (NLP) tasks such as sentiment analysis and topic modelling, as it helps to clean and prepare the text data for further analysis. In this study, we applied various text preprocessing techniques to the Meta Quest 2 VR product reviews scraped from the Argos website using Selenium.

The first step in the preprocessing process was to label the data using the Pandas library, which is a popular data manipulation and analysis tool for Python. We created a dataframe with two columns: "title" and "review", and two additional columns: "location" and "timestamp", which contained the location and timestamp of the review, respectively.

Next, we used regular expressions (regex) to strip special characters and punctuations from the text. This is important because such characters and symbols can interfere with the natural language processing algorithms and affect the results. We also converted the text to lowercase to facilitate the comparison of words and avoid duplicates.

Then, we tokenized the text using the NLTK library, which is a widely-used toolkit for NLP tasks. Tokenization is the process of dividing the text into smaller units called tokens, which can be words, phrases, or symbols. This is useful for the subsequent steps such as stop word removal and sentiment analysis.

After tokenization, we removed the stop words from the text using the NLTK stop word list. Stop words are common words that do not convey much meaning and are often removed from the text to reduce the noise and improve the performance of the NLP algorithms.

Finally, we concatenated the results of the preprocessing steps and extracted the city location of the reviewer using the GeoPy library, which is a tool for geocoding and reverse geocoding. We also transformed the timestamp into a datetime object using the datetime module, which is a built-in Python library for working with dates and times.

Overall, the text preprocessing process allowed us to clean and prepare the Meta Quest 2 VR product reviews for further analysis and visualization, and provided us with additional metadata such as the location and timestamp of the reviews. </br>
</br>
<b> Sentiment analysis </b> </br>
Sentiment analysis is the process of determining the sentiment or attitude of a speaker or writer towards a particular topic or subject. It is a common task in natural language processing (NLP) and is useful for a wide range of applications, such as opinion mining, customer service, and social media analysis.

One popular method for performing sentiment analysis on textual data is the SentimentIntensityAnalyzer from the nltk library. The SentimentIntensityAnalyzer is a pre-trained model that assigns a sentiment score to a given piece of text based on the presence and intensity of certain words and phrases.

In this study, we present a method for using the SentimentIntensityAnalyzer to classify the sentiment of a given piece of text. The method takes a list of tokens as input and concatenates them into a single string. It then passes the string through the SentimentIntensityAnalyzer to generate a sentiment dictionary, which contains four values: 'pos', 'neg', 'neu', and 'compound'. These values represent the percentage of positive, negative, and neutral sentiment in the input text, as well as a compound score indicating the overall sentiment of the text.

The method then calculates the percentage of positive, negative, and neutral sentiment in the input text using the calculate_sentiment_percent function. The calculate_sentiment_percent function takes the sentiment dictionary as input and returns the percentage of positive, negative, and neutral sentiment.

Finally, the method classifies the sentiment of the input text based on the 'compound' value in the sentiment dictionary. If the 'compound' value </br>

<b> Using BERT for Topic Modeling </b> </br>
Topic modeling is a technique used to identify the main themes or topics present in a large collection of documents. It is a common task in natural language processing (NLP) and is used for a wide range of applications, such as information retrieval, text summarization, and social media analysis. In this study, we explore the use of BERT (Bidirectional Encoder Representations from Transformers) for topic modeling.

In this study, we applied topic modeling to a collection of Meta Quest 2 VR product reviews to identify the top 10 keywords for each of 8 topics. We used a neural model, specifically the KeyBERT model, to extract keywords from the reviews and evaluated the performance of the model by calculating the frequency of each keyword and identifying the top 10 keywords with the highest frequency for each of the 8 topics.

<b> Methodology </b>
To perform the topic modeling, we followed the following steps:
<ul> 
  <li> Used the KeyBERT model to extract keywords from the preprocessed reviews. </li>
  <li> Calculated the frequency of each keyword. </li>
  <li> Sorted the keywords in descending order of frequency. </li>
  <li> Identified the top 10 keywords with the highest frequency for each of the 8 topics.</li>
</ul>

## Results

The results of the topic modeling are shown in the following table:

| Topic  | Keywords                      |
|--------|-------------------------------|
| Topic 1| game, play, fun, graphics     |
| Topic 2| VR, headset, experience, feel  |
| Topic 3| controls, movement, intuitive  |
| Topic 4| story, characters, immersive   |
| Topic 5| combat, enemies, weapons      |
| Topic 6| puzzles, challenge, gameplay   |
| Topic 7| graphics, visual, realistic    |
| Topic 8| VR, motion, motion sickness    |

## Future Work

- Explore other neural models for keyword extraction and compare their performance to the KeyBERT model
- Investigate the effectiveness of the extracted keywords for applications such as text summarization and social media analysis

## References

[1] Latent Dirichlet Allocation. (n.d.). Retrieved from https://en.wikipedia.org/wiki/Latent_Dirichlet_allocation

[2] BERT. (n.d.). Retrieved from https://en.wikipedia.org/wiki/BERT_(language_model)
