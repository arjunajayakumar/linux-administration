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