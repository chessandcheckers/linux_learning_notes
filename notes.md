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

The task here is to find a file somewhere on the server that satisfies the following conditions:

- owned by user `bandit7`
- belongs to group `bandit6`
- exactly 33 bytes in size

Unlike previous levels, the target file is not located inside the current directory.
Therefore, we need to search the entire filesystem for the owner, group, size of the file. 
We do so using the `find` command.

---
## Level 7 -> 8

This level requires us to search for a specific word which has the password. 
We have to search for this word among a file containing ginormous amount of data, which is impossible to search manually.

For situations like this, we use the `grep` command. 
`grep` is used to search for a word inside a file. It prints entire lines containing the needful data.

The query should be sequenced as: `grep (word) (filename).(filetype)`

---
## Level 8 -> 9

Here we need to combine commands to access the necessary password.
Withing data.txt there exists a unique line of text which is our password. 

We cannot use `grep` because the data is not known to us and it is unique. `grep` searches only for known text. 

We use `sort` to sort the data within our file. 
Since we are searching for only unique data, we shall use a combination of `uniq -u`.
`uniq` is used to remove consecutive duplicates and leaves a single copy of the data. 
`uniq -d` shows only duplicate values.
`uniq -u` shows only lines that appear exactly once.

Structuring the whole thing is important. We use the command `sort data.txt | uniq -u`.
The pipeline `|` here acts as a bridge between the two commands. `sort data.txt` is one command and `uniq -u` is the other. 
`|` is used here because we want the output of the left side command to become the input of the right side. 

---
## Level 9 -> 10

The password we require is preceded by many `=`.
It is one of the very few human readable texts.
Every time we need to extract human readable text from a binary file, we should think of `strings` command.
We cannot use `cat` here because the file is mostly binary data which is hard to read.
We also cannot use `grep` directly because it cannot read easily readable texts.

The way to this level is to use `strings [filename] | grep "="`
Here, `grep` is used to find the lines with "=". 

---
## Level 10 -> 11

This level introduces us to encryption, specifically `base64` encoded data.
`base64` is an encoding scheme/format not encryption. This is important.
Encoding converts data into a publicly standardized format and doesn't require a secret key which makes it easy for anyone to decode it easily. For example base64, ASCII, url encoding.

Encryption prioritizes data security. It converts data into unreadable ciphertext which protects it from unauthorized users. A secret cryptic key and a decrytion algorithm is used to revert the data back to its original form. 

As a way to start, you can start by entering `base64 --help` in the prompt.
The output will contain something like:
`Usage: base64 [OPTION]... [FILE]`
This is basically the format to use `base64`
You will also see some options:
`OPTIONS:`
`  -d or --decode : used to decode data [aliases: -D]`
`  -i, --ignore-garbage : when decoding, ignore non-alphabetic characters`
`  -w, --wrap <COLS> : wrap encoded lines after COLS character (default 76, 0 to disable wrapping)`
`  -h, --help : Print help`
`  -V, --version : Print version`

Since here we want the decoded text from the file `data.txt`, the command we shall use is:
`base64 -d data.txt`

---
## Level 11 -> 12

This level introduces another encoding technique called `ROT13`.
`ROT13` is used when the characters have been encoded by rotating them or shifting them by 13 positions.
Applying `ROT13` twice will lead us back to the original text as 13+13=26 and there are 26 letters in the alphabet.
However, Linux doesn't have a dedicated `ROT13` command. We use `tr` instead, which stands for `translate`. It replaces one set of characters with another. 
Its general syntax is: `tr 'SET1' 'SET2'`
As with `base64`, we can ask the terminal for help with `ROT13` or `tr` too using the command `man tr` or `tr --help` 

As we know from the logic, we are rotating by 13 positions. So, A -> N, B -> O, C -> P, and so on till Z -> M.
So, our command will be comething like: 
`tr 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz' 'NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm' < data.txt`
or we can also write it as:
`cat data.txt | tr 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz' 'NOPQRSTUVWXYZABCDEFGHIJKLMnopqrstuvwxyzabcdefghijklm'`

---
## Level 12 -> 13

This level teaches us to investigate an unknown file.
The file we need to read is a hexdump file which has been repeatedly compressed. 
Hexdump is a hexadecimal representation of the file. It is stored as bytes. 
We use `xxd` command to deal with hexdumps. For the manual: `xxd --help` or `man xxd`.
This gives us multiple options:
Options:
    -a          toggle autoskip: A single '*' replaces nul-lines. Default off.
    -b          binary digit dump (incompatible with -ps). Default hex.
    -C          capitalize variable names in C include file style (-i).
    -c cols     format <cols> octets per line. Default 16 (-i: 12, -ps: 30).
    -E          show characters in EBCDIC. Default ASCII.
    -e          little-endian dump (incompatible with -ps,-i,-r).
    -g bytes    number of octets per group in normal output. Default 2 (-e: 4).
    -h          print this summary.
    -i          output in C include file style.
    -l len      stop after <len> octets.
    -n name     set the variable name used in C include output (-i).
    -o off      add <off> to the displayed file position.
    -ps         output in postscript plain hexdump style.
    -r          reverse operation: convert (or patch) hexdump into binary.
    -r -s off   revert with <off> added to file positions found in hexdump.
    -d          show offset in decimal instead of hex.
    -s [+][-]seek  start at <seek> bytes abs. (or +: rel.) infile offset.
    -u          use upper case hex letters.
    -R when     colorize the output; <when> can be 'always', 'auto' or 'never'. Default: 'auto'.
    -v          show version: "xxd 2025-11-26 by Juergen Weigert et al.".

We want to reverse the hexdump hence we will use the `-r` option. 

First, we start off by creating an empty directory using `mktemp -d` and then copy the file `data.txt` into it using `cp ~/data.txt .`
After that, we create another file within which we will copy the contents of `data.txt` after converting them to binary.
We do so by `xxd -r data.txt data`. Here `data` is the output file.
Once that is clear, we need to convert the contents of `data` into its original format.
To do so, we need to know the filetype of `data`. We use `file data` to get the output.

We find that `data` is gzip compressed. 
Further steps would be to understand gzip, so we do `gzip --help`
We go down this rabbit hole of `gzip` and `bzip2` till we come to `POSIX tar archive (GNU)` or something like that.

A common beginners mistake is to do `posix --help` or the like. Even i did that mistake.
But here, we must do `tar --help` because it is a `tar` archive. `tar`  saves many files together into a single tape or disk archive, and can restore individual files from the archive. 

We continue with `tar -xf data`. Here `-x` is used to extract the file data, `-f` is used to use the file.
Keep doing these processes till you enter `file <file_name>` and get an output of `ASCII text`.
This file holds your password. 
This level is the most educational one i came across. 

---
## Level 13 -> 14

