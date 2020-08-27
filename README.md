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

![images](image/shell.png?raw=true "Title")


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

Permissions
----------- 
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

Permission categories
---------------------
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


Secret Decoder ring
-------------------
```
[arjun@localhost Desktop]$ ls -l
drwxrwxr-x. 2 arjun arjun  6 Aug 27 03:30  1

```
![images](images/decoderring.jpg?raw=true "Title")

Changing permissions
--------------------
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