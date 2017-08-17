## 6.0 Introduction

Computer forensics is defined as the examination of digital media with the aim of identifying, preserving, recovering, analysing and presenting facts and opinions about digital information. We're only going to focus on a tiny portion of the forensics field: file forensics. Our aim is going to be to recover the data from files.

## 6.1 Files

What are files? Well, a file is just a bunch of data. Each file is interpreted differently depending on the program that is used to read the file. To a computer, the file is just a series of 0s and 1s. Viewing a file as the 0s and 1s would make the file much too long, however. So we encode them into hex and we can view that with a hex editor, such as [Okteta](https://utils.kde.org/projects/okteta/). We can learn a lot from looking at the raw hex of a file. One of the things we can find information on is the file header.

## 6.2 File Header

Since a file is just a series of 0s and 1s, you need to open the right file with the right program to get something meaningful. So, how does a computer know what program to use when you double click it?

On Windows, the file extension makes a big difference. Windows knows which programs are associated with which file extension. If you open `file.txt` it knows to open it in a text editor. But what about on Linux? Linux doesn't focus so much on the file extension, it focuses on the file header, casually known as the 'magic bytes' of a file. If you were to open the Okteta hex editor and open a zip file, you would see that the first few bytes of the file will always be one of three things:

```
50 4B 03 04 If the zip file is a normal zip file with something in it.
50 4B 05 06 If the zip file is empty.
50 4B 07 08 If the zip file has been split into multiple parts.
```

This is the file header and it just tells the computer which format the rest of the data in the file will be in. There are too many file headers to list here but if you follow this link, you will see a handy list.

[List of file signatures on Wikipedia](https://en.wikipedia.org/wiki/List_of_file_signatures)

We can make use of Linux's ability to know which files are which based on the file header with the 'file' command. Here's the usage:

`$ file filename`

This will tell you what the file header says the file is.

## 6.3 Strings

The file header is not the only useful bit of information you can find in a file with a hex editor. If you open a binary file in a hex editor like 'Bless', you will often be able to see the contents of the strings that were in the code. That's because Bless automatically tries to convert the hex data into ASCII text side by side. Most of the time, the hex was never intended to be ASCII so it will just produce junk but, if you come across any text in the code, it will be handily converted for you.

There's actually a faster way to go looking for strings in text files. It's called... 'Strings'. It's a Terminal program. The usage is simple:

`$ strings file`

That will output all the strings it finds in a text file. It will also produce lots of junk because it doesn't know for sure what is supposed to be text and what is just data. By default it will ignore very short strings, so watch out for that! There is a way to change the default: look at `man strings` and see if you can find the right option.

