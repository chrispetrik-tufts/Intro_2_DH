---
layout: page
title: NER Assignment
description: Gibbon NER Assignment
---

# NER Assignment
Georeferencing automatically detected place names in Edward Gibbon's *Decline and Fall of the Roman Empire* using the Pleiades gazatteer and `spaCy`.

Your assignment this week is to output a `CSV` file of place names, frequency and coordinates, as we did in class for a chapter of Gibbon of your choice. Try to find a chapter with a lot of places as we will be turning this data into an online map next week. The steps are:

* Choose a chapter from the text
* Begin a function by parsing input text
* Create a `spaCy` dictionary of entities and frequency
* Use the Pleiaes data from class to find coordinates for each place name
* Run your function on your chosen chapter
* Save your final `CSV`
* Come to class on Monday, ready to use it


```python
# import and download any relevant data
!python -m spacy download en_core_web_sm
import pandas as pd
import spacy
import wget

import os
if not os.path.isfile('gibbon_text.csv'):
    wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/gibbon_text.csv')

import collections
```

    Collecting en-core-web-sm==3.4.1
      Downloading https://github.com/explosion/spacy-models/releases/download/en_core_web_sm-3.4.1/en_core_web_sm-3.4.1-py3-none-any.whl (12.8 MB)
    [K     |████████████████████████████████| 12.8 MB 1.6 MB/s eta 0:00:01    |█████████▋                      | 3.9 MB 1.6 MB/s eta 0:00:06
    [?25hRequirement already satisfied: spacy<3.5.0,>=3.4.0 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from en-core-web-sm==3.4.1) (3.4.2)
    Requirement already satisfied: langcodes<4.0.0,>=3.2.0 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (3.3.0)
    Requirement already satisfied: pydantic!=1.8,!=1.8.1,<1.11.0,>=1.7.4 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (1.10.2)
    Requirement already satisfied: jinja2 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.11.3)
    Requirement already satisfied: spacy-loggers<2.0.0,>=1.0.0 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (1.0.3)
    Requirement already satisfied: requests<3.0.0,>=2.13.0 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.27.1)
    Requirement already satisfied: tqdm<5.0.0,>=4.38.0 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (4.64.0)
    Requirement already satisfied: packaging>=20.0 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (21.3)
    Requirement already satisfied: murmurhash<1.1.0,>=0.28.0 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (1.0.9)
    Requirement already satisfied: preshed<3.1.0,>=3.0.2 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (3.0.8)
    Requirement already satisfied: wasabi<1.1.0,>=0.9.1 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (0.10.1)
    Requirement already satisfied: numpy>=1.15.0 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (1.21.5)
    Requirement already satisfied: setuptools in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (61.2.0)
    Requirement already satisfied: typer<0.5.0,>=0.3.0 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (0.4.2)
    Requirement already satisfied: srsly<3.0.0,>=2.4.3 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.4.5)
    Requirement already satisfied: pathy>=0.3.5 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (0.6.2)
    Requirement already satisfied: spacy-legacy<3.1.0,>=3.0.10 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (3.0.10)
    Requirement already satisfied: catalogue<2.1.0,>=2.0.6 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.0.8)
    Requirement already satisfied: thinc<8.2.0,>=8.1.0 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (8.1.5)
    Requirement already satisfied: cymem<2.1.0,>=2.0.2 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.0.7)
    Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from packaging>=20.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (3.0.4)
    Requirement already satisfied: smart-open<6.0.0,>=5.2.1 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from pathy>=0.3.5->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (5.2.1)
    Requirement already satisfied: typing-extensions>=4.1.0 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from pydantic!=1.8,!=1.8.1,<1.11.0,>=1.7.4->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (4.1.1)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (1.26.9)
    Requirement already satisfied: certifi>=2017.4.17 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2021.10.8)
    Requirement already satisfied: idna<4,>=2.5 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (3.3)
    Requirement already satisfied: charset-normalizer~=2.0.0 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.0.4)
    Requirement already satisfied: confection<1.0.0,>=0.0.1 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from thinc<8.2.0,>=8.1.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (0.0.3)
    Requirement already satisfied: blis<0.8.0,>=0.7.8 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from thinc<8.2.0,>=8.1.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (0.7.9)
    Requirement already satisfied: click<9.0.0,>=7.1.1 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from typer<0.5.0,>=0.3.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (8.0.4)
    Requirement already satisfied: MarkupSafe>=0.23 in /Users/chris/opt/anaconda3/lib/python3.9/site-packages (from jinja2->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.0.1)
    [38;5;2m✔ Download and installation successful[0m
    You can now load the package via spacy.load('en_core_web_sm')



```python
nlp = spacy.load('en_core_web_sm')

gibbon_by_chapter = pd.read_csv('gibbon_text.csv').rename(columns={'Unnamed: 0':'chapter'})

first_chapter = gibbon_by_chapter['StringText'][0]
```


```python
# any helper functions you may need
#make sure to run 'import collections'
#chapter = #some string ''
first_chapter_doc = nlp(first_chapter)
for entity in first_chapter_doc.ents:
    if (entity.label_ == 'GPE') or (entity.label_ == 'LOC'):
        print(entity.text)


def get_pleiades_id(term):
    """
    Iterates through all of the possible names in the names.csv file
    Returns None if no matched names
    """
    name_row = names.loc[names['attested_form'] == term]
    if len(name_row) == 1:
        return int(name_row.place_id.iloc[0])
    else:
        name_row = names.loc[names['romanized_form_1'] == term]
        if len(name_row) == 1:
            return int(name_row.place_id.iloc[0])
        else:
            name_row = names.loc[names['romanized_form_2'] == term]
            if len(name_row) == 1:
                return int(name_row.place_id.iloc[0])
            else:
                name_row = names.loc[names['romanized_form_3'] == term]
                if len(name_row) == 1:
                    return int(name_row.place_id.iloc[0])
                else:
                    return None
                
                
def get_lat(pl_id):
    places_row = places.loc[places['id'] == pl_id]
    if len(places_row) == 1:
        return places_row.representative_latitude.iloc[0]
    
def get_long(pl_id):
    places_row = places.loc[places['id'] == pl_id]
    if len(places_row) == 1:
        return places_row.representative_longitude.iloc[0]
    
    
gibbon_by_chapter = pd.read_csv('gibbon_text.csv').rename(columns={'Unnamed: 0':'chapter'})


nlp = spacy.load('en_core_web_sm')
```

    Rome
    Nerva
    Trajan
    Marcus Antoninus
    Rome
    Rome
    Aethiopia
    Europe
    Germany
    the Atlantic Ocean
    Euphrates
    Arabia
    Africa
    Britain
    Britain
    Boadicea
    Britain
    Ireland
    Britain
    Scotland
    Antoninus Pius
    Antoninus
    Edinburgh
    gloomy hills
    Rome
    Trajan
    the Euxine Sea
    Trajan
    Philip
    Tigris
    Armenia
    the Persian gulf
    Arabia
    India
    Bosphorus
    Colchos
    Iberia
    Albania
    Armenia
    Mesopotamia
    Assyria
    Jupiter
    Jupiter
    Armenia
    Mesopotamia
    Assyria
    Euphrates
    Trajan
    Antoninus
    Caledonia
    the Upper Egypt
    Italy
    Rome
    Antoninus
    Marcus
    Euphrates
    Europe
    Rome
    Italy
    Spain
    East
    oblong
    Rome
    Britain
    Lower
    the Upper Germany
    Noricum
    Pannonia
    Maesia
    Syria
    Egypt
    Africa
    Spain
    Italy
    Marseilles
    Mediterranean
    Italy
    Misenum
    Naples
    Liburnians
    Misenum
    Mediterranean
    Provence
    Britain
    Spain
    Europe
    Mediterranean
    the Atlantic Ocean
    Lusitania
    Baetica
    Portugal
    East
    North
    Grenada
    Andalusia
    Baetica
    Spain
    Asturias
    Biscay
    Castilles
    Murcia
    Valencia
    Catalonia
    Arragon
    Tarragona
    Rome
    Alps
    Rhine
    Ocean
    France
    Alsace
    Switzerland
    Rhine
    Liege
    Luxemburg
    Mediterranean
    Languedoc
    the Celtic Gaul
    Lugdunum
    Rhine
    Rhine
    the Lower Germany
    Britain
    England
    Wales
    Scotland
    Edinburgh
    Britain
    Brigantes
    North
    South Wales
    Norfolk
    Suffolk
    Spain
    Britain
    Hercules
    Antoninus
    Lombardy
    Italy
    Po
    Piedmont
    Romagna
    Alps
    Venice
    Italy
    Rome
    Naples
    Campania
    Naples
    Italy
    Istria
    Rome
    Illyricum
    Pannonia
    Maesia
    Thrace
    Macedonia
    Greece
    Alps
    Bavaria
    Augsburg
    Austria
    Austria
    Styria
    Carinthia
    the Lower Hungary
    Sclavonia
    Noricum
    Pannonia
    Moravia
    Austria
    Hungary
    Austria
    Illyricum
    Croatia
    Bosnia
    Maesia
    Transylvania
    Hungary
    Moldavia
    Walachia
    the Ottoman Porte
    Maesia
    Servia
    Bulgaria
    Thrace
    Macedonia
    Greece
    Hellespont
    Rome
    Macedonia
    Asia
    Thessaly
    Thebes
    Argos
    Sparta
    Athens
    Greece
    Achaia
    Europe
    Asia
    Trajan
    Mediterranean
    Euphrates
    Europe
    Asia
    Troy
    Ionia
    Bithynia
    Constantinople
    Trebizond
    Syria
    the Roman Asia
    Armenia
    Trebizond
    Asia
    Europe
    Circassia
    Mingrelia
    Alexander
    Syria
    Upper Asia
    Euphrates
    Mediterranean
    Syria
    Egypt
    the Red Sea
    Palestine
    Syria
    Wales
    Palestine
    America
    Europe
    Syria
    Euphrates
    the Red Sea
    Egypt
    Africa
    Asia
    Egypt
    Nile
    Mediterranean
    Egypt
    Barca
    Africa
    Mediterranean
    Sahara
    Africa
    Tripoli
    Algiers
    Numidia
    Jugurtha
    Numidia
    Mauritania
    Mauritania
    Tingitana
    Ocean
    Morocco
    Africa
    Africa
    Spain
    Atlantic
    Mediterranean
    Hercules
    Gibraltar
    the Mediterranean Sea
    Spain
    Great Britain
    Sardinia
    Sicily
    Greece
    Asia
    Malta
    Rome
    Antoninus
    the Western Ocean



```python
# final functions
places = pd.read_csv('places.csv')
names = pd.read_csv('names.csv')


def get_locations(chapter, output_name):
    chapter_doc = nlp(chapter)
    place_freq = collections.defaultdict(int)
    for entity in first_chapter_doc.ents:
        if (entity.label_ == 'GPE') or (entity.label_ == 'LOC'):
            place_freq[entity.text] += 1 # the utility of defaultdict!
    place_freq = dict(place_freq)
    place_freq_df = pd.DataFrame.from_dict(place_freq, orient='index').reset_index().rename(columns={'index':'place_name',0:'frequency'})
    place_freq_df['pleiades_id'] = place_freq_df['place_name'].apply(get_pleiades_id)
    place_freq_final = place_freq_df.dropna().reset_index(drop=True)
    place_freq_final['lat'] = place_freq_final['pleiades_id'].apply(get_lat)
    place_freq_final['long'] = place_freq_final['pleiades_id'].apply(get_long)
    place_freq_final.to_csv(f'{output_name}.csv')
    return place_freq_final
```


```python
# try your function out
get_locations(gibbon_by_chapter['StringText'][37], 'gibbon_chapter_38_places')
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
      <th>place_name</th>
      <th>frequency</th>
      <th>pleiades_id</th>
      <th>lat</th>
      <th>long</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rome</td>
      <td>12</td>
      <td>423025.0</td>
      <td>41.891775</td>
      <td>12.486137</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Euphrates</td>
      <td>6</td>
      <td>912849.0</td>
      <td>35.543310</td>
      <td>39.606018</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arabia</td>
      <td>2</td>
      <td>981506.0</td>
      <td>27.500000</td>
      <td>32.500000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Africa</td>
      <td>7</td>
      <td>775.0</td>
      <td>32.500000</td>
      <td>7.500000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Ireland</td>
      <td>1</td>
      <td>20487.0</td>
      <td>53.184028</td>
      <td>-7.717526</td>
    </tr>
    <tr>
      <th>5</th>
      <td>India</td>
      <td>1</td>
      <td>50004.0</td>
      <td>22.500000</td>
      <td>77.500000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Iberia</td>
      <td>1</td>
      <td>863807.0</td>
      <td>41.836468</td>
      <td>44.689138</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Caledonia</td>
      <td>1</td>
      <td>89132.0</td>
      <td>57.500000</td>
      <td>-4.500000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Misenum</td>
      <td>2</td>
      <td>432941.0</td>
      <td>40.786279</td>
      <td>14.084884</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Naples</td>
      <td>3</td>
      <td>433014.0</td>
      <td>40.839995</td>
      <td>14.252870</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Tarragona</td>
      <td>1</td>
      <td>246349.0</td>
      <td>41.116892</td>
      <td>1.258338</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Lugdunum</td>
      <td>1</td>
      <td>167717.0</td>
      <td>45.758866</td>
      <td>4.819482</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Hercules</td>
      <td>2</td>
      <td>266032.0</td>
      <td>37.500000</td>
      <td>-0.500000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Illyricum</td>
      <td>2</td>
      <td>481865.0</td>
      <td>42.427292</td>
      <td>17.965028</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Macedonia</td>
      <td>3</td>
      <td>491656.0</td>
      <td>41.250000</td>
      <td>21.750000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Augsburg</td>
      <td>1</td>
      <td>118580.0</td>
      <td>48.365463</td>
      <td>10.894765</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Thebes</td>
      <td>1</td>
      <td>541138.0</td>
      <td>38.319156</td>
      <td>23.317577</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Argos</td>
      <td>1</td>
      <td>570106.0</td>
      <td>37.631561</td>
      <td>22.719464</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Sparta</td>
      <td>1</td>
      <td>570685.0</td>
      <td>37.077905</td>
      <td>22.427298</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Athens</td>
      <td>1</td>
      <td>579885.0</td>
      <td>37.972634</td>
      <td>23.722746</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Achaia</td>
      <td>1</td>
      <td>570028.0</td>
      <td>38.102121</td>
      <td>22.224586</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Troy</td>
      <td>1</td>
      <td>550595.0</td>
      <td>39.957433</td>
      <td>26.238459</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Ionia</td>
      <td>1</td>
      <td>550597.0</td>
      <td>38.162194</td>
      <td>27.357498</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Constantinople</td>
      <td>1</td>
      <td>520998.0</td>
      <td>41.006371</td>
      <td>28.965352</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Trebizond</td>
      <td>2</td>
      <td>857359.0</td>
      <td>41.004269</td>
      <td>39.723312</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Nile</td>
      <td>1</td>
      <td>727172.0</td>
      <td>19.211409</td>
      <td>30.567330</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Algiers</td>
      <td>1</td>
      <td>295276.0</td>
      <td>36.768912</td>
      <td>3.053218</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Sardinia</td>
      <td>1</td>
      <td>472014.0</td>
      <td>39.871087</td>
      <td>8.957517</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Sicily</td>
      <td>1</td>
      <td>462492.0</td>
      <td>37.643297</td>
      <td>13.932018</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Malta</td>
      <td>1</td>
      <td>462311.0</td>
      <td>35.908887</td>
      <td>14.408042</td>
    </tr>
  </tbody>
</table>
</div>




```python
def get_attested_names(pl_id):
    attested = []
    for col in names.columns[10:14]: # all of the different name columns
        for name in names.loc[names['place_id'] == pl_id][col].to_list(): # querying dataframe 
            if not isinstance(name, float): # removing any nan values
                attested.append(name)
    return list(set(attested))
```


```python
place_freq_final = get_locations(gibbon_by_chapter['StringText'][37], 'gibbon_chapter_38_places')
place_freq_final[f'attested_names'] = place_freq_final[f'pleiades_id'].apply(get_attested_names)
```


```python
place_freq_final
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
      <th>place_name</th>
      <th>frequency</th>
      <th>pleiades_id</th>
      <th>lat</th>
      <th>long</th>
      <th>attested_names</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rome</td>
      <td>12</td>
      <td>423025.0</td>
      <td>41.891775</td>
      <td>12.486137</td>
      <td>[Ῥώμῃ, Rhṓmē, Rome, Roma, Rōma, Rhome]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Euphrates</td>
      <td>6</td>
      <td>912849.0</td>
      <td>35.543310</td>
      <td>39.606018</td>
      <td>[Εὐφράτης, Nahr el-Furat, Fırat Nehri, al-Furā...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arabia</td>
      <td>2</td>
      <td>981506.0</td>
      <td>27.500000</td>
      <td>32.500000</td>
      <td>[Arabia, Ἀραβία]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Africa</td>
      <td>7</td>
      <td>775.0</td>
      <td>32.500000</td>
      <td>7.500000</td>
      <td>[Africa]</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Ireland</td>
      <td>1</td>
      <td>20487.0</td>
      <td>53.184028</td>
      <td>-7.717526</td>
      <td>[Hibernia, Ierne, Éire, Ireland, Ἰέρνη]</td>
    </tr>
    <tr>
      <th>5</th>
      <td>India</td>
      <td>1</td>
      <td>50004.0</td>
      <td>22.500000</td>
      <td>77.500000</td>
      <td>[India]</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Iberia</td>
      <td>1</td>
      <td>863807.0</td>
      <td>41.836468</td>
      <td>44.689138</td>
      <td>[Iberes, Ἰβηρία, Iberia]</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Caledonia</td>
      <td>1</td>
      <td>89132.0</td>
      <td>57.500000</td>
      <td>-4.500000</td>
      <td>[Caledonia, Caledoni, Calidonia]</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Misenum</td>
      <td>2</td>
      <td>432941.0</td>
      <td>40.786279</td>
      <td>14.084884</td>
      <td>[Misenon, Misenum, Μισηνόν]</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Naples</td>
      <td>3</td>
      <td>433014.0</td>
      <td>40.839995</td>
      <td>14.252870</td>
      <td>[Napoli, Neapolis, Parthenope, Naples, Νεάπολις]</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Tarragona</td>
      <td>1</td>
      <td>246349.0</td>
      <td>41.116892</td>
      <td>1.258338</td>
      <td>[Tarrakon, Tarragona, Col. Tarraco, Col. Iulia...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Lugdunum</td>
      <td>1</td>
      <td>167717.0</td>
      <td>45.758866</td>
      <td>4.819482</td>
      <td>[Lyon, Lugdunensis colonia, Lougdounon, Loúgdo...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Hercules</td>
      <td>2</td>
      <td>266032.0</td>
      <td>37.500000</td>
      <td>-0.500000</td>
      <td>[Hercules, Σκομβραρία, Scombraria]</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Illyricum</td>
      <td>2</td>
      <td>481865.0</td>
      <td>42.427292</td>
      <td>17.965028</td>
      <td>[Illyricum]</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Macedonia</td>
      <td>3</td>
      <td>491656.0</td>
      <td>41.250000</td>
      <td>21.750000</td>
      <td>[Macedonia]</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Augsburg</td>
      <td>1</td>
      <td>118580.0</td>
      <td>48.365463</td>
      <td>10.894765</td>
      <td>[Augsburg, Aelia Augusta, Augusta Vindelicum]</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Thebes</td>
      <td>1</td>
      <td>541138.0</td>
      <td>38.319156</td>
      <td>23.317577</td>
      <td>[Thíva, Thiva, Thēbai, Θῆβαι, Thebai, Θήβα, Th...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Argos</td>
      <td>1</td>
      <td>570106.0</td>
      <td>37.631561</td>
      <td>22.719464</td>
      <td>[Ἄργος, Árgos, Argos, Pelasgia]</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Sparta</td>
      <td>1</td>
      <td>570685.0</td>
      <td>37.077905</td>
      <td>22.427298</td>
      <td>[Sparta]</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Athens</td>
      <td>1</td>
      <td>579885.0</td>
      <td>37.972634</td>
      <td>23.722746</td>
      <td>[Athína, Αθήνα, Ἀθῆναι, Athina, Athenae, Athen...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Achaia</td>
      <td>1</td>
      <td>570028.0</td>
      <td>38.102121</td>
      <td>22.224586</td>
      <td>[Ἀχαία, Achaioi, Ἀχαιοί, Aigialos, Αἰγιάλεια, ...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Troy</td>
      <td>1</td>
      <td>550595.0</td>
      <td>39.957433</td>
      <td>26.238459</td>
      <td>[Hisarlik, Troía, Ilium, Τροία, Hisarlık, Troy...</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Ionia</td>
      <td>1</td>
      <td>550597.0</td>
      <td>38.162194</td>
      <td>27.357498</td>
      <td>[Jamanāja, Yamanāja, Yaman, Ionia, Jaman, Jaen...</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Constantinople</td>
      <td>1</td>
      <td>520998.0</td>
      <td>41.006371</td>
      <td>28.965352</td>
      <td>[Constantinople, Istanbul, Constantinopolis]</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Trebizond</td>
      <td>2</td>
      <td>857359.0</td>
      <td>41.004269</td>
      <td>39.723312</td>
      <td>[Ṭrabīzonṭā, Trapezunt, I Pontica garrison, Aṭ...</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Nile</td>
      <td>1</td>
      <td>727172.0</td>
      <td>19.211409</td>
      <td>30.567330</td>
      <td>[an-Nīl, Νεῖλος, Neilos, al-Nil, Nile river, N...</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Algiers</td>
      <td>1</td>
      <td>295276.0</td>
      <td>36.768912</td>
      <td>3.053218</td>
      <td>[Icosium, al-Jazā’ir, GdLRGFQ, Algiers, الجزائ...</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Sardinia</td>
      <td>1</td>
      <td>472014.0</td>
      <td>39.871087</td>
      <td>8.957517</td>
      <td>[Sardo, Ἰχνοῦσσα, Σαρδώ, Sardegna, Sardinia, I...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Sicily</td>
      <td>1</td>
      <td>462492.0</td>
      <td>37.643297</td>
      <td>13.932018</td>
      <td>[Trinacria, Sicilia, Sicily, Σικελία, Sizilien...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Malta</td>
      <td>1</td>
      <td>462311.0</td>
      <td>35.908887</td>
      <td>14.408042</td>
      <td>[Malta, Melita, Μελίτη]</td>
    </tr>
  </tbody>
</table>
</div>




```python
# save result as CSV
place_freq_final.to_csv('Gibbon_chapter_38.csv')
```


```python
pd.read_csv('Gibbon_chapter_38.csv')
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
      <th>Unnamed: 0</th>
      <th>place_name</th>
      <th>frequency</th>
      <th>pleiades_id</th>
      <th>lat</th>
      <th>long</th>
      <th>attested_names</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Rome</td>
      <td>12</td>
      <td>423025.0</td>
      <td>41.891775</td>
      <td>12.486137</td>
      <td>['Ῥώμῃ', 'Rhṓmē', 'Rome', 'Roma', 'Rōma', 'Rho...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Euphrates</td>
      <td>6</td>
      <td>912849.0</td>
      <td>35.543310</td>
      <td>39.606018</td>
      <td>['Εὐφράτης', 'Nahr el-Furat', 'Fırat Nehri', '...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Arabia</td>
      <td>2</td>
      <td>981506.0</td>
      <td>27.500000</td>
      <td>32.500000</td>
      <td>['Arabia', 'Ἀραβία']</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Africa</td>
      <td>7</td>
      <td>775.0</td>
      <td>32.500000</td>
      <td>7.500000</td>
      <td>['Africa']</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Ireland</td>
      <td>1</td>
      <td>20487.0</td>
      <td>53.184028</td>
      <td>-7.717526</td>
      <td>['Hibernia', 'Ierne', 'Éire', 'Ireland', 'Ἰέρνη']</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>India</td>
      <td>1</td>
      <td>50004.0</td>
      <td>22.500000</td>
      <td>77.500000</td>
      <td>['India']</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Iberia</td>
      <td>1</td>
      <td>863807.0</td>
      <td>41.836468</td>
      <td>44.689138</td>
      <td>['Iberes', 'Ἰβηρία', 'Iberia']</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Caledonia</td>
      <td>1</td>
      <td>89132.0</td>
      <td>57.500000</td>
      <td>-4.500000</td>
      <td>['Caledonia', 'Caledoni', 'Calidonia']</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Misenum</td>
      <td>2</td>
      <td>432941.0</td>
      <td>40.786279</td>
      <td>14.084884</td>
      <td>['Misenon', 'Misenum', 'Μισηνόν']</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Naples</td>
      <td>3</td>
      <td>433014.0</td>
      <td>40.839995</td>
      <td>14.252870</td>
      <td>['Napoli', 'Neapolis', 'Parthenope', 'Naples',...</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Tarragona</td>
      <td>1</td>
      <td>246349.0</td>
      <td>41.116892</td>
      <td>1.258338</td>
      <td>['Tarrakon', 'Tarragona', 'Col. Tarraco', 'Col...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Lugdunum</td>
      <td>1</td>
      <td>167717.0</td>
      <td>45.758866</td>
      <td>4.819482</td>
      <td>['Lyon', 'Lugdunensis colonia', 'Lougdounon', ...</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Hercules</td>
      <td>2</td>
      <td>266032.0</td>
      <td>37.500000</td>
      <td>-0.500000</td>
      <td>['Hercules', 'Σκομβραρία', 'Scombraria']</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>Illyricum</td>
      <td>2</td>
      <td>481865.0</td>
      <td>42.427292</td>
      <td>17.965028</td>
      <td>['Illyricum']</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Macedonia</td>
      <td>3</td>
      <td>491656.0</td>
      <td>41.250000</td>
      <td>21.750000</td>
      <td>['Macedonia']</td>
    </tr>
    <tr>
      <th>15</th>
      <td>15</td>
      <td>Augsburg</td>
      <td>1</td>
      <td>118580.0</td>
      <td>48.365463</td>
      <td>10.894765</td>
      <td>['Augsburg', 'Aelia Augusta', 'Augusta Vindeli...</td>
    </tr>
    <tr>
      <th>16</th>
      <td>16</td>
      <td>Thebes</td>
      <td>1</td>
      <td>541138.0</td>
      <td>38.319156</td>
      <td>23.317577</td>
      <td>['Thíva', 'Thiva', 'Thēbai', 'Θῆβαι', 'Thebai'...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>17</td>
      <td>Argos</td>
      <td>1</td>
      <td>570106.0</td>
      <td>37.631561</td>
      <td>22.719464</td>
      <td>['Ἄργος', 'Árgos', 'Argos', 'Pelasgia']</td>
    </tr>
    <tr>
      <th>18</th>
      <td>18</td>
      <td>Sparta</td>
      <td>1</td>
      <td>570685.0</td>
      <td>37.077905</td>
      <td>22.427298</td>
      <td>['Sparta']</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>Athens</td>
      <td>1</td>
      <td>579885.0</td>
      <td>37.972634</td>
      <td>23.722746</td>
      <td>['Athína', 'Αθήνα', 'Ἀθῆναι', 'Athina', 'Athen...</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>Achaia</td>
      <td>1</td>
      <td>570028.0</td>
      <td>38.102121</td>
      <td>22.224586</td>
      <td>['Ἀχαία', 'Achaioi', 'Ἀχαιοί', 'Aigialos', 'Αἰ...</td>
    </tr>
    <tr>
      <th>21</th>
      <td>21</td>
      <td>Troy</td>
      <td>1</td>
      <td>550595.0</td>
      <td>39.957433</td>
      <td>26.238459</td>
      <td>['Hisarlik', 'Troía', 'Ilium', 'Τροία', 'Hisar...</td>
    </tr>
    <tr>
      <th>22</th>
      <td>22</td>
      <td>Ionia</td>
      <td>1</td>
      <td>550597.0</td>
      <td>38.162194</td>
      <td>27.357498</td>
      <td>['Jamanāja', 'Yamanāja', 'Yaman', 'Ionia', 'Ja...</td>
    </tr>
    <tr>
      <th>23</th>
      <td>23</td>
      <td>Constantinople</td>
      <td>1</td>
      <td>520998.0</td>
      <td>41.006371</td>
      <td>28.965352</td>
      <td>['Constantinople', 'Istanbul', 'Constantinopol...</td>
    </tr>
    <tr>
      <th>24</th>
      <td>24</td>
      <td>Trebizond</td>
      <td>2</td>
      <td>857359.0</td>
      <td>41.004269</td>
      <td>39.723312</td>
      <td>['Ṭrabīzonṭā', 'Trapezunt', 'I Pontica garriso...</td>
    </tr>
    <tr>
      <th>25</th>
      <td>25</td>
      <td>Nile</td>
      <td>1</td>
      <td>727172.0</td>
      <td>19.211409</td>
      <td>30.567330</td>
      <td>['an-Nīl', 'Νεῖλος', 'Neilos', 'al-Nil', 'Nile...</td>
    </tr>
    <tr>
      <th>26</th>
      <td>26</td>
      <td>Algiers</td>
      <td>1</td>
      <td>295276.0</td>
      <td>36.768912</td>
      <td>3.053218</td>
      <td>['Icosium', 'al-Jazā’ir', 'GdLRGFQ', 'Algiers'...</td>
    </tr>
    <tr>
      <th>27</th>
      <td>27</td>
      <td>Sardinia</td>
      <td>1</td>
      <td>472014.0</td>
      <td>39.871087</td>
      <td>8.957517</td>
      <td>['Sardo', 'Ἰχνοῦσσα', 'Σαρδώ', 'Sardegna', 'Sa...</td>
    </tr>
    <tr>
      <th>28</th>
      <td>28</td>
      <td>Sicily</td>
      <td>1</td>
      <td>462492.0</td>
      <td>37.643297</td>
      <td>13.932018</td>
      <td>['Trinacria', 'Sicilia', 'Sicily', 'Σικελία', ...</td>
    </tr>
    <tr>
      <th>29</th>
      <td>29</td>
      <td>Malta</td>
      <td>1</td>
      <td>462311.0</td>
      <td>35.908887</td>
      <td>14.408042</td>
      <td>['Malta', 'Melita', 'Μελίτη']</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
