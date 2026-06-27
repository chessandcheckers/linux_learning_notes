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

This is where we start to encounter multiple files. 
After changing the directory to `inhere` we are shown multiple file like -file00, -file01, etc.
The aim of this level is to check the filetype of each folder, but without opening each individual folder. 

To achieve this, we use the `file./*` command to identify the type of data stored in each folder.
The output is all the folders and the type of data stored in them. 

---
## Level 4 -> 5

Inside `inhere` we are faced with various subdirectories containing many files. The goal is to search for the only human-readable text among them.
Previously, we used `file./*`. This however wont work here as we are searching for the file within directories, not just filders. 

We shall use `find` command for this. 
The format of this command is: `find [WHERE] [WHAT TO LOOK FOR]`

Here, the [WHERE] part is the current directory, therefore we use `find .`
For home directory we use `find ~`. 
For the entire system we use `find /`

An example of this would be: `find . -type f`, where `-type f` stands for file types.
`-type d` is for directories, `-type l` is for links. 

In case we are searching for specific names, we will use:
`find . -name "[name.filetype]"`

If we are searching for files of same type then:
`find . -name "*.txt"`

---
## Level 5 -> 6

Our task here is to find the directory inside `inhere` which satisfies the following conditions:
- human readable text
- exactly 1033 bytes in size
- not executable

Again, we use `find` to execute this.
For the size, we define it as `-size 1033c`. The `c` we see beside the `size` parameter is used for bytes.

---
## Level 6 -> 7


### 📄 Task

The task here is to find a file somewhere on the server that satisfies the following conditions:

- owned by user `bandit7`
- belongs to group `bandit6`
- exactly 33 bytes in size

Unlike previous levels, the target file is not located inside the current directory. Therefore, we need to search the entire filesystem for the owner, group, size of the file. 
We do so using the `find` command.

