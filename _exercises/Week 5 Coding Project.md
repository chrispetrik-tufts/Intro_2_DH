---
layout: page
title: Exercises Week Five
description: Select exercises from Python Crash Course
---
## 5.1 Conditional Tests


```python
dog = 'axl'
```


```python
print("is dog == 'axl'? true")
```

    is dog == 'axl'? true



```python
print(dog == 'axl')
```

    True



```python
print("is dog != 'axl'? false")
```

    is dog != 'axl'? false



```python
print(dog != 'axl')
```

    False


### Do some numbers


```python
x = 71
y = 2
z = 71
print("Is x < y? False")
print (x < y)
```

    Is x < y? False
    False



```python
print("Is x >= z? True")
print (x >= z)
```

    Is x >= z? True
    True


## 5.2 More conditional tests


```python
title = 'Please Work'
print ("Is title == 'please work'? false")
print(title == 'please work')
```

    Is title == 'please work'? false
    False



```python
title = 'Please Work'
print ("Is title.lower() == 'please work'? true")
print(title.lower() == 'please work')
```

    Is title.lower() == 'please work'? true
    True



```python
print("Is 16 == 4 * 4? true")
print(16 == 4 * 4)
```

    Is 16 == 4 * 4? true
    True



```python
print("Is 69 > 15? true")
print(69 > 15)
```

    Is 69 > 15? true
    True



```python
print("Is 69 <= 15? False")
print(69 <= 15)
```

    Is 69 <= 15? False
    False



```python
print("Is 15 == 15 and 125 > 130? false")
print(15 == 15 and 125 == 130)
```

    Is 15 == 15 and 125 > 130? false
    False



```python
print("Is 15 == 15 or 125 > 130? true")
print(15 == 15 or 125>130)
```

    Is 15 == 15 or 125 > 130? true
    True



```python
dogs = ["Axl", "Rootbeer", "Scooter"]
```


```python
print("Is 'Georgia' in dogs? false")
print("Georgia" in dogs)
```

    Is 'Georgia' in dogs? false
    False



```python
print("is 'Georgia' not in dogs? true")
print("Georgia" not in dogs)
```

    is 'Georgia' not in dogs? true
    True


## 5.6 Stages of life


```python
age = 21
if age < 2:
    print("You are a baby")
elif age >= 2 and age < 4:
    print("You are a toddler.")
elif age >=4 and age < 13:
    print("You are a kid.")
elif age >= 13 and age < 20:
    print("You are a teenager.")
elif age >=20 and age < 65:
    print("You are an adult.")
else:
    print("You are an elder")
```

    You are an adult.


## 5.7 Favorite Fruit


```python
favorite_fruits = ["grapes", "apples", "blueberries"]
```


```python
if "grapes" in favorite_fruits:
    print("I really like grapes")
    
if "burbger" in favorite_fruits:
    print("I really like burbger")
    
if "snickers_Bar" in favorite_fruits:
    print("I really like snickers bars")
    
if "apples" in favorite_fruits:
    print("I really like apples")
    
if "blueberries" in favorite_fruits:
    print("I really like blueberries")
```

    I really like grapes
    I really like apples
    I really like blueberries


## 5.8 Hello Admin


```python
usernames = ["admin", "xX_S00pEr_sNIPeZ_Xx", "cmp123456789", "booger", "plutarch"]
```


```python
for username in usernames:
    if username == 'admin':
        print(f"Hello {username}, would you like to see a status report?")
    else:
            print(f"Hello {username}, get off Chris's computer")
```

    Hello admin, would you like to see a status report?
    Hello xX_S00pEr_sNIPeZ_Xx, get off Chris's computer
    Hello cmp123456789, get off Chris's computer
    Hello booger, get off Chris's computer
    Hello plutarch, get off Chris's computer


## 5.9 No users


```python
usernames = ["admin", "xX_S00pEr_sNIPeZ_Xx", "cmp123456789", "booger"]
usernames.clear()

if usernames:
    for username in usernames:
        if username == 'admin':
            print(f"Hello {username}, would you like to see a status report?")
    else:
            print(f"Hello {username}, get off Chris's computer")
else:
    print("We need to find some users!")
```

    We need to find some users!


## 5.10 Checking Usernames


```python
current_users = ["admin", "xX_S00pEr_sNIPeZ_Xx", "cmp123456789", "booger", "plutarch"]
```


```python
new_users = ["cmp123456789", "dsr3302", "hells_reaper_13", "fellis2872", "booger"]
```


```python
for username in new_users:
    if username.lower() in current_users:
        print(f"{username} is not available, please choose a new username.")
    else:
        print(f"{username} is available")
```

    cmp123456789 is not available, please choose a new username.
    dsr3302 is available
    hells_reaper_13 is available
    fellis2872 is available
    booger is not available, please choose a new username.



```python

```
