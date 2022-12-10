---
layout: page
title: Sentiment Analysis
description: This lesson uses Sentiment Analysis.
---

# Sentiment Analysis

Source: https://programminghistorian.org/en/lessons/sentiment-analysis

## Reflection

In this lesson, I learned how to conduct "sentiment analysis" on texts and how to interpret the results. It was fun working on the natural language processing tools in a way different from how we learned about the package in class.

One of the exciting things about the distribution scores is that they are based on a percentile. The program does not use a larger number if the words are more sentimentally loaded (regardless of the meaning or direction). For example, I could write, "I vigorously dashed to the store" or "I ran to the store." The first one is much less neutral so the neutral value would be lower. The second example would be a much more neutral sentence with a near-perfect neutral rating. However, both scores would add up to 1. This method discredits loaded texts. Although the system can understand whether something is overall neutral, positive, or negative, it fails to understand the total weight of a sentence. 

This program would benefit someone in HR when analyzing large numbers of emails. If a particular individual is sending emails with very high negativity ratings, it would be reasonable grounds to read some of these emails to see whether they are treating their staff correctly. 

This program is not very useful in an academic setting aside from being used for distant reading things nobody wants to read. For example, I could take a body of authors with all their works. I could run this sentiment analysis over the entire corpus and find which authors are the least optimistic. There may be a correlation between time period, political status, or socioeconomic status and positivity. This question would be very interesting. If the sentiment analysis algorithm aligns with our current thoughts about our authors, it would be good evidence for the program's effectiveness.

## Getting Started with NLTK


```python
import nltk
nltk.download('vader_lexicon')
nltk.download('punkt')
```

    [nltk_data] Downloading package vader_lexicon to
    [nltk_data]     /Users/chris/nltk_data...
    [nltk_data]   Package vader_lexicon is already up-to-date!
    [nltk_data] Downloading package punkt to /Users/chris/nltk_data...
    [nltk_data]   Package punkt is already up-to-date!





    True



## Calculate Sentiment for a Paragraph


```python
from nltk.sentiment.vader import SentimentIntensityAnalyzer
```


```python
sid = SentimentIntensityAnalyzer()
```


```python
message_text = '''Like you, I am getting very frustrated with this process. I am genuinely trying to be as reasonable as possible. I am not trying to "hold up" the deal at the last minute. I'm afraid that I am being asked to take a fairly large leap of faith after this company (I don't mean the two of you -- I mean Enron) has screwed me and the people who work for me.'''
```


```python
print(message_text)

# Calling the polarity_scores method on sid and passing in the message_text outputs a dictionary with negative, neutral, positive, and compound scores for the input text
scores = sid.polarity_scores(message_text)
```

    Like you, I am getting very frustrated with this process. I am genuinely trying to be as reasonable as possible. I am not trying to "hold up" the deal at the last minute. I'm afraid that I am being asked to take a fairly large leap of faith after this company (I don't mean the two of you -- I mean Enron) has screwed me and the people who work for me.



```python
for key in sorted(scores):
        print('{0}: {1}, '.format(key, scores[key]), end='')
```

    compound: -0.3804, neg: 0.093, neu: 0.836, pos: 0.071, 

## Determine Appropriate Scope for E-mail


```python
import nltk.data
from nltk.sentiment.vader import SentimentIntensityAnalyzer
from nltk import sentiment
from nltk import word_tokenize

sid = SentimentIntensityAnalyzer()

tokenizer = nltk.data.load('tokenizers/punkt/english.pickle')

message_text = '''It seems to me we are in the middle of no man's land with respect to the  following:  Opec production speculation, Mid east crisis and renewed  tensions, US elections and what looks like a slowing economy (?), and no real weather anywhere in the world. I think it would be most prudent to play  the markets from a very flat price position and try to day trade more aggressively. I have no intentions of outguessing Mr. Greenspan, the US. electorate, the Opec ministers and their new important roles, The Israeli and Palestinian leaders, and somewhat importantly, Mother Nature.  Given that, and that we cannot afford to lose any more money, and that Var seems to be a problem, let's be as flat as possible. I'm ok with spread risk  (not front to backs, but commodity spreads). The morning meetings are not inspiring, and I don't have a real feel for  everyone's passion with respect to the markets.  As such, I'd like to ask  John N. to run the morning meetings on Mon. and Wed.  Thanks. Jeff'''

sentences = tokenizer.tokenize(message_text)

for sentence in sentences:
        print(sentence)
        scores = sid.polarity_scores(sentence)
        for key in sorted(scores):
                print('{0}: {1}, '.format(key, scores[key]), end='')
        print()

```

    It seems to me we are in the middle of no man's land with respect to the  following:  Opec production speculation, Mid east crisis and renewed  tensions, US elections and what looks like a slowing economy (?
    compound: -0.5267, neg: 0.197, neu: 0.68, pos: 0.123, 
    ), and no real weather anywhere in the world.
    compound: -0.296, neg: 0.216, neu: 0.784, pos: 0.0, 
    I think it would be most prudent to play  the markets from a very flat price position and try to day trade more aggressively.
    compound: 0.0183, neg: 0.103, neu: 0.792, pos: 0.105, 
    I have no intentions of outguessing Mr. Greenspan, the US.
    compound: -0.296, neg: 0.216, neu: 0.784, pos: 0.0, 
    electorate, the Opec ministers and their new important roles, The Israeli and Palestinian leaders, and somewhat importantly, Mother Nature.
    compound: 0.4228, neg: 0.0, neu: 0.817, pos: 0.183, 
    Given that, and that we cannot afford to lose any more money, and that Var seems to be a problem, let's be as flat as possible.
    compound: -0.1134, neg: 0.097, neu: 0.823, pos: 0.081, 
    I'm ok with spread risk  (not front to backs, but commodity spreads).
    compound: -0.0129, neg: 0.2, neu: 0.679, pos: 0.121, 
    The morning meetings are not inspiring, and I don't have a real feel for  everyone's passion with respect to the markets.
    compound: 0.5815, neg: 0.095, neu: 0.655, pos: 0.25, 
    As such, I'd like to ask  John N. to run the morning meetings on Mon.
    compound: 0.3612, neg: 0.0, neu: 0.848, pos: 0.152, 
    and Wed.
    compound: 0.0, neg: 0.0, neu: 1.0, pos: 0.0, 
    Thanks.
    compound: 0.4404, neg: 0.0, neu: 0.0, pos: 1.0, 
    Jeff
    compound: 0.0, neg: 0.0, neu: 1.0, pos: 0.0, 



```python

```
