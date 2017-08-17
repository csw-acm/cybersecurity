5.0 Introduction

Now we'll touch briefly on cryptography, including the differences between encoding and encryption. You'll need to know how to count for this chapter but you won't need any more maths than that!

5.1 Encoding vs Encryption

Encoding and encryption are often mixed up but the truth is that they're very different. Encoding is just converting something from one format into another. There are no passwords involved and it's not designed for security. Instead, it's meant to allow data to be used on other systems that support different formats. Let's have a look at some encoding.

Take the number 31337. If we were to encode it into hexadecimal format it would be: 7A69.

There's nothing really secure about that; you can easily convert it back from hex and get 31337 again and so could anybody else. The only thing that might stop people would be if they didn't know what it was encoded in. That isn't a good security practice at all.

Now let's look at encryption. To encrypt something, you convert it from one format into another, similar to encoding. But that's where the similarities end. The goal of encryption is to transform data so that it can't be easily read by anyone other than the intended recipient.

5.2 Number Bases

Before we look at various encoding methods, we should talk about alternate number bases. This sounds intimidating but it's actually a very simple concept.

Don't panic if you don't understand this! It's nice to know it but you won't need to learn how to calculate these manually. There are plenty of online tools that will do this for you!

Think about what happens when you count. You start from 0, then count all the way up to 9. After 9, you run out of numbers, so you have to turn the 9 back into a 0 and then you just add a 1 to the left of it. This counting system is called 'base-10' and it developed because humans have 10 fingers to count on.

Let's look at it in a bit more detail. We can lay the number 5281 like so:

1000	100	10	1
5	2	8	1
So there are 5 [1000]s. Then there are 2 [100]s. There are 8 [10]s and there is 1 [1].

Can you see that we actually count in multiples of 10? So we start with 1s, then 10s, then 10 x 10 (100s), then 10 x 10 x 10 (1000s) and so on.

That's how humans count but what about computers? Computers count in binary, which is 'base-2'. What that means is that there are only two numbers: 0 and 1. So what happens if you want a 2? Well just like in base-10, when you run out of numbers, you start from the beginning and add 1 to the column on the left.

In base-10 : base-2 would be:

0 : 0

1 : 1

2 : 10

3 : 11

4 : 100

5 : 101

6 : 110

7 : 111

8 : 1000

9 : 1001

10 : 1010

See how that went? Let's make it a bit easier and lay it out in a table. Let's show you the number 10 in binary:

8	4	2	1
1	0	1	0
So, there are 1 8s, 0 4s, 2 1s, and 0 1s. Add all that up and you get 10!

But how did we get the numbers at the top of the table? Well, like with counting in 10s they are multiples of 2. So we start with 1, then go to 2, then 2 x 2 (4), then 2 x 2 x 2 (8). See how that works?

Now let's do hexadecimal. Hex is 'base-16'. This can get a bit weird. Why? Because you can't use 15 to represent 15 in base-16, because remember that 15 is actually a 1 and a 5. But after 9 we run out of numbers to use, so we have to use letters.

Let's see how it works, in base-10 : base-16 would be:

0 : 0

1 : 1

2 : 2

3 : 3

4 : 4

5 : 5

6 : 6

7 : 7

8 : 8

9 : 9

10 : A

11 : B

12 : C

13 : D

14 : E

15 : F

16 : 10

17 : 11

18 : 12

19 : 13

20 : 14

That should hopefully kind of make sense to you. After 9, you start from A and then go to F in hex. That's because you can't add a 1 to the left and start from 0 otherwise you would be counting in base-10!

Let's show you the number 31337 in hex:

4096	256	16	1
7	A	6	9
With these larger numbers it's easier to think of division. Let's do some basic maths:

How many times does 4096 go into 31337?

31337 / 4096 = 7.6506

So, 4096 goes into 31337 7 times. Write down 7 to begin with.

Then we do:

4096 x 7 = 28672

...and:

31337 - 28672 = 2665

So, the number left is 2665.

2665 / 256 = 10.4102

So, 256 goes into 2665 10 times. Remember, after 9 we start on letters, so that would be an A. So write down A to the right of 7.

Now we go:

256 * 10 = 2560

...and then:

2665 - 2560 = 105

So, we have 105 left.

105 / 16 = 6.5625

So, 16 goes into 105 6 times. Write down 6 next to the A.

Then we do:

16 * 6 = 96

...and:

105 - 96 = 9

Remember the last column is 1s so 1 goes into 9 9 times. So, write down 9.

You should have:

7A69

If you followed along so far, then congratulations! We won't be teaching you how to calculate the other number bases manually but there are a lot more number bases out there!

Base-64 is a common one, sometimes base-32 is used also. There are online tools which can handle the conversion for you but it's important to know how those tools work. One day they may not be available to you!

5.3 Character Encoding

If you followed along in the section about number bases, you may be confused about something. If all the computer ever understands is numbers, what's all this text doing all over the place? Well, that's accomplished by something called 'character encoding'. The most common type of character encoding is ASCII (American Standard Code for Information Interchange). It is really just a list of which numbers convert to which letters.

If you expect something to be a string, then the numbers will be interpreted as characters and you will see them on your screen as text.

Let's have a look at the ASCII table:

ASCII table

We can see here that numbers are just being translated to the characters we see on the screen.

5.4 Encryption

There are many different forms of encryption; too many to go through in this manual. Breaking them is a highly advanced topic that we won't be going into. Unless someone has chosen an incredibly bad encryption algorithm, you will most likely find it an easier task to attack the password rather than the algorithm itself.

There are two main ways we can attack a password. The first is called a 'dictionary' attack. It's quite simple: you create a 'wordlist' which contains a lot of different common words and hope that the password is one of those words. Then you have a program that goes through the list and tries them all very, very quickly. Some good dictionaries can be found online and contain the top 100000 most commonly used passwords, amongst other things. A dictionary attack is very fast but its success depends on the password being somewhere in the dictionary file you provide.

The second way to attack a password is called a 'brute force' attack. A brute force attack does not use a wordlist, instead it tries every combination of letters and numbers to try to crack the password. This is very slow, of course! If you think about a password of 1-12 characters in length, with mixed case letters and numbers then the number of possible combinations is: 3,279,156,381,453,603,096,810.

That's insane right?! Well, that depends on the kind of computer setup you are using to crack the passwords. What about if you used a weaker password? Say, only 8 characters? That's only 221,919,451,578,090 possible combinations.

What's the difference? Well, with cloud computing, the password with 8 characters would only take an hour or so to be cracked but the password with 12 characters would take 10 years!

What if you didn't use any upper case letters or numbers? The 8 character password would crack in 2 seconds and the 12 character password in 2 weeks.

5.5 Steganography

While encryption is the art of hiding the meaning of information, steganography is the art of hiding the information's existence. At the most basic level, you could open up another file (like an image) in a text editor and hide a message inside of it. You'd have to be careful to put it in exactly the right place to avoid corrupting the image, but it could work.

There are more advanced forms of steganography too. You could change some of the pixels in an image in just the right way to spell out a message, or change an audio file's frequency just enough. These more advanced forms of steganography and are very difficult to detect.
