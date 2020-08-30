# Linux-administration

## 01 Linux Fundementals
### Linux directory structure

![images](images/directoryStructure.png?raw=true "Title")

The most common directories known are,

```
* /     - "root" the top of the linux system hierarchy
* bin   - binaries and other executable programs
* /etc  - system configuration files
* /home - Home directories
* /opt  - optional or third party software gets intalled here(softwares which are not budled with ubuntu. 
          eg: google earth, vlc etc...)
* /tmp  - temporary space. typically cleared on reboot.good to keep temporaray files
* /usr  - user related programes
* /var  - varuiable files. most notably log files.
``` 

Applications that are not part of the base OS can be installed in,

```
* /usr/local
* /opt
```
### The shell

* it is the default interface to shell.
* A program that accepts your commands and execute that commands.
* Also called a command line intrepretter

```
In the command line $ - indicates that we are using the system as a normal user
                    # - inndicates that we are using the system as a super user. super user is also known as root user or root.
```
#### Root, the superuser
* Root is all powerful
* Normal accounts can only do a subset of the things root can do.
* Root access is typically restricted to system administrators
* Root access may be reqiired to install, start, or stop an aplication
* Day to day activities will be performed using a normal account

#### Tilde Expansion
```
~jason  = /home/jason
~pat    = /home/pat
~root   = /root
~ftp    = /srv/ftp
```


~  - represents home directory

![images](images/telda.png?raw=true "Title")

#### Basic Linux commands
```
* ls    - list directory contents.
* cd    - change the current directory
* pwd   - displys the present working directory
* cat   - concatenates and displays fles
* echo  - displays arguments to the screen
* man   - displays the online manual
* exit  - exits the shell or your current session
* clear - clears the screen
```
#### Getting help at command line

Navigating Man pages
--------------------
```
Enter - move down one line
Space - move down one page
g     - move to the top of the page
G     - move to the bottom of the page
q     - Quit   
```
Enviornment variables
----------------------
* Storage location that has a name and a value
* Typically uppercase
* Access the contents by executing:
  `echo $VAR_NAME`

Paths
-----
* An enviornment variables
* Controls command search path
* contains a list of directories

```
which command : which - locate a command
search Man Pages : man -k SEARCH_TERM
```

Summary
-------
* Man is used to display documnentataion
* $PATH controls your search path
* learn full path to commands with which
* ask commands for help with --help or -h
* search man pages by using man -k 

#### Working with directories

* are containers for other files and directories
* Provide a tree like structure
* can be accessed by name or shortcut

Directory shortcuts
-------------------
```
.   - this directory
..  - The parent directory
cd  - change to the previous directory
/   - directory seperator
```
#### Creating and removing directories

##### create directory
mkdir[-p] directory. p - stands for parent
```
eg: mkdir -p dir/dir1/dir2
    mkdir dir/dir1/dir2 - we can't create directories with sub folders with out -p
``` 
##### remove/delete directory
rmdir[-p] "directory" - remove a directory
```
eg: rmdir -p dir/dir1/dir2
```
##### recursively removes a directory
rm -rf directory 

```
eg: rm -rf dir/dir1
```

### Listing files with LS output

#### Decoding ls -l Output

```
-rw-rw-r--. 1 arjun arjun 0 Aug 26 09:14 current
```
```
Permissions                   -rw-rw-r--
Number of links               1
Owner name                    arjun
Group name                    arjun
number of bytes in the file   10400
last modification time        aug 26 09:14
file name                     current
```

##### Listing all files, including Hidden Files
1. Hidden files begin with a period. sometimes called "dot files"
2. Hidden files are not displayed by default
3. To show hidden files with ls, use ls -a
4. Command options can be combined:
   ls -l -a is the same as ls -la and ls -al

##### Listing files by types
Use ls -F to reveal file types.
    /   Directory
    @ Link
    * Executable

##### Symbolic links

* A link is a points to the actual file or directory
* Use the link as if were the file
* A link can be used to create a shortcut
    * use for long file or dirctory names
    * Use to indicate the current version of the software

