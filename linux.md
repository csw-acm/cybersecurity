## 1.0 Introduction
Linux is an operating system (like Windows). It is free and open source, which means that anyone can look through its code. It gets its name from Linus Torvalds, the creator of the Linux kernel. The kernel is the core of the operating system. There are many different Linux operating systems, called distributions. Some of the most widely used ones are Red Hat, Ubuntu and Debian. All Linux distributions have one thing in common: they are all built around the Linux kernel.

Getting to know Linux is very important, as most security tools that you will get to know and use are built for the Linux operating system. Some may have Windows versions but, for the most part in the security community, Linux is the dominant operating system. We will mainly be using the Linux command line, which is called the Terminal.

Before we go into the usage of the Terminal, there are some important key points to learn that many people trip up on at the beginning. There are also some tips that can make life much easier for you.

* Linux is case sensitive. That means the folder `Hello` and the folder `HELLO` are entirely different folders.
* Linux does not like spaces in file or folder names. It's common to use an underscore `_` where you would usually put a space.
* The Linux Terminal has tab completion. This means that you can start typing, press the tab key part of the way through and it will guess what you were typing. So if there was a file in the directory called `passwords` and you typed pass and pressed `tab`, it would fill in passwords for you. On the other hand, if there were too many matches it would not complete. E.g if there were two files, `passports` and `passwords`, and you typed pass, it would not know which you meant so it would not autocomplete until you typed the next letter and pressed `tab` again.
* You can use the up arrow or down arrow keys in the Terminal. The 'up arrow' will take you to the previously typed command; you can keep going further and further back up to a certain point. Once you've gone back, you can use `down arrow` to scroll through to the more recent commands.

## 1.1 Terminal
Linux is not focused on the GUI (Graphical User Interface). While many Linux distributions do come with a GUI, it is usually more of an afterthought. Anything you can do on Linux can be done from the Terminal. More importantly, once you become comfortable using the Linux Terminal, you will find that many things are actually easier or faster to do from the Terminal. You may one day find yourself opening the Terminal to copy files from one location to another, instead of opening the file browser.

The first step in using the Terminal is, of course, to open the Terminal application. There should be an icon for the Terminal at the top of the screen. Or you can find it under "Accessories" in the Main Menu. Once you have it open, you will be greeted by some text on a black screen. This text is called the prompt.

The prompt will be in this format:

`username@hostname location $`

So in your case it will most likely look like this:

`agent@cpa ~ $`
The ~ is just a short way of indicating that you are in the home folder. The hostname is just the name of the computer. It may seem obvious now which computer you are using but it isn't always. If you are connecting remotely and you have many sessions open to many different computers, the reminder can be helpful. The $ sign indicates the end of the prompt. Anything after the $ is a command that you can type. The prompt is called the prompt because it means the Terminal is ready for input. If you run a program from the Terminal and you don't see the prompt, this means that the program is still working and the Terminal isn't ready for another command yet.

Now we'll end this section on an important note, which will be repeated frequently throughout the field manual:

**Linux is case sensitive! Unlike in Windows, the files 'password', 'PASSWORD', 'Password' and 'PaSSwOrD' are all different files.**

## 1.2 List (ls)
Now that you have the Terminal open and are at the prompt, you may be wondering how you can start to navigate around. The first thing to do would be to look in the current folder to see what exists. You can LIST all the files and folders in the current directory by typing ls and pressing enter. It’s easy to remember if you just think ls stands for list.

Many commands can take arguments. Each command has a full list of arguments that it accepts in its `man page` (see Chapter 1.4 for more details) but we will cover some of the more common usage examples here.

`$ ls -l`

Shows the list of files and folders in long form. Here you can see who owns the files and folders, what the permissions are (who can access them and do what i.e read, write, execute). You can also see the date modified and file size (in bytes).

`$ ls -a`

Shows hidden files. In Linux, putting a `.` at the beginning of a file or folder name turns it into a hidden file/folder. If you type `ls -a`, it will show you all the files/folders including the hidden ones.

`$ ls -t`

Lists the files and folders in order of date modified - most recent first.

`$ ls -alt`

In Linux, arguments can be combined together. For example the above, which is a combination of all the options we covered.

## 1.3 Change Directory (cd)

Now that you can list all the files and folders in your current location, how can you move about the filesystem? Well, this is where the cd command comes in. It stands for 'Change Directory'. A directory is the Linux name for a folder and we'll be using it from now on instead of `folder`.

To enter a directory, just type:

`$ cd directoryname`
You can also go back a directory by typing:

`$ cd ..`

