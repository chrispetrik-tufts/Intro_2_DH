---
layout: page
title: Parsing TEI Document Assignment
description: Assignment for TEI
---

# Parsing a TEI Document - Assignment

## Instructions

1. Parse the tei text of Gibbon's _Decline and Fall_ as found in `gibbon.xml`.
2. Extract all the footnotes and remove extraneous white space.
3. Place footnotes in a dataframe.
4. Save the dataframe as a csv file.

## Parsing TEI


```python
# imports
from bs4 import BeautifulSoup
import re
import pandas as pd
```


```python
# load xml file
with open('../in-class/gibbon.xml', encoding='utf8', mode='r') as f:
    tei_string = f.read()
```


```python
# use BeatifulSoup to instntiate tei object
tei_object = BeautifulSoup(tei_string)
```


```python
# find all foot notes
foot_notes = tei_object.find_all('note', attrs={'place': 'bottom'})
```


```python
# clean margin notes and add to a list
clean_foot_notes = []
for foot_note in foot_notes:
    foot_note = re.sub(r'[\ \n]{2,}', '', foot_note.text)  # remove excess space
    clean_foot_notes.append(foot_note)
```


```python
# convert list to dataframe
foot_notes_df = pd.DataFrame(clean_foot_notes)
```


```python
# check dataframe
foot_notes_df.head()
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
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>\nPons Aureoli,thirteen miles from Bergamo, an...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>On the death of Gallienus, ſee Trebellius Poll...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Some ſuppoſed him, oddly enough, to be a baſta...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>\nNotoria,a periodical and official diſpatch w...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Hiſt. Auguſt. p. 208. Gallienus deſcribes the ...</td>
    </tr>
  </tbody>
</table>
</div>




```python
# save datafram as csv
foot_notes_df.to_csv('foot_notes.csv')
```


```python

```