##### Listing files by time and in reverse
ls -t       List files by time
ls -r       list files in reverse order
ls -latr    long listing including all files reverse sorted by time
ls -R       lists files recursively
ls -d       list directory name, not contents
ls --color  colorize the output

##### The tree command
Similar to ls -R but creates visual output

tree -d List directories only
tree -C colorize output

##### Working with spaces in names
* just say no to spaces!
* Alternatives:
  * Hyphens(-)
  * Underscores(_)
  * CamelCase

* Encapsulate the entire file name in quotes
* Use a backslash(\) to escape spaces

### File and directory permisions expalined part 1

##### Permissions
```
[arjun@localhost Desktop]$ ls -l
total 4
drwxrwxr-x. 2 arjun arjun  6 Aug 27 03:30  1
```
```
Symbol                    Type
------                    ----
-                         Regular file
d                         Directory
l                         Symbolic link
r                         read
w                         write
x                         execute

```

##### Permission categories

```
Symbol    Category
u           User
g           Group
o           Other
a           All
```

Groups

* Every user is in at least one group called primary group
* Users can belong to many groups
* Groups are used to organize users
* The groups command displays a users groups
* you can also use id -Gn


##### Secret Decoder ring
```
[arjun@localhost Desktop]$ ls -l
drwxrwxr-x. 2 arjun arjun  6 Aug 27 03:30  1

```
![images](images/decoderring.jpg?raw=true "Title")

##### Changing permissions

```
item        Meaning
chmod       change mode command 
ugoa        User category user, group, other, all
+-=         Add, subtract, or set permissions
rwx         read,write, execute

```

chmod g+w  - Add write permission to the group
chmod g-w  - remove wrote permission to the group
chmod g+wx - giving write and read permission
chmod a=r  - giving all users read permission

##### Numeric based Permissions

```
 r      w     x
 0      0     0   Value for off
 1      1     1   Binary value for on
 4      2     1   base 10 value for on 
```
##### Permission description
![images](images/binaryDesc.jpg?raw=true "Title")

##### order Has meaning
![images](images/order.jpg?raw=true "Title")

##### Commonly used permissions
![images](images/commonlyUsed.jpg?raw=true "Title")

* 777 or 666 permission allows everone full permission to the directory
* if multiple users need write access, consider using groups and limiting their access to members of the group
* generally it is a good practice to avoid 666 and 777

##### Working with groups
* New files belong to your primary group
* The chggrp command changes the group
```
eg: chgrp sales sales.data
```
##### File creation mask
* File creation mask determines default permissions
* if nomask were used permissions would be:
  * 777 for directories
  * 666 for files

##### The umask command
```
eg: umask [-s] [mode]
```
* Sets the file crea tion mask to mode, if given.
* Use -S to for symbolic notation

##### common umask modes
* 022
* 002
* 077
* 007

![images](images/special_modes.jpg?raw=true "Title")

##### Summary
Permissions are classified in to:
* Symbolic permissions
* Numeric/octal permissions
* Effect of permissions on directory is slightly diffretnt than files inside it
* file permissions can be chnaged ny using chmod and group permissions can be chnaged by sing chgrp command
* 

### Finding files and directories

#### The find command
```
eg: find[path] [expression]
```
Recursively finds files in path that match expression. if no arguments are supplied it find all files in the current directory.

##### Find Options
```
-name pattern  - find files and directories that match pattern.
-iname pattern - like -name, bt ignores case
-ls            - performs an ls on each of the found items
-mtime days    - finds files that are days old.
-size num      - finds file that are of size num
-newer file    - finds files that are of newer than file
-exec command {} \;
Run command against all the files that are found. 
```
```
find                           - find everthing in the working directory
find .                         - find everything in the current directory
find /sbin -name makedev       - find the file/folder named makedev(case sensitive)
find /sbin -iname makedev      - find the file/folder named makedev(case insensitive)
find /bin -name *v             - find file that ends with v
find . -mtime +10 -mtime -13   - find files in which is greater than 10 days and less than 13 days
find -name s* -ls              - find files that starts with s and perform ls on it
find -size +1M                 - find files which is greater than 1 MB
find . -type d -newer file.txt - find files which is newer than file.txt
find . -exec {} \;             - find all files in the current directory and executes the file command(tells which type of file)
file file.txt                  - outputs the type of file
```

