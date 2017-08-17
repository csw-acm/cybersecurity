3.0 Introduction

There are several common flaws that you might often find in websites. The most important thing to remember when looking to attack a website is to start from the basics. Have you looked at the page source yet? Do you notice anything in the HTML comments? The page source is the one place you should always look first.

3.1 Client-Side & Server-Side

Before we can talk in depth about web attacks, we must first know how websites are structured.

First, we have client-side. This is the part that you see when you browse to a website. You actually have control over this part of the website; you can save the page to your desktop, change the HTML or the JavaScript, open it in your browser and you will be able to see the changes.

Then we have server-side. You have no control over this section of the website. It includes things like the database or, if the website uses PHP, then the PHP is run on the server and generates the HTML that you see when you browse to the page. That's why when you browse to a site that uses PHP and you look in the source code, you only see HTML without any PHP.

When you are creating a website, you should always make sure that any password checks are done server-side. That way, they aren't visible to the client. That isn't always done, however. By looking in the page source, particularly through the JavaScript, you might see some password checks in there.

If you see something like this in the JavaScript:

if (password == "letmein")

...then I wonder what the password could possibly be? Silly, right? But it happens.

Remember, anything client-side is not secure. Did the developer disable a button by changing the HTML to have 'disabled' in there? Just edit the HTML to remove 'disabled' from the HTML with the developer tools. Suddenly, the button is clickable again. Client-side is under the user's control.

3.2 Command Injection

This is a pretty cool flaw when you find it. Say, for example, you have a file sharing site that shows you a list of folders. At the bottom there is a text input which allows you to enter a folder name to view the contents of that folder.

Folder1

Folder2

Folder3



Show Contents [        ] [List]

What would happen on the server if you typed 'Folder1' and hit search? Well, the server could actually handle it in several ways, but one potential way is for it to send a terminal command:

ls Folder1

...and use the output of the command to show the new listing nicely on the website.

Can we take advantage of this? Absolutely. In the Linux Terminal, there is a way to enter more than one command on a line. That is to use the semicolon character ;. The semicolon just means: the command that came before it was one line, the command that comes after is another line.

Try it - in the Terminal type:

echo "Hello1"; echo "Hello2"

and hit 'enter'.

See how it prints, one after the other:

Hello1

Hello2

Two commands, one line. So going back to our first example, when you type:

Folder1

...into the form, it performs:

ls Folder1

What would happen if instead in the form you typed:

Folder1; echo "Hello"

Well, then the command the server would run would look like:

ls Folder1; echo "Hello"

So then Folder1 would be updated on the site as normal, but somewhere on the site you would get the word "Hello" output, since it was echo'd out.

Now we've managed to run our own command on the server.

3.3 SQL Injection

SQL injection is actually very similar to command injection, but it requires us to know a little bit about SQL.

SQL stands for Structured Query Language; it's a language that allows us to interact with databases. The normal structure of an SQL query is this:

SELECT username, email FROM users WHERE username='Bob'

This will find or SELECT the username and email address FROM the users table of anyone (WHERE) the username matches 'Bob'. Basically, it will find any user with the username Bob and show the username and the email address.

So, now that we know a bit about how SQL queries are structured, let's imagine a site with a forgotten password form. You enter your email address and it searches the users table for the account that has that email address. Let's think about what that query would look like:

SELECT email FROM users WHERE email='test@example.com'

Now let's think about what we can enter in the email address field to change the query. The first thing to do would be to check if it's vulnerable.

Let's try entering:

' OR 1=1

What does that make the query look like now?

SELECT email FROM users WHERE email='' OR 1=1

This selects email addresses from the users table where the email is blank OR 1=1. What is 1=1? Well, it's TRUE. Let's think a bit more about how SQL matches against things.

So in the table we have:

test@example.com

test2@example.com

test3@example.com

If the SQL query was looking for: test2@example.com it would first try to match against test@example.com. It would see that it doesn't match so it would return FALSE. Then it would move on to test2@example.com and try to match. It would see it matches and return TRUE. Then it would move on to the next, which doesn't match and would return FALSE.

By doing OR 1=1, we have told it to match everything. So, you would see a list of all the email addresses that are registered output to the page.

Let's consider a slightly more advanced command. The query that is running isn't much use, as it will only give us email addresses. What if we also wanted passwords? Well, you can't change the SELECT part of the SQL query since it's before the user input but, like with command injection, we can use a semicolon ; to run a second SQL query.

Let's look at what we need to achieve:

SELECT email FROM users WHERE email=''; SELECT email, username, password FROM users WHERE email='admin@example.com'