The `..` directory is available in every directory and it just represents the directory above. So if you were in `/home/agent/Desktop` then the `..` directory references `/home/agent`. It's a hidden directory (because it starts with a `.`) but if you use ls -a to view hidden files you will be able to see it in the list. You might also notice a `.` directory. This actually represents the current directory.

You don't necessarily have to go just one directory down. If you know the whole path you can do lots at once. In Linux, directories are separated by a `/` as opposed to a `\` in Windows.

So, for example, you could do:

`cd /home/agent/Desktop`

## 1.4 Move (mv)
OK, so now you want to move a file from one location to another location. You can use the mv command. It stands for 'move', so it's easy to remember.

Imagine you have a file here, called 'file.txt', and you want to move it to `/home/agent/Desktop/`

The command would be:

`$ mv file.txt /home/agent/Desktop/file.txt`

It's really important that you put the file name in the location that you want the file to be moved to. That's because you can also use `mv` to rename a file. For example:

`$ mv file.txt new_file_name.txt`

That would keep the file in the same place but change the name of it.

## 1.5 Copy (cp)

OK, so what if you don't want to move something and you just want to copy it instead? The cp command will help you here!
The cp command will make a copy of a file in the location you specify but it will keep the original file intact.
The usage is like this:

`$ cp file.txt /home/agent/Desktop/file.txt`

This will copy the file into the user's Desktop folder. You could also change the filename with:

`$ cp file.txt /home/agent/Desktop/new_file_name.txt`

## 1.6 Manpages

An important habit to get into when working with the Terminal is reading the manual for any programs that you are running. Every command that you can run from the Terminal is actually a program and they all have manuals. Usually, there are a lot more options than you think and most of them have their uses.

To read the manual for a program just type `man programname` and press `enter`.

This will bring up the manual page for that program. You can use the arrow keys to scroll up or down through the manual. To exit the manual page, just press `q` on the keyboard.

These manuals are called man pages. Since every command you can run from the Terminal is actually a program, the command man is actually a program also. It even has a man page. So you can even type `man man`.

Now let's get a little practice in reading man files. We covered the basic usage of the ls command in a previous chapter but let's take a look at its man file. So type:

`$ man ls`

You will see:
```
Name
  ls - list directory contents
Synopsis
  ls [OPTION]... [FILE]...
```

Interestingly, we can see that the ls command can take arguments. What this means is that you can either type ls on its own, or you can combine it with various other options. Looking below under the 'Description' heading, you will see a list of the options

If you keep scrolling down with the arrow keys, you will find one of the options is `-l`. The description of that option is: 'use a long listing format'. Let's try it. Press `q` to exit the man page and type:

`$ ls`

and press 'enter'.

Now type:

`$ ls -l`

and press 'enter'.

You will see that using the `-l` argument changed the output of the `ls` command quite a bit. In fact, using `-l` will allow you to see who owns the file or directory, what the permissions are and so on.

Now if you look in the man page once again you will find another option: `-t`. `-t` sorts the files and directories by date modified from newest to oldest. Let’s combine `-l` with `-t`.

If we wanted to, we could do:

`$ ls -l -t`
But that's the long way of writing it out. It's much more common to just type:

`$ ls -lt`

Now if you look back at the Synopsis, you will see it mentions `[FILE]`. What does this mean?

It can be a little confusing, but in Linux everything is considered a file. Files are files, directories are files... everything is a file. So when it says `[FILE]` it really means a directory.

So if you were to type:

`$ ls Directory`

It would list all the files in the 'Directory' directory.

Because everything is considered a file, if you were to try it on a file, you wouldn't get an error.

`$ ls File`

This would just give you the file name of `File`.

## 1.7 Display Contents / Concatenate (cat)

The `cat` command is a bit of a weird one. It's short for Concatenate so it can be used to join two files together. By far its most common usage, however, is to just display text files on the screen without having to open a text editor.

To show the contents of a text file you can just do:

`$ cat filename`

...and the contents of the text file will be printed to the Terminal.

If you want to use it to join two files together you can do:

`$ cat filename1 filename2`

It's important to note that this will join the two text files together and print the result to the Terminal; it won't overwrite the files or save the changes to the files.

If you want to actually use it to create a new file by combining two files, you need to use *redirection*. Redirection is not unique to the `cat` command; it's available everywhere in the Terminal. Using redirection, you can take the result of any command that is printed to the Terminal and redirect the output to a file. The *redirection* character is `>` or `>>`. `>` will output the contents to a file and, if the file already exists, will overwrite that file. `>>` will output the contents to a file and, if the file already exists, will just add it to the end of the file.

So you could do:

`$ cat filename1 filename2 > new_file`

...or:

`$ cat filename1 filename2 >> appended_file`

You don't necessarily have to cat only two files you can do it with as many as you like:

`$ cat filename1 filename2 filename3`

