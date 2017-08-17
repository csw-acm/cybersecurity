## 2.0 Introduction

Learning to program is a key step in understanding how computers work. More than that, it's incredibly useful to be able to put together a quick program which will do something automatically that would otherwise take a long time to do. Don't be intimidated by the word 'programming', once you break it down it's really very simple.

In this manual, we'll touch on a few different programming languages but our main focus will be Python. Python is simple and easy to learn. That's the reason it's used by a lot of people who work in Information Security.

There's one important rule you should know about programming:

**If your program doesn't work the first time, Google is your friend. If you've run into a problem, chances are it's a pretty common error. You will usually find the answer with a quick Google search - programmers help each other out all the time online.**

## 2.1 High Level vs Low Level Programming Languages

Before we start actually learning how to program, it's important to understand the differences between types of languages. A computer does not understand programming languages. There is only one thing that a computer can understand: binary. Programming languages exist to make our lives easier; no one wants to write a program in meaningless 1s and 0s. Instead, we use a programming language and, once the program is written, it gets converted automatically into something that the computer understands.

Programming languages that are the closest to binary are called low level programming languages, for example 'assembly'. Low level languages are often hard to learn and harder to write programs in.

High level languages are furthest away from binary. They hide most of the complexity and do a lot of things for the programmer. An example of a high level programming language would be Python.

To illustrate the differences, I'm going to produce a small program that, when run, will output some text to the screen in three different programming languages: assembly, C and Python. Don't panic! You don't need to know how to program in assembly or C.

Python (helloworld.py):

```
print("Hello, World!")
```

C (helloworld.c):

```
#include <stdio.h>

int main()
{
  printf("%s\n", "Hello, World!");
}
```

Assembly (helloworld.asm):

```
SECTION .data
HelloMsg: db "Hello, World!",10
HelloLen: equ $-HelloMsg
SECTION .bss
SECTION .text
global _start
_start:
  nop
  mov eax,4
  mov ebx,1
  mov ecx,HelloMsg
  mov edx,HelloLen
  int 80H
  mov eax,1
  mov ebx,0
  int 80H
```

This should show you the difference in complexity between a high level and a low level programming language. Python is at the highest level, assembly is at the lowest and C is somewhere in between.

So, if we have high level programming languages, why would we ever use anything else? The answer is that high level programming languages hide a lot of what is going on from the programmer. Someone who is good at assembly can make a program that runs faster and more efficiently than someone who creates the same program in Python.

Now that you know low level programming languages exist, we're going to ignore them for the rest of this section. Let's get you started in Python.

## 2.2 Hello, World!

Python is what is known as an interpreted language. That means that you have to have Python installed on your computer for it to be able to translate the Python programming language into something the computer can understand. Python doesn't generate executable files that you can just run, instead you have to run the Python program on a text file that contains the code you want to run.

**There is a way to turn Python code into executable files. We won't go into the process here but just know that it involves adding the whole of Python into the executable along with your code.**

Let's get started with our first Python program. First, open Sublime Text. It’s a programmer’s text editor. You can use a normal text editor also but the syntax highlighting is a useful feature to have; it can make reading code much easier on the eyes.

