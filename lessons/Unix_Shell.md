# The Unix Shell
2015-07-24 UBC SWC workshop,
Instructor: Tiffany Timbers

#Introduce Software Carpentry

#Checkin
* Data downloaded and saved to Desktop?
* Can you open the Shell (Terminal on a Mac, Gitbash on Windows, or Shell on Linux)?
* Type `git status` and you should see `fatal: Not a git repository (or any of the parent directories): .git`

# Introduce the Shell
* Explain how the shell relates to the keyboard, the screen, the operating system, and 
users' programs.
* Explain when and why command-line interfaces should be used instead of graphical 
interfaces
* Introduce Nelle Nemo

## The Filesystem
Open the shell & explain the prompt: `$`


Read, evaluate, print loop example:
~~~
whomami
~~~

Another example, we can see where we are in the filesystem by typing:
~~~
pwd
~~~

Explain root directory in the Shell `pwd` output. Then go to filesystem and show it there.
Also, draw on whiteboard.

How do we see what is in the directory we are in? Use the list command:
~~~
ls
~~~

How do we navigate the filesystem? Use the change directory command:
~~~
cd Desktop
~~~

Now when we ask what our present working directory is we get:
~~~
/Users/tiffanytimbers/Desktop
~~~

Let's use these skills to navigate to the `nelle` directory in the data we downloaded 
(note - you might need to unzip the folder you downloaded). It should be here:
~~~
/Users/tiffanytimbers/Desktop/data/Shell/nelle
~~~

Let's take a look at what is in the `nelle` directory using the list command again:
~~~
ls
~~~

There's quite a few things in this directory, we can see which are files and which are
folders using the -F flag/option
~~~
ls -F
~~~

There are also hidden files & directories, we can see them using the -a flag
~~~
ls -a
~~~

To learn what other options you can use with a command, you can look at the documentation.
You can do this one of two ways, depending on the Shell you are using. 
~~~
man ls
~~~
or 
~~~
ls --help
~~~

note - if you use the `man` command, you need to type `q` to exit the documentation screen.


Let's move into the molecules directory using `cd`
~~~
cd
~~~

How do we get back to the `nelle` directory? Let's take a look at the hidden files in this
directory:
~~~
ls -a -F
~~~

We can see two weirdly named directories named `./` and `../` - these are the relative 
paths to the current and parent directory, respectively. We can use them to move to the 
`nelle` directory:
~~~
cd ..
~~~

* Discuss relative versus absolute path

* Introduce tab completion via navigating into `cd north-pacific-gyre` and `cd 2012-07-03`

#### Multiple Choice Questions 1 & 2 via Socrative.org (2 questions)

## Creating Things
* Navigate back to `nelle` directory
* Introduce `mkdir` via `mkdir thesis`
* Use `ls -F` to see what changed
* Look to see if there is anything inside the `thesis` directory via `ls thesis -F`
* Move into the `thesis` directory 
* Create a new document there called `draft.txt` via `nano draft.txt`
* Introduce nano, explain why we use it for the workshop, and what they might want to use
outside of the workshop.
* In nano, write: `It's not "publish or perish" anymore, it's "share and thrive".` and 
save and exit out of nano
* Check to see what is in the `thesis` directory now: `ls`

## Removing Things
* Let's delete what we just wrote via `rm draft.txt`
* See what has changed via `ls`
* Explain how deleting is FOREVER in the Shell
* Recreate a file called `draft.txt` in the `thesis` directory containing: `It's a start`
* Let's try to delete whole `thesis` directory, first need to navigate up via `cd ...` and 
the try `rm thesis`
* We get an error because `thesis` is a directory
* To remove a directory we need to use `rmdir thesis`
* This doesn't work either because there are files in the directory. We have two options,
individually delete the files inside the directory and then delete the directory or use a 
command which recursively deletes files: `rm -r thesis`. Use `rm -r` with CAUTION!
* Delete thesis directory via option 1: `rm thesis/draft.txt` and then `rmdir thesis`

## Moving Things
* Let's create the `thesis` directory one last time: `mkdir thesis`
* And create a file called `draft.txt` containing `"some short funny quote about thesese or persistance"`
* Let's rename this file and give it a much more informative name, e.g., `quotes.txt`
* We rename files via the `mv` command: `mv thesis/draft.txt thesis/quotes.txt`
* Check that this worked: `ls thesis`
* Note `mv` also works on directories
* We can also use the `mv` command to actually move things, for example moving `quotes.txt`
to the `nelle` directory: `mv thesis/quotes.txt .`
* Check that this worked: `ls . thesis`

## Copying Things
* We can also copy things via the `cp` command
* Let's put a copy of `quotes.txt` back in the thesis directory: `cp quotes thesis/quotes.txt`
* Check that this worked via `ls . thesis` 

#### Multiple Choice Questions 3 $& 4 via Socrative.org (2 questions)

## Pipes and Filters
Now that we know a few basic commands, we can finally look at the shell's most powerful 
feature: the ease with which it lets us combine existing programs in new ways. 

We'll start with a directory called molecules that contains six files describing some 
simple organic molecules. The .pdb extension indicates that these files are in Protein 
Data Bank format, a simple text format that specifies the type and position of each atom 
in the molecule.