##### Locate - a fast locate

locate pattern
--------------
* list files that matrch pettern
* faster than the find command
* queries an index
* results are not in real time
* May not be enabled on all systems
 ```
 locate sales - find the files which matches the pattern. no need to specify the full name
 ```

 find works in real time and locate not. locate is faster than find

 ### Viewing files and the nanao editor

 ##### Displaying contents of files
 cat file     - display contents of file
 more file    - browse through a text file
 less file    - more features than more
 head file    - output the beginning(or top) portion of file
 tail file    - output the ending(or bottom) portion of file.

 * Head and tail displays only 10 lines by default
 * We can chnage this behaviour with -n
    * n = number of lines
    * tail -15 file.txt

    eg:
    ```
    head -5 test.txt - will display top 5 lines of test.txt
    tail -6 test.txt - will display the last 6 lines of test.txt
    tail -f test.txt - follow the file. ie new updations are getting updated in the terminal. eg: log file
    ```

* view files in real time :
  ```
  tail -f file follow the file: displays data as it is being written to the file
  ```
### Text editors
#### Nano editor
* simple editor.not much advanced than vim and emacs

commands
```
ctrl + 0 - save
ctrl + x - exit
```

#### Vi editor
* Has advanced and powerful features
* Not intuitive
* Harder to learn than nano
* requies time investment

```
vi [file]   - edit file
vim [file]  - same as vi, but more features
view[file]  - Starts vim in read-only mode
```
* vi has the concept of modes.
    * command mode
    * insert mode
    * Line mode

```
Vi command Mode and Navigation
k   Up one line
j   Down one line
h   Left one character
i   right one charcter
w   right one word
b   left one word
^   go to the beginning of the line
$   go to the end of the line

```

##### Vi navigation keys
![images](images/vi.jpg?raw=true "Title")

##### Vi Insert mode
```
i   Insert at the cursor position
I   Insert at the beginning of the line
a   Append after the cursor position
A   Appnend at the end of the line
```
##### Vi line mode
```
:w                    writes(saves) the file
:w!                   forces the files to be saved
:q                    Quit
:q!                   Quit without saving changes
:wq!                  write and quit
:x                    same as :wq
:n                    positions the cursor at line n
:$                    positions the cursor on the last line
:set nu               turn on line numbering
:set nonu             turn off line numbering
:help [subcommand]    get help    
```

##### Vi modes
```
Mode        key
command     Esc
insert      i l a A
line        :
```

##### Vi repeating commands
* repeat command by preceding it with a number
    * 5k=Move up a line 5 times
    * 80i<Text> <Esc> = insert<Text>80 times
    * 80i_<Esc>=insert80"_" characters

##### Vi-Deleting text
```
x     delete a character
dw    delete a word
dd    delete a line
D     delete from the current position
```

##### Vi-changing text
```
r   replace the current character
cw  change the current word
cc  change the current line
c$  change the ttext from current position
C   same as c$
~   reversres the case of a character
```


##### Vi-copying and pasting
```
yy            Yank(copy) the current line.
y<position>   Yank the <position>
p             Paste the most recent deleted or yanked text
```
##### Vi Undo/Redo
```
u       undo
ctrl-R  redo
```

