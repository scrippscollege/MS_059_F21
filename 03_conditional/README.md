# Python and Viz (Scripps College F2021) 03

# Python for Everybody (Scripps College F2021)

*Python for Everybody: Exploring Data Using Python 3 Dr. Charles R. Severance*

ported to Jupyter Notebooks by Douglas Goodwin, 2021.

Content Copyright 2009- Dr. Charles R. Severance with edits and additions by Douglas Goodwin.

This work is licensed under a Creative Commons Attribution-NonCommercial- ShareAlike 3.0 Unported License. This license is available at <https://creativecommons.org/licenses/by-nc-sa/3.0/>

## Chapter 3: Conditional execution

We look at how Python executes some statements and skips others.

### Videos

* [Conditional Execution - Part 1](https://youtu.be/2aA3VBdcl6A)
* [Conditional Execution - Part 2](https://youtu.be/OczkNrHPBps)
* [Worked Exercise 3.1](https://youtu.be/oUMQbZ4SBuM)
* [Worked Exercise 3.2](https://youtu.be/-iUA4cCKRlM)

### Slides

* [Pythonlearn-03-Conditional.pptx](https://www.py4e.com/lectures3/Pythonlearn-03-Conditional.pptx)

### References

* [Chapter 3: Conditionals](https://www.py4e.com/html3/03-conditional)

### Tools:

* [Autograder: Exercise 3.1](https://www.py4e.com/lessons_launch/pythonauto_03_01)
* [Autograder: Exercise 3.3](https://www.py4e.com/lessons_launch/pythonauto_03_03)
* [Quiz: Conditional Execution](https://www.py4e.com/lessons_launch/py4e_03_if_quiz)

## 3.1 Boolean expressions

A boolean expression is an expression that is either true or false. The following examples use the operator ==, which compares two operands and produces True if they are equal and False otherwise:

```python no-exec id=e4719b33-459a-45a3-9965-9c9b135b181c
>>> 5 == 5
True
>>> 5 == 6
False
```

True and False are special values that belong to the class bool; they are not strings:

```python no-exec id=4e1490f9-75d9-4a4a-95cb-b06baa29d10a
>>> type(True)
<class 'bool'>
>>> type(False)
<class 'bool'>
```

The == operator is one of the comparison operators; the others are:

comparisondescriptionx != yx is not equalx > yx is greater than yx < yx is less than yx >= yx is greater than or equal to yx <= yx is less than or equal to yx is yx is the same as yx is not yx is not the same as y

Although these operations are probably familiar to you, the Python symbols are different from the mathematical symbols for the same operations. A common error is to use a single equal sign (=) instead of a double equal sign (==). Remember that = is an assignment operator and == is a comparison operator. There is no such thing as =< or =>.

## 3.2 Logical operators

There are three logical operators: and, or, and not. The semantics (meaning) of these operators is similar to their meaning in English. For example,

```python no-exec id=d338f222-b8d8-4405-80a8-8c293734fb80
x > 0 and x < 10
```

is true only if x is greater than 0 and less than 10.

```no-exec id=e8671991-bd47-4550-8f67-11c09a78909e
n%2 == 0 or n%3 == 0
```

is true if *either* of the conditions is true, that is, if the number is divisible by 2 or 3.

Finally, the not operator negates a boolean expression, so not (x > y) is true if x > y is false;that is,if x is less than or equal to y.

Strictly speaking, the operands of the logical operators should be boolean expres- sions, but Python is not very strict. Any nonzero number is interpreted as “True.”

```no-exec id=2bda4e63-b4a8-4a2d-8ca0-b40920fda582
>>> 17 and True
True
```

This flexibility can be useful, but there are some subtleties to it that might be confusing. You might want to avoid it until you are sure you know what you are doing.

## 3.3 Conditional execution

In order to write useful programs, we almost always need the ability to check condi- tions and change the behavior of the program accordingly. Conditional statements give us this ability. The simplest form is the if statement:

```no-exec id=3ef34f1f-b852-45dc-b86a-44e5e04a1292
if x > 0 :
  print('x is positive')
```

The boolean expression after the if statement is called the condition. We end the if statement with a colon character (:) and the line(s) after the if statement are indented.

[Fig 3.1, if logic][nextjournal#file#015c17d1-7b51-4321-bc83-42d6fb0ab462]

If the logical condition is true, then the indented statement gets executed. If the logical condition is false, the indented statement is skipped.

if statements have the same structure as function definitions or for loops\[^1\]. The statement consists of a header line that ends with the colon character (:) followed by an indented block. Statements like this are called compound statements because they stretch across more than one line.

\[^1\]: We will learn about functions in Chapter 4 and loops in Chapter 5.

There is no limit on the number of statements that can appear in the body, but there must be at least one. Occasionally, it is useful to have a body with no statements (usually as a place holder for code you haven’t written yet). In that case, you can use the pass statement, which does nothing.

```python no-exec id=1ed318e8-8d7d-4dbf-8a62-c06c3decab2b
if x < 0 :
  pass # need to handle negative values!
```

If you enter an if statement in the Python interpreter, the prompt will change from three chevrons to three dots to indicate you are in the middle of a block of statements, as shown below:

```python no-exec id=fd803b8b-6c1e-47d2-9d44-e1031ffb8d75
>>> x = 3
>>> if x < 10:
... print('Small') ...
Small
>>>
```

When using the Python interpreter, you must leave a blank line at the end of a block, otherwise Python will return an error:

```python no-exec id=21485aa4-1e0a-4005-8e80-9da9b24e724e
>>> x = 3
>>> if x < 10:
... print('Small') ... print('Done')
  File "<stdin>", line 3
    print('Done')
^
SyntaxError: invalid syntax
```

A blank line at the end of a block of statements is not necessary when writing and executing a script, but it may improve readability of your code.

## 3.4 Alternative execution

A second form of the if statement is alternative execution, in which there are two possibilities and the condition determines which one gets executed. The syntax looks like this:

```python no-exec id=8a48c2cd-b048-4b7a-ae8a-e8222bd416ab
if x%2 == 0 :
  print('x is even')
else :
  print('x is odd')
```

If the remainder when x is divided by 2 is 0, then we know that x is even, and the program displays a message to that effect. If the condition is false, the second set of statements is executed.

[Figure 3.2: If-Then-Else Logic][nextjournal#file#b416f9d3-1e09-40a6-aaca-d3a74c88607a]

Since the condition must either be true or false, exactly one of the alternatives will be executed. The alternatives are called branches, because they are branches in the flow of execution.

## 3.5 Chained conditionals

Sometimes there are more than two possibilities and we need more than two branches. One way to express a computation like that is a *chained conditional*:

```python no-exec id=d32768d5-d337-45c6-b71e-50ecaa16d454
if x < y:
  print('x is less than y')
elif x > y:
  print('x is greater than y')
else:
  print('x and y are equal')
```

*elif* is an abbreviation of “else if.” Again, exactly one branch will be executed. There is no limit on the number of elif statements. If there is an else clause, it has to be at the end, but there doesn’t have to be one.

```python no-exec id=337bb602-6f70-4b13-8833-e6e7b254fcf1
if choice == 'a':
  print('Bad guess')
elif choice == 'b':
  print('Good guess')
elif choice == 'c':
  print('Close, but not correct')
```

[Figure 3.3: If-Then-ElseIf Logic][nextjournal#file#52526ea0-a56d-4075-9f9e-7ad449335c6d]

Each condition is checked in order. If the first is false, the next is checked, and so on. If one of them is true, the corresponding branch executes, and the statement ends. Even if more than one condition is true, only the first true branch executes.

## 3.6 Nested conditionals

One conditional can also be nested within another. We could have written the three-branch example like this:

```python no-exec id=cc44ed2f-df88-4615-aee4-459f038291f4
if x == y:
  print('x and y are equal')
else:
  if x < y:
    print('x is less than y')
  else:
    print('x is greater than y')
```

The outer conditional contains two branches. The first branch contains a simple statement. The second branch contains another if statement, which has two branches of its own. Those two branches are both simple statements, although they could have been conditional statements as well.

Although the indentation of the statements makes the structure apparent, nested conditionals become difficult to read very quickly. In general, it is a good idea to avoid them when you can.

Logical operators often provide a way to simplify nested conditional statements. For example, we can rewrite the following code using a single conditional:

```python no-exec id=3cc917e5-fbd1-443e-8429-8df5229a8568
if 0 < x:
  if x < 10:
    print('x is a positive single-digit number.')
```

The print statement is executed only if we make it past both conditionals, so we can get the same effect with the and operator:

[Figure 3.4: Nested If Statements][nextjournal#file#47c64aa6-9c97-4a7f-8670-d9efd518172b]

```python no-exec id=b51d2312-c446-4feb-92f8-b27f196d5c23
if 0 < x and x < 10:
  print('x is a positive single-digit number.')
```

## 3.7 Catching exceptions using try and except

Earlier we saw a code segment where we used the input and int functions to read and parse an integer number entered by the user. We also saw how treacherous doing this could be:

```python no-exec id=71b6555c-5283-4038-95de-f5215cb6ccc3
>>> prompt = "What is the air velocity of an unladen swallow?\n"
>>> speed = input(prompt)
What is the air velocity of an unladen swallow?
What do you mean, an African or a European swallow?
>>> int(speed)
ValueError: invalid literal for int() with base 10:
>>>
```

When we are executing these statements in the Python interpreter, we get a new prompt from the interpreter, think “oops”, and move on to our next statement.

However if you place this code in a Python script and this error occurs, your script immediately stops in its tracks with a traceback. It does not execute the following statement.

Here is a sample program to convert a Fahrenheit temperature to a Celsius temperature:

```python no-exec id=5fa8ffec-8b14-472e-ad1c-ea2cd70521b1
inp = input('Enter Fahrenheit Temperature: ')
fahr = float(inp)
cel = (fahr - 32.0) * 5.0 / 9.0
print(cel)
```

Code: <http://www.py4e.com/code3/fahren.py>

If we execute this code and give it invalid input, it simply fails with an unfriendly error message: python [fahren.py](http://fahren.py) Enter Fahrenheit Temperature:72 22.22222222222222 python [fahren.py](http://fahren.py) Enter Fahrenheit Temperature:fred Traceback (most recent call last): File "[fahren.py](http://fahren.py)", line 2, in  fahr = float(inp) ValueError: could not convert string to float: 'fred' There is a conditional execution structure built into Python to handle these types of expected and unexpected errors called “try / except”. The idea of try and except is that you know that some sequence of instruction(s) may have a problem and you want to add some statements to be executed if an error occurs. These extra statements (the except block) are ignored if there is no error. You can think of the try and except feature in Python as an “insurance policy” on a sequence of statements. We can rewrite our temperature converter as follows:

```python no-exec id=23f75b24-cea7-43d7-a983-81e75e21aa38
inp = input('Enter Fahrenheit Temperature:')
try:
  fahr = float(inp)
  cel = (fahr - 32.0) * 5.0 / 9.0
  print(cel)
except:
  print('Please enter a number')
```

# Code: <http://www.py4e.com/code3/fahren2.py>

Python starts by executing the sequence of statements in the try block. If all goes well, it skips the except block and proceeds. If an exception occurs in the try block, Python jumps out of the try block and executes the sequence of statements in the except block.

```no-exec id=0b9d79df-ac74-4f29-95cc-eb91922870f9
python fahren2.py
Enter Fahrenheit Temperature:72
22.22222222222222
```

```no-exec id=0bab99a4-f95c-4c38-858d-50339cf0a704
python fahren2.py
Enter Fahrenheit Temperature:fred
Please enter a number
```

Handling an exception with a try statement is called catching an exception. In this example, the except clause prints an error message. In general, catching an exception gives you a chance to fix the problem, or try again, or at least end the program gracefully.

# Appendix

[github-repository][nextjournal#github-repository#77fbe67d-f80f-4a2a-aee4-fef9b7b91b9b]


[nextjournal#file#015c17d1-7b51-4321-bc83-42d6fb0ab462]:
<https://nextjournal.com/data/?node-id=015c17d1-7b51-4321-bc83-42d6fb0ab462&filename=Fig%203.1%2C%20if%20logic&node-kind=file>

[nextjournal#file#b416f9d3-1e09-40a6-aaca-d3a74c88607a]:
<https://nextjournal.com/data/?node-id=b416f9d3-1e09-40a6-aaca-d3a74c88607a&filename=Figure%203.2%3A%20If-Then-Else%20Logic&node-kind=file>

[nextjournal#file#52526ea0-a56d-4075-9f9e-7ad449335c6d]:
<https://nextjournal.com/data/?node-id=52526ea0-a56d-4075-9f9e-7ad449335c6d&filename=Figure%203.3%3A%20If-Then-ElseIf%20Logic&node-kind=file>

[nextjournal#file#47c64aa6-9c97-4a7f-8670-d9efd518172b]:
<https://nextjournal.com/data/?node-id=47c64aa6-9c97-4a7f-8670-d9efd518172b&filename=Figure%203.4%3A%20Nested%20If%20Statements&node-kind=file>

[nextjournal#github-repository#77fbe67d-f80f-4a2a-aee4-fef9b7b91b9b]:
<https://github.com/scrippscollege/MS_059_F21>

<details id="com.nextjournal.article">
<summary>This notebook was exported from <a href="https://nextjournal.com/a/?change-id=CzjKArPbUrSqM4eZ4q4Sc8">https://nextjournal.com/a/?change-id=CzjKArPbUrSqM4eZ4q4Sc8</a></summary>

```edn nextjournal-metadata
{:article {:nodes {"015c17d1-7b51-4321-bc83-42d6fb0ab462" {:id "015c17d1-7b51-4321-bc83-42d6fb0ab462", :kind "file"}, "0b9d79df-ac74-4f29-95cc-eb91922870f9" {:id "0b9d79df-ac74-4f29-95cc-eb91922870f9", :kind "code-listing"}, "0bab99a4-f95c-4c38-858d-50339cf0a704" {:id "0bab99a4-f95c-4c38-858d-50339cf0a704", :kind "code-listing"}, "1ed318e8-8d7d-4dbf-8a62-c06c3decab2b" {:id "1ed318e8-8d7d-4dbf-8a62-c06c3decab2b", :kind "code-listing"}, "21485aa4-1e0a-4005-8e80-9da9b24e724e" {:id "21485aa4-1e0a-4005-8e80-9da9b24e724e", :kind "code-listing"}, "23f75b24-cea7-43d7-a983-81e75e21aa38" {:id "23f75b24-cea7-43d7-a983-81e75e21aa38", :kind "code-listing"}, "2bda4e63-b4a8-4a2d-8ca0-b40920fda582" {:id "2bda4e63-b4a8-4a2d-8ca0-b40920fda582", :kind "code-listing"}, "337bb602-6f70-4b13-8833-e6e7b254fcf1" {:id "337bb602-6f70-4b13-8833-e6e7b254fcf1", :kind "code-listing"}, "3cc917e5-fbd1-443e-8429-8df5229a8568" {:id "3cc917e5-fbd1-443e-8429-8df5229a8568", :kind "code-listing"}, "3ef34f1f-b852-45dc-b86a-44e5e04a1292" {:id "3ef34f1f-b852-45dc-b86a-44e5e04a1292", :kind "code-listing"}, "47c64aa6-9c97-4a7f-8670-d9efd518172b" {:id "47c64aa6-9c97-4a7f-8670-d9efd518172b", :kind "file"}, "4e1490f9-75d9-4a4a-95cb-b06baa29d10a" {:id "4e1490f9-75d9-4a4a-95cb-b06baa29d10a", :kind "code-listing"}, "52526ea0-a56d-4075-9f9e-7ad449335c6d" {:id "52526ea0-a56d-4075-9f9e-7ad449335c6d", :kind "file"}, "5fa8ffec-8b14-472e-ad1c-ea2cd70521b1" {:id "5fa8ffec-8b14-472e-ad1c-ea2cd70521b1", :kind "code-listing"}, "71b6555c-5283-4038-95de-f5215cb6ccc3" {:id "71b6555c-5283-4038-95de-f5215cb6ccc3", :kind "code-listing"}, "77fbe67d-f80f-4a2a-aee4-fef9b7b91b9b" {:id "77fbe67d-f80f-4a2a-aee4-fef9b7b91b9b", :kind "github-repository", :ref "main"}, "8a48c2cd-b048-4b7a-ae8a-e8222bd416ab" {:id "8a48c2cd-b048-4b7a-ae8a-e8222bd416ab", :kind "code-listing"}, "b416f9d3-1e09-40a6-aaca-d3a74c88607a" {:id "b416f9d3-1e09-40a6-aaca-d3a74c88607a", :kind "file"}, "b51d2312-c446-4feb-92f8-b27f196d5c23" {:id "b51d2312-c446-4feb-92f8-b27f196d5c23", :kind "code-listing"}, "cc44ed2f-df88-4615-aee4-459f038291f4" {:id "cc44ed2f-df88-4615-aee4-459f038291f4", :kind "code-listing"}, "d32768d5-d337-45c6-b71e-50ecaa16d454" {:id "d32768d5-d337-45c6-b71e-50ecaa16d454", :kind "code-listing"}, "d338f222-b8d8-4405-80a8-8c293734fb80" {:id "d338f222-b8d8-4405-80a8-8c293734fb80", :kind "code-listing"}, "e4719b33-459a-45a3-9965-9c9b135b181c" {:id "e4719b33-459a-45a3-9965-9c9b135b181c", :kind "code-listing"}, "e8671991-bd47-4550-8f67-11c09a78909e" {:id "e8671991-bd47-4550-8f67-11c09a78909e", :kind "code-listing"}, "fd803b8b-6c1e-47d2-9d44-e1031ffb8d75" {:id "fd803b8b-6c1e-47d2-9d44-e1031ffb8d75", :kind "code-listing"}}, :nextjournal/id nil, :article/change {:nextjournal/id #uuid "6123ff23-3702-45eb-ae37-719a94414251"}}}
```
</details>
