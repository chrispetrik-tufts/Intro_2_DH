---
layout: page
title: Exercises Week Seven
description: Select exercises from Python Crash Course
---
# 8.1 Message


```python
def display_message():
    """What I am learning about"""
    message = "I am learning about storing code in functions"
    print(message)
```


```python
display_message()
```

    I am learning about storing code in functions


# 8.2 Favorite Book


```python
def favorite_book(title): 
    """Make a message about my favorite books"""
    print(f"one of my favorite books is {title}")
    
favorite_book('Candide')
```

    one of my favorite books is Candide


# 8.3 T Shirt


```python
def make_shirt(size, text):
    """Shirt specifications"""
    print(f"\n Make a {size} sized shirt.")
    print(f"It says, '{text}'.")
```


```python
make_shirt('medium', 'metallica')
```

    
     Make a medium sized shirt.
    It says, 'metallica'.



```python
make_shirt(text="I'm with stupid", size="small")
```

    
     Make a small sized shirt.
    It says, 'I'm with stupid'.


# 8.5 Cities


```python
def describe_city(city, country='Iceland'):
    """describe cities"""
    sentence = f"{city.title()} is in {country.title()}"
    print(sentence)
```


```python
describe_city('Reykjavik')
```

    Reykjavik is in Iceland



```python
describe_city('Reykjanesbær')
```

    Reykjanesbær is in Iceland



```python
describe_city('boston', 'the united states')
```

    Boston is in The United States


# 8.6 City Names


```python
def city_country(city, country):
    """return city, country"""
    return f"{city.title()}, {country.title()}"
```


```python
city_0 = city_country('Boston', 'United States')
print(city_0)
```

    Boston, United States



```python
city_1 = city_country('Paris', 'France')
print(city_1)
```

    Paris, France



```python
city_2 = city_country('Warsaw', 'Poland')
print(city_2)
```

    Warsaw, Poland


# 8.7 Albums


```python
def make_album(artist, title, tracks=0):
    """making dictionaries for albums"""
    album_dict = {
        'artist' : artist.title(),
        'title' : title.title(),
        }
    if tracks: 
        album_dict['tracks'] = tracks
    return album_dict
```


```python
album_0 = make_album('alice in chains', 'facelift')
print(album_0)
```

    {'artist': 'Alice In Chains', 'title': 'Facelift'}



```python
album_1 = make_album('nirvana', 'nevermind')
print(album_1)
```

    {'artist': 'Nirvana', 'title': 'Nevermind'}



```python
album_2 = make_album('soundgarden', 'superunknown', tracks=16)
print(album_2)
```

    {'artist': 'Soundgarden', 'title': 'Superunknown', 'tracks': 16}



```python
album_3 = make_album('stone temple pilots', 'core', tracks=12)
print(album_3)
```

    {'artist': 'Stone Temple Pilots', 'title': 'Core', 'tracks': 12}



```python

```