* Take a look at what is in the `molecules` directory: `ls molecules`
* Let's look in one of these files, we can use the `cat` command to do this: 
`cat octane.pdb`
* What if we want to quickly look at the number of lines, characters or words in these 
files? We could do that using the `wc` command: `wc octane.pdb`
* How can get this information for all of these files?
* We can use `*` to do this! `wc *.pdb`
* If we are only interested in the number of lines in each file we can use the `-l` flag:
`wc -l *.pdb`
* Which of these files is the shortest? It's pretty obvious with only 6 files, but what if 
we have 6000 files?
* We could solve this problem as so:
`wc -l *.pdb > lengths.txt`
`cat lengths.txt`
`sort -n lengths.txt > sorted_lengths.txt`
`cat sorted_lengths.txt`
`head -1 sorted_lengths.txt`
* Easy and clear, right? Not really! We can do better by using pipes!
`wc -l *.pdb | sort -n`
* We can even add the third command on with another pipe!
`wc -l *.pdb | sort -n | head -1`
  
#### Multiple Choice Questions 5 via Socrative.org (1 question)

#### Challenge Question 1 (keynote slides)

## Loops
We have learned a number of ways to save time (e.g. tab completion, wild-cards and pipes),
now we are going to learn another way to save time, that works especially well when you 
need to do the same task over and over again.
* Go to loops figure of `animals` and `creatures` directories
* Get students to move to `nelle/creatures`
* Inside this directory we have 2 files: `ls`
* We are going to work towards a loop that renames these files, but let's start with a 
simpler case, let's make a loop that prints the first 3 lines of these files:
`$ for filename in basilisk.dat unicorn.dat`
`> do`
`> head -3 $filename`
`> done`
* It works! Now what if we had 600 files? We don't want to type each out individually...
We can use a wild-card to make this easier!
`$ for filename in *.dat`
`> do`
`> head -3 $filename`
`> done`
* OK, now that we understand loops, let's go back to our original problem and write a loop
to rename these files:
`$ for filename in *.dat`
`> do`
`> mv $filename original-$filename`
`> done`

#### Multiple Choice Questions 6 via Socrative.org (1 question)

* Loops are fantastic and they save us a lot of time, but when we make mistakes, we can 
make a lot of them with a loop. 
* One way to avoid this is to use the echo command to print the commands to the screen 
instead of actually running them. If that looks good then we can go ahead and remove the 
command and run the loop.
`$ for filename in *.dat`
`> do`
`> echo head -3 $filename`
`> done`

#### Challenge Question 2

## Shell Scripts
We are now going to learn how to take the commands that we repeat frequently and save them 
in a file so that we can re-run all of the operations again later by typing a single 
command. We will essentially writing small programs.
* Direct students to `molecules` directory
* Create a file called `middle.sh` containing: `head -15 octane.pdb | tail -5` which will
print lines 11-15 of the file `octane.pdb`
* Now we can simply run this set of commands by simply typing: `bash middle.sh` to execute
the commands within the file.
* This program isn't very flexible and can currently only be used on `octane.pdb`
* We can make it more flexible by using variables and taking in command line arguments. In 
the script we replace `octane.pdb` with `$1` (a special variable): `head -15 $1| tail -5`
* Now when we call `middle.sh` we can now specify which file we want to apply this to. 
E.g., `bash middle.sh cubane.pdb`
* What if we want to make it even more flexible? Say, for example which lines we want to 
grab? We can do this by using more variables: `head -$2 $1 | tail -$3`
* So lets grab lines 3-5 of a file: `bash middle.sh cubane.pdb 5 3
* Now, we know what this script does, but will we remember in 6 months from now? I wont!
* We can use comments to document what the code does for our future selves and for anyone
who we share it with: 
`# Selects lines from the middle of a file`
`# Usage: middle.sh filename end_line number_of_lines`
`head -$2 $1 | tail -$3`

#### Multiple Choice Questions 7 via Socrative.org (1 question)

## History

How do you save what you have been doing?? You can use the history to be a basis for 
your script!

If we want to see all the commands we used today, we simply type `history`


For example, say we wanted to make a file called record.txt that keeps track of the date,
the username, and the directory every time we ran our analysis pipeline so that we can 
keep track of when, who and where the analysis was being done. We could do that by typing 
the following commands:


~~~
date > record.txt
whoami >> record.txt
pwd >> record.txt
cat record.txt
~~~


But this time consuming to type out every time. Let's use the history to grab what we just 
typed and use that as the basis for our script.


~~~
history | tail -5 > make_record.sh
nano make_record.sh
~~~


You might notice that this looks a bit different from the scripts we have been writing, it
contains some extra information that might trip up the Shell. But, we can simply use our 
editor to fix it.


Let's try running it:
~~~
bash make_record.sh
~~~


#### Challenge Question

Notice that every time we run `make_record.sh` is overwrites the previous file? How could
we avoid this? For example, how could we specify a new name for the file every time we run
the script? 


Enter answers in Etherpad


My answer:

~~~
date > $1
whoami >> $1
pwd >> $1
cat $1
~~~


## Finding Things

* `grep`
#### Multiple Choice Questions 8 via Socrative.org (1 question)

* `find`
#### Multiple Choice Questions 9 via Socrative.org (1 question)
