---
layout: page
title: Variables, String, and Numbers
description: The exercises that we learned in class about variables, strings, and numbers.
---

# Variables


```python
greeting = "Hello world!"
```


```python
print(greeting)
```

    Hello world!



```python
Axl = "my dog"
print(Axl)
```

    my dog



```python
print(Axl)
```

    my dog



```python
axl = "his dog"
print(axl)
```

    his dog



```python
print(axl)
```

    his dog



```python
ex_1 = "this is a string"
print (ex_1)
```

    this is a string



```python
ex_2 = 'this is also a string'
print(ex_2)
```

    this is also a string



```python
ex_3 = "here is a string that doesn't work'
print(ex_3)
```


      Input In [13]
        ex_3 = "here is a string that doesn't work'
                                                   ^
    SyntaxError: EOL while scanning string literal




```python
ex_4 = "I asked the question, 'When should I use single or double quotes?'"
print(ex_4)
```

    I asked the question, 'When should I use single or double quotes?'



```python
historian = "edward gibbon"
print(historian)
```

    edward gibbon



```python
print(historian.title())
```

    Edward Gibbon



```python
novelist = "Becky Chambers"
print(novelist.lower())
```

    becky chambers



```python
"becky" == "becky"
```




    True




```python
"becky" == "Becky"
```




    False




```python
first_name = "ada"
last_name = "lovelace"
```


```python
full_name = first_name + " " + last_name
print(full_name)
```

    ada lovelace



```python
greeting = f"Hello, {first_name} {last_name}"
print(greeting.title())
```

    Hello, Ada Lovelace



```python
print ("my dog")
```

    my dog



```python
print ("Axl")
```

    Axl


## whitespace


```python
print ("tab")
```

    tab



```python
print ("\ttab")
```

    	tab



```python
print ("Languages: \nGreek\nLatin\nEnglish")
```

    Languages: 
    Greek
    Latin
    English



```python
str_rspace = "string        "
print(str_rspace)
```

    string        



```python
print(str_rspace.rstrip())
```

    string



```python
example = str_rspace + "."
print(example)
```

    string        .



```python
example_2 = str_rspace.rstrip() + "."
```


```python
print(exaple_2)
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    Input In [10], in <cell line: 1>()
    ----> 1 print(exaple_2)


    NameError: name 'exaple_2' is not defined



```python
print(example_2)
```

    string.



```python
# integers
238 + 4834
```




    5072



## Numbers

## Also the other ones above


```python
54 * 4
```




    216




```python
num = 45
```


```python
num + 5
```




    50




```python
type(num)
```




    int




```python
30 / 10 # this will return a float
```




    3.0




```python
f = 30/7
```


```python
f
```




    4.285714285714286




```python
type(f)
```




    float




```python
3 **
```


      Input In [24]
        3 **
            ^
    SyntaxError: invalid syntax




```python
3**3
```




    27



## Lists


```python
# lists are data structures in python
```


```python
subjects = ['classics', 'history', 'philosophy']
```


```python
print(subjects)
```

    ['classics', 'history', 'philosophy']



```python
print(subjects[0])
```

    classics



```python
print(subjects[2])
```

    philosophy



```python
print(subjects[-1])
```

    philosophy



```python
message = f"My most difficult subject is {subjects[1].title()}."
print(message)
```

    My most difficult subject is History.



```python
# how to modify a list
print(subjects)
```

    ['classics', 'history', 'philosophy']



```python
subjects[1] = 'sociology'
```


```python
print(subjects)
```

    ['classics', 'sociology', 'philosophy']



```python
# append
subjects.append('history')
print(subjects)
```

    ['classics', 'sociology', 'philosophy', 'history']



```python
subjects.append('compsci', 'Latin')
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Input In [37], in <cell line: 1>()
    ----> 1 subjects.append('compsci', 'Latin')


    TypeError: list.append() takes exactly one argument (2 given)



```python
subjects.append('compsci')
```


```python
print(subjects)
```

    ['classics', 'sociology', 'philosophy', 'history', 'compsci']



```python
subjects.append('archaeology')
print(subjects)
```

    ['classics', 'sociology', 'philosophy', 'history', 'compsci', 'archaeology']



```python
# insert
subjects.insert(0, 'religion')
```


```python
print(subjects)
```

    ['religion', 'classics', 'sociology', 'philosophy', 'history', 'compsci', 'archaeology']



```python
subjects.insert(2, 'Latin')
```


```python
print(subjects)
```

    ['religion', 'classics', 'Latin', 'sociology', 'philosophy', 'history', 'compsci', 'archaeology']



```python
# delete item
del subjects['-1']
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Input In [45], in <cell line: 2>()
          1 # delete item
    ----> 2 del subjects['-1']


    TypeError: list indices must be integers or slices, not str



```python
del subjects[-1]
```


```python
print(subjects)
```

    ['religion', 'classics', 'Latin', 'sociology', 'philosophy', 'history', 'compsci']



```python
# pop method
popped_subjects = subjects.pop(0)
print(popped_subjects)
print(subjects)
```

    religion
    ['classics', 'Latin', 'sociology', 'philosophy', 'history', 'compsci']



```python
#remove
subjects.remove('sociology')
print(subjects)
```

    ['classics', 'Latin', 'philosophy', 'history', 'compsci']



```python

```
