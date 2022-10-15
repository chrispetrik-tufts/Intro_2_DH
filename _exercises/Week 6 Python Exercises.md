---
layout: page
title: Exercises Week Six
description: Select exercises from Python Crash Course
---
## 6.1 People


```python
#6-1. Person: Use a dictionary to store information about a person you know. Store their first name, last name, age, and the city in which they live. You should have keys such as first_name, last_name, age, and city. Print each piece of information stored in your dictionary.
```


```python
Person = {'first_name': 'Georgia', 'last_name': 'Petrik', 'age': 23, 'city': 'Milton'}
```


```python
Person
```




    {'first_name': 'Georgia', 'last_name': 'Petrik', 'age': 23, 'city': 'Milton'}



## 6.2 Favorite numbers


```python
#6-2. Favorite Numbers: Use a dictionary to store people’s favorite numbers. Think of five names, and use them as keys in your dictionary. Think of a favorite number for each person, and store each as a value in your dictionary. Print each person’s name and their favorite number. For even more fun, poll a few friends and get some actual data for your program.
```


```python
favorite_numbers = {'Christopher': 16, 'Dad': 16, 'Dustin': 15, 'David': 34, 'Tom': 12}
```


```python
number = favorite_numbers['Christopher']
print(f"Christopher's favorite number is {number}.")
```

    Christopher's favorite number is 16.



```python
number_1 = favorite_numbers['Dad']
print(f"Dad's favorite number is {number_1}.")
```

    Dad's favorite number is 16.



```python
number_2 = favorite_numbers['Dustin']
print(f"Dustin's favorite number is {number_2}.")
```

    Dustin's favorite number is 15.



```python
number_3 = favorite_numbers['David']
print(f"Davids's favorite number is {number_3}.")
```

    Davids's favorite number is 34.



```python
number_4 = favorite_numbers['Tom']
print(f"Tom's favorite number is {number_4}.")
```

    Tom's favorite number is 12.


## 6.3 Glossary


```python
#6-3. Glossary: A Python dictionary can be used to model an actual dictionary. However, to avoid confusion, let’s call it a glossary.

#Think of five programming words you’ve learned about in the previous chapters. Use these words as the keys in your glossary, and store their meanings as values.
#Print each word and its meaning as neatly formatted output. You might print the word followed by a colon and then its meaning, or print the word on one line and then print its meaning indented on a second line. Use the newline character (\n) to insert a blank line between each word-meaning pair in your output.
```


```python
programming_words = {'title': 'makes everything title case', 'lower': 'makes everything lower case', 'upper': 'makes everything upper case', 'for': 'starts a for loop', 'variable': 'takes on the value of something'}
```


```python
print(programming_words)
```

    {'title': 'makes everything title case', 'lower': 'makes everything lower case', 'upper': 'makes everything upper case', 'for': 'starts a for loop', 'variable': 'takes on the value of something'}



```python
word = 'title'
print(f"\n{word.title()}: {programming_words[word]}")
word = 'lower'
print(f"\n{word.title()}: {programming_words[word]}")
word = 'upper'
print(f"\n{word.title()}: {programming_words[word]}")
word = 'for'
print(f"\n{word.title()}: {programming_words[word]}")
word = 'variable'
print(f"\n{word.title()}: {programming_words[word]}")
```

    
    Title: makes everything title case
    
    Lower: makes everything lower case
    
    Upper: makes everything upper case
    
    For: starts a for loop
    
    Variable: takes on the value of something


## 6.4 Glossary Part 2


```python
programming_words = {'title': 'makes everything title case', 'lower': 'makes everything lower case', 'upper': 'makes everything upper case', 'for': 'starts a for loop', 'variable': 'takes on the value of something'}
for word, meaning in programming_words.items():
    print(f"\n {word.title()}: {meaning.lower()}")
```

    
     Title: makes everything title case
    
     Lower: makes everything lower case
    
     Upper: makes everything upper case
    
     For: starts a for loop
    
     Variable: takes on the value of something


## 6.5 Rivers


```python
#6-5. Rivers: Make a dictionary containing three major rivers and the country each river runs through. One key-value pair might be 'nile': 'egypt'.

#Use a loop to print a sentence about each river, such as The Nile runs through Egypt.
#Use a loop to print the name of each river included in the dictionary.
#Use a loop to print the name of each country included in the dictionary.
```


```python
rivers = {
    'nile': 'egypt',
    'mississippi': 'u s',
    'ganges': 'bangladesh'
}
```


```python
for river, country in rivers.items():
    print(f"The {river.title()} runs through {country.title()}")
```

    The Nile runs through Egypt
    The Mississippi runs through U S
    The Ganges runs through Bangladesh



```python
for river in rivers.keys():
    print(f"My river is the {river.title()}")
```

    My river is the Nile
    My river is the Mississippi
    My river is the Ganges



