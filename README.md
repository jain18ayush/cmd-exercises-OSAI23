# Learn Enough Command Line to be Dangerous - Exercise Answers

# 3: Inspecting files

## 3.1: Downloading a file

### Exercise 1

Q: Use the command curl -I www.learnenough.com to fetch the HTTP header for the Learn Enough website. What is the HTTP status code of the address? How does this differ from the status code of learnenough.com? 

A: 200 ok , status code of learnenough.com is 301 Moved Permanently

### Exercise 2

Q: Using ls, confirm that sonnets.txt exists on your system. How big is it in bytes?

A: `ls -l sonnets.txt` , 96635 bytes

### Exercise 3

Q: Using the -h (“human-readable”) option to ls, list the long form of the sonnets file with a human-readable byte count. 

A:`ls -lh sonnets.txt`

### Exercise 4

Q: Suppose you wanted to list the files and directories using human-readable byte counts, all, by reverse time-sorted long-form. Why might this command be the personal favorite of the author of this tutorial?

A: `ls -hartl` , hartl the author's last name

---
## 3.2: Making heads and tails of it

### Exercise 1

Q: By piping the results of tail sonnets.txt through wc, confirm that (like head) the tail command outputs 10 lines by default. 

A: `tail sonnets.txt | wc`

### Exercise 2

Q: By experimenting with different values of n, find a head command to print out just enough lines to display the first sonnet in its entirety

A: `head -n 18 sonnets.txt`

### Exercise 3

Q: Pipe the results of the previous exercise through tail (with the appropriate options) to print out only the 14 lines composing Sonnet 1.

A: `head -n 18 sonnets.txt | tail -n 14`

### Exercise 4

Q: To simulate the creation of a log file, run ping learnenough.com > learnenough.log in one terminal tab. (The ping command “pings” a server to see if it’s working.) In a second tab, type the command to tail the log file. (At this point, both tabs will be stuck, so once you’ve gotten the gist of tail -f you should use the technique from Box 4 to get out of trouble.)

A: `ping learnenough.com > learnenough.log` , `tail -f learnenough.log` , `ctrl-c`

---
## 3.3: Less is more

### Exercise 1

Q: Run less on sonnets.txt. Go down three pages and then back up three pages. Go to the end of the file, then to the beginning, then quit. 

A: press `spacebar` x3, press `ctrl-b` x3, `G`(capital g), `1G` , `q`

### Exercise 2

Q: Search for the string “All” (case-sensitive). Go forward a few occurrences, then back a few occurrences. Then go to the beginning of the file and count the occurrences by searching forward until you hit the end. Compare your count to the result of running grep All sonnets.txt | wc.

A: `/All`, press `n`, press `N`, 10 "Alls", type`grep All sonnets.txt | wc`

### Exercise 3

Q: Using less and / (“slash”), find the sonnet that begins with the line “Let me not”. Are there any other occurrences of this string in the Sonnets?

A: `less sonnets.txt`, `/Let me not`, no

### Exercise 4

Q: By searching for the string “sort” in the man page for ls, discover the option to sort files by size. What is the command to display the long form of files sorted so the largest files appear at the bottom?

A: `ls -Slr`

---
## 3.4: Grepping

### Exercise 1

Q: By searching man grep for “line number”, construct a command to find the line numbers in sonnets.txt where the string “rose” appears. 

A: `grep -n rose sonnets.txt`

### Exercise 2

Q: You should find that the last occurrences of “rose” is (via “roses”) on line 2203. Figure out how to go directly to this line when running less sonnets.txt.

A: `less sonnets.txt`, `2203G`

### Exercise 3

Q: By piping the output of grep to head, print out the first (and only the first) line in sonnets.txt containing “rose”.

A: `grep -n rose sonnets.txt | head -n 1`

### Exercise 4

Q: In Listing 16, we saw two additional lines that case-insensitively matched “rose”. Execute a command confirming that both of the lines contain the string “Rose” (and not, e.g., “rOSe”).

A: `grep Rose sonnets.txt`

### Exercise 5