Or you can use the wildcard operator *. The wildcard operator allows you to match any files. For example:

`$ cat *`

This would cat all the files in the current directory together.

You can also combine it with text, so:

`$ cat *.txt`
This would cat together all the files that end in `.txt`.

This also is not specific only to `cat`; you can use the wildcard operator in other commands also.

# 1.8 Grep

Unlike the other commands that we've covered so far, grep doesn't stand for something simple. It actually stands for *Globally Search a Regular Expression and Print*. This sounds scary but it isn't. It basically lets you search for words in files.

Typical usage would be:

`$ grep searchquery filename`

This would look for the word `searchquery` in the file `filename` and if it finds the word there, it will print out the line it found the word on.

It's really useful if you want to look in large files for something. It can also be useful if you're looking in a lot of files for one particular thing.

Using the wildcard operator `*`, which we learned about in the section on cat, we can actually do:

`$ grep password *.txt`

This would look in all the files in the current directory that end in `.txt` and print out any lines with the word `password` in them. Imagine doing that by hand from the GUI if you had more than 10 files that end in `.txt`!

This is a good place to learn about the pipe `|` operator. That isn't a lowercase `L`, that's the straight line character, which is called the pipe. The pipe lets you redirect output from one command into another command. This is similar to the `>` character, which redirects to a file, but instead the `|` character allows you to redirect to the input of another command.

So for example, if instead of the contents of the files, you wanted to search for a filename you could do:

`$ ls | grep filename`

That would first run the `ls` command but it won't print the output to the screen. Instead, it will send the output to `grep`.

Now you know that the usage for `grep` is `grep searchterm thingtosearch.` In this case, we already have `grep searchterm`, so the output of the `ls` command is redirected to be the thing to search.

You can probably guess that this will search for the searchterm (in this case `filename`) in the output of the ls command and it will print the filename to the screen if it finds it. If it doesn't find it, it will print nothing to the screen.
1.9 Running Programs
When you type cd or ls or any of the other commands we have run so far, it's important to understand what happens. Those commands are all programs and they're stored in a variety of places on the filesystem. One thing they all have in common is that they are all stored somewhere in the `PATH`.

The `PATH` is just a variable (or setting if you prefer) that tells the computer where to look for programs. You can see your `PATH` if you type echo `$PATH`. `echo` is a program that just outputs something. You could type `echo echo` and it would output `echo` to the Terminal. But because `$PATH` is a variable, `echo` will output the contents to the screen. In this case, it will output a whole bunch of directory paths separated by a `:`. The way it works is, when you type a command, it will look for the program in those directories starting with the first one in the list. If it doesn't find it there, it will move on to the next directory and so on. If it doesn't find the program in any of them, it will give you a `command not found` error.

So, what do you do if you want to run a program directly, instead of having to install it by putting it into one of those directories first? The most common way to do it is to use:

`$ ./programname`

This says, look in the directory I'm currently in and run the program with this name.

Alternatively you can do:

`$ ./directory/programname`

This executes a program in a different directory.

## 1.10 Permissions (chmod)

You've just downloaded a program, you've tried to run it and it tells you `Permission denied`. What's going on? Well, it comes down to permissions. By default, the program you downloaded does not have `execute` permissions. We need to assign those permissions first.

You will be using a program called chmod to change the permissions on the file here. The easiest way would be to use:

`$ chmod +x program`

Here the `+x` basically means, give execute permissions where the `x` stands for execute.

You could also do:

`$ chmod -x program`

This would remove execute permissions.

Or:

`$ chmod +w file`

This adds write permissions, and so on. Using `chmod` this way is the most basic way to manage permissions. There are more complex methods but we won't be covering them here.

## 1.11 Stopping Program Execution

You have a program running and you realised you ran it by mistake, or it's not doing what you wanted. What do you do? Do you have to wait for the program to stop running? Do you close your Terminal window and open a new one?

The answer is no, that's entirely unnecessary. Just press `CTRL+C` to cancel the running process. This will interrupt the program and stop the execution.

## 1.12 Redirection and Wildcards

The first type of redirection is *file redirection*. When you run a command that outputs some results to the Terminal, you can redirect that output to a file.

There are two file redirection operators. The first is `>`. This operator will output the results of the command before it to a text file that you name after it. If the text file already exists, it will overwrite it, so be careful!

Example usage:

`$ cat filename1 filename2 > new_file`

You can also use file redirection to append to an existing file by using the `>>` operator. This will either create a new file, if the file doesn't already exist, or, if the file does exist, it will add the output to the end of the file.
Example usage:

`$ cat filename1 filename2 >> existing_file`

