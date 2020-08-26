# linux-administration

## Linux directory structure

![alt text](images/directory structure.png)

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

![alt text](images/shell.png)

~  - represents home directory

![alt text](images/telda.png)

### Basic Linux commands
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
### Getting help at command line

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

### Working with directories

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
find /sbin -iname makedev      -  find the file/folder named makedev(case insensitive)
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