##### Vi searching
```
/<pattern>      start a forward search
?<pattern>      start a reverse search
```
### Editing files with Emacs 
 
 ```
 emacs [file] edit file

 C - <char>     Ctrl while pressing <char>
 M(right alt key) - <char>     "Meta" key (alt key) while pressing <char>
 M - <char>     Esc, then type <char>
 ```

 ##### Emacs commands
 ```
 Ctrl-h           Help
 Ctrl-X C-c       exit
 Ctrl-X C-s       save the file
 Ctrl-h t         built-in tutroial
 Ctrl-h k <key>   describe key
```
 ##### Emacs navigation
 ```
 Ctrl-p   previous line
 Ctrl-n   next line
 Ctrl-b   backward one character
 Ctrl-f   forward one character
 Ctrl-f   forward one word
 M-f      forward one word
 M-b      backward one word 
 Ctrl-a   go to the beginnning of the line
 Ctrl-e   go to the end of the line  
 M-<      go to the beginning of the file
 M->      go to the end of the file
 ```

 ##### Emacs - deleting text
 ```
 Ctrl-d    Delete a character
 M-d    Delete a word
 ```

 ##### Emacs - Copying, Pasting, and Undo
 ```
 Ctrl-k    Kill(cut)
 Ctrl-y    Yank(paste)
 Ctrl-x u  Undo 
 ```

 ##### Emacs - Searching
 ```
 Ctrl-S     Start a forward search
 Ctrl-r     Start a reverse search
 ```

 ##### Emacs - Repeating Commands
 ```
 Ctrl-u N <command>  Repeat <command> N times 
 ```

 ### Deleting, copying, moving and renaming files

 ##### Removing files
 ```
 rm file      Remove file
 rm -r dir    remove the directory nad its contents recursively
 rm -f file   force removal and never propmt confirmation
 ```

 ##### Copying files
 ```
cp source_file destination_file         copy source file to destination file
cp src_file1 [src_fileN ...] dest_dir   copy source_files to destination_directory   
```
##### cp Options
```
cp -i                                       - run in interactive mode
cp -r  source_directory destination         - copy src_directory recursively to destination
```

##### Moving and renaming files
```
mv                        move or rename files and directories
mv source destination     move source to destination
mv -i source destination  move source to destination in interactive mode 
```

##### Sort Data
```
sort file     - sort text in file
```

##### Sort options
-k F    Sort by key. F is the filed number
-r      Sort in reverse order
-u      Sort unique

##### creating a collection of files
```
tar [-] c|x|t f tarfile [pattern]   - Create, extract or list contents of a tar archive using pattern, if supplied
```

##### Tar Options
```
C         Create a tar archive
X         extract files from the archive
t         display the table of contents(lists)
V         be verbose
Z         Use compression
f file    Use this file
```

###### Compressing files to save space
```
gzip      - compress files
gunzip    - uncompress files
gzcat     - concatenates compressed files
zcat      - conatenates compressed files
```

##### Disk Usage
```
du        Estimates file usage
du -k     display sizes in kilobytes
du -h     display sizes in human readable format
```

## 02 Intermediate Linux skills

##### Wild cards

* A charcter or string used for pattern matching
* Globbing expands the wildcard pattern into a list of files and/or directories(paths)
* Wildcards can be used with most commands
```
  * ls
  * rm
  * cp
```  
* *- matches zero or more characters
  * *.txt
  * a*
  * a*.txt
* ?- matches excatly one character
  * ?.txt
  * a?
  * a?.txt  

##### More wildcards - Character classes
* [] - A character class
  * Matches any of the characters included between the brackets. Matches exactly one character.
  * [aeiou]
  * ca[nt]*
    * can
    * cat
    * candy
    * catch
* [!] - Matches any of the charcters NOT included between the brackets. Matches exactly one character
  * [!aeiou]*
    * baseball
    * cricket 
##### More wildcards - ranges
* use two charcters seperated by a hypen to create a range in a character class 
* [a-g]*    - Matches all files that start with a, b, c d, e, f, or g.
* [3-6]*    - Matches all files that start with 3,4,5 or 6

##### Named character classes
```
* [[:alpha:]]
* [[:alnum:]]
* [[:digit:]]
* [[:lower:]]
* [[:space:]]
* [[:upper:]]
```     
##### Matching wildcard patterns
* \ - escape charcter. Use if you want to match a wildcard character
  * Match all files that end with a question mark:
    * *\?
      * done?

