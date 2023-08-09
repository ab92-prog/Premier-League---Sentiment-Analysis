# Premier-League---Sentiment-Analysis
I have scrapped data from news API on Premier League News articles few days ago . I have tried to create a sentiment analysis model.
## Sentiment Analysis of News Articles about Premier League using TextBlob

This code snippet demonstrates how to perform sentiment analysis on a collection of news articles related to the "Premier League". We use the TextBlob library for sentiment analysis and the NewsAPI to gather the articles.

### Code Explanation

1. **Import Required Libraries:**

```python
import requests
import re
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from nltk.stem import WordNetLemmatizer
from textblob import TextBlob
import matplotlib.pyplot as plt
```

2. **Define NewsAPI Endpoint and Parameters:**

```python
url = "https://newsapi.org/v2/everything"
params = {
    "q": "Premier League",
    "language": "en",
    "sortBy": "relevancy",
    "apiKey": "YOUR_NEWSAPI_API_KEY"
}
```

3. **Make a Request to NewsAPI:**

```python
response = requests.get(url, params=params)
articles = response.json()["articles"]
```

4. **Preprocess Text:**

```python
def preprocess_text(text):
    text = text.lower()
    text = re.sub(r"[^a-zA-Z0-9\s]", "", text)
    text = re.sub(r"\s+", " ", text)
    words = word_tokenize(text)
    words = [word for word in words if word not in stopwords.words("english")]
    lemmatizer = WordNetLemmatizer()
    words = [lemmatizer.lemmatize(word) for word in words]
    preprocessed_text = " ".join(words)
    return preprocessed_text

preprocessed_articles = []
for article in articles:
    text = article["description"]
    preprocessed_text = preprocess_text(text)
    preprocessed_articles.append(preprocessed_text)
```

5. **Perform Sentiment Analysis:**

```python
sentiment_scores = []
for article in preprocessed_articles:
    blob = TextBlob(article)
    sentiment_scores.append(blob.sentiment.polarity)
```

6. **Visualize Sentiment Scores:**

```python
article_labels = [f"Article {i+1}" for i in range(len(sentiment_scores))]
plt.bar(article_labels, sentiment_scores)
plt.title("Sentiment Scores for News Articles")
plt.xlabel("Article")
plt.ylabel("Sentiment Score")
plt.show()
```

This code snippet demonstrates sentiment analysis using TextBlob on a set of news articles related to the Premier League. By visualizing the sentiment scores, you can quickly gauge the emotional tone of the articles.

Remember to replace `YOUR_NEWSAPI_API_KEY` with your actual NewsAPI API key.

---

Feel free to incorporate this code explanation into your README file to help others understand how to perform sentiment analysis on news articles related to the Premier League using TextBlob and NewsAPI data.
