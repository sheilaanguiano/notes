# Development Tools

# Table of Contents
1. [Introduction to the Terminal](#terminal)
2. [Introduction to Git](#git)


## Introduction to the Terminal <a name="terminal"></a>
### The Command Shell
#### What's the Terminal?
* The Graphical User Interfaces or GUIs you see on desktop and mobile apps and websites have their place. You can easily see what options are available to you, and click on the one you want.
* The terminal lets you run commands that are far more powerful than anything a GUI can do for you.
-   Apps that run in the terminal use what's called a  **command-line interface**, or CLI.
-   So how do you access the terminal?
    -   Most operating systems offer some sort of terminal-like program by default.
    -   On Mac and Linux machines, it's usually simply called Terminal.
    -   On Windows, it's called Command Prompt, although there are alternatives like PowerShell.
-   The vast majority of servers where developers deploy their software are running operating systems that are compatible with Unix, a powerful OS developed in the 1960s.
-   These compatible OSs include Linux and Mac OS.
#### The Shell 
-   By default, terminals run a program called a  **shell**.
    -   There are many different shell programs available, most of them with names ending in "sh" like  `zsh`,  `ksh`, and so on.
    -   Most operating systems today run a shell called Bash, and that's what we use for this course.
    -   All the different shells work very similarly, so the things you learn in Bash will be applicable in the other shells, too.
```bash
shei@MacBook-Air~%
```
-   You can see a bunch of text here, ending in a dollar sign (`$`).
    -   This is the shell  **prompt**. The shell is "prompting" you to type something.
    -   Most shell prompts end with a dollar sign like this.
     -   The blinking box following the dollar sign is the  **cursor**. It's the place that text you type will appear. It mostly works like the cursors you've seen in word processors and web forms, but with a few exceptions.
    -   You can type text with the letter keys on your keyboard, and you can delete it with the backspace key.
    -   You can move back and forth within the text you've typed on this line with the left and right arrow keys.
    -   But you can only type on this one line; you can't move off of it.
    -   If you press the up and down arrow keys, it will instead cycle through entries you've made previously. This is called command history, and we'll talk about it more in an upcoming video.
-   We can run commands at the prompt to execute other programs inside the shell.
    -   The output of these commands will be shown in the terminal.
    -   Because the shell offers you a single line of text where you enter commands, this is often referred to as the  **command line**.

* `ls`  used for listing files
* `whoami` prints the name of the current user account
* `cat` concatenates, or joins, the contents of files together
* `clear` clears output from the terminal screen, moving the prompt up to the top. Shortcut: "Ctrl" key, and press "l". (That's a lower-case "L".)

#### Command Arguments
The first word you enter at a command line is the name of the command. Most commands can take **arguments** following the command name.
Commands can take multiple arguments, separated by spaces.
```bash
treehouse:~/workspace$ cat statue.txt cart.txt 
A statue of a hunter standing over a dead bear. Creepy. 
A stand selling hot dogs and bottles of diet cola.
```
Now here's another command that takes arguments: the `echo` command. `echo` takes arguments and converts them into output: `echo hello`
-   That makes  `echo`  a great way to understand how command line arguments work.
-   `echo`  can take multiple arguments. It will print all of its arguments out, joined together with spaces:  `echo Each of these words is an argument.`
-   You can use any combination of characters as an argument, not just letters, so the last argument in that last command includes both the word argument  and  the period.
-   If you need to take multiple words and convert them to a single argument, you can surround them with quotation marks.
-   You can use either single quotes:  `echo 'Everything between the quotes is one single argument.'`
-   Or double quotes:  `echo "Everything between the quotes is one single argument."`
-   Notice that the quotation marks were consumed by the shell; they never reach the  `echo`  program. They're not treated as part of the resulting argument, and so they don't appear in the output.
-   Now with a command like  `echo`, the difference between one argument and many arguments may not seem that important.
-   But even with  `echo`, we can show you a situation where the difference matters.
-   Here's an echo command with many arguments, each with two spaces between them:  `echo There are two spaces between each of these words.`
-   The spaces between arguments are also consumed by the shell, so even though there are two spaces between each argument, those spaces never reach the  `echo`  program.  `echo`  just joins all its arguments together with a single space, so the double spaces are lost.
-   If you want to preserve the double spaces, you have to make them part of a single argument using quotes:  `echo 'There are two spaces between each of these words.'`
- Using spaces in a file name is normally not a good idea,
#### Command Options
Command Arguments are all the same to the shell, but there's a type of argument that many commands treat specially: options. **options** generally make some small change to the way a command works.
-   For example, we can get the  `ls`  command to display all files, even files that are hidden, by passing it the  `-a`  option as an argument:  `ls -a`
-   On Unix-like systems, a file is treated as "hidden" if its file name begins with a dot.
- Here's another option for the `ls` command: `-t`, which causes files to be sorted by the time they were created: `ls -t`
- It can be hard to remember what those single-letter options stand for, so many commands also support longer option names.
	 -   For example, the  `ls`  command lets you use a  `--all`  option instead of  `-a`  to list all files:  `ls --all`
	-   Not all single-letter options have a longer equivalent, though. For example there is no longer version of  `ls`'s  `-t`  option, so you'll have to use the abbreviation:  `ls --all -t`

#### Shortcuts
-   At various points, you're inevitably going to make typos that prevent a command from working.

-   That's why the shell keeps a list of the commands you're entered previously.  You can view it with the command  `history`:  `history`
-   You can also press the up arrow on your keyboard bring up commands you've run previously.
-   Pressing the up arrow key takes you back through the list of old commands. If you go too far, you can press the down arrow key to go forward again.
-   When you get to the command where you made a typo, you can edit it to fix the issue. Then just press Enter to run the updated command.
-   Or, if there's a command you want to run again as-is, just hit up-arrow to bring it up, and press Enter to run it.
-   By default, your shell may lose all its history when you close the terminal, and it may not save very many old commands. But it's possible to configure it to save history between terminal sessions, and to save thousands of previous commands. You can find directions to do so  [here](https://web.archive.org/web/20181120100558/https://www.digitalocean.com/community/tutorials/how-to-use-bash-history-commands-and-expansions-on-a-linux-vps).

Another good way to fix typos is to prevent them in the first place. To do that, you can let your shell do the typing for you, with a feature called  **tab completion**. You just type the first few letters of a command or argument, then press the Tab key. The shell will attempt to figure out what you mean and complete the word for you.

-   Let's say I wanted to run the  `whoami`  command, to get the current user name.
    -   I type the first few letters:  `whoa`, and press the Tab key on my keyboard.
    -   The  `whoami`  command is the only one that starts with  `whoa`, so the shell realizes that's what I must be trying to run. It types the remaining letters of the command name for me, followed by a space.
    -   Now I can just press Enter to run the command.
-   Tab completion works with file name arguments, too.

### Directories and Files
#### Directories
-   Most operating systems have a concept of "folders", which group a collection of files together.
-   In the shell, folders are usually referred to as "directories". Folders and directories are the same thing, but the term directory dates from before modern operating systems and their "folders" metaphor.
-  `pwd`, which stands for "print working directory":  `pwd`
-   You can change between directories using the  `cd`  command.  
-   If we try to run commands that work on files from other directories, they won't work, because those files aren't in this directory.
    -   When one directory contains another, it is said to be the  **parent directory**.
    -   A directory that's inside another is said to be a  **child directory**  or  **subdirectory**.
    -  `/home/treehouse/workspace/mall/starbunks` Each slash separates one directory name from another.
    -   When you see a list of nested directories separated by slashes like this, it's called a  **file system path**, or just "path" for short.
    -   Just as you might follow a path through a forest, a path through a file system indicates the route you need to follow through directories to get to a particular directory or file.
    -   Unix-like operating systems use forward slashes like you see here.
    -   Windows paths use backslashes instead of forward slashes, but they work the same way.
	-   `ls -a`, to list all files. That listing includes two strange-looking names,  `.`  and  `..`. The names use period characters, but they're read aloud as "dot".
    -   `.`  refers to whatever directory we're currently in. So we can type  `cd .`, but that will just change us to the same directory, so it doesn't seem to do anything:  `cd .`
    -   But  `..`  refers to whatever directory is the  parent  of the current directory.
 
You can use tab completion with directory names, too, and it's very helpful when changing directories. Any time you're referring to a directory, you can put a slash at the end of the directory name, and it means the same thing as if you'd just put the directory name by itself.

#### Relative Paths
-   A  **relative path**  is a file path that's relative to your starting location in the file system.
	- Suppose we want to print the contents of the `menu.txt` file in the `starbunks` directory we saw before.
```bash
treehouse:~/workspace$ cat mall/starbunks/menu.txt
```
Because you provided a path, the operating system knows how to go from folder to folder to find the file. You can do the same with `ls`
#### Absolute Paths
-   If I change up to the parent directory enough times, eventually I'll reach a directory where I can't go any further.
    -   This is the  **root directory**. If you imagine the file system like a tree, with directories as branches, the root directory would be the base that all the other branches spring out of.
    -   The root directory doesn't have a name.
    -   Its path is just a single slash (`/`).
    -   Instead of typing  `cd ..`  a bunch of times, I can type  `cd /`  to jump to the root directory:  `cd /` . This works no matter what directory you're in
    -  An  **absolute path**  is one that starts at the root directory.

#### Directory Shortcuts
-   On Unix-like systems, as a safety feature, you can't run an executable file just by typing its name:  `hello.sh` (.sh is the extension for a shell program"
-  You have to provide the executable's name as part of a path. You can do it with `..` or  you can form a path just by using  `.`  to represent the current directory, a slash, and the name of the executable:  `./hello.sh`
- Executable files are outside the scope of this course. But you can learn how to write a shell script, make it executable, and run it  [here](https://web.archive.org/web/20180428191724/http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_02_01.html).
- Another special symbol we've seen is `..`, which represents the parent directory.
	-   Suppose we want to change to the  `dentist`  directory that's within the parent directory. We don't have to  `cd ..`  and then  `cd dentist`. Instead, we can type  `cd ../dentist`:  `cd ../dentist`
- Each user account has its own subdirectory under the  `home`  directory, represented by `~`. -   For ordinary users, their home directory is really the only one on your system that they should make changes to.

#### Wildcard Expansion
-   Now for a special symbol that works totally differently than the others, the asterisk:  `*`
    -   The asterisk is used for  **wildcard expansion**, where a pattern is used to complete one or more file or directory names.

I'm going to change to a subdirectory within this workspace's  `library`  directory devoted to novels by author Kim Stanley Robinson:  `cd ~/workspace/library/fiction/kim_stanley_robinson/`. There's files for the books in his "Mars Trilogy": "Red Mars", "Green Mars", and "Blue Mars". There's also a file for the new "Red Moon" novel. And finally there's some kind of executable script here.
    -   So suppose I wanted to run a command on all the files with a  `.txt`  extension.  `echo *.txt`
    -   You can see that the  `*.txt`  gets expanded out to four arguments, one for each file it matched. There's an argument here for each text file in this directory. Notice that the shell script was  not  included, because its file name ends in  `.sh`, not  `.txt`.

- Wildcard expansion can find all file names that end a certain way, but it can also find all file names that start a certain way.
- To match all files, regardless of how they start or end, use just a star: `echo *` .But be warned, sometimes a wild card will match files you don't want.

### Common Commands
#### Viewing Files with "less"
**Pager programs** are interactive programs that display a file on your terminal screen, one page at a time.
When I say they're interactive, I mean that they don't finish running immediately; they wait for input from you.
The original pager on most Unix-like systems is a program called  `more`
Many systems have another, newer pager program installed that's inspired by `more`, called `less`.
When you want to quit  `less`, you press the "q" key.
Unlike `more`, `less` doesn't leave the file contents up on your terminal screen when it's done. It restores everything just the way it was.

#### Working with Files
 `cp` command, which lets you copy files and directories. Run the `cp` command. I give it two arguments: the name of the file I want to copy, and the name of the file I want to copy it to: `cp bird.txt pigeon.txt`
	 -   The  `-r`  option stands for  `recursive`, as in "copy recursively". To do something recursively means to do it in a recurring or repeating fashion.  In this case, it means that not only will the  `offices`  directory be copied, its contents and all of the contents of its subdirectories will be copied, too
`mv` move
`rm` which stands for remove
`rm -r` removes the directory and all subdirectories
`mkdir` creates a new directory

#### File and Directory Naming Conventions
* File names are case-sensitive on Windows and Linux systems, stick to lowercase
* If you're creating a file or directory you intend to share, you should stick to ASCII characters - un-accented characters from the English alphabet.
* Spaces are legal in file or directory names, but you should avoid them
	* it's better to separate them with underscores: `mkdir peter_f_hamilton`
	* Sometimes you'll see dashes used: `mkdir peter-f-hamilton`
	* STICK TO ONE

#### The Manual
We'll admit, it's a little difficult to remember how to use some of these commands. It gets better as you get more practice using them, but even experienced shell users have to look up commands or options that they don't use as often.

`man` short for manual
	* So you can use the arrow keys to scroll, and type "q" to quit
#### Other things to Explore

* `find` command is used to recursively search through a directory and all its subdirectories for files You can read more about `find`  [here](https://web.archive.org/web/20180625211551/https://opensource.com/article/18/4/how-use-find-linux).
* `grep` command is used to print lines in a file that match a particular pattern. You can read more about `grep`  [here](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html).
*  `vi`  stands for "visual", is the default editing program installed on most Unix-like operating systems. -   It's not fancy, but it  is  widely available. At some point you are likely to find you have to use it, because it's the only editor available on the system you're working on. Some developers love it, though, and use it for their daily work, especially an expanded version called `vim` (which stands for "vi improved"). You can read more about `vi`  [here](https://web.archive.org/web/20190119024038/https://ryanstutorials.net/linuxtutorial/vi.php).
* `nano` is an editor installed by default on some, but not all Unix-like systems. You can read more about `nano`  [here](https://web.archive.org/web/20190119024442/https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/).

#### Project Ideas

Noah Veltman has created  [a murder mystery you can solve in the shell](https://github.com/veltman/clmystery).

## Introduction to Git <a name="git"></a>
### First Commits
#### Introduction
Version control systems (VCS)  keep old versions of your files for you. Version Control is so important that many different systems have been created over the years such as Subversion, Mercurial and Git

**Git is the most popular VCS. Why?**
- Common commands are easy
- Great for collaboration
- Safer than other VCSs

[gitmersion](http://gitimmersion.com/index.html)

#### Git Overview

- Git is a version control system. It helps you control the different versions of the files in your project.
- The collection of all the old versions of your project's files is known as a **Git repository**. It's basically just a folder in which you can edit your files, then run Git commands to store your changes.
- Each time you complete a change to some or all of your project's files, you can take a snapshot of their current contents. These snapshots are known as **commits**.
- Git is a distributed version control system, as opposed to a centralized system. In a distributed system, you can copy a complete repository with the full project history to every developer's machine.
- Bash is a command shell that runs on many Mac, Linux, and even some Windows computers when you open their terminals.
- Bash prompts usually end in a dollar sign. When you read Git tutorials out on the web, you may see a dollar sign; that usually indicates that the text following it should be typed at a shell prompt.
- When Git is installed on a system, like it is here in this workspace, it places an executable named git where it can be run from any shell prompt. This is the gitcommand.
- All the commands we're going to show you during this course will use this executable, so they're all going to start with git followed by a space.
Then we need to specify the subcommand or options we want.
- Git command line options consist of either a single dash followed by a single letter, or a double-dash [type --] followed by a word.
git --help will print out some help on using the Git program.


**Common Git subcommands**

The ｀git clone｀ and ｀git init｀ commands are used to set up new repositories.
The ｀git add｀, ｀git status｀, and ｀git commit｀ commands are the most frequently used subcommands in all of Git. They're used when committing new versions of files.
The git log command is also important; it lets you view a list of your old commits.
The git mv and git rm commands move and remove files that are being tracked by Git. We'll learn about those in Stage 2 of this course.
The git push and git pull commands are used to synchronize commits with Git repositories on other computers
