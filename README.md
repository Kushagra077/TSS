pip install azure-ai-textanalytics


import os
from azure.core.credentials import AzureKeyCredential
from azure.ai.textanalytics import TextAnalyticsClient

def analyze_sentiment(text):
    # Set your Azure Cognitive Services credentials
    azure_key = "YOUR_AZURE_KEY"
    azure_endpoint = "YOUR_AZURE_ENDPOINT"

    # Create a TextAnalyticsClient
    credential = AzureKeyCredential(azure_key)
    client = TextAnalyticsClient(endpoint=azure_endpoint, credential=credential)

    # Perform sentiment analysis
    response = client.analyze_sentiment([text])

    # Extract sentiment analysis summary
    sentiment = response[0].sentiment
    positive_score = response[0].confidence_scores.positive
    negative_score = response[0].confidence_scores.negative
    neutral_score = response[0].confidence_scores.neutral

    # Return sentiment analysis summary
    summary = f"Sentiment: {sentiment}\nPositive score: {positive_score}\nNegative score: {negative_score}\nNeutral score: {neutral_score}"
    return summary
text = "I love this movie!"
result = analyze_sentiment(text)
print(result)
