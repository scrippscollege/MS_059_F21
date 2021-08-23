# Python and Viz (Scripps College F2021) 09

Python for Everybody: Exploring Data Using Python 3 Dr. Charles R. Severance

ported to Jupyter Notebooks by Douglas Goodwin, 2021.

Content Copyright 2009- Dr. Charles R. Severance with edits and additions by Douglas Goodwin.

This work is licensed under a Creative Commons Attribution-NonCommercial- ShareAlike 3.0 Unported License. This license is available at <https://creativecommons.org/licenses/by-nc-sa/3.0/>

# Chapter 9: Dictionaries

The Python dictionary is one of its most powerful data structures. Instead of representing values in a linear list, dictionaries store data as key / value pairs. Using key / value pairs gives us a simple in-memory "database" in a single Python variable.

### Videos

* [Dictionaries - Part 1](https://youtu.be/yDDRMb-1cxI)
* [Dictionaries - Part 2](https://youtu.be/LRSIuH94XM4)
* [Dictionaries - Part 3](https://youtu.be/ZDjiFB1Ib84)
* [Counting Word Frequency using a Dictionary](https://youtu.be/lLbyEYjU55A)

### Slides

* [Pythonlearn-09-Dictionaries.pptx](https://www.py4e.com/lectures3/Pythonlearn-09-Dictionaries.pptx)

### References

* [Chapter 9: Dictionaries](https://www.py4e.com/html3/09-dictionaries)
* [Fun: Sesame Street - The Count](https://www.youtube.com/watch?v=EHJ9uYx5L58)

### Tools:

* [Autograder: Exercise 9.4](https://www.py4e.com/lessons_launch/pythonauto_09_04)
* [Quiz: Dictionaries](https://www.py4e.com/lessons_launch/py4e_09_dict_quiz)

## A dictionary is like a list, but more general. In a list, the index positions have to be integers; in a dictionary, the indices can be (almost) any type.

You can think of a dictionary as a mapping between a set of indices (which are called keys) and a set of values. Each key maps to a value. The association of a key and a value is called a key-value pair or sometimes an item.

As an example, we’ll build a dictionary that maps from English to Spanish words, so the keys and the values are all strings.

The function dict creates a new dictionary with no items. Because dict is the name of a built-in function, you should avoid using it as a variable name.

```python no-exec id=17b46acc-5dcc-49c3-af97-2f274d2277a5
>>> eng2sp = dict()
>>> print(eng2sp)
{}
```

The curly brackets, {}, represent an empty dictionary. To add items to the dictio- nary, you can use square brackets:

```python no-exec id=4153b052-585c-40e8-85ed-35c553e181d9
>>> eng2sp['one'] = 'uno'
```

This line creates an item that maps from the key 'one' to the value “uno”. If we print the dictionary again, we see a key-value pair with a colon between the key and value:

```python no-exec id=f75241d1-8906-4c48-9f9e-075e2f64c87c
>>> print(eng2sp)
{'one': 'uno'}
```

This output format is also an input format. For example, you can create a new dictionary with three items. But if you print eng2sp, you might be surprised:

```python no-exec id=50ea517e-412f-4ff6-9bd1-1dc51ebf4f61
>>> eng2sp = {'one': 'uno', 'two': 'dos', 'three': 'tres'}
>>> print(eng2sp)
{'one': 'uno', 'three': 'tres', 'two': 'dos'}
```

The order of the key-value pairs is not the same. In fact, if you type the same example on your computer, you might get a different result. In general, the order of items in a dictionary is unpredictable.

But that’s not a problem because the elements of a dictionary are never indexed with integer indices. Instead, you use the keys to look up the corresponding values:

```python no-exec id=2ab14efc-f7ab-48a2-a43c-62326203c276
>>> print(eng2sp['two']) 'dos'
```

The key 'two' always maps to the value “dos” so the order of the items doesn’t matter. If the key isn’t in the dictionary, you get an exception:

```python no-exec id=cf00e326-e8b7-4cf7-82c5-ff15198bbd0f
>>> print(eng2sp['four'])
KeyError: 'four'
The len function works on dictionaries; it returns the number of key-value pairs:
>>> len(eng2sp)
3
```

The in operator works on dictionaries; it tells you whether something appears as a key in the dictionary (appearing as a value is not good enough).

```python no-exec id=b647d0ab-6bcc-4d3a-bdcf-216d8a0224a1
>>> 'one' in eng2sp
True
>>> 'uno' in eng2sp
False
```

To see whether something appears as a value in a dictionary, you can use the method values, which returns the values as a type that can be converted to a list, and then use the in operator:

```python no-exec id=77403411-6376-425d-ab6c-a354aa89e089
>>> vals = list(eng2sp.values())
>>> 'uno' in vals
True
```

The in operator uses different algorithms for lists and dictionaries. For lists, it uses a linear search algorithm. As the list gets longer, the search time gets longer in direct proportion to the length of the list. For dictionaries, Python uses an algorithm called a hash table that has a remarkable property: the in operator takes about the same amount of time no matter how many items there are in a dictionary. I won’t explain why hash functions are so magical, but you can read more about it at [wikipedia.org/wiki/Hash_table](http://wikipedia.org/wiki/Hash_table).

## **Exercise 1**:

Download a copy of the file [www.py4e.com/code3/words.txt](https://www.py4e.com/code3/words.txt)

Write a program that reads the words in words.txt and stores them as keys in a dictionary. It doesn’t matter what the values are. Then you can use the in operator as a fast way to check whether a string is in the dictionary.

## 9.1 Dictionary as a set of counters

Suppose you are given a string and you want to count how many times each letter appears. There are several ways you could do it:

1. You could create 26 variables, one for each letter of the alphabet. Then you could traverse the string and, for each character, increment the corresponding counter, probably using a chained conditional.
2. You could create a list with 26 elements. Then you could convert each character to a number (using the built-in function ord), use the number as an index into the list, and increment the appropriate counter.
3. You could create a dictionary with characters as keys and counters as the corresponding values. The first time you see a character, you would add an item to the dictionary. After that you would increment the value of an existing item. Each of these options performs the same computation, but each of them implements that computation in a different way.

An implementation is a way of performing a computation; some implementations are better than others. For example, an advantage of the dictionary implementa- tion is that we don’t have to know ahead of time which letters appear in the string and we only have to make room for the letters that do appear.

Here is what the code might look like:

```python no-exec id=c1daef52-07b4-4d28-abef-ab06c0570574
word = 'brontosaurus'
d = dict()
for c in word:
  if c not in d:
    d[c] = 1
  else:
    d[c] = d[c] + 1
print(d)
```

We are effectively computing a histogram, which is a statistical term for a set of counters (or frequencies).

The for loop traverses the string. Each time through the loop, if the character c is not in the dictionary, we create a new item with key c and the initial value 1 (since we have seen this letter once). If c is already in the dictionary we increment d\[c\].

Here’s the output of the program:

```python no-exec id=a569ca58-c07c-4b59-925c-2b91006a469c
{'a': 1, 'b': 1, 'o': 2, 'n': 1, 's': 2, 'r': 2, 'u': 2, 't': 1}
```

The histogram indicates that the letters “a” and “b” appear once; “o” appears twice, and so on. Dictionaries have a method called get that takes a key and a default value. If the key appears in the dictionary, get returns the corresponding value; otherwise it returns the default value.

For example:

```python no-exec id=6a3303c1-9fe2-4cda-840f-cfd4d7a5fc1c
>>> counts = { 'chuck' : 1 , 'annie' : 42, 'jan': 100}
>>> print(counts.get('jan', 0))
100
>>> print(counts.get('tim', 0))
0
```

We can use get to write our histogram loop more concisely. Because the get method automatically handles the case where a key is not in a dictionary, we can reduce four lines down to one and eliminate the if statement.

```python no-exec id=58de06e9-b284-485c-a857-74e915796c50
word = 'brontosaurus'
d = dict()
for c in word:
    d[c] = d.get(c,0) + 1
print(d)
```

The use of the get method to simplify this counting loop ends up being a very commonly used “idiom” in Python and we will use it many times in the rest of the book. So you should take a moment and compare the loop using the if statement and in operator with the loop using the get method. They do exactly the same thing, but one is more succinct.

## 9.2 Dictionaries and files

One of the common uses of a dictionary is to count the occurrence of words in a file with some written text. Let’s start with a very simple file of words taken from the text of Romeo and Juliet. For the first set of examples, we will use a shortened and simplified version of the text with no punctuation. Later we will work with the text of the scene with punctuation included.

```no-exec id=745d5612-49cd-469f-8aff-70b11bcce2cd
But soft what light through yonder window breaks
It is the east and Juliet is the sun
Arise fair sun and kill the envious moon
Who is already sick and pale with grief
```

We will write a Python program to read through the lines of the file, break each line into a list of words, and then loop through each of the words in the line and count each word using a dictionary.

You will see that we have two for loops. The outer loop is reading the lines of the file and the inner loop is iterating through each of the words on that particular line. This is an example of a pattern called nested loops because one of the loops is the outer loop and the other loop is the inner loop.

Because the inner loop executes all of its iterations each time the outer loop makes a single iteration, we think of the inner loop as iterating “more quickly” and the outer loop as iterating more slowly.

The combination of the two nested loops ensures that we will count every word on every line of the input file.

```python no-exec id=a1b560c7-ec3e-40ce-9c01-2e2aa8606e26
fname = input('Enter the file name: ')
try:
  fhand = open(fname)
except:
  print('File cannot be opened:', fname)
  exit()

counts = dict()
for line in fhand:
  words = line.split()
  for word in words:
    if word not in counts:
      counts[word] = 1
    else:
      counts[word] += 1
print(counts)

# Code: http://www.py4e.com/code3/count1.py
```

In our else statement, we use the more compact alternative for incrementing a variable. `counts[word] += 1` is equivalent to `counts[word] = counts[word] + 1`. Either method can be used to change the value of a variable by any desired amount. Similar alternatives exist for -=, \*=, and /=. When we run the program, we see a raw dump of all of the counts in unsorted hash order. (the romeo.txt file is available at [www.py4e.com/code3/romeo.txt](https://www.py4e.com/code3/romeo.txt))

```no-exec id=8bf32dae-e2a1-4a3b-abad-58f1fef3a811
python count1.py
Enter the file name: romeo.txt
{'and': 3, 'envious': 1, 'already': 1, 'fair': 1,
'is': 3, 'through': 1, 'pale': 1, 'yonder': 1,
'what': 1, 'sun': 2, 'Who': 1, 'But': 1, 'moon': 1,
'window': 1, 'sick': 1, 'east': 1, 'breaks': 1,
'grief': 1, 'with': 1, 'light': 1, 'It': 1, 'Arise': 1,
'kill': 1, 'the': 3, 'soft': 1, 'Juliet': 1}
```

It is a bit inconvenient to look through the dictionary to find the most common words and their counts, so we need to add some more Python code to get us the output that will be more helpful.

## 9.3 Looping and dictionaries

If you use a dictionary as the sequence in a for statement, it traverses the keys of the dictionary. This loop prints each key and the corresponding value:

```python no-exec id=8cfebb05-3433-4b91-9caf-9e9bd2f2e6b5
counts = { 'chuck' : 1 , 'annie' : 42, 'jan': 100}
for key in counts:
  print(key, counts[key])
```

Here’s what the output looks like:

```python no-exec id=b7717fd0-eedb-4dc9-96d1-3820a5323972
jan 100
chuck 1
annie 42
```

Again, the keys are in no particular order. We can use this pattern to implement the various loop idioms that we have de- scribed earlier. For example if we wanted to find all the entries in a dictionary with a value above ten, we could write the following code:

```python no-exec id=cfd5486a-6f4d-411e-b3a6-f04a115654fc
counts = { 'chuck' : 1 , 'annie' : 42, 'jan': 100}
for key in counts:
  if counts[key] > 10 :
    print(key, counts[key])
```

The for loop iterates through the keys of the dictionary, so we must use the index operator to retrieve the corresponding value for each key. Here’s what the output looks like:

```no-exec id=ff024e4e-3da4-4a42-b479-1c1353187cdf
jan 100
annie 42
```

We see only the entries with a value above 10. If you want to print the keys in alphabetical order, you first make a list of the keys in the dictionary using the keys method available in dictionary objects, and then sort that list and loop through the sorted list, looking up each key and printing out key-value pairs in sorted order as follows:

```python no-exec id=05500e63-5ab9-4508-9daf-4010bc245dad
counts = { 'chuck' : 1 , 'annie' : 42, 'jan': 100}
lst = list(counts.keys())
print(lst)
lst.sort()
for key in lst:
  print(key, counts[key])
```

Here’s what the output looks like:

```python no-exec id=fec463f8-b9a8-42f7-ae56-680d1cfb66ca
['jan', 'chuck', 'annie']
annie 42
chuck 1
jan 100
```

First you see the list of keys in unsorted order that we get from the keys method. Then we see the key-value pairs in order from the for loop.

## 9.4 Advanced text parsing

In the above example using the file romeo.txt, we made the file as simple as possible by removing all punctuation by hand. The actual text has lots of punctuation, as shown below.

```no-exec id=40381828-b2d0-453d-9a66-b5662a78442d
But, soft! what light through yonder window breaks?
It is the east, and Juliet is the sun.
Arise, fair sun, and kill the envious moon,
Who is already sick and pale with grief,
```

Since the Python split function looks for spaces and treats words as tokens separated by spaces, we would treat the words “soft!” and “soft” as different words and create a separate dictionary entry for each word.

Also since the file has capitalization, we would treat “who” and “Who” as different words with different counts.

We can solve both these problems by using the string methods lower, punctuation, and translate. The translate is the most subtle of the methods. Here is the documentation for translate: line.translate(str.maketrans(fromstr, tostr, deletestr))

Replace the characters in fromstr with the character in the same position in tostr and delete all characters that are in deletestr. The fromstr and tostr can be empty strings and the deletestr parameter can be omitted. We will not specify the tostr but we will use the deletestr parameter to delete all of the punctuation. We will even let Python tell us the list of characters that it considers “punctuation”:

```python no-exec id=a85b71b7-8453-44df-bbed-1f2a2d6dfa34
>>> import string
>>> string.punctuation '!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'

# The parameters used by translate were different
# in Python 2.0. We make the following
# modifications to our program:

import string
fname = input('Enter the file name: ')
try:
  fhand = open(fname)
except:
  print('File cannot be opened:', fname)
  exit()

counts = dict()
for line in fhand:
  line = line.rstrip()

  line = line.translate(line.maketrans('', '', string.punctuation)) line = line.lower()
  words = line.split()
  for word in words:
    if word not in counts:
      counts[word] = 1
    else:
      counts[word] += 1

print(counts)

# Code: http://www.py4e.com/code3/count2.py
```

Part of learning the “Art of Python” or “Thinking Pythonically” is realizing that Python often has built-in capabilities for many common data analysis problems. Over time, you will see enough example code and read enough of the documentation to know where to look to see if someone has already written something that makes your job much easier. The following is an abbreviated version of the output:

```no-exec id=f9b8f8d3-e42e-4398-a1e4-f410a311f7cc
Enter the file name: romeo-full.txt
{'swearst': 1, 'all': 6, 'afeard': 1, 'leave': 2, 'these': 2,
'kinsmen': 2, 'what': 11, 'thinkst': 1, 'love': 24, 'cloak': 1,
a': 24, 'orchard': 2, 'light': 5, 'lovers': 2, 'romeo': 40,
'maiden': 1, 'whiteupturned': 1, 'juliet': 32, 'gentleman': 1,
'it': 22, 'leans': 1, 'canst': 1, 'having': 1, ...}
```

Looking through this output is still unwieldy and we can use Python to give us exactly what we are looking for, but to do so, we need to learn about Python tuples. We will pick up this example once we learn about tuples.

## 9.5 Debugging

As you work with bigger datasets it can become unwieldy to debug by printing and checking data by hand. Here are some suggestions for debugging large datasets:

1. **Scale down the input If possible, reduce the size of the dataset**. For example if the program reads a text file, start with just the first 10 lines, or with the smallest example you can find. You can either edit the files themselves, or (better) modify the program so it reads only the first n lines. If there is an error, you can reduce n to the smallest value that manifests the error, and then increase it gradually as you find and correct errors.
2. **Check summaries and types** Instead of printing and checking the entire dataset, consider printing summaries of the data: for example, the number of items in a dictionary or the total of a list of numbers. A common cause of runtime errors is a value that is not the right type. For debugging this kind of error, it is often enough to print the type of a value.
3. **Write self-checks** Sometimes you can write code to check for errors automatically. For example, if you are computing the average of a list of numbers, you could check that the result is not greater than the largest element in the list or less than the smallest. This is called a “sanity check” because it detects results that are “completely illogical”. Another kind of check compares the results of two different computations to see if they are consistent. This is called a “consistency check”.
4. **Pretty print the output** Formatting debugging output can make it easier to spot an error.

Again, time you spend building scaffolding can reduce the time you spend debugging

## 9.6 Glossary

**dictionary** A mapping from a set of keys to their corresponding values.

**hashtable** The algorithm used to implement Python dictionaries.

**hash function** A function used by a hashtable to compute the location for a key.

**histogram** A set of counters.

**implementation** A way of performing a computation.

**item** Another name for a key-value pair.

**key** An object that appears in a dictionary as the first part of a key-value pair.

**key-value pair** The representation of the mapping from a key to a value.

**lookup** A dictionary operation that takes a key and finds the corresponding value.

**nested loops** When there are one or more loops “inside” of another loop. The inner loop runs to completion each time the outer loop runs once.

**value** An object that appears in a dictionary as the second part of a key-value pair. This is more specific than our previous use of the word “value”.
