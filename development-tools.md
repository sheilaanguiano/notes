# Development Tools
----------------

Author: Sheila Anguiano

-----------------

# Table of Contents
1. [Regular Expressions in JavaScript](#regex)
2. [Introduction to the Terminal](#terminal)
3. [Introduction to Git](#git)
4. [HTTP Basics](#http)
5. [Introduction to REST API's](#intro-rest-api)
6. [GitHub Basics](#github)
7. [Docker](#docker)


## Regular Expressions in JavaScript <a name="regex"></a>
### Regular Expressions
A regular expression is a way to describe a patterns in a string. **Regex** is a common way to shorten the term Regular Expression.
**Matches** matches the string you're typing in, these are case insensitive
A `.` dot has a special meaning in regular expressions. It matches any single character.

#### Matching Specific Characters
Regex uses a parser which compares each character in a regular expression with a character in the string in the same position, in other words, the regex parser requires two things: an expression also called a pattern and a string to match
```javascript
toyboats? // The ? mark matches the character that appears directly before it zero times or one time. In this case the lowercase "s" is optional, so this Regrex will match toyboats and toyboat BUT NOT toyboatss
```
You can also account for spaces or to include matches with lower or uppercase Letters using a **character set**
```javascript
[Ttj]oy ?boats?
/* This will match
toyboat
toyboats
toy boats
Toy boats
joyboats
*/
```
You can put as many letter as you want in the set but it will only match ONE position of the string, in the above position is the first position.
#### Matching Character Ranges
```javascript
[A-Za-z]oy[ -]?[Bb]oats?
/* This will match
toyboat
toyboats
toy boats
Toy boats
joy boats
toy-boats
toy-Boats
soy-Boats
*/

...[0-9] [A_Z]able
/* To match
8345 Gable
7238 Gable
2349 Table
8475 Cable
0994 Fable
1047 Zable
*/
```
#### Using Wildcard Characters
A wild card matches more than one character in a string, while we've using characters sets to match more than one character, there are shorter ways to match some cases. For example instead of using `[0-9]` to match any numeral character use `\d`. The `\` is found often in regular expressions but it's meaning can differ according to where it's used. usually it's a way to say that the character that follows has a special meaning
[0-9]								\d
[A_Za-z0-9_]					\w
[\t\r\n\f]						\s
any character					.

Often when you're composing regex, you'll want to control what character you include 

#### Finding Repeating Characters
Often when constructing a regular expression, you'll need a way to handle repeating characters.Two regex characters you'll use often are the `*` asterisk and the `+` plus symbol. These two symbols both can match more than one character

toy\w*		will match toy & toycar but NOT toyboat
toy\w+		will match only toyboat and toycar

There is also a time when you want to specify an exact number of characters like 3 digits in a phone's area code or the last four digits of a serial number. 

{3} 				three repetitions
{3, }				three or more
{3,5}			repetitions between 3 and 5
```javascript
//Matching social security pattern numbers
\d{3}-\d{2}-\d{4}
/* To match
000-35-6548
000-67-6587
*/

\w{5, 9} // This will match anycharacter that has between 5-9 characters
\w{5, } // This will match any string with more than 5 characters
```
#### Excluding Characters
`[^]`			negated character set
`[^@ ]`		match any character except @
`[^@.]`		match any character except @ and .

Just remember that a `.` inside a set, is just a dot, but outside is a special character. You can avoid this behaviour by scaping it `\.`
Regular expressions include characters which are the opposite of the digit, word or white space
 \d 		digit						\D		not  digit
 \w		word					\W 		not word
 \s		whitespace			\S		not whitespace
 
#### Alternation
Alternation is like the OR operator from JavaScript. It tells the parser to either math cone pattern or another
`toy | sail` This regex will match patters that only match toy or sail

#### Groups
```javascript
(toy|sail|tug) boat

/* This wil match
toy boat
sail boat
tug boat
*/
```
#### Beginning and Ending of Strings
^		beginning of a string
$ 		end of a string

```javascript
^(www\.)?google\.(com\net)$
// will only match google.com, google.net & www.google.com
//BUT NOT wwgoogle.com, www.google.commmmm

```
#### Project Notes
`/^[a-z]+$/ `		This regex validates a username with only lowercase characters

https://regex101.com/
https://www.regular-expressions.info/lookaround.html



#### Validating a Form
** Validaton** is the process of guarding agains receiving bad or inaccurate data. Regular expressions can help your program know whether to accept the value by matching the input with the pattern you expect. Validation can reduce user frustration, while ensuring you get valid data to use in your application. 
To accomplish this form validation, we'll use two methods
`test()` To test whether a string matches a regular expression
`replace()` To eplace text in a string by matching a pattern
```javascript
//This is called LITERAL SYNTAX
const regexObject = /^word$/
```
You can also create Regex by using the regular expression constructor
```javascript
const regexObject = new RegExp("/^word$/")
```
This ways is useful for dynamically creating regular expressions, for example is the user is typing in an expression to use for searching a block, you could take the input and pass it to the regex constructor. Then you could use the expression to search for the text and return the result.
Use the literal syntax when you already know the regex you want to use

[Documentation for JavaScript's RegExp object on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
[Article on form validation on MDN](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms/Form_validation)

#### Using Regex in JavaScript
```javascript
regex.test(testString) // True or False
string.replace(regex, replacementString ) // will give you a newString
```
#### Flags
Flags in Regular expressions modify the way the expression behaves. There are a number of flags, but we'll focus on 3
`i`		Case-insensitive. Using `i` will make the parser disregard case when searching for matches
`g`		Stands for global and tells the parses to find ALL matches contained in the string
`m`		Stands for multiline. Normally a caret will only match the beginning of a string

To add any these flags to a regex in JavaScript put them after the last slash of a regex literal, you can put them in any order.  
```javascript
'LION'.replace(/lion/i, 'mouse'); // This changes the string to "mouse"
'She ate watermelon at the waterpark'.replace(/water/, ''); // "She ate melon at the waterpark"
'She ate watermelon at the waterpark'.replace(/water/g, ''); // "She ate melon at the park"
const treat = `cheese
cheese
cheese`;
treat.replace(/^cheese$/, 'fruit'); // returns the same string with cheese 3 times because of the multiline
treat.replace(/^cheese$/m, 'fruit')// returns just the first word replaced
treat.replace(/^cheese$/mg, 'fruit')// returns the 3 word replaced to fruit
```

[Here's a site that tries to find the best regular expression for email addresses.](https://emailregex.com/)
[HTML5 email built-in support for email validation](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email#validation)
### Reformatting User Input
Manipulate data you get from the user and display it in a different format
#### Using Replace with Captured Groups
Parentheses capture the parts of the string they match. You can use these captured groups with a $ sign, followed by a number which matches the index of the captured group
```javascript
//The two sets of parenthesis capture two values, the first the word
//character, and the digit character.
/(\w)\w+(\d)/
```
While JAvaScript indexing is generally 0 based, however captured values in regular expression always begin at an index of 1. We can use these captured values with JavaScript replaced method
```javascript
let string = 'abc';
string.replace(/(\w)(\w)(\w)/, '$3 $2 $1')  // This returns "c b a" 

//Now we want to put a decial point in the middle of 4 numbers and a dollar sign in the beginning
let string = '5337';
let regex = /(\d*)(\d{2})/
let replacement = '$$$1.$2' // The first 2 '$' will print a literal $ dollar sign while the other is for the captured group
string.replace(regex, replacement); // "$53.37"

```
#### Reformatting a Telephone Number
The act the user tales when they're satisfied with the form input is to move focus away from the input. The `blur` event occurs on an input element when it loses focus, so we can use this to trigger our handler

[MDN Guide for Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)
[MDN Reference for the RegExp object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
[Fairly comprehensive reference on regular expressions](http://www.regular-expressions.info/)


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

- The `git clone` and `git init` commands are used to set up new repositories.
- The `git add`, `git status`, and `git commit` commands are the most frequently used subcommands in all of Git. They're used when committing new versions of files.
- The `git log` command is also important; it lets you view a list of your old commits.
- The `git mv` and `git rm` commands move and remove files that are being tracked by Git.
- The `git push` and `git pull` commands are used to synchronize commits with Git repositories on other computers

#### Initializing a Repository
 We need to change  into our project directory so we can turn it into a Git repo. Once inside your directory, you need to initialize the new repository with `git init` in your terminal, press enter to run it

You won’t see the `.git` directory at first. But `ls` has a special command line option that will cause it to show all files, `ls -a` will show even the hidden ones.
#### First Commits
Let’s add files to your new Git repo.

- Git commands won’t work outside a Git repo.
- Whenever you exit a repo directory, be sure to change back into the directory with cd before issuing any Git commands.

We’ve initialized a Git repository in our project’s directory. But our project files haven’t been added to the repository yet. In fact, Git has no idea they exis

Our project directory is known in Git terminology as the working directory, because it’s the directory where we actually edit and do other work in our files. 

There are three states every files goes through in a Git repository

When you make changes to a files in the working directory, it’s “modified”
You don’t necessarily want to include all of these modified files in your next commit, so you need to specify which ones you will include. You do this by adding files to the index, more commonly known as the “staging area”  or “cache”. The staging area is where you place the files you’re going to commit. Files you’ve added to the index are referred to as “staged” files.
When you’ve staged all the files you want, you make a commit, and that’s when the files are actually added to your Git repository.
Then, when you next make a change to any of those files, they’re treated as “modified”. You can stage and commit the files again to save a new version of them. And the cycle repeats.

We can find out what state our project files are in, using the `git status` command. Its output includes a list of “untracked files”. This are files that Git isn’t “tracking” yet - it’s not keeping track of changes to them so we’re not saving a new version of them.
It’s output also includes helpful messages suggesting commands to run next

**Staging Files**
- Many git commands produce output only when there's an error.Empty output means “everything is fine”
- The `git add` command adds a file to the staging area, the place we compose our commit.

**Commiting Files**
We use the git commit command to commit our staged changes.
You need to provide a message to go with every commit, a brief note explaining what the commit does.
We do this with the -m option. -m should be followed by a string in quotation marks. 
```bash
git commit - m “Add main site page”
```
*As a rule of thumb, a commit message should complete the phrase “This commit will:..”*

**Git Configuration**
- In addition to a commit message, Git, needs to know your name and e-mail addres so it can attach them to the commit. This is another of Git’s collaboration features. It allows other people working on the project to contact you if they need to ask about the commit.
- The name and e-mail address are permanently stored as part of Git’s configuration. The gut config command allows you to add and edit values in that configuration.

Most shells keep a history of commands you’ve entered. You can hit the up arrow key to bring up previous commands, so you don’t have to type them again.

**Using and editor to commit messages**
If you leave off the `-m` command like options when running git commit. Git will launch a text editor so you can enter a commit message. On most systems Git uses an editor named vi by default, but you can change this

http://heather.cs.ucdavis.edu/~matloff/UnixAndC/Editors/ViIntro.html

**Viewing Git Logs**
Once a commit is complete, it’s a permanent part of the repository’s history
You can review that history with the git log subcommand. For each commit git logs shows:
- Author name and email
- Date and time of  the commit
- The commit message
- If you want, you can add the -p option to git log: git log -p that will show the actual lines that were added in each file.
- Anytime a git command shows output that’s too long for the screen, it’ll show the output using a pager program.
[What's the shell](http://linuxcommand.org/lc3_lts0010.php)

## HTTP Basics <a name="http"></a>

## Introduction to Rest API's <a name="#intro-rest-api"></a>
### Getting the REST You Need
The RESTful API design pattern is a common, useful, and real world design pattern for turning your web app into a useful tool for building mobile apps, bots, desktop and server scripts, and more. Let's talk about what REST is, the building blocks and terminology of REST, and how you'll be using REST here at Treehouse.
### Introduction
APIs are one of the most commonly used interfaces for sharing information across both internal products and third party data sources, such as Twitter and Google.

REST stands for Representational State Transfer. REST sits on top of HTTP and defines how your API works. Mostly, it's a set of rules for how to use the HTTP framework to access bits and pieces of your application or data in reliable and predictable ways.

REST is really just another layer on top off HTTP. When you build a website or app, you’re building a user interface for your app’s logic and data model. The point of the API though, is not to create a traditional user interface (UI), but to provide a programmatic interface. A code UO, if you will for that same logic and data model. The major difference is that the burden of creating the interface is on the users of the API and not the creator.

API stands for Application Programming Interface, which is a  pretty jargony way of talking about code that makes easier for things outside of the application to interact with the application. Why do we want to provide gateways like this? Building a REST API that works with any external client, anywhere on the internet, saves us a lot of headaches 

The web by design is stateless. This means that every request that you make to a website is like meeting that site for the first time. REST doesn’t write this. It puts all of the work of remembering state on the client, which is your computer program. After each request, the server forgets your client entirely. In fact, you might not even be talking to the same server each time. Your client though, can, and will hold on, to whatever state information it needs, like authentications keys or previous endpoints.

TN:
https://teamtreehouse.com/library/http-basics

### Endpoints
When we talk about language, we have many different types of words, nouns, verbs, adjectives, adverbs, etc. When we talk about REST APIs , we really only care about two of those word types:  nouns and verbs.
A noun names something. IN a REST API, we have these things called resources.  What’s a resource? Usually, it’s a model in our application, like player’s scores on your game, the match. These resources are things we want to be able to retrieve, create or modify through our API.

We do that retrieving, creating and modifying, and even deleting, at specific URLs which are called endpoints. Endpoints represent either a single record or a collection of records

Examples of endpoints:
/api/v1/games			← Collection
/api/v1/games/1234		← Single resources because of the identifier at the end

Whether you use singular or plural names for your resources, keeping your URL designs consistent goes a long way towards discoverability and usability of your API.

 Now, let’s talk about verbs. They’re things for doing or want to do. In RESTful API design, they’re actions you’re going to take on resources, but instead of being in your URL, they’re represented by the type of request the client makes to the API. We have 4 verbs or HTTP methods, that we use for REST APis

GET: used for fetching either a collection of resources or a single resource
POST: used to add a new resource to a collection. For example we wouldn’t POST to players/567 or games/1234 because they aren't collections.
We could, however, POST to /players or /games to create a new player or a new game
PUT: is the HTTP method, or verb that we use when we want to update a record. We wouldn’t use PUT on collection or list URLs
DELETE: used for sending a DELETE request to a detail record, a URL for a single record, should elete just that record. Sending DELETE to an entire collection would delete the whole collection but that’s usually not implemented, with good reason
 
With a combination of nouns and verbs, we can write just about any sentence we want, at least within the constraints of our API

TN:
A resource is a piece of data, which usually comes out of a database (but doesn't have to!). Resources are gathered together into collections. Resources are usually available at endpoints that point to either individual resources or collections of resources. Endpoints don't represent actions that you take on those resources, though. Actions are determined by the data provided to an endpoint and the HTTP method used to access the endpoint.

By combining endpoints and HTTP methods, we can build complete sentences with just HTTP and REST.

URL vs URI, what’s the difference?
The acronyms URL and URI are often interchangeable. Although they can be referencing the same thing, there are some distinctions:
URI stands for “Uniform Resource Identifier”, the keyword being “identifier”. This can mean name, location or both:  Example /api/v1/games/1234
URL stands for “Uniform Resource Locator”, the keyword being “locator” so it provides full details to locate the resource. Example: https://teamtreehouse.com/alenaholligan
The part that makes something a URL is the combination of the name and an access method, such as https:// or mailto:.
URLs are URIS, but the opposite is not true. So saying URI is always technically accurate, but if you're discussing something that’s both a full URL and a URI (which URLs are) ot’s best to call it a “URL” because it’s more specific.

https://teamtreehouse.com/library/http-basics/get-and-post-requests-in-a-browser/html-review-and-uris-vs-urls
https://danielmiessler.com/study/url-uri/
https://tools.ietf.org/html/rfc3986#section-1.1.3

### Requests
The request that a user sends in, can provide a lot more information than just the end points and HTTP can provide a lot more information than just end points and HTTP can. Different aspects of the request can be used to change the format of the response.

Using Postman
We can send more information to the API through parameters
HTTP headers are one of the most amazing and useful pieces to a great API

	HTTP Headers
Accept: Specifies the file format the requester wants
Accept-language
Cache-control: Specifies whether the response can be generated from a cache or a quick-to-access memory bank of data or not


Again, you don’t have to implement all of the headers. You don’t have to implement any of them. But smarter clients and smarter APIs take advantage of the Http spec, to make transactions cleaner and more explicit. When consuming a third party API make sure you check the documentation to understand which headers that API accepts..

PENDING

You might be thinking that your user will send all of their GET request content to you in the query string where they are URL encoded. POST request on the other hand encode the content as either 

### Response
Like an HTTP request, an HTTP response also has headers. In Postman, we can also view the response Headers
- Content-Type: is used to specify what type of response is returned. This should match the type that was requested
- Status Codes:
    * 200-299   Good
    * 300-399   Understood but located elsewhere/ perform redirects
    * 400-499   Client Errors
    * 500-599   Server's end error

[HTTP Headers](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields#Response_fields)
[HTTP Status Codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)

### Security
An API that can't keep up with the demand is almost worse than no API at all. The firs step towards making sure that your API is available for clients is usually *caching*

A cache is usually a service that runs in memory to hold recently requested results, like a newly created record, or a large data set.

This helps to prevent database calls and even constly calculations on your data. Maybe your data is spread across several databases, or tables in your database, and gathering up all of that information, sorting it, and presenting it to the user takes several seconds. Putting that final calculated data into a cache means that subsequent lookups only take as long as required for your cache to find and return the right key.

The second step on our path to having a resilient API is rate limiting, which simply means that each user is allowed a certain number of request to your API in a given time period, once a user exhaust their allotment, they'll have to wait untilk the timer runs out so they can get more. This helps prevents your API to get flooded wtih request as well as to prevent **distributed denial of service or **DD0S** attacks*

Finally, authentification. It's hard to rate limit users when you don't have any idea which request is from which user. When building an API, how your user gets accounts is up to you, and whatever tools you're using, but there are some common ways like:
* API TOKENS: When setting up an API account a user is given a token and a secret pair. The user wull pass those credentials when making a request to the server, this allow the API's server to verify the communication. The servers takes the pair of credentials and checks that they're active proper users in the database, it's a lot like including a user name and a password when you log into a site. Users need to include their token with every request because of the statelessness of HTTP.

Most of the time, the token and secre are included as keys in the JSON or XML data that a client will send, but it is possible for them to be included in the authentication headers in the HTTP request.

Make sure you understand where the information will be included when consuming or building an API 

There are othe rmethod of handling authetication like cross realm authetication, HTTP Digest and others, but a lot of tgem will be specific to the API or tools you're using, POSTMAN should allow you to send any type of authetication request that you encounter
[Memcached](http://www.memcached.org/)

## GitHub Basics<a name="github"></a>
### Hello GitHub
#### Introduction
* Git: Version control system that's typically used with Github
* GitHUb: Website for hosting and collaborating on Projects

With git every developer has a **local** copy of the repository on their computer and then as they make changes they can upload those changes to GithUb and share them with a larger team

#### Search and Explore
A **repository** is the most basic element of Github, this folder contains all the project files, including documentation and stores the history of each file
- code view: You'll find the files included in the repo
    * license file
    * README
- issues: used to track bugs and feature request
- pull requests
* githubcom/explore we can browse through popular repos

#### Social Coding
*Star*ring a Project is the simplest way to let someone know that you appreceiate their project, 
*watch* to get project notifications
*fork* is a copy of a repository, similar to a branch and is typically used when you don't have access to a project, but let's you freely experiment with the project
*Create a repo*

### Working By Yourself
#### Using Issues
Issues are typically used to track bugs or features, but really issues can be uses for justa about any task you want to track hahahs

#### Mastering Markdown
Markdown is text to HTML conversion system that allows you to write in plain-text and then easily convert to HTML

#### Create a Branch
Branching allow you to conveniently work on multiple versions of your code at once. It's an exact copy of the original branch as it was at that point in time. This means you're free to experiment and commit changes safe in the knowledge that your new branch won't be merged until you're ready 

* branch names cannot have spaces
* `git checkout -b branch-name` switches branches
* `touch file-name.ext` creates a file from the terminal
* `git push origin branch`

#### Open a Pull Request
Pull request are use to propose changes to the project files. They're a way to start a discussion about commits and are often use for code review.

*Conversation View* :A pull request is typically used as a discussion about the changes being made to the repository
*Commits View* Contain information about who's made changes to the files. Each commit is an updated view of the repository, allowing us to see how changes have happened from commit to commit
*Files Changed View*: Allows you to see the changes that is being proposed, called the *dif*. The green text it's what has been added or red if something has been deleted. You can add line comments here as part of the code review

Most project teams require someone to sign off on the change before is merged

#### Conflict Resolution
When you're just getting started uwing Git and GitHub avoid make any edits on the website, doing all your work locally will help you avoid conflicts

### Working on a Team
#### Creating an Organization
You can create a free organization on GitHub, you can do this on the "+" sign on the top right side of the screen
#### Creating a Team
Teams allow you to share a set of permissions with groups of like people.

Inside your organization > Teams tab> Create a new team
- Setting (tab menu)
- Collaborators & Teams (left menu)
    - Then give the team the permission level (3 levels)

#### Creating a Repository in your Organization
Inside your Organization, click the "+" sign and create a new repo, just on the OWNER pick the organzation and not your USER

#### Open a Pull Request for your Team to Review
When you're working with a team is important to be clear about WHAT you're changing, and WHY you're making that change

Title: Kepp this action oriented
Description: Write the what and why, and you can do team-mentions to notify your team

#### Workflow Demostration
`git branch --remote`
`git checkout`

Pull request can have a few different methods of getting merged
- a team member always merges the pull requests
- the person that submitted the pull request will merged it 

### Create a Web Presence
#### GitHub Pages

### Get Involved in Open Source
#### Introduction to Open Source
Open source software is software that is modifiable and enhanceable by anyone becayse the software's license allows it. This code is publicly viewable on Github and doesn't require private access to view the code.
- Add a LICENSE
MIT License

[Choose an Open Source License](https://choosealicense.com/)

#### How to Find an Open Source Project
- GitHub Explore

#### Contributing to a Project with an Issue
How to create a great bug report
- Check existing issue (to not create duplicate issue)
- If it's not there then we create a clear title
- In the body, we describe reproducible steps so the maintainers and contributors see what I can see
- Include systems details (OS details, language version)
- Include intput and output, using markdown

#### Creating your Own Fork of an Open Source Repository
* Owner - Who owns the repo a user or an organization
* Collaborators - Teammates
* Mainteiner - Is someone the owner trusts to review pull request and keep the project on track
* Contributor - Someone who doesn't have direct push access to the code
* Community Members - People that use the project

As a contributor you need to **fork* the repository. A fork is a GitHUB feature where we take a copy of the repos in its current state and we move into our user account or organization.

Since a fork is owned by us (user/org) we can make changes directly and then submit a pull request between both repos
[Contributing to Projects](https://docs.github.com/en/get-started/quickstart/contributing-to-projects)

#### Contributing to a Project wit h a Pull Request
It is important to remember that not all Pull Requests will be merged. Try to keep your pull requests valuable to the main project by providing documentation, a bug fix, or a new feature. Avoid “gotcha” pull requests that only fix a single bit of wording. Regardless, not all pull requests get merged (and I have had dozens that get closed without merging). Don’t feel bad: keep at it and with more context and experience you will be an open source machine in no time.

- Add Unit Tests
- Include Screenshots
- Follow the style of the project


## Introduction to Docker <a name="docker"></a>
#### Why Docker?
Docker bundles your app together with all the libraries and services it depends on into a package called a container, which can then be delivered as a single unit wherever it needs to go. It's kind of like a shipping container. Because shipping containers are all the same shape, they can all be handled the same way, regardless of what they contain. Likewise, no matter what your app's architecture looks like, bundling it into a Docker container allows your coworkers or customers to deploy it anywhere, without worrying about what its components look like.

Dockerfile -- Dockerfiles define how an app should be built/packaged and deployed with Docker. They are simple text files with a number of reference commands defined in the Docker documentation.

#### Building and Image and Running a Container

* Software Delivery Pipelines -- When an app is setup so that it’s easily sent through the process of build, test, and deployment. Often referred to as CI or CD (Continuous Integration or Continuous Delivery).
* Dockerized App -- An app that has a Dockerfile made for it and can be built into a Docker image and run as a container.
* Container -- You can think of a container for an app as a real-life shipping container for freight. An app container is also like a VM, but far more lightweight and with the same security and operational isolation from system resources.

#### What is Docker 
Developers using Docker don't have to worry about installing and configuring complex supporting software like databases, or worry about which version of a language an app is built on. When a developer **Dockerizes** an app all the complexity of building the app is pushed into what Docker calls containers. You can thing of these like shipping containers of software. Containers are easily built, run and shared by any developer with access to the docker file. Docker is used by developers to ensure their apps work on every machine they're deployed to, and operation staff use Docker to better scale systems in production. Enterprise companies use Docker to build agile software delivery pipelines, so they can ship new features quickly, with better security. Docker lets enterpirses deploy to both Linux and Windows Servers easily. Employees joining a new project, no longer have to wait hours while the supporting software installs, you don't have to carefully explain how to setup various services, docker files abstract away the installaion dependencies, allowing you to easily package the app for nunning and test or production environments.

Containers are similar to Virtual Machines, both allow you to install a set of ap  ps and the services they depend on without mixing them whitout mixinf them with the software of the host OS, but containers don't emulate a virtual CPU, memory and other hardware like Virtual Machines do, they run directly on the host computer's hardware, making them more effcient in many situations.

To run an app in a Docker container
1. Write a docker file
2. Use the docker command line interface to build and image. And image is essentially a binary file that contains the app defined by the docker file, then you can share the image with others who can run it as a container.

Docker is useful for building and deploying single apps or services, but it's even better when you're building complex distributed systems, ther are existing tools such as **Docker Compose** which is a Docker file for multiple Docker containers and Docker Swarm which allows you to build,deploy and monitor multiple docker containers at once, either as a single services or as a set of services.

Docuker also has a rich networking API

[Infrastructure as Code](https://martinfowler.com/bliki/InfrastructureAsCode.html)
[It works on my Machine](https://www.usenix.org/conference/ures14/technical-sessions/presentation/it-works-my-machine-how-container-technologies)

#### Why should you use Docker
When to use Docker:
- zrunning apps easily with little knowledge of how the app works internally
- Deploy your app to dev, testing, staging, and production environments
- Sharing your app with others
- Docker can act like a version control system for those dependencies
- Can help maintain consistency between your developers work stations and the testing and production environments.
- Deploying distributed apps to 1000s of machines

### Fundamentals of Docker
#### Virtual Machines versus Containers
Long ago , developers had to install all of their app dependencies on the OS itself before they could begin development work, but this came with many drawbacks. Then came **Virtual Machines**, VMs emulated entire computers within a developer's computer allowing developers to install all their app's dependencies while keeping them isolated from the main OS, but they were slow, big and impractical to distribute
In 2010 a software project called Vagrant came long, that promised to automate the creation of VMs
In 2013 Docker arrived

Docker Containers - Pros:
- Faster startup time
- Resource re-use
- Native hardware access
- Less redundancy

Docker Containers - Cons
- May be no faster than a VM

Docker runs containers on top of light weight virtualized environmets without fully virtualized in the home machine, because docker doesn't virtulize entire OS, it can run much quicker and be far more affordable tan a traditional VM. To run virtual machines, the host OS runs software called a **hypervisor**. A hypervirsor manages the life cycle of VM's starting and stopping them as needed, managing their resources and keeping the whole setup secure by isolating the VMs from the host OS and from each other. And entire guest operating system runs within each virtual machine and your apps dependencies as well as the app itself are run within the guest OS, contrast this with Docker, where containers are run by the Docker daemon software, docker containers omits most of the guest OS except for a few packages, meaning most of the container resources are devoted to your apps dependencies, it doesn't need a guest OS, it simply share the host resourcces like processors, memory and networking devices between each container

* OS - Operating System, think Windows, MacOS/OS X, Linux (Ubuntu, RedHat, etc.)
* Emulation - When a system will replicate all the functionality of another system so that it’s transparent to the user what the underlying hardware is.
* Virtual Machine - an emulation of a computer system.
* Container - a lightweight isolated environment for an app or service to run.

#### Building Blocks of Docker
Docker packages apps into a single unit called an **image**. When these images are run via Docker they're called **containers**. Where a single container is an instance of an image, it's possible to run many containers based on a single image. An image is a mutable file that is essentially a snapshot of a container. Images can be store in the **Docker Registry** which is like GitHub for
docker images, because images can become pretty large, they're designed to be composed of layers of other images, that means, we only have to send small amounts of data over the network when transferring images. To make all this magic happen, Docker uses three major components:
* Docker Daemon:  which is a process running on your host OS
* Docker Registries: Whihc are server daemons connect to in order to retrieve images they need
* Docker Client: which issues command to the Docker daemon.

The Docker daemon coordinates running containers, packaging images, and transferring images to an from reegistries
[Docker Component](https://docs.docker.com/get-started/overview/)
[Introduction to Docker, VMS and Containers](https://www.freecodecamp.org/news/a-beginner-friendly-introduction-to-containers-vms-and-docker-79a9e3e119b)


#### Docker Networking
There are many real world use cases for connecting two containers together, such as running a JavaScript forntend that fetches data from a Node.js backend, or spending up to ten servers running big-data processing software, like **Spark**, using Docker's networking each container can share the workload. Networking is one of Docker's most fundamental strengths, form exposing prots to sharing a network between containers.
Example:
- `docker pull nginx` : Retieve an NGINX image from the docker registry
- `docker inspect nginx`: will give us all the image's config in JSON format, like the ExposedPorts
- `docker run -p 8080:80 --detach niginx` create a container form the image. Normally, it would attach or terminal to the NGINX process, and not let us do anything else until we hold the NGINX, but adding this option will leave the container running in the background, so we can do other things. Finally we need to add the name of the image we want to use. docker will spun a contaner from the nginx image, show is an ID for the new container, the return us to our shell props
- `docker ps`

### Building Images Using Docker
### Managing Images and Containers