### I/O redirection
There are three different I/O types:
```
I/O Name              Abbrevation           File Description
standarad input         stdin                     0
standard output         stdout                    1  
standard error          stderr                    2    
```

##### Redirection
```
>         redirects standard output to a file. Overwrites(truncating) existing contents
>>        redirects standard output to a file. appends to any existing contents
<         redirects input from a file to  a command
&         used with redirection to signal that a file descriptor is being used 
2>&1      combine stderr and standard output
2>file    redirect standard error to a file
```

#### The null device
```
>/dev/null  redirect output to nowhere

```
### Comparing files
* Comparing the contents of files
```
diff file1 file2      compare two files
sdiff file1 file2     side-by-side comparison
vimdiff file1 file2   highlight differences in vim
```

* diff output
```
$ diff file1 file2
3c3   - LineNumFile-Action-LineNumFile2
      - Action = (A)dd (C)hange (D)elete
...
```
$ diff file1 file2
3c3
< this is a line in a file.
---
> this is a line in a file!
```
< Line from file1
> Line from file2
```

* sidff Output
```
$ sdiff file1 file2
line in file2 | line in file2
              > more in file2
| differing lines
< line from file1
> line from file2
```

* vimdiff
```
ctrl -w w   go to next window
:q          quit (close current window)
:qa         quit all(close both files)
:qa!        force quit all
```

### Searching in files using pipes
##### The grep command
grep display lines matching a pattern
```
grep pattern file
```
##### grep options
```
-i  performs a search, ignoring case
-c  count the number of occurences in a file
-n  precede output with line numbers
-v  invert match. print lines that don't match 
```
eg:
```
[arjun@localhost Desktop]$ grep o secret          - perform a search for 'o' in secret 
2 site: facebook.com
3 user: jason

[arjun@localhost Desktop]$ grep -v o secret       - Perform a invert search 
1 tags: credentials
4 pass: Abee!

[arjun@localhost Desktop]$ grep User secret       - case sensitive

[arjun@localhost Desktop]$ grep -i User secret    - avoid case sensitivity
3 user: jason

[arjun@localhost Desktop]$ grep -ci User secret   - count the number of occurances
1

[arjun@localhost Desktop]$ grep -ni User secret   - will show the line number
3:3 user: jason
[arjun@localhost Desktop]$ cat secret
1 tags: credentials
2 site: facebook.com
3 user: jason
4 pass: Abee!
5 tags: credentials
new last line
[arjun@localhost Desktop]$ 
```
##### The file command
```
file file_name    : display the file type
```
eg:
```
$file sales.data
sales.data: ASCII text
$file *
bin: directory
jason.tar: POSIX tar arhive

```
##### Searching for text in binary files
```
strings       : Display printable strings
```

##### Pipes
```
| Pipe symbol

command-output | command0input
```
```
grep pattern file 

is same as 

cat file | grep pattern
```

##### The cut command
```
cut[file]     : Cutout seletced portions of file. if file is ommited, use standard input
```
##### Cut options
```
-d delimiter      Use delimeter as the field seperator
-f N              display the Nth field
```

##### Searching and pipe examples
* Find all users named "arjun" in /etc/passwd
* Print account name and real name
* Print in alphabetical order by account name
* Print in tabular format
```
[arjun@localhost Desktop]$ grep arjun /etc/passwd | cut -d: -f1,5 | sort | tr ":" " " | column -t
arjun:Arjun,,,,

```
This command will serach for arjun in /etc/passwd and cut the filed f1 and field 5, sort it and replace the colon with space and display the whole result as column

##### Piping out to  a pager
* more
* less