In order to achieve this, we need to enter into the form:

'; SELECT email, username, password FROM users WHERE email='admin@example.com'

Now you should have the email address, username and password for the admin@example.com account.

3.4 Cross-Site Request Forgery (CSRF)

Cross-Site Request Forgery sounds intimidating, but the concept is actually very simple. Imagine that you know there is a URL in the Admin section of a site that will add a user account if you visit that link. For example:

https://example.com/admin/adduser.php?username=hacked&password=password1234

But of course, you go to that link and it tells you 'Access Denied', because that page is only available to the Admin. You happen to know the Admin's email address, so you fake an email from his bank that tells him his credit card details were stolen and to "click this link for more information". However, the link doesn't go to his bank, it goes instead to that URL that adds an account.

If the Admin is logged into his Admin account and he goes to that link, then the account will be created. It's the same as if the Admin clicked the 'Add Account' button in the Admin page. This is Cross-Site Request Forgery.

3.5 Cross-Site Scripting (XSS)

Cross-Site Scripting is a little different. It's actually an attack, not on the site itself, but on the people who view the site. Imagine a forum that you've signed up to. It allows you to make posts. What would happen if you added some JavaScript to the post?

For example in your post you could try:

<script>alert("Hello, noobs!");</script>

If you posted that, what would happen to the people who viewed your post? Well, their browser would see the <script> </script> tags and interpret the bit between them as JavaScript. So to everyone who viewed your post, a pop up window would appear calling them 'noobs'.

Kind of annoying but no big deal, right? Wrong. You can do a lot with JavaScript. The most common type of attack is to use JavaScript to steal a user's log in cookie (called a session cookie) and send it to another site.

The hacker can then collect all the session cookies and add one to his browser, refresh his page and then he will be logged in as that user without ever having to enter a password or even using the login form.

3.6 Filters

The four types of attacks we've covered so far have one thing in common: they rely on user input to work. Many places have closed down these holes by using filters. A filter will basically try to look for anything that doesn't belong in the user input and filter it out.

As an example, if it were a filter against command injection, they might filter out the semicolon character ;. Is that enough? There are other characters that can achieve the same thing. For example, you could use a && instead of a ;. There are plenty of other ways around filters for you to look up.

3.7 Web Requests

There are two main type of web requests. GET requests and POST requests. A GET request is all in the URL so it looks like this:

https://example.com/index.php?username=luffy&loggedin=true

A POST request is sent in the HTTP headers, so you while it's easy to modify the URL in a GET request, sending a POST request is actually much harder.

We can use a Terminal program called curl to send POST requests. It's actually a tool that comes built into many Linux distributions by default.

To send a POST request we can do:

$ curl https://example.com/index.php --data "username=luffy&loggedin=true"

Now that we know how to send web requests, let's talk about the User Agent. Whenever you make a request on a website, the browser sends a header that contains various pieces of information about the connection. It includes a field called the 'User Agent'. The User Agent just tells the website which browser you are using to connect. This is helpful because, if you are browsing from a phone with a smaller screen, the website can detect it and send you to a page that is designed for smaller screens.

There may come a time when you need to fake your User Agent. Perhaps the easiest way is to use a browser extension (we have one installed on the computer provided).

Remember, if a page sends you to a different site depending on your User Agent, it may be that one version of a site is vulnerable while the normal site is not.

3.8 Cookies

Previously we mentioned session cookies, which are a type of cookie. A cookie is just a bit of data that sites can save to your browser. When you go to the site that matches the cookie, the browser sends the cookie to the site and the site can read the data in it. Cookies all have an expiry time that are set, so eventually they will expire and be deleted from your browser. Cookies consist of a 'name' and a 'value'.

Session cookies are cookies that keep track of your 'session'. That is, when you log in, a session cookie is created. That's why, when you close a browser window and go back to the site, you'll still be logged in. Each site can handle session cookies differently.

There are sites that are vulnerable to session guessing. Session guessing can be done if the value of a session cookie is not properly randomised. For example, if I log in and my session cookie has a value of 72, then you log in and your session cookie has a value of 73. If you edit your session cookie to have a value of 72 instead of 73 then refreshed the page, you would be logged in as me! A secure session cookie is always a random value that isn't easily guessed.

3.9 Robots

Unicode robot

Not those kind of robots. The robots.txt file on a website is a list of websites that a search engine should not be allowed to index (add to their search database). If you can find this file, it's usually a nice juicy list of all the secret web pages that the owners of the website don't want you to find!
