## Level 0

This is the initiatory level in bandit.
We start off by opening our command prompt and connect to the 
server using SSH: ssh bandit0@bandit.labs.overthewire.org -p 2220

We use a different username for each level (bandit0, bandit1, and so on) 

Here, the problem was to open the given readme file. 
Used the `cat` command to open the readme file.
`cat` is used to display contents in the terminal.

---
## Level 0 -> 1

I start off each level using the `pwd` command, which shows us the 
current directory. 
After that, used `ls` to check for files in the current directory. 
`ls` is used to list files. 

Here, I am encountered with a '-' file.
This is not a normal filename, '-' is treated as a special symbol in linux.
Again, used the `cat` command to open this but with a slight twist.

---
## Level 1 -> 2

Upon using `ls` we encounter another problem - a different type of filename called '--spaces in this filename'
We shall use cat to solve this too, but we must find a way to eliminate the spaces in the filename
(no pun intended)
We may use either single quotes or the backslash.

---
## Level 2 -> 3

This is where things start getting multi-layered.
We must first change the directory to `inhere` then figure out how to access the files.
Using `ls` is not enough as `ls` only shows the files which are visible to all. 
In this level, we are introduced to hidden files, which we can open using `ls -a` command.
After this, we again use the `cat` command to open the file.

---
## Level 3 -> 4