### copying files over the network
```
SCP   - Secure copy
SFTP  - SSH file transfer protocol
```
* Command line SCP Clients
```
* scp
* sftp
* PuTTY Secure Copy client-pscp.exe
* PuTTY Secure file transfer client-psftp.exe
```
* graphcal SCP/SFTP Clients
```
* Cyberduck
* FileZilla
* WinSCP
```
* scp/sftp command line utilities
```
scp source destination  : copy source to destination
sftp host               : start a secure file transfer session with host        
```
* ftp command line utility
```
ftp host    : start a file transfer session with host
Note than ftp is not a secure mechanism for tranfering files. because it will send the credentials as plain text and not encrypted
```
* sftp eg:
```
sftp servername
sftp> pwd   - will print the working directory of the remote machine
lpwd        - will print the local working directory
put z.text  - will copy z.text to the remote machine
rm z.text   - will remove z.text from remote
sftp adminuser@linuxsvr

```
* scp eg:
```
scp z.txt servername:/tmp/   - we need to prove the remote location
scp z.txt servername:~       - copy z.txt to the home directory  
scp z.txt adminuser@linuxsvr:/home/adminuser - copy file as a adminuser
```

### Customizing the shell Prompt
* Customizing the prompt with PS1
```
\d    Date in ""Weekday month date" format "Tue may 26"
\h    Host name up to the first perriod
\H    Hostname
\n    NewLine
\t    Current time in 24-hour HH:MM:SS format
\T    Current time in 12-hour HH:MM:SS format
\@    Current time in 12-hour am/pm format
\A    Current time in 24-hour HH:MM format
\u    Username of the current user
\w    Current working directory
\W    Basename of the current working directory
\$    if the effective UID is 0, a #, otherwise a $
```
### Shell aliases
* they are shortcuts
* use for long commands
* use for commands you type often
syntax:
```
alias [name[=value]]

* List or create aliases
* user name = value to create a new alias
```
* eg:
```
[arjun@localhost ~]$ alias ll='ls -l'
```
* Fix typos
```
$ alias grpe= 'grep'
```
* Make linux behave like another OS
```
$ alias cls = 'clear'
```
* Remove Alias
```
unalias name : Remove the 'name' alias.
unalias -a   : Remove all aliases
```
##### Persisiting aliases 
* Add aliases to our perrsonal initialization files
  * .bash_profile

### Processes and Job control
syntax:
```
ps    : Display process status
```
##### ps Options
```
-e              : everything, all processes
-f              : full format listing
-u username     : display username's processes
-p pid          : display information for PID
```
##### Common ps commands
```
ps -e             display all process
ps -ef            display all processes, full
ps -eH            display a process tree
ps -e --forest    display a process tree
ps -U username    display users processes
```
##### other ways to view processes
```
pstree      display processes ina tree format
top         interactive process viewer
htop        interactive process viewer
```

##### Background and foreground process
```
command &     Start command in background
ctrl - C      kill the foregriund process
ctrl - Z      suspend the foreground process
bg [%num]     background suspended process
fg [%num]      foreground a background process
kill          kill aprocess by job number or PID
jobs [%num]   list jobs
```

##### Killing Processes
```
ctrl-c            kills the background proc
kill [-sig] pid   send a signal to a process
kill -l           display a list of signals
kill 123      
kill -15 123
kill -TERM 123 kill -9 123
```

### Scheduling repeated jobs with cron
* Cron - A time based jon scheduling service
* crontab - A program to create, read , update, and delete your job schedules
* use cron to schedule and automate tasks

##### using Crontab command
```
crontab file    install a new crontab from file
crontab -l      list your cron jobs
crontab -e      edit your cron jobs
crontab -r      remove all of your cron jobs
```

### Switching users and running commands as others
```
The su command
su [username]     : Change user ID or become superuser
-                 : an hyphen is used to provide an enviorment similar to what the user would expect had     the user logged correctly
-c command        :specify a command to be executed
```

##### Sudo
```
sudo -l               : list available commands
sudo command          : run command as root
sudo -u root command  : same as above
sudo -u user command  : run as user
sudo su               : switch to the superuser account
sudo su -             : switch to the superuser account with root's enviornment
sudo su - username    : switch to the username account   
sudo -S               : start a shell
sudo -u root -S       : same as sudo -S
sudo -u user -S       : start a shell as user 
```
##### Changing the sudo configuration
```
visudo          : edit the /etc/sudoers file
``` 
## 02 Linux Boot Process