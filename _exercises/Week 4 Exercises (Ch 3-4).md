## 3.1 Names


```python
names = ["Frank", "Chris", "Aidan", "David"]
```


```python
print(names[0])
```

    Frank



```python
print(names[1])
```

    Chris



```python
print(names[2])
```

    Aidan



```python
print(names[3])
```

    David


## 3.2 Send a message


```python
names = ["Frank", "Chris", "Aidan", "David"]
```


```python
print(f'you smell bad, {names[0]}')
print(f'you smell bad, {names[1]}')
print(f'you smell bad, {names[2]}')
print(f'you smell bad, {names[3]}')
```

    you smell bad, Frank
    you smell bad, Chris
    you smell bad, Aidan
    you smell bad, David


## 3.3 Transportation List


```python
mode = ["snowboards", "the joey", "cars"]
```


```python
print(f'I like {mode[0]}')
print(f'I like {mode[1]}')
print(f'I like {mode[2]}')
```

    I like snowboards
    I like the joey
    I like cars


## 3.4 Guest List


```python
invitees = ["marcel proust", "kevin abstract", "alexander the great"]
```


```python
print(f'Hey {invitees[0].title()}, my place tonight?')
print(f'Hey {invitees[1].title()}, my place tonight?')
print(f'Hey {invitees[2].title()}, my place tonight?')
#were we supposed to do titling?
```

    Hey Marcel Proust, my place tonight?
    Hey Kevin Abstract, my place tonight?
    Hey Alexander The Great, my place tonight?


## 3.5 New Guest List


```python
invitees = ["marcel proust", "kevin abstract", "alexander the great"]
```


```python
print(f'Hey {invitees[0].title()}, my place tonight?')
print(f'Hey {invitees[1].title()}, my place tonight?')
print(f'Hey {invitees[2].title()}, my place tonight?')
```

    Hey Marcel Proust, my place tonight?
    Hey Kevin Abstract, my place tonight?
    Hey Alexander The Great, my place tonight?



```python
#removing someone
loser = invitees.pop()
print(f"{loser.title()} is a loser and cannot make it")
```

    Alexander The Great is a loser and cannot make it



```python
#finding someone new
greater_person = 'Catullus'
```


```python
invitees.append(greater_person)
print(f'Hey {invitees[0].title()}, my place tonight?')
print(f'Hey {invitees[1].title()}, my place tonight?')
print(f'Hey {invitees[2].title()}, my place tonight?')
```

    Hey Marcel Proust, my place tonight?
    Hey Kevin Abstract, my place tonight?
    Hey Catullus, my place tonight?


## 3.6 More Guests


```python
#old code
invitees = ["marcel proust", "kevin abstract", "alexander the great"]
print(f'Hey {invitees[0].title()}, my place tonight?')
print(f'Hey {invitees[1].title()}, my place tonight?')
print(f'Hey {invitees[2].title()}, my place tonight?')

#bigger table
print("I got a bigger table")

#new beginning
invitees.insert(0, "isaac newton")

#new mid
invitees.insert(2, "phoebe bridgers")

#new end
invitees.append("sappho")

#all invites
print(f'Hey {invitees[0].title()}, my place tonight?')
print(f'Hey {invitees[1].title()}, my place tonight?')
print(f'Hey {invitees[2].title()}, my place tonight?')
print(f'Hey {invitees[3].title()}, my place tonight?')
print(f'Hey {invitees[4].title()}, my place tonight?')
print(f'Hey {invitees[5].title()}, my place tonight?')
```

    Hey Marcel Proust, my place tonight?
    Hey Kevin Abstract, my place tonight?
    Hey Alexander The Great, my place tonight?
    I got a bigger table
    Hey Isaac Newton, my place tonight?
    Hey Marcel Proust, my place tonight?
    Hey Phoebe Bridgers, my place tonight?
    Hey Kevin Abstract, my place tonight?
    Hey Alexander The Great, my place tonight?
    Hey Sappho, my place tonight?


## 3.7 Shrinking the Guest list


```python
print(invitees)
```

    ['isaac newton', 'marcel proust', 'phoebe bridgers', 'kevin abstract', 'alexander the great', 'sappho']



```python
invitees.pop()
print("you cannot come anymore, sorry")
```

    you cannot come anymore, sorry