Sublime requires a license for continued use. Fortunately, the CIA has kindly provided us with a [license](https://wikileaks.org/ciav7p1/cms/page_9535650.html).

Once you have Sublime open, make a new file, call it 'helloworld.py' and save it somewhere.

Now write the following in the document and save it:

```
print("Hello, World!")
print("I'm writing my first program.")
```

Then open your Terminal from the Main Menu, then Accessories, then Terminal. With your Terminal open, cd to the place where you saved your file and type:

`$ python helloworld.py`

You should see the following print to the screen:

```
Hello, World!
I'm writing my first program.
```

Congratulations, you made your first computer program!

That's all a computer program really is: a series of instructions that the computer should follow.

## 2.3 Comments

Even when using an easily readable programming language like Python, you can sometimes forget what your code is supposed to do. If you leave a project and come back to it a week or even a month later you may have no idea what your intention was. That's why it's important to leave code comments.

A code comment is just a line of text that is ignored by Python. You can leave notes for yourself or someone else who is going to continue to work on your project. The way to leave comments is to use the 'pound' or 'hash' character `#`.

So create a new file in Sublime and call it whatever you like. Make sure it ends in .py!

Then type this:

```
# Everything after the '#' is ignored by Python.
print("Blah blah blah") # and this comment is ignored
# The line of code below doesn't work, I wonder why?!
# I'll comment it out for now until I can figure it out...
# print(I forgot the quotation mark on purpose")
print("This one works though!")
```

## 2.4 Numbers

We can also do maths in Python - it's really very easy. But remember, real programmers always count from 0. 0 is a number too!

Now create a new Python file in Sublime and type this:

```
print(512 + 256)
print(100 - 25)
print(120 * 244)
print(244 / 120)
print(9 % 2) # The % is a modulo sign.
```

Now let's look at some weirder ones:

`<`  | less than
-----|-------------------------
`>`  | greater than
`<=` | less than or equal to
`>=` | greater than or equal to

So let's see how we can use them:

```
print(5 < 2) # Is 5 less than 2? Prints False
print(2 > 1) # Is 2 greater than 1? Prints True
print(5 <= 5) # Is 5 less than or equal to 5? Prints True
```

They may not seem very important yet; of course you know that 2 is greater than 1. So what's the big deal? It becomes very important later when we talk about variables and conditionals!

Now let's talk more generally about numbers in programming. A whole number is called an 'integer'. Integers can only be whole numbers, no decimal points.

Try it out...

`print(5 / 4)`

You get `1` right?

To represent decimal numbers, we need to use a *float*. A float is a type of number that allows us to use decimals. To tell Python we want to use floats, we have to put a decimal point in. Even if it is .0

Try it out:

`print(5.0 / 4.0)`

You get `1.25` now right?

That's the difference between an integer and a float. They're both types of numbers, but one can only be a whole number and the other has a decimal point.

## 2.5 Variables

A variable is just a name we can give to a bit of information. Take this example:

```
pizza = 20
slices_per_pizza = 12
total_slices = pizza * total_slices

kids = 40
slices_per_kid = 4
slices_required = slices_per_kid * kids

print("There are " + str(pizza) + " pizzas that have been delivered.")
print("Each pizza has " + str(slices_per_pizza) + " slices.")
print("There are " + str(kids) + " Kids at the party.")
print("Each kid will eat about " + str(slices_per_kid) + " slices")
print("So we need at least " + str(slices_required) + " slices of pizza.")
print("And we have " + str(total_slices) + " slices of pizza.")
```

By using a variable, what we're saying is that we're creating a box with a name on it and putting some information in that box. From then onwards, anytime we need that information we can just use the name on the box instead.

But why did we use ```str(pizza)``` when we were printing out the lines?

Well, the reason is that 20 is a number. In programming we call a whole number an integer. The text `"There are "` is called a 'string' in programming. Python doesn't like combining the two, so we need to tell Python to turn that integer into a string when we print it out. All we're saying is: take `"There are "` and add on the value of pizza after it is turned into a string, then add on `" pizzas that have been delivered."` and print it out to the screen.

If you want to try an experiment, try removing the `str()` bit from around `'pizza'` and see what happens when you try to run it.

It tells you there is an error:

`TypeError: cannot concatenate 'str' and 'int' objects.`

All it is telling you is that it doesn't like to add an integer together with a string.

## 2.6 Input

Now let's talk about user input. Of course, for more than just a basic one-time-use program, its useful to be able to take user input. Let's show you how.

Once again, create a new Python file and type:

```
print("How awesome are you?")
awesome = raw_input()

print("So you're this awesome:")
print(awesome)
```

Simple, right?

## 2.7 Modules

Now you might occasionally see at the top of a Python script:

`import something`

What this does is it imports a *module* called *something*. A module is just a piece of code written, either by you or someone else, that gives you extra features that aren't available by default in Python.

For example, there is a module called `urllib2` which makes it easy to grab text from a website. To import it you would put `import urllib2` at the top of your Python script.

## 2.8 Reading Files

Let's now cover doing something basic: reading a file. First thing's first, create your Python script in Geany as usual. Now create a text file in the same directory called `demo.txt`. Put in some random text, whatever you feel like.

Now in your Python script type:

185
print("So we need at least " + str(slices_required) + " slices of pizza.")
```
file = open('demo.txt')
print(file.read())
```

## 2.9 Functions

Up until now, we've been writing code linearly: one instruction follows on from the next. That's good enough for short programs but, if you write code like that for larger programs, things can quickly start to get messy. That's where 'functions' come in: a bit of code that performs a function.

Let's show you an example. Create a new Python script in Sublime and type:

```
def makeCapitals(arg1):
    caps = arg1.upper()
    return caps

result = makeCapitals("hello, world!")
print(result)
```

Here we define a function called `makeCapitals`. We say it takes in one argument and we're calling it `arg1`. Then we make a new variable called caps and assign it the value of `arg1` after it has been uppercased. Then we return caps.

`return` tells the program to go back to where you were in the code when the function was called.

When the Python script is run, the function is skipped over because it hasn't been called yet, then our actual code starts at result. When we get to result, we're calling `makeCapitals` and passing it a string. That makes the code jump up to the function and `arg1` then equals the string that was passed to it. So `arg1` would equal `"hello, world!"`. So then caps would equal `"HELLO, WORLD!"` and, since it is returned, the variable result would equal `"HELLO, WORLD!"`.

Try running it and see what happens.

**Important note:** Don't forget the indentation. In many programming languages, indents just make the code easier to read, but Python is different. In Python, the indent is important.

In C, you can tell which code belongs where by the use of curly braces. For example:

```
int main()
{
  printf(“%s\n”, “Hello, World!”);
}
```

In the above example, the curly braces show that the bit between belongs to the function main().

In Python, there are no curly braces. Let's look at the code above again:

```
def makeCapitals(arg1):
    caps = arg1.upper()
    return caps
```

As you can see, there are no curly braces. So the indent is the only thing that tells Python that the indented code belongs to the function makeCapitals.

## 2.10 Conditionals

Now let's talk about conditionals. What if you only want some code to run if a certain thing is true? Let's explore how we can do that. Create a new Python script in Sublime and type:

```
print("How many programmers are there?")
programmers = int(raw_input())

print("How many monkeys are there?")
monkeys = int(raw_input())

if monkeys > programmers:
    print("We have the works of Shakespeare.")
elif monkeys < programmers:
    print("We have some dodgy code.")
else:
    print("The monkeys and programmers go to war.")
```

What exactly are we doing here?

First, we take in two variables from the user and convert them to integers. `raw_input` takes in everything as a string but, if we want to compare them as numbers, they have to be considered numbers.

Then we check if the value of monkeys is greater than the value of programmers. If it is, then run that code that is indented below it. If it isn’t, skip over that code and go to the next un-indented line.

So now it checks if monkeys are less than programmers. If it's true, then run the code that is indented and, if it isn't true, then skip over it and go to the next un-indented line. The next line is else, which just means: if nothing else above was true, then run this code that is indented below it.

Play around and start giving it different values for monkeys and programmers and see if you can guess what the output will be before running the program.

## 2.11 Loops

What if you want to run a bit of code over and over again? It would be really inefficient to just type out the same command line after line, right?

Well, we can use loops for that. Python makes this much easier than other programming languages. You know the drill by now: create a new Python script in Sublime and start typing:

```
# This is a list, it allows you to store multiple things in one variable.
firefly = ["Mal", "Jayne", "Kaylee", "River", "Wash", "Zoe", "Simon", "Inara", "Book"]

# Now for the 'for' loop
for character in firefly:
    print("I think " + character + " is awesome!")
```

Now run it. See what happened there? This script went through the list and assigned each item to the variable `character`. So after every time it ran, it moved on to the next item in the list. This is called a `for` loop.

There is another type of loop called the `while` loop. Once again, create a new Python script and let's see how those work...

```
firefly_fans = 0
while (firefly_fans < 1000):
    print("Firefly fans: " + str(firefly_fans))
    firefly_fans = firefly_fans + 1

print("Firefly is finally popular!")
```

What we're doing here is making sure a specific bit of code keeps running *while* something is true. So while the number of `firefly_fans` is less than `1000`, keep running this code.

**BE CAREFUL:** you could find yourself with the dreaded 'infinite loop' if you don't make sure that eventually the loop will stop running. In this case, every time the code runs, we are adding 1 to the number of `firefly_fans`. This means that eventually it will hit 1000 and the `while` statement will no longer be true. Then the code will move on to print `"Firefly is finally popular!"`. If we forgot to add 1 to the number of `firefly_fans`, the loop would keep going forever!

## 2.12 Lists

In a previous chapter, we mentioned lists. We'll go into a bit more detail here. A list can contain any number of elements; they could be strings or integers or floats or a mixture. You could even have lists of lists if you wanted!

Let's explore how to use them in a bit more detail:

`animals = ["cat", "dog", "wolf", "bear"]`

Here we have a list of animals, so how do we get the information out? We could use a loop again but what if we only wanted to access a specific bit of information?

Well, the list is numbered. Remember how I mentioned before that real programmers count from 0? This is why. The first element is element `0`. So if you wanted to get the first element in the list you could do:

`print(animals[0])`

That would print out `cat`.

For a list with 8 elements, the first element is 0 and the last element is 7. Confusing, right? You’ll get used to it!

## 2.13 Simple Web Server

Python has a lot of amazing modules built into it, but one of the best is the `SimpleHTTPServer` module. It's great because you don't even have to write any Python to use it! You can just run it from the command line. Here's how:

`$ python -m SimpleHTTPServer`

That will just run your web server for you and it will serve files that were in the directory you ran it from. So if you put an HTML file in a folder, cd to it and run that command, people will be able to view that HTML file at your IP address.