There is an interesting form of file redirection that is worth mentioning. In Linux, there are two types of output. Standard Output (`stdout`) and Standard Error (`stderr`). As they sound, one is for normal output and the other is for outputting errors. When you redirect, you are redirecting only `stdout` by default. You can redirect `stderr` instead by doing `2>` or `2>>`. If you want to redirect both stdout and stderr then you need to do `&>` or `&>>`.

The second type of redirection is *input redirection*. You can redirect the output of a command into the input of another command. For example, you could type:

`$ ls | grep password.txt`

This would do an `ls` to list all the files in the directory but it wouldn't output them to the Terminal. Instead, it will take that output and send it to the next command, which is grep. Grep would search the output for password.txt and, if it found it, it would print `password.txt` to the Terminal. If it didn't find anything, it wouldn't print anything to the Terminal.

Finally, let's look at the wildcard operator. The wildcard operator can stand for anything. So if you were to do:

`$ cat *`
...it would print the contents of all the files in the current directory, one after the other.
If you only wanted files that start with the word `pass` then you could type:

`cat pass*`

Then only files that start with `pass` would be printed to the screen.

You could also do the opposite and do:

`$ cat *.txt`

This would print all the files that end in `.txt`.

## 1.13 Find (find)

The `find` command is one of the most useful and most frustrating commands on Linux. It will definitely trip you up if you are not careful. It's mentioned here after the section on redirection for a reason. You will need to read Section 1.9 carefully before this section can be understood.

The find command can, unsurprisingly, be used to search for files.

You can type:

`$ find [location to search] [how to search] [what to search]`

For example you can type:

`$ find / -name "passwords"`

...to look for every folder on the filesystem for files called `passwords`.

If you type that, you will be sure to get lots of errors about permissions. That's because as a normal user, you don't have permission to go to many of those places. The best thing to do is to ignore those errors. To do that, you need to redirect stderr to a file.

You can just redirect it to any file and then delete the file. Or you can redirect it to `/dev/null`. `/dev/null` basically means nowhere.

So a cleaner way of searching would be:

`$ find / -name "passwords" 2> /dev/null`

This would only show you results you have permission to access and hide any permission denied errors from you.

The find command is massive, and it takes many other arguments than just `-name`. We won't go into all of them here, but now that you know how to read man pages, `man find` should be extremely helpful in listing them all.

## 1.14 Processes (ps)

On any operating system, programs run as *processes*. For example, if you bring up the Task Manager in Windows you can click on the Processes tab and see a list of all the running programs on your computer. On Linux, we can do the same thing. For this, we use the `ps` command.

The output of running the ps command looks something like this:

```
agent@cpa:~ $ ps

PID TTY     TIME CMD

900 pts/0   00:00:00 bash

928 pts/0   00:00:00 ps
```

You will see in this example that there are only two processes running for this user. Bash is the 'Bourne Again Shell', which is just the terminal. The other process running is ps. That's because ps is a program and, by running it, it can find itself in the process list. By reading man ps you can find out that by default ps will only show you processes for the user you are currently running as. It does, however, take have some options that which can change this behaviour.

`-u`

Will allow you to see more information about all the running processes.

`-ax`

Will allow you to see all processes running on the system, not only those for your user.

Combining the two, we can use ps -aux to see a lot more information. Interestingly, we can also see the parameters that were passed to any running program when it was started. This is why it's unsafe to pass a password into a program from the Terminal. For example:

`$ ./secureprogram -password "mysupersecretpassword"`

This is a bad idea because, while the program `secureprogram` is running, any user will be able to use `ps -aux` to see that `mysupersecretpassword` was sent to the program as a password.

## 1.15 History

It's interesting to note that everything you type in the Terminal window is logged into a file. This file is called the history file. Typing history will show you everything you have been typing in the Terminal. It's important to know it exists. You can also clear it by typing `history -c`.

The Terminal history is an important source of information if a system you are defending has been attacked and the attacker failed to clean up after himself. For an attacker, it could be an even more important source of information. If you ever typed a password in the Terminal, it will be shown there. So it's important to clear the history file after such cases.

## 1.16 Secure Shell (SSH)

SSH stands for 'Secure Shell'. It's a method of logging into a remote system. SSH is protected by strong encryption so any commands you send are protected from eavesdropping. It's important to become familiar with SSH, as its use is very common in the industry.

The most common usage of SSH is:

`$ ssh username@domain.com`

Then you will be asked to enter a password. You will need to log in with a username that has SSH access enabled. Once you are logged in, a prompt will be provided by the remote server. Anything you then type into the Terminal will be as if you have typed it on the server you are logged into.

Once you are finished and want to exit out of the SSH session, you can simply type exit in the terminal and you will be kicked back to the prompt on your local computer.