```python
for country in rivers.values():
    print(f"My country is {country.title()}")
```

    My country is Egypt
    My country is U S
    My country is Bangladesh


## 6.7 People


```python
#6-7. People: Start with the program you wrote for Exercise 6-1 (page 99). Make two new dictionaries representing different people, and store all three dictionaries in a list called people. Loop through your list of people. As you loop through the list, print everything you know about each person.
```


```python
Person_0 = {'first_name': 'Georgia', 'last_name': 'Petrik', 'age': 23, 'city': 'Milton'}
People.append(Person_0)
```


```python
Person_1 = {'first_name': 'Christopher', 'last_name': 'Petrik', 'age': 21, 'city': 'Milton'}
People.append(Person_1)
```


```python
Person_2 = {'first_name': 'Spencer', 'last_name': 'Knotts', 'age': 20, 'city': 'Glen Ellyn'}
People.append(Person_2)
```


```python
People = []
```


```python
for person in People:
    name = f"{person['first_name'].title()} {person['last_name'].title()}"
    age = person['age']
    city = person['city'].title()
    print(f"{name} is {age} years old and from {city}")
```

    Georgia Petrik is 23 years old and from Milton
    Christopher Petrik is 21 years old and from Milton
    Spencer Knotts is 20 years old and from Glen Ellyn


## 6.8 Pets


```python
#6-8. Pets: Make several dictionaries, where each dictionary represents a different pet. In each dictionary, include the kind of animal and the owner’s name. Store these dictionaries in a list called pets. Next, loop through your list and as you do, print everything you know about each pet.
```


```python
pets = []
pet_0 = {'name':'Axl', 'species': 'dog', 'owner': 'Christopher', 'number of legs':4}
pet_1 = {'name':'Michael', 'species': 'fish', 'owner': 'Christopher', 'number of legs':0}
pet_2 = {'name':'Bobo', 'species': 'monkey', 'owner': 'Willard', 'number of legs':2}
pets.append(pet_0)
pets.append(pet_1)
pets.append(pet_2)
```


```python
for pet in pets:
    print(f"\nI know this about {pet['name'].title()}:")
    for key, value in pet.items():
        print(f"\t{key}: {value}")
```

    
    I know this about Axl:
    	name: Axl
    	species: dog
    	owner: Christopher
    	number of legs: 4
    
    I know this about Michael:
    	name: Michael
    	species: fish
    	owner: Christopher
    	number of legs: 0
    
    I know this about Bobo:
    	name: Bobo
    	species: monkey
    	owner: Willard
    	number of legs: 2


## 6.9 Places


```python
#6-9. Favorite Places: Make a dictionary called favorite_places. Think of three names to use as keys in the dictionary, and store one to three favorite places for each person. To make this exercise a bit more interesting, ask some friends to name a few of their favorite places. Loop through the dictionary, and print each person’s name and their favorite places.
```


```python
favorite_places = {
    'Axel': ['Gothenburg', 'Val Royeaux'],
    'Christopher': ['Paros', 'St. Agatha Church', 'Brighton'],
    'Georgia': ['Tarryall River Ranch', 'Barn']
    }

for name, places in favorite_places.items():
    print(f"\n{name.title()} likes the following places:")
    for place in places:
        print(f"- {place.title()}")
```

    
    Axel likes the following places:
    - Gothenburg
    - Val Royeaux
    
    Christopher likes the following places:
    - Paros
    - St. Agatha Church
    - Brighton
    
    Georgia likes the following places:
    - Tarryall River Ranch
    - Barn


## 6.11 Cities


```python
#6-11. Cities: Make a dictionary called cities. Use the names of three cities as keys in your dictionary. Create a dictionary of information about each city and include the country that the city is in, its approximate population, and one fact about that city. The keys for each city’s dictionary should be something like country, population, and fact. Print the name of each city and all of the information you have stored about it.
```


```python
cities = {
    'gothenburg': {
        'country': 'sweden',
        'population': 579_281,
        'fact': 'spiffy looking',
        },
    'boston': {
        'country': 'united states',
        'population': 689_326,
        'fact': 'gross',
        },
    'philadelphia': {
        'country': 'united states',
        'population': 1_582_000 ,
        'fact': 'grossest',
        }
    }

for city, city_info in cities.items():
    country = city_info['country'].title()
    population = city_info['population']
    fact = city_info['fact']

    print(f"\n{city.title()} is in {country}.")
    print(f"  It has a population of about {population}.")
    print(f"  The {city.title()} is {fact}")
```

    
    Gothenburg is in Sweden.
      It has a population of about 579281.
      The Gothenburg is spiffy looking
    
    Boston is in United States.
      It has a population of about 689326.
      The Boston is gross
    
    Philadelphia is in United States.
      It has a population of about 1582000.
      The Philadelphia is grossest



```python

```
