# sentiment-analysis
By using sentiment analysis giving the rating
# Importing necessary libraries
import pandas as pd
from textblob import TextBlob
import matplotlib.pyplot as plt  

# Importing the CSV file
dfd = pd.read_csv("sentiment12.csv")

# Function to classify sentiment 
def classify_sentiment(text):
    polarity = TextBlob(str(text)).sentiment.polarity
    return 'Good' if polarity > 0 else 'Bad'
# Applying sentiment classification
dfd['Review'] = dfd['Comment'].apply(classify_sentiment)
# Showing the result
print(dfd[['Comment', 'Review']])
dfd.to_excel("sentiment_ratings_output.xlsx", index=False)
rating_counts = dfd['Review'].value_counts()

#showing  result in bar graph
plt.figure(figsize=(6,4))
plt.bar(rating_counts.index, rating_counts.values, color=['green', 'red'])
plt.title('Count of Good vs Bad Comments')
plt.xlabel('Rating')
plt.ylabel('Number of Comments')
plt.show()

# calculating the percentage of good or bad 
rating_counts = dfd['Review'].value_counts()
total_reviews = len(dfd)
better= rating_counts.get('Good', 0)
worst =rating_counts.get('Bad', 0)
good_percent= (better / total_reviews) * 100
bad_percent = (worst/ total_reviews) * 100
print(f"Good Reviews: {better} ({good_percent:.2f}%)")
print(f"Bad Reviews: {worst} ({bad_percent:.2f}%)")