Q: Write a command confirming that the number of lines matching “Rose” but not matching “rose” is equal to the expected 2.

A: `grep Rose sonnets.txt | grep -v rose | wc`

---
## 3.5: Summary

### Exercise 1

Q: Pipe history to less to examine your command history. What was your 17th command?

A: `history | less` , uname -r

### Exercise 2

Q: By piping the output of history to wc, count how many commands you’ve executed so far. 

A: `history | wc`, 401

### Exercise 3

Q: By piping the output of history to grep, determine the number for the last occurrence of curl. 

A: `history | grep`, 402

### Exercise 4

Q: Use the result from the previous exercise to re-run the last occurrence of curl. 

A: `!402`, `!401`

### Exercise 5

Q: What do the O and L options in Listing 8 mean?

A: `-O` = remote-output = write output to a file named as the remote file, `-L` = location/follows redirects

---
# 4: Directories

## 4.1: Structure

### Exercise 1

Q: Write in words how you might speak the directory ~/foo/bar. 

A: root slash foo slash bar

### Exercise 2

Q: In /Users/bill/sonnets, what is the home directory? What is the username? Which directory is deepest in the hierarchy? 

A: home dir = users, username = bill, deepest directory = sonnets

### Exercise 3

Q: For a user with username bill, how do /Users/bill/sonnets and ~/sonnets differ (if at all)?

A: `~/sonnets` belongs to the superuser/root, `/Users/bill/sonnets` belongs to a user named bill

---
## 4.2: Making directories

### Exercise 1

Q: What is the option for making intermediate directories as required, so that you can create, e.g., ~/foo and ~/foo/bar with a single command?

A: `-p`

### Exercise 2

Q: Use the option from the previous exercise to make the directory foo and, within it, the directory bar (i.e., ~/foo/bar) with a single command.

A: `mkdir -p ~/foo/bar`

### Exercise 3

Q: By piping the output of ls to grep, list everything in the home directory that contains the letter “o”. 

A: `ls -a | grep o`

---
## 4.3: Navigating directories

### Exercise 1

Q: How do the effects of cd and cd ~ differ (or do they)? 

A: they don't differ, they both change the current directory to home directory

### Exercise 2

Q: Change to text_directory, then change to second_directory using the “one directory up” double dot operator ... 

A: `cd text_directory`, `cd ..`

### Exercise 3

Q: From wherever you are, create an empty file called nil in text_directory using whatever method you wish. 

A: `cd text_directory`, `touch nil`

### Exercise 4

Q: Remove nil from the previous exercises using a different path from the one you used before. (In other words, if you used the path ~/text_directory before, use something like ../text_directory or /Users/<username>/text_directory.) 

A: `../nil`

---
## 4.4: Renaming, copying, deleting directories

### Exercise 1

Q: Make a directory foo with a subdirectory bar, then rename the subdirectory to baz. 

A: `mkdir ~/foo/bar`, `mv ~/foo/bar ~/foo/baz`

### Exercise 2

Q: Copy all the files in text_files, with directory, into foo. 

A: `cp -r ../text_files foo`

### Exercise 3

Q: Copy all the files in text_files, without directory, into bar. 

A: `cp -r ../text_files/ bar`

### Exercise 4

Q: Remove foo and everything in it using a single command. 

A: `rm -rf foo`

---
## 4.5: Summary

### Exercise 1

Q: Using a single command-line command, make a directory foo, change into it, create a file bar with content “baz”, print out bar’s contents, and then cd back to your home directory.

A: `mkdir foo && cd foo && touch baz > bar && cd`

### Exercise 2

Q: What happens when you run the previous command again? How many of the commands executed? Why? 

A: no commands are executed because it won't create the same directory again

### Exercise 3

Q: Explain why the command rm -rf / is unbelievably dangerous, and why you should never type it into a terminal window, not even as a joke. 

A: force removes all files on the system

### Exercise 4

Q: How can the previous command be made even more dangerous? Hint: Refer to Box 11. (This command is so dangerous you shouldn’t even think it, much less type it.) 

A: by adding `sudo` to the beginning, anybody can use the command