```python
invitees.pop()
print("you cannot come anymore, sorry")
```

    you cannot come anymore, sorry



```python
invitees.pop()
print("you cannot come anymore, sorry")
```

    you cannot come anymore, sorry



```python
invitees.pop()
print("you cannot come anymore, sorry")
```

    you cannot come anymore, sorry



```python
print(invitees)
```

    ['isaac newton', 'marcel proust']



```python
print(f"hey {invitees[0].title()}, you still want to come over?")
print(f"hey {invitees[1].title()}, you still want to come over?")
```

    hey Isaac Newton, you still want to come over?
    hey Marcel Proust, you still want to come over?


## 3.8 Seeing the world


```python
locations = ["China", "Japan", "France", "Greece", "Singapore"]
print(locations)
print(sorted(locations))
print(locations)
locations.reverse()
print(locations)
locations.reverse()
print(locations)
locations.sort()
print(locations)
locations.sort(reverse=True)
print(locations)
```

    ['China', 'Japan', 'France', 'Greece', 'Singapore']
    ['China', 'France', 'Greece', 'Japan', 'Singapore']
    ['China', 'Japan', 'France', 'Greece', 'Singapore']
    ['Singapore', 'Greece', 'France', 'Japan', 'China']
    ['China', 'Japan', 'France', 'Greece', 'Singapore']
    ['China', 'France', 'Greece', 'Japan', 'Singapore']
    ['Singapore', 'Japan', 'Greece', 'France', 'China']


# Chapter 4

## 4.1 Pizza time


```python
pizzas = ["cheese", "sausage", "pineapple"]
```


```python
for pizza in pizzas:
    print(pizza)
```

    cheese
    sausage
    pineapple



```python
for pizza in pizzas:
    print(f"I like {pizza} pizza")
```

    I like cheese pizza
    I like sausage pizza
    I like pineapple pizza



```python
for pizza in pizzas:
    print(f"I like {pizza} pizza")
print("I like pizza a lot")
```

    I like cheese pizza
    I like sausage pizza
    I like pineapple pizza
    I like pizza a lot


## 4.2 Animals


```python
animals = ["dogs", "cats", "horses"]
```


```python
for animal in animals:
    print(animal)
```

    dogs
    cats
    horses



```python
for animal in animals:
    print(f"{animal} have four legs")
```

    dogs have four legs
    cats have four legs
    horses have four legs



```python
for animal in animals:
    print(f"{animal} have four legs")
print("these animals have four legs")
```

    dogs have four legs
    cats have four legs
    horses have four legs
    these animals have four legs


## 4.3 Counting to Twenty


```python
for num in range(1,21):
    print(num)
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20


## 4.6 Odd numbers


```python
for num in range(1,21,2):
    print(num)
```

    1
    3
    5
    7
    9
    11
    13
    15
    17
    19


## 4.10 Slices


```python
animals = ["dogs", "cats", "horses", "hyenas", "lions", "elephants", "zebras", "chamelons", "lizards"]
```


```python
print("The first three animals in the list are:")
for animal in animals [0:3]:
    print("\t" + animal)
```

    The first three animals in the list are:
    	dogs
    	cats
    	horses



```python
print("Three animals from the middle of the list are:")
for animal in animals[3:6]:
    print("\t" + animal)
```

    Three animals from the middle of the list are:
    	hyenas
    	lions
    	elephants



```python
print("The last three animals in the list are:")
for animal in animals[6:9]:
    print("\t" + animal)
```

    The last three animals in the list are:
    	zebras
    	chamelons
    	lizards


## 4.11 My Pizzas and your Pizzas


```python
pizzas = ["cheese", "sausage", "pineapple"]
friend_pizzas = pizzas[:]
```


```python
pizzas.append("pepperoni")
```


```python
friend_pizzas.append("beans")
```


```python
print("My favorite pizzas are:")
for pizza in pizzas:
    print("\t" + pizza)
```

    My favorite pizzas are:
    	cheese
    	sausage
    	pineapple
    	pepperoni



```python
print("My friend's favorite pizzas are:")
for pizza in friend_pizzas:
    print("\t" + pizza)
```

    My friend's favorite pizzas are:
    	cheese
    	sausage
    	pineapple
    	beans



```python

```
