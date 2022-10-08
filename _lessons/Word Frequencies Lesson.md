---
layout: page
title: Word Frequencies Lesson
description: This lesson uses word frequencies.
---

# Word Frequencies

## Source
[William J. Turkel and Adam Crymble, "Counting Word Frequencies with Python," Programming Historian 7 (2021), https://doi.org/10.46430/phen0078.](https://programminghistorian.org/en/lessons/counting-frequencies)

## Reflection

This is my third attempt at running a successful programming historian. This one held my hand a lot better than the other two, and it was the only one that I was able to relatively complete. Obviously, I did not figure out how to fix the obo.py issues, but I think that the skills that I developed were worth the pain. 
I learned how to count my words, break my sentences into lists (similarly to how we did these exercises in class), and count the frequencies and pairs. I think that I would have liked to understand how the teacher was applying this to the website through the lessons beforehand, but I will probably do the other programming historian lessons later. Anyways, I think this will be very useful for me if I ever decide to measure word frequencies within a text. Moreover, if I figure out how to classify certain words, it will help me see what types of words go with what. For example, I could see what words exclusively apply to gods and what words exclusively apply to humans based solely on the code that I wrote. I could make classifying lists which align with the different functions. That being said, I think this is a bit further down the line for me. Another thing that I had an issue with was quotation marks. I did not figure out how to rid the text of quotation marks. I think that looking at the different word frequencies would matter because if the program sees "Jesus" and "'Jesus" as two different words, then I am going to have issues with the statistics being squewed. I would like to learn how to remedy this issue in the future.

## Code


```python
# count-list-items-1.py

wordstring = 'And I looked back at the footprints in the sand asking, "Jesus, where were you in my time of need?" '
wordstring += 'And He said, "Bruh, I carried you through all that," or something along those lines'

wordlist = wordstring.split()

wordfreq = []
for w in wordlist:
    wordfreq.append(wordlist.count(w))

print("String\n" + wordstring +"\n")
print("List\n" + str(wordlist) + "\n")
print("Frequencies\n" + str(wordfreq) + "\n")
print("Pairs\n" + str(list(zip(wordlist, wordfreq))))
```

    String
    And I looked back at the footprints in the sand asking, "Jesus, where were you in my time of need?" And He said, "Bruh, I carried you through all that," or something along those lines
    
    List
    ['And', 'I', 'looked', 'back', 'at', 'the', 'footprints', 'in', 'the', 'sand', 'asking,', '"Jesus,', 'where', 'were', 'you', 'in', 'my', 'time', 'of', 'need?"', 'And', 'He', 'said,', '"Bruh,', 'I', 'carried', 'you', 'through', 'all', 'that,"', 'or', 'something', 'along', 'those', 'lines']
    
    Frequencies
    [2, 2, 1, 1, 1, 2, 1, 2, 2, 1, 1, 1, 1, 1, 2, 2, 1, 1, 1, 1, 2, 1, 1, 1, 2, 1, 2, 1, 1, 1, 1, 1, 1, 1, 1]
    
    Pairs
    [('And', 2), ('I', 2), ('looked', 1), ('back', 1), ('at', 1), ('the', 2), ('footprints', 1), ('in', 2), ('the', 2), ('sand', 1), ('asking,', 1), ('"Jesus,', 1), ('where', 1), ('were', 1), ('you', 2), ('in', 2), ('my', 1), ('time', 1), ('of', 1), ('need?"', 1), ('And', 2), ('He', 1), ('said,', 1), ('"Bruh,', 1), ('I', 2), ('carried', 1), ('you', 2), ('through', 1), ('all', 1), ('that,"', 1), ('or', 1), ('something', 1), ('along', 1), ('those', 1), ('lines', 1)]



```python
# this time, I am doing it with list comprehension

wordstring = 'And I looked back at the footprints in the sand asking, "Jesus, where were you in my time of need?" '
wordstring += 'And He said, "Bruh, I carried you through all that," or something along those lines'
wordlist = wordstring.split()

wordfreq = [wordlist.count(w) for w in wordlist] # a list comprehension

print("String\n" + wordstring +"\n")
print("List\n" + str(wordlist) + "\n")
print("Frequencies\n" + str(wordfreq) + "\n")
print("Pairs\n" + str(list(zip(wordlist, wordfreq))))
```

    String
    And I looked back at the footprints in the sand asking, "Jesus, where were you in my time of need?" And He said, "Bruh, I carried you through all that," or something along those lines
    
    List
    ['And', 'I', 'looked', 'back', 'at', 'the', 'footprints', 'in', 'the', 'sand', 'asking,', '"Jesus,', 'where', 'were', 'you', 'in', 'my', 'time', 'of', 'need?"', 'And', 'He', 'said,', '"Bruh,', 'I', 'carried', 'you', 'through', 'all', 'that,"', 'or', 'something', 'along', 'those', 'lines']
    
    Frequencies
    [2, 2, 1, 1, 1, 2, 1, 2, 2, 1, 1, 1, 1, 1, 2, 2, 1, 1, 1, 1, 2, 1, 1, 1, 2, 1, 2, 1, 1, 1, 1, 1, 1, 1, 1]
    
    Pairs
    [('And', 2), ('I', 2), ('looked', 1), ('back', 1), ('at', 1), ('the', 2), ('footprints', 1), ('in', 2), ('the', 2), ('sand', 1), ('asking,', 1), ('"Jesus,', 1), ('where', 1), ('were', 1), ('you', 2), ('in', 2), ('my', 1), ('time', 1), ('of', 1), ('need?"', 1), ('And', 2), ('He', 1), ('said,', 1), ('"Bruh,', 1), ('I', 2), ('carried', 1), ('you', 2), ('through', 1), ('all', 1), ('that,"', 1), ('or', 1), ('something', 1), ('along', 1), ('those', 1), ('lines', 1)]



```python
# now I am going to look through my python dictionary, similarly to what we did in class
Chris = 'maybe a top 40 student in his section of comp5'
print(Chris[0])
```

    m



```python
print(Chris[5])
```

     



```python
print(Chris[6])
```

    a



```python
chris_list = ['maybe', 'a', 'top', '40', 'student', 'in', 'his', 'section', 'of', 'comp5']
print(chris_list[4])
```

    student



```python
print(chris_list[0][1])
```

    a



```python
d = {'world': 1, 'hello':0}
print(d['hello'])
```

    0



```python
print(d['world'])
```

    1



```python
# I don't know why my result is different from the one on the website because we have the same input
print(d.keys())
```

    dict_keys(['world', 'hello'])


### Word Frequency Pairs


```python
def wordListToFreqDict(wordlist):
    wordfreq = [wordlist.count(p) for p in wordlist]
    return dict(list(zip(wordlist,freq)))
```


```python
def sortFreqDict(freqdict):
    aux = [(freqdict[key], key) for key in freqdict]
    aux.sort()
    aux.reverse()
    return aux
```


```python
import urllib.request, urllib.error, urllib.parse, obo
```


    ---------------------------------------------------------------------------

    ModuleNotFoundError                       Traceback (most recent call last)

    Input In [36], in <cell line: 1>()
    ----> 1 import urllib.request, urllib.error, urllib.parse, obo


    ModuleNotFoundError: No module named 'obo'



```python
url = 'http://www.oldbaileyonline.org/browse.jsp?id=t17800628-33&div=t17800628-33'

response = urllib.request.urlopen(url)
html = response.read().decode('UTF-8')
text = obo.stripTags(html).lower()
wordlist = obo.stripNonAlphaNum(text)
dictionary = obo.wordListToFreqDict(wordlist)
sorteddict = obo.sortFreqDict(dictionary)

for s in sorteddict: print(str(s))
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    Input In [29], in <cell line: 5>()
          3 response = urllib.request.urlopen(url)
          4 html = response.read().decode('UTF-8')
    ----> 5 text = obo.stripTags(html).lower()
          6 wordlist = obo.stripNonAlphaNum(text)
          7 dictionary = obo.wordListToFreqDict(wordlist)


    NameError: name 'obo' is not defined



```python
#html-to-freq.py

import urllib.request, urllib.error, urllib.parse, obo

url = 'http://www.oldbaileyonline.org/browse.jsp?id=t17800628-33&div=t17800628-33'

response = urllib.request.urlopen(url)
html = response.read().decode('UTF-8')
text = obo.stripTags(html).lower()
wordlist = obo.stripNonAlphaNum(text)
dictionary = obo.wordListToFreqDict(wordlist)
sorteddict = obo.sortFreqDict(dictionary)

for s in sorteddict: print(str(s))
```


    ---------------------------------------------------------------------------

    ModuleNotFoundError                       Traceback (most recent call last)

    Input In [32], in <cell line: 3>()
          1 #html-to-freq.py
    ----> 3 import urllib.request, urllib.error, urllib.parse, obo
          5 url = 'http://www.oldbaileyonline.org/browse.jsp?id=t17800628-33&div=t17800628-33'
          7 response = urllib.request.urlopen(url)


    ModuleNotFoundError: No module named 'obo'



```python
# I really tried with this one, but I could not load the package. I think this was something covered in the previous lessons from this person, but I did not do have time to do them
```

### Removing Stop Words


```python
#this is my list of stop words, but I cannot add it to obo.py because I do not know how to make that
stopwords = ['a', 'about', 'above', 'across', 'after', 'afterwards']
stopwords += ['again', 'against', 'all', 'almost', 'alone', 'along']
stopwords += ['already', 'also', 'although', 'always', 'am', 'among']
stopwords += ['amongst', 'amoungst', 'amount', 'an', 'and', 'another']
stopwords += ['any', 'anyhow', 'anyone', 'anything', 'anyway', 'anywhere']
stopwords += ['are', 'around', 'as', 'at', 'back', 'be', 'became']
stopwords += ['because', 'become', 'becomes', 'becoming', 'been']
stopwords += ['before', 'beforehand', 'behind', 'being', 'below']
stopwords += ['beside', 'besides', 'between', 'beyond', 'bill', 'both']
stopwords += ['bottom', 'but', 'by', 'call', 'can', 'cannot', 'cant']
stopwords += ['co', 'computer', 'con', 'could', 'couldnt', 'cry', 'de']
stopwords += ['describe', 'detail', 'did', 'do', 'done', 'down', 'due']
stopwords += ['during', 'each', 'eg', 'eight', 'either', 'eleven', 'else']
stopwords += ['elsewhere', 'empty', 'enough', 'etc', 'even', 'ever']
stopwords += ['every', 'everyone', 'everything', 'everywhere', 'except']
stopwords += ['few', 'fifteen', 'fifty', 'fill', 'find', 'fire', 'first']
stopwords += ['five', 'for', 'former', 'formerly', 'forty', 'found']
stopwords += ['four', 'from', 'front', 'full', 'further', 'get', 'give']
stopwords += ['go', 'had', 'has', 'hasnt', 'have', 'he', 'hence', 'her']
stopwords += ['here', 'hereafter', 'hereby', 'herein', 'hereupon', 'hers']
stopwords += ['herself', 'him', 'himself', 'his', 'how', 'however']
stopwords += ['hundred', 'i', 'ie', 'if', 'in', 'inc', 'indeed']
stopwords += ['interest', 'into', 'is', 'it', 'its', 'itself', 'keep']
stopwords += ['last', 'latter', 'latterly', 'least', 'less', 'ltd', 'made']
stopwords += ['many', 'may', 'me', 'meanwhile', 'might', 'mill', 'mine']
stopwords += ['more', 'moreover', 'most', 'mostly', 'move', 'much']
stopwords += ['must', 'my', 'myself', 'name', 'namely', 'neither', 'never']
stopwords += ['nevertheless', 'next', 'nine', 'no', 'nobody', 'none']
stopwords += ['noone', 'nor', 'not', 'nothing', 'now', 'nowhere', 'of']
stopwords += ['off', 'often', 'on','once', 'one', 'only', 'onto', 'or']
stopwords += ['other', 'others', 'otherwise', 'our', 'ours', 'ourselves']
stopwords += ['out', 'over', 'own', 'part', 'per', 'perhaps', 'please']
stopwords += ['put', 'rather', 're', 's', 'same', 'see', 'seem', 'seemed']
stopwords += ['seeming', 'seems', 'serious', 'several', 'she', 'should']
stopwords += ['show', 'side', 'since', 'sincere', 'six', 'sixty', 'so']
stopwords += ['some', 'somehow', 'someone', 'something', 'sometime']
stopwords += ['sometimes', 'somewhere', 'still', 'such', 'system', 'take']
stopwords += ['ten', 'than', 'that', 'the', 'their', 'them', 'themselves']
stopwords += ['then', 'thence', 'there', 'thereafter', 'thereby']
stopwords += ['therefore', 'therein', 'thereupon', 'these', 'they']
stopwords += ['thick', 'thin', 'third', 'this', 'those', 'though', 'three']
stopwords += ['three', 'through', 'throughout', 'thru', 'thus', 'to']
stopwords += ['together', 'too', 'top', 'toward', 'towards', 'twelve']
stopwords += ['twenty', 'two', 'un', 'under', 'until', 'up', 'upon']
stopwords += ['us', 'very', 'via', 'was', 'we', 'well', 'were', 'what']
stopwords += ['whatever', 'when', 'whence', 'whenever', 'where']
stopwords += ['whereafter', 'whereas', 'whereby', 'wherein', 'whereupon']
stopwords += ['wherever', 'whether', 'which', 'while', 'whither', 'who']
stopwords += ['whoever', 'whole', 'whom', 'whose', 'why', 'will', 'with']
stopwords += ['within', 'without', 'would', 'yet', 'you', 'your']
stopwords += ['yours', 'yourself', 'yourselves']
```


```python
def removeStopwords(wordlist, stopwords):
    return [w for w in wordlist if w not in stopwords]
```

### Putting it all together


```python
import urllib.request, urllib.error, urllib.parse
import obo

url = 'http://www.oldbaileyonline.org/browse.jsp?id=t17800628-33&div=t17800628-33'

response = urllib.request.urlopen(url)
html = response.read().decode('UTF-8')
text = obo.stripTags(html).lower()
fullwordlist = obo.stripNonAlphaNum(text)
wordlist = obo.removeStopwords(fullwordlist, obo.stopwords)
dictionary = obo.wordListToFreqDict(wordlist)
sorteddict = obo.sortFreqDict(dictionary)

for s in sorteddict: print(str(s))
```


    ---------------------------------------------------------------------------

    ModuleNotFoundError                       Traceback (most recent call last)

    Input In [42], in <cell line: 2>()
          1 import urllib.request, urllib.error, urllib.parse
    ----> 2 import obo
          4 url = 'http://www.oldbaileyonline.org/browse.jsp?id=t17800628-33&div=t17800628-33'
          6 response = urllib.request.urlopen(url)


    ModuleNotFoundError: No module named 'obo'



```python
# once again, I think that this is another issue with obo.py and me not knowing how to make it
```


```python

```
