---
layout: post
title: "Overthewire Labs Bandit 0-6"
date: 2025-08-28
---

Bandit

Bandit 0
It was about connecting via ssh
Connect to the lab via:
ssh -p 2220 bandit0@bandit.labs.overthewire.org

Then the password was also provided by the room

Bandit 0-1
Goal: Get the password in the home directory

ls
the readme file is there

nano readme

And the password was also there:
xx

Bandit 1

Connected again to the ssh and used the password.

Based on the instructions:
Generate a hard to guess temporary directory if needed via
mktemp -d 

I listed all files and directories via:
ls -la

the filename of the file with password in home directory is hyphen
searched for how to open this file

cat ./-

I got the password.

Bandit 2

The next password is in a file with a filename with spaces: 

Connected again to the ssh and used the password.

I listed all files and directories via:
ls -la

Searched for how to read files with spaces
Basically to wrap them in quotes
cat ./"file name"

Then I got the password

Bandit 3

The next password is a hidden file.

Connected again to the ssh and used the password.

Listed all files and directories and went to inhere directory. Listed the presen directory again with same flags to display hidden files and directories:
ls -la
cd inhere
ls -la

then used the same technique for reading file with spaces
cat ./"file name"

Bandit 4

The password is in human-readable file in inhere directory.

Connected again to the ssh and used the password.

checked the files
ls -la
cd ./inhere

Most of files contain unreadable words except for one.

cat filexx

Found the password.

Bandit 5

The password is in inhere directory and has some conditions:

human-readable
1033 bytes in size
not executable

Connected again to the ssh and used the password.

I listed all files and went to the inhere folder
ls -la
cd ./inhere

I read the du and find commands' manual
man du
man find

I used du at first, to list all the files and directories' size, I was able to find manually the 1033 bytes file. It's only one.
du -a -b

Then I used find as well.
find -size 1033c

Then used cat command to show the text.
cat ./filexx

Then, I found the password.

Bandit 6

The password is in somewhere in the server directory and has some conditions:

owned by user bandit7
owned by group bandit6
33 bytes in size

Connected again to the ssh and used the password.

I was trying to use the find cmd, but kept getting errors:
find / -user bandit7 -group bandit6 -size 33c

I thought all results are permission denied, it turned out that it was too noisy results.

I saw a walkthrough with this cmd, further narrowing the result with -type f(ile) cmd and sending the errors to null via 2>/dev/null:
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null

Then file with password was found.


