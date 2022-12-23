# Sentiment Analysis and Topic Modeling of Meta Quest 2 Product Reviews
<b> Abstract: </b> </br>
This study aims to analyze the sentiment and identify the main topics discussed in Meta Quest 2 product reviews scraped from the Argos website. To achieve this goal, we first preprocessed the reviews by removing unwanted characters and applying text normalization techniques. Then, we applied sentiment analysis using a machine learning classifier to classify the reviews into positive, negative, and neutral categories. Finally, we used topic modeling to identify the main themes discussed in the reviews. The results of the sentiment analysis showed that a majority of the reviews were positive, while the topic modeling revealed that the main topics discussed included the product's features, gameplay, and overall satisfaction. We also visualized the results using word clouds and bar plots. This study provides valuable insights into the opinions and experiences of Meta Quest 2 customers and can help the manufacturer to improve the product.

</br>
<b> Introduction </b> </br>
Sentiment analysis and topic modelling are two important techniques in natural language processing (NLP) that have gained significant attention in recent years due to their potential applications in various fields such as marketing, customer service, and social media analysis. Sentiment analysis aims to identify the emotional state of the writer or speaker, while topic modelling is a method of uncovering the hidden structure of a large and complex text dataset by discovering the underlying topics and themes. 

In this study, we conducted sentiment analysis and topic modelling on product reviews of Meta Quest 2 VR, a virtual reality game for the PlayStation 4 console. The reviews were scraped from the Argos website using Selenium, a web automation tool. The data preprocessing steps included removing special characters, punctuations, and stop words, as well as tokenizing the reviews.

For sentiment analysis, we used the NLTK vader library, which is a pre-trained model that uses a lexicon of words and emojis to identify the sentiment of a text as positive, negative, or neutral. For topic modelling, we employed keyBERT, a transformer-based model trained on a large corpus of scientific articles and capable of extracting relevant keywords and themes from the text.

To visualize the results of our analysis, we created line charts, word clouds, and bar plots using various Python libraries such as Matplotlib and Wordcloud.

Overall, this study provides insights into the sentiments and themes expressed by the Meta Quest 2 VR customers, which can be useful for the game developers and marketers to understand the opinions and preferences of their target audience.

