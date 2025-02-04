[Pure Bash Bible](https://github.com/dylanaraps/pure-bash-bible/tree/master)

# linux-commands-to-learn

## Terminal
- A shell is a program that takes commands from the user and gives them to the os kernel to execute it.
- Linux is case senitive.
- `sudo apt update && sudo apt install vim` => To install an application.

### Getting help

#### Using less

##### Shortcuts in less
- `h` => getting help
- `q` => quit
- `enter` => show next line
- `space` => show next screen
- `g / G` => go to first / last line- `g / G` => go to first / last line
- `/string` => search forwards for stirng
  - `n / N` => next / previous appeearance
- `?string` => search backwards for string
  - `n / N` => next / previous appeearance

#### Man pages
- `man command` => Example: `man ls`
- `man` uses `less` to show the manual.

##### Searching for a command, feature or keyword in all man pages
- `man -k uname`
- `man -k "copy files"`
- `apropos passwd`

#### checking if a command is a shell built-in or an executable file
- `type rm` => rm is /usr/bin/rm
- `type cd` => cd is a shell builtin

##### To get help for builtins
- `help command` or `command --help`

### Keyboard Shortcuts
- `Ctrl + Alt + T` => Open a new terminal
- `TAB` => automcompletes the command or the filename if it is unique
- `TAB TAB` (press twice) => displaying all commands or filenames that start with the written letters
- `Ctrl + L` => To clear the terminal (similar to `clear`)
- `Ctrl + D` => To close the bash shell (similar to `exit`)
- `Ctrl + C` => To interrupt the process running in the current terminal
- `Ctrl + Z` => To sleep the currently running program
- `Ctrl + A` => Moves the cursor to the beginning of the line
- `Ctrl + E` => Moves the cursor to the end og the line
- `Ctrl + U` => Cuts all characters before the cursor

### Bash History
- Arrow keys help to navigate the history.
- The history is stored in `~/.bash_history`
- The number of commands stored in the history file is controlled by `$HISTFILESIZE`
- The number of commands displayed by `history` is controlled by `$HISTSIZE`
- The `~/.bash_history` file is updated when the used is logging out.
- `history` => To display the history
- `!number` => To run a history command by its history line number
- `!-number` => To run the numberth command (count strats from the last command)
- `!!` => To rerun the last command
- `!string` => To rerun the latest string command from the history (Eg: `!ping`)
  - This can be dangerous, becous you dont see the executed command before execution
- `!string:p` => To print the lastest string command from the history (Eg: `!ping:p`)
- `Ctrl + R` and then start typing => To reverse recall (search) a command from the bash history
  - `enter` => To run the found command
  - `Ctrl + G` => To leave history searching mode
- `history -d number` => To delete a command from the history with the specified line number
- `history -c` => To clear the history

#### To record time information in the history
- `echo 'HISTTIMEFORMAT="%d/%m/%y %T"' >> ~/.bashrc`

### Getting root access (sudo, su)
- On linux there are 2 main categories of users:
  1. **non-privileged users** have no special rights on the system
  2. The **root user** (superuser or the administrator)

- **Root privileges** are the powers that the root account has on the system. The root account is the most privileged on the system and has absolute power over it
- Root exists on any Linux system is there's only one
- It's not recommended to use root for ordinary tasks
- `id` => To print the current logged in user
- `sudo su` + enter password => To become root temporarily in the terminal until logout (`exit`)
- `sudo su -` => As above, but also executes all login scripts and puts you in the roots home directory.
- `sudo command` => To run the command as a superuser (this is the recommended way)
- `su` + enter root password => To become the root user in the terminal
  - on some distributions this method is disabled by default

- If a user does not have a password, we can not login with it.
- `sudo passwd username` => To set or change the users password
- `passwd` => To change your own password

## Linux File System

- On a Linux system, everything is considered to be a file (including physical devices and directories)
- On Linux file and directory names are case-sensitive
- The type of a file in linux is determined by a code in the file header,it does not depend on the file name extension
- File extensions only used by GUI applications

### File types in Linux
- the first character of the `ls -l` helps to specify the file type:
  - `-` => regular file
  - `d` => directory
  - `l` => symbolic link
  - `b` => block device (represents a physical hardware device)
  - `c` => character device (represents a physical hardware device)
  - `s` => socket (used by processes to communicate, not by TCP/IP)
  - `p` => a named pipe (also used by processes to communicate)

- `ls -F` also halps to specify the file types by adding a symbol to the end of the filenames:
  - `` => regular, non executeable file
  - `/` => directory
  - `*` => executeable file
  - `@` => Symbolic link
  - `=` => Socket
  - `|` => A named pipe

- `file filename` => Printing the detailed type of the specified file
- `file *` => Printing the detailed type for all files in the current directory

### Common directories
- `/bin` contains binaries or user executable files which are available to all users
- `/sbin` conatins applications that only the superuser will need
- `/boot` conatins files required for starting the system
- `/home` is where the non root users' home directories are placed
- `/dev` conatins device files for every hardware device attached to the system
- `/etc` contains most, if not all system wide configuration files (users, passwords, groups, network config, etc)
- `/lib` contains shared library files used by different applications (the package manager uses it)
- `/media` external storages mounted automatically here
- `/mnt` is like `/media`, but not used these days (mount point for cd roms and floppy disks)
- `/tmp` contains temporary files, usually saved by running applications
  - please consider that, files maybe deleted from here at any time without prior notice
- `/proc` is a virtual directory that contains information about the computer hardware (CPU, RAM, etc)
- `/sys` contains information about devices, drivers and some kernel features
- `/srv` contains data for servers
- `/run` is a temporary file system which runs in RAM, used only by processes, different distros use it in different ways
- `/usr` was the initial place for user home directories
  - nowadays it contains shared things betwwen useres like `/usr/bin` or `/usr/sbin`
- `/var` contains variable length files such as logs (`/var/log`)


### Linux Paths
- **absolute** paths start from the root
- **relative** paths start from the current directory

- `.` => represents the current working directory
- `..` => represents the parent directory
- `~` => represents the current user's home directory

- `cd` => changes the current directory to the current user's home directory
- `cd ~` => the same as above
- `cd -` => changes the current directory to the latest one
- `cd /path_to_dir` => changes the current directory to `/path_to_dir`
- `pwd` => prints the current working directory

- `sudo apt update && sudo apt install tree` => installs tree
- `tree /directory` => lists recurively the contents of `/directory`
- `tree -d .` => prints recurively *only the directories* contaioned by the current directory
- `tree -f .` => lists recurively the contents with *absolute paths* of the current directory

### The ls command

- `ls` / `ls .` => lists the current directory
- `ls /path_to_dir` => lists the path_to_dir directory
- `ls -l` => detailed listing, shorts by name
- `ls -a` => listing including hidden files
- `ls -ld /path_to_dir` => does not list the contents of the directory, but prints informations about the directory
- `ls -lh` => displays sizes in human readable format
- `ls -lS` => sorts by size (for directies displays the size of the inode structure, not the actual directory size)
- `sudo du -sh` => same as above, but it prints the real size of the directories
- `df -h` => To print the actual disk space usages, free space etc. of available file systems

- `ls -lX` => shorts by extension
- `ls --hide=*.log` => excludes all log files from the listing
- `ls -lR` => lisiting all directores recursively
- `ls -li` => listing the inode number

- `ls -lt` => shorting by modification time, newest first
- `ls -ltu` => shorting by access time, newest first
- `ls -lu` => showing access time, but sorts by name
- `ls -lr` => adding `-r` to any listing, reverses the display order

### File Timestamps
- In Linux the time is stored as an integer value and represents the number of seconds since 1970.01.01. 0:00 UTC

- Every file in Linux has three timestamps:
  1. The **access timestamp** or **atime** is the las time the file was read (`ls -lu`)
  2. The **modified timestamp** or **mtime** is the last time the contents of the file was modified (`ls -l`, `ls -lt`)
  3. The **changed timestamp** or **ctime** is the last time when some metadata related to the file was changed (`ls -lc`)

- `stat filename` => prints statistics about the specified file, including the timestamps above

- `ls -l --full-time /etc` => displays the full timestamp
- `touch filename` => creating an empty file is not exsists, update (all) timestamps if the file exsists
- `touch -a filename` => changing only the access time (and changed time due to metadata change) to the current time
- `touch -m filename` => changing the modification time (and changed time due to metadata change) to the current time
- `touch -m -t 201812301530.45 filename` => changing the modification time to a specific date and time (and changed time to the current date time due to metadata change)
- `touch -d "2010-10-31 15:45:30" filename` => changing both atime and mtime to a specific date and time (and changed time to the current date time due to metadata change)
- `touch a.txt -r b.txt` => changing the timestams of a.txt to the same as b.txt (reference file)

- `date` => displaying the current local date and time
- `date -u` => displaying the current UTC date and time
- `date --set="2 OCT 2020 18:00:00"` => setting the date and time of the system

- `cal` => showing this months calendar
- `cal 2025` => showing calendar for a specific year
- `cal 7 2025` => showing calendar to a specific month of a year
- `cal -3` => showing the calendar of previous, current and next month

### Viewing Files(cat, less, more, head, tail, watch)

#### cat

- `cat filename` => displaying the contents of a file (useful for small files)
- `cat filename1 filename2` => displaying more files (concatenating their contents)
- `cat filename1 filename2 > filename3` => displaying more files (concatenating their content into filename3)

- `cat -n filename` => displaying the files with line numbers

#### less
- `less filename` => displaying the contents of a file (useful for larger files)
- Shortcuts:
  - `h` => getting help
  - `q` => quit
  - `enter` => show next line
  - `space` => show next screen
  - `g / G` => go to first / last line- `g / G` => go to first / last line
  - `/string` => search forwards for stirng
    - `n / N` => next / previous appeearance
  - `?string` => search backwards for string
    - `n / N` => next / previous appeearance

#### tail
- useful for watching log files
- `tail filename` => showing the last 10 lines of a file
- `tail -n number filename` => showing the last number of lines of a file
- `tail -n +20 filemane` => showing the last lines of a file, starting from line number 20
- `tail -f filename` => showing the last 10 lines of a file, with live refresh if the file changes
  - `Ctrl + C` => exit from watch mode and returns the prompt

#### head
- `head filename` => showing the first 10 lines of a file
- `head -n 15 filename` => showing the first 15 lines of a file

#### watch
- `watch -n 3 ls -l` => running repeatedly a command in every 3 seconds
- `watch -n 3 -d ls -l` => running repeatedly a command in every 3 seconds with highlighting the differences
  - `Ctrl + C` => to interrupt it

### Working with files and directories (touch, mkdir, cp, mv, rm, shred)

#### touch
- `touch filename` => creating a new file or updateing the timestamps if the file already exsists

#### mkdir
- `mkdir dirname` => creating a new directory
- `mkdir dirname1 dirname2` => creating several directories
- `mkdir -p mydir1/mydir2/mydir3` => creating a directory and its parents as well
  - without `-p` it returns an error if `mydir1` or `mydir1/mydir2` does not exsist

#### cp

- `cp file1 file2` => copying `file1` to `file2` in the current directory
  - if `file2` does not exsists then creates it, otherwise overwrites it
- `cp file1 dir1/file2` => copying `file1` to `dir1/file2`
- `cp -i file1 file2` => copying `file1` to `file2` int the current directory, but prompts the user (y/n) in case of an overwrite
- `cp -p file1 file2` => copying `file1` to `file2` int the current directory, and preserving the file permissions, group and ownership (otherwise the new files will be owned by the user perfomring the copy operation)

- `cp -v file1 file2` => copying `file1` to `file2` int the current directory, but beeing verbose
- `cp -r dir1/* dir2/` => recursive copy the contents of dir1 into dir2
- `cp -r dir1 dir2/` => recursive copy the dir1 directory itself into dir2
  - if the source is a directory, we must use `-r`
- `cp -r file1 file2 dir1 dir2 destination_directory/` => copying more source files and directories to a destination directory

#### mv
- `mv file1 file2` => renaming file1 to file2 (also works with directies)
- `mv file1 dir1/` => moving file1 to dir1
- `mv -i file1 dir1/` => moving file1 to dir1, with prompting (y/n) in case of being overwritten
- `mv -n file1 dir1/` => moving file1 to dir1, with preventing an existing target file beeing overwritten
- `mv -u file1 dir1/` => moving file1 to dir1, only if the target file is not exisit or the source file is newer (really useful with shell scripts)
- `mv file1 dir1/file2` => moving file1 into dir1 as file2
- `mv file1 file2 dir1/ dir2/ destination_directory/` => moving more source files and directories (the directory will be moved) to a destination directory

#### rm
- it is not possible to undo rm
- `rm file1` => removing a file
- `rm -i file1` => removing a file with confirmation
- `rm -v file1` => being verbose when removing a file
- `rm -r dir1/` => removing a directory
- `rm dir1/*` => removing the contents of a directory
  - when using wildcards with `rm` it is extremly important to check with `echo` the correctness of the expression
    - `echo dir1/*`
- `rm -rf dir1/` => removing a directory without promting
- `rm -ri fil1 dir1/` => removing a file and a directory prompting the user for confirmation

#### shred
- `shred -vu -n 100 file1` => secure removal of a file (verbose with 100 rounds of random contents overwriting, so it isnt possible to restore it from the disk anymore)

### Piping and Command Redirections

- Every Linux command or program we run has three data streams connected to it:
  1. **STDIN (0)** - Standard Input - The data that the program is working with
  2. **STDOUT (1)** - Standard Output - Data printedby the program
  3. **STDERR (2)** - Standard Error - For errors from the application

- Using the *pipe symbol* `|` we can connect two or more commands at a time:


`command1 | command2 | command3 ...`

#### Piping Examples

- `ls -lSh /etc/ | head` => listing the first 10 files by size
- `ps -ef | grep sshd` => checking if sshd is running
- `ps aux -sort=-%mem | head -n 3` => listing the top first 3 process by memory consumption

#### Redirection

- `ls -l > list.txt` => redirecting the output of ls into list.txt (with being overwrite if list.txt already exsisted)
- `ls -l >> list.txt` => appending the output of ls into the end of list.txt
- `tail -n 10 /var/log/*.log > output.txt 2> errors.txt` => redirecting both output and error
- `tail -n 2 /etc/passwd /etc/shadow > output_errors.txt 2>&1` => redirecting both the output and errors to the same file
  - `2>&1` redirecting stderr (2) to stdout (1)
- `cat -n /var/log/auth.log | grep -ai "authentication failure" > auth.txt ` => piping and redirection

#### tee

- `ifconfig | grep ether` => printing to the terminal
- `ifconfig | grep ether > mac.txt` => redirecting to file

- what if we want both print to console and save to file at the same time? `tee`
- `ifconfig | grep ether | tee mac.txt` => printing to the terminal and redirecting to file (with overwrite by default)
- `ifconfig | grep ether | tee -a mac.txt` => printing to the terminal and redirecting to file, with appending option
- `ifconfig | grep ether | tee -a mac.txt mac2.txt` => printing to the terminal and redirecting to multiple files, with appending option

### Finding Files

#### which

- `which command` => locating the command in the PATH and returns its absolute path (returns only the first match)
- `which -a command` => same as above, but returning all matches
  - Eg: `which -a find`
- `which command1 command2 command3` => same as above but locating all the given commands

#### locate (plocate)
- `plocate` is faster than `find`, because it does not find in the file system in real time
- `plocate` uses a prebuilt database
  - the database should be updated regularly (by a cron job or manually): `sudo updatedb`
- `find` command has more options
- `sudo apt update && sudo apt install plocate` => installing plocate, the new implementation of locate

- `plocate string` => searching for string in every absolut path, returns a list of absolute paths that contains the searched string.
  - It is important to note that, it searches for matches in the path, so for example if the search matches a directory, then the result list will contain every file in that directory

- `plocate -b name_of_file` => searching for a specific filename (basename), returns a list of files which has a name that contains the searched string
- `plocate -r regex` => searching for exact matches with the given regular expression
  - Eg `plocate -r '/passwd$'`
- `plocate -e string` => checking for existance (really checks the file, not uses the database)
- `plocate -i string` => case insensitive search

#### find
- searches for files in a directory and recursively in its subdirectories
- `find PATH OPTIONS`
- Eg `find ~ -type f -size +1M` => findingall files in ~ bigger than 1 MB
- Options:
  - `-type f | d | l | s | p` => file | directory
  - `-name filename`
    - `find . -name todo.txt`, looks for exact name matching
    - `find . -name "todo*"` => wildcards works aswell
  - `-iname filename` => case insensitive, looks for exact name matching
  - `-size n | +n | -n` => exact | greater than | smaler than (possible to use this option many times in one find)
  - `-perm permission` => Eg `-perm 755`
  - `-links n | +n | -n`
  - `-atime n | -mtime n | -ctime n`
    - Eg `find /var -type f -mtime 0 -ls` => files that has been modified during the last 24 hours
      - `-mtime` option uses days as an int value
    - Eg `find /var -type f -mtime 1 -ls` => files that has been modified between 1 and 2 days ago
    - Eg `find /var -type f -atime +1 -ls` => files that has been last accessed more than 1 day ago
  - `-amin n | -mmin n | -cmin n` => same as above, but uses minutes instead of days
    - `find =var -type f -mmin -60` => files in /var that has been modified in the last hour
  - `-user owner` => files that belongs a user
  - `-group group_owner`
  - `-delete` => deleting the founc files, this is **very danger**
  - `-ls` => executing `ls -l` for all found files
  - `-maxdepth number` => searches maximum number levels deep in the specified directory
  - `-inum number` => searching based on inode number
  - `-links number` => searching based on the number of links
  - `-not` => use in front of any option to negate it
    - Eg `find /etc -type f - not -group root -ls` => files that do not belong to root group
  - `-exec command` => executing a command for all found files
    - Eg `find /etc -type f -mitme 0 -exec cat {} \;` => the contents of the files that has been modified during the last day
      - `{}` the found file names will be substituted here
      - ` \;` ends the command to execute
    - Eg `sudo mkdir /root/backup && sudo find /etc -type f -mtime -7 -exec cp {} /root/backup \;` => copy all configuration files that has been modified during the last seven days

#### Searching for text patterns (grep)

- `grep` searches for a pattern referenced to as a regular expression and print out all lines that matches the given pattern
- `grep [options] pattern file`
- Its input can be a file or the output of another command
- Eg `grep user /etc/ssh/ssh_config`
- `grep "command line" /etc/ssh/ssh_config` => if the pattern contains whitespaces enclose it with quotes
- Options:
  - `-n` => print line number
  - `-i` => case insensitive
  - `-v` => inverse match
  - `-w` => search for whole words
  - `-a` => search in binary files
  - `-R` => search in a directory recursively
  - `-c` => display only the number of matches
  - `-C n` => display a centext (n lines before and after the match)

  - `-s` => suppress error messages about nonexisting or unreadable files

#### Comparing Files

- `cmp file1 file2` => comparing two files byte by byte and returns the location of the first mismatch
  - if the two files are identical nothing is returned
  - works with binary files aswell
- another way to compare binary files is to calculate and compare their hashes
  - `sha256sum file1 file2` => if the hashes are the same, the files are the same
- `diff file1 file2` => displaying the difference between file1 and file2 line by line
  - works only for text files, compares line by line
- `diff -B file1 file2` => ignoring blank lines
- `diff -w file1 file2` => ignoring white spaces
- `diff -i file1 file2` => ignoring case differences
- `diff -c file1 file2` => printing a more detailed comparison
- `diff -y file1 file2` => printing a really detailed two columns output with the files contents indicating the differences

### vim
- basic text editor
- `sudo apt update && sudo apt install vim`
- `vimtutor` => opening a vim tutorial where you can practice
- `vim filename` => opening a file in vim to edit
  - if the file exsist opens it, otherwise creates it and opens it
- `vim file1 file2` => Opening more files
  - `:n` => jump to next file
  - `:p` => jump to prev file
- `vim -o file1 file2` => Opening more files in stacked windows
  - `Ctrl + w` => move between windows
- `vim -d file1 file2` => opening more files and highlighting the differences
  - `Ctrl + w` => move between files
- `:wq` => exit from vim
- VIM has 3 modes:
  - command (when we open a file, we are here)
  - insert
  - last line
- VIM Config File: `~/.vimrc`
  - Last Line Mode commands (separated by newline) from this file will be executed when we open vim
- Entering the **Insert Mode** from the **Command Mode:**
  - `i` => insert before the cursor
  - `I` => insert at the beginning of the line
  - `a` => insert after the cursor
  - `A` => insert at the end of the line
  - `o` => insert on the next line
  - `O` => insert on the previous line

- Entering the **Last Line Mode** from the **Command Mode:**
  - `:`

- Returning to **Command Mode** from any other mode:
  - `ESC`

- Shortcuts in **Last Line Mode**:
  - `w!` => write/save the file
  - `q!` => quit the file without saving
  - `wq!` => save/write and quit
  - `e!` => undo to the last saved version of the file
  - `n` => move to line number n (Eg `10`)
  - `set nu` => set line numbers (does not permanent)
  - `set nonu` => unset line numbers (does not permanent)
  - `syntax on|off` => syntax highlighting on/off (does not permanent)
  - `%s/search_string/replace_string/g` => replaceing all occurance of `search_string` to `replace_string`
    - Eg `%s/no/XXX/g` => replaceing all occurance of `no` to `XXX`
  - `!bash_command` - executing a bash command while running vim
    - Eg `!ls`

- Shortcuts in **Command Mode**:
  - `x` => remove char under the cursor
  - `dd` => cut the current line
  - `5dd` => cut 5 lines
  - `ZZ` => save and quit
  - `u` => undo the last modification
  - `Ctrl + r` => redo the previous operation
  - `G` => move to the end of the file
  - `gg` => move to the beginning of the file
  - `$` => move to the end of the line
  - `v` => select a character to copy
    - move the cursor horizontally to select multiple characters
  - `Shift + v` => select the current line(s) to copy
    - move the cursor vertically to select more lines
  - `Ctrl + v` => select the rectangular box to copy
  - `y` => yank/copy to clipboard
  - `p` => paste after the cursor
  - `P` => paste before the cursor
  - `/string` => search for string forwards
  - `?string` => search for string backwards
  - `n` => next occurance
  - `N` => previous occurance
  - `*` => searches the next occurance of the word that the cursor is on
  - `#` => searches the previous occurance of the word that the cursor is on

### Compressing and Archiving files (tar)
- `tar -c` => creating an archive
  - Eg `tar -czvf etc.tar.gz /etc/`
    - `-v` => verbose
    - `-z` => compress the archive (using gzip or gnuzip)
    - `-j` => compress the archive with bzip2 algorithm
      - slower than gnuzip, but creates smaller output
      - in this case it is common to use .tar.bzip2 extension
    - `-f` => allows to specify the name of the archive (it is mandatory to specify the file name after this option)
  - Eg `tar -czvf archive.tar.gz file1 file2 dir1/` => creating archive from multiple files
  - Eg `tar --exlude='*.mkv' --exclude='.config' -czvf myhome.tar.gz ~` => how to exclude files from the archive
- `tar -x` => extracting an archive
  - Eg `tar -xzvf etc.tar.gz` => extracting the archive in to the current directory
  - Eg `tar -xzvf etc.tar.gz -C my_backup/` => extracting the archive into my_backup/ directory
  - if we dont specify the algorithom (`z` or `j`) tar will auto detect it
- `tar -t` => display the content of an archive
  - Eg `tar -tf etc.tar.bz2 | grep sshd_config` => checking whether sshd_config is in the tar

- `sudo tar -cjvf etc-$(date +%F).tar.bz2 /etc/` => how to **inject archivation date** into the archive's name

### Hard Links and Inode structure
- Each file on the disk has a data structure called **index node** or **inode** associated with it.
- This structure stores metadata information about the file such as the type, file's permissions, file's owner and group owner, timestamp information, file size and so on. (ls -l lists some of these informations)
- **It actually contains all file information except the file contents and the name.**
- Directories stores the filename inode number pairs. (And this is considered a hardlink)
- Each inode is uniquely identified by an integer called inode number (ls -i)

- A **Hard Link** is an association between a file structure (inode) and a file name
  - It is possible to have more associations (names) to the same file structure (inode)
  - `ls -l` (after the permissions) or `stat` shows the number of hard links to a file
  - `ln existing_name new_name` => creating a new hardlink to `existing_name` with the name of `new_name`
    - they both will have the same inode number
  - If we change the data through a hard link, the other hard links to the same data will also see the change
  - If we remove a hard link, the name entry will be deleted and the hard link count will decrease
    - If we remove the last hard link, then the inode and the file with the data itself will be deleted
  - If we move the pointed file, the hard links will still work
  - `find . -inum number` => finding hard links based on inode number
  - `find /usr/ -type f -links +1` => searching all files in /usr/ that has more than one hardlink
  - **Can't create** a hardlink on a **directory** or to a file on a **different partition** or **disk**

#### Symlinks
- symlinks are similar to shortcuts in windows
- symlink is a special file type (so they have their own inode structure) that contains a reference to another file or directory
- So Hardlinks reference a file's inode and symlinks reference another files (or directories).
- If we delete the file that the symlink references, the symlink will be broken
- If we move the refenrenced file, the sym links will be broken
- `ln -s existing_name new_name` => creating a new symlink to `existing_name` with the name of `new_name`
- `ls -l` denotes symlinks with a `->` and also displays the file it points to
- symlinks can cross the filesystem (hardlinks can't!)
- the permissions of a symlinkdoesnotmatter because the permissions of the target file will be checked

## User Account Management

### Important files:
- `/etc/passwd` => basic information about all user account in the system: username:x:uid:gid:comment:home_directory:login_shell
  - every user can read it
- `/etc/shadow` => users's passwords in an encrypted format ($type$salt$hash), expiration related data, etc
  - only the root can read it
  - for more info `man shadow`
  - with using a random salt value, the same passwords will generate a different hash
- `/etc/group` => groups
- `/etc/login.defs` => conatins the default options for new users

### Groups (groups, id)
- The main purpose of groups is to define a set of permissions for a given file that can be sharedamong the users within the same group
- There are two types of groups that a user canbelong to:
  1. **primary (or login) group:** the group id is stored in `/etc/passwd` and the groupname in `/etc/group`
    - this group is assigned to the files that are created by the user
    - `ls -l` => after the hardlink count: owner and the groupowner is specified
    - each user must belong to exactly one primary group
    - in `/etc/group` the primary group can be found using the gid (group id) from `/etc/passwd`
  2. **secondary groups:** stored in `/etc/group`
    - a user can be a member of none or multiple secondary groups
    - in `/etc/group` the secondary groupscan be found using the username (as the last field of a line)
      - if more users belong to the same group, they are separated by a comma

- `groups` => listing of all groups that the current user belongs to (the first is the primary one)
- `groups username` => same as above, but for the specified user
- `id` => printing information about the current user and its groups
- `id username` => same as above, but for the specified user

- `sudo groupadd group1` => create a new group called group1

### Creating User Accounts (useradd)
- `sudo useradd username` => creating a new user (and its primary group with the same name)
  - `sudo passwd username` => set a password for the user, so we can login with it
  - `sudo passwd -e 2025-01-10 username` => specifying an expiration date for the password (for temporary users)
- `sudo useradd -m username`* => creating a new user (and its primary group with the same name) + create a `/home/username` home directory for the user
- `sudo useradd -m -d /home/james username`* => creating a new user (and its primary group with the same name) + create a `/home/james` home directory for the user
- `sudo useradd -c "C++ Developer" username`* => creating a new user (and its primary group with the same name) + with a comment field in `/etc/passwd`
- `sudo useradd -s "/bin/bash" username`* => creating a new user (and its primary group with the same name) + with a default shell field in `/etc/passwd`
  - `/bin/false` => (for users to run only one service and nothing more) logging in to the shell wont work (logs out)
  - `/usr/sbin/nologin` => (for users to run only one service and nothing more) logging in to the shell wont work (throws an error)
- `sudo useradd -G sudo,adm,mail username`* => creating a new user (and its primary group with the same name) + with the secondary groups of sudo, adm, mail
- * common option to use when we create a new user

- `sudo chage -l username` => showing aging information for a user account

- `adduser` => user frendly version of `useradd`, but its not on every distribution

### Changing and Removing User Accounts (usermod, userdel)

- `usermod`
  - has exactly the same options as useradd, but modifies the user instead of creating it
  - Eg `sudo usermod -c "Golang developer" james` => Modify the comment of the user
  - Eg `sudo usermod -g daemon james` => modify the primary groupof the user
  - Eg `sudo usermod -G group1,group2 james` => add a new secondary groups to the user
    - **all previous secondary groups are deleted for the user**
  - Eg `sudo usermod -aG group1,group2 james` => remain the users previous secondary groups and add the new ones

- `userdel` => to delete user account withh its all associated files
  - also deletes the group with the same name if no other user is a member of it
  - Eg `sudo userdel u1` => delete u1 user (but its home directory is still there)
  - `sudo userdel -r u1` => delete the user, also delete its home directory and its mail spool
  - the files owned by the user outside its home directory will still remain

- `man deluser` => a friendlier command to delete users

### Creating an admin user
- by default, only the user created during linux installation can sudo commands
- the needed group to be able to sudo is called `sudo` on debian and `wheel` on redhat

1. `sudo useradd -m -s /bin/bash username` => create the user
2. `sudo passwd username` => create its password
3. `su username` => test the user
4. `sudo cat /etc/shadow` => we got an error, because we cant sudo
5. `exit` => logout
6. `sudo usermod -aG sudo username` => add the user to the sudo group
  - if the group does not exsist, we can create it and it will work
7. `su username` => test the user
8. `sudo cat /etc/shadow` => success!!!!
9. `exit` => logout

### Group management (groupass, groupdel, groupmod)
- `sudo groupadd groupname` => creating a new group
- `sudo groupmod -n new_name old_name` => changing the name of a group
- `sudo groupdel groupname` => deleting a group
  - it is not possible to remove the primary group of a user without first removing the user

### User Account monitoring (whoami, who, id, w, uptime, last)

- **RUID** (real user id) is the id of the user who initially logs in
- **EUID** (effective user id) is the id of the current user in the shell

- `whoami` => the user that has the id of EUID
  - `id -un` => same as above
- `who` => the currewntly logged in RUID users
- `id` => prints the EUID user and its groups
- `who -H` => all logged in RUID users with column headings
- `who -aH` => all logged in RUID users, with more information
- `w` => who are logged in and what is their current process
  - `uptime` => shows the uptime part of `w`
- `last` => shows the list of the last logged in/out users
- `last username` => shows the list of the last logins for username

## Linux File Permissions
- File permissions (file modes) specify who can access, change or execute a fileon a Linux System
- It ensures that only authorized users and processes can access files and directories
- Each file or directory has an owner and a group. By default, the owner is the user who creates the file and the group is the primary group of the user
- The ownership of a file or a directory can be changed only by root using the `chown` and `chgrp` commands
- For each file the permissions are assigned to three different categories:
  1. the file owner
  2. the group owner
  3. others (anyone else or the whole world)
- There are three file permission types that apply to each category:
  - the read permission (r - 4)
  - the write permission (w - 2)
  - the execute oermission (x - 1)
- to view file permissions:
  - `ls -l`
  - `stat`
- The number that represents the permission is base-8, can be a 3 or 4 digit number with digits from 0 to 7. The leading zero (0) can be omitted.
- 0755 = 755 and 0644 = 644
- When a 3 digit number is used, the forst digit represents the permissions of the file's owner, the second one the file's group, and the last one the permission of the others class,
- The permission number of a specific user class is represented by the sum of the values of the permissions for the groups

### Changing file permissions
- `chmod` is the command used to change the permissions ofthe file or a directory using either the symbolic or the numeric notation
- only the root or the file's owner can change the file's permissions

- `chmod [who][OPERATION][permissions] filename`
  - **who** signifies the user category whose permissions will be changed
    - `u`: the **user** that owns the file
    - `g`: the **group** that the file belongs to
    - `o`: the **other** users
    - `a`: all three of the above

  - the **OPERATION** flag define whether the permissions are to be removed, added or set:
    - `-` means to remove the specified permissions
    - `+` means to add the specified permissions
    - `=` means to change the current permisisons to the specified permissions
  - the **permissions** are specified using letters: `r`, `w` and `x`
- Eg `chmod u-x,g+w,o+x filename`
- Eg `chmod ug-r, o-rwx filename`
- Eg `chmod a+r filename` => add read to all
- Eg `chmod ug=rw, o= filename` => rw-rw----, `=` is to specify exact rwx values
  - if there are no permissions specified after the `=`, then --- will set

- `chmod 644 filename` => absolute changing mode (used to set the permission for all user classes)
- `chmod -R 750 dirname` => to set the permissions recursivelly for all files (and directories) inside dirname
  - this may not be the best idea, because directories and files will have the same permissions
  - Eg a directory with `rw-` permisions would be unuseable
- `chmod --reference=reference_filename filename` => set permissions based on a reference file

### Permissions of directories
- Permissions on directories has a completely different effect than on files
- `r` on a directory only means that the directory's contents can be shown by running ls
  - it does not give you access to the contents of the directory
  - imagine as a glass box - you can see inside it, but can't touch it
- `w` has no effect if the `x` is not set
- `wx` together means the directory's contents can be modified:
  - create new files or subdirectories allowed
  - rename or delete existing files or directories allowed
- `x` means access to that directory's contents
  - `cd` into it is allowed
  - create or remove files (or directories) is allowed
- **if we have the `x` permision for a directory and there is a file inside it with `000` permissions, we still can delete it**

### Set permissions recursively for files and directories separately
- set the permissions int the home directory for all files to 640 (rw-r-----) and for all directies to 750 (rwxr-x---)
- `find ~ -type f -exec chmod 640 {} \;` => set the permissions for files
- `find ~ -type d -exec chmod 750 {} \;` => set the permissions for directories

Typical values:
  - the typical default permission for new files is **644** `rw-r--r--`
  - for sensitive files use **600** `rw-------`
  - for standard directories or cli apps use **755** `rwxr-xr-x`
  - for private directories or cli apps use **700** `rwx------`


### Changing file ownership (chown, chgrp)
- In Linux all files are assiciated with an owner and a group owner
- The `chown` and `chgrp` commands are used to change the files owner and group
- **Only root can change the file owner**
- Normal users can change the group for files that they own, and only for groups that they are a member of
- root can change the group ownership for all files
- `ls -l filename` => to see the owner and group owner of a file (or directory)
- Eg `sudo chown username filename` => setting the owner to username for filename
- Eg `sudo chown username file1 file2 file3` => setting the owner for multiple files
- Eg `sudo chown username:groupname filename` => it is possible to set the owner and the group owner at the same time
- Eg `sudo chown -R username:groupname directory` => set the owner and group owner for all files and directories recursively within the specified directory
- Eg `chgrp group_name filename`

### Special Permissions - SUID (Set User ID)
- Besides `r`, `w` and `x` for the owner, group and others there are 3 extra special permissions for each file or directory: `SUID` or **Set User ID**, `SGID` or **Set Group ID** and **Sticky Bit**
- These special permissions are for a file or directory overall, not just for a user category
- By default Linux commands and programs run with the same exact permissions of the user who executes them
  - Eg the cat command runs with the privileges of its runner, so you can see only those files contents that you have the permisison for
- **When an executable file with SUID is executed then the resulting process will have the permissions of the owner of the command, not the permissions of the user who executes the command**


- Setting SUID:
  - Absolute Mode: `sudo chmod 4XXX file`
  - Relative Mode: `sudo chmod u+s file`
  - `ls -l /usr/bin/passwd` => -rw**s**r-xr-x
  - `stat /usr/bin/passwd` => 4755
  - In case of -rw**S**r-xr-x (capital S) there is not execute permission is set to the file
- It is useful for example to be able to set passwords for non privileged users
  - So `passwd` always run in the name of root, so it can modify the file that stores the passwords (`/etc/shadow`)
- There are a lot of linux commands that use the SUID bit to give the command elevated privileges when runned by a regular user
  - `find /usr/bin -perm -4000` => `-4000` means all files that has at least these permissions
- **For security reasons it is necesarry to ensure that insecure programs with the SUID bit set are not installed on the system**

### Special Permissions - SGID (Set Group ID)
- **SGID** is set mainly to directories
- If you set SGID on directories, all files or directories created inside that directory will be owned by the same group owner of the directory where SGID was configured
- This is useful in creating shared directories, which are directories that are writeable at the group levels

- Setting SGID:
  - Absolute Mode: `chmod 2XXX directory`
  - Relative Mode: `chmod g+s directory`
  - `ls -ld directory` => drwxrw**s**---
    - In case of a **S** there is no execute permission is applied to the directory

### Special Permissions - The Sticky Bit
- By default if a user has permissions on a directory, he can remove all the files in that directory, even though the files permissions would not allow it
- The **Sticky Bit** is applied to directories
- A user may only delete files that he owns or for which he has explicit write permission granted, even when he has write access to the directory
- The sticky bit allows you to create a directory that everyone can use as a shared file storage. The files are protected because no one can delete anyone ele's files
- It is useful for directories that are designed to be world writeable (`/tmp` or `/var/tmp`), but it may not be desirable to allow any user to delete files at will
- Setting the sticky bit:
  - Absolute Mode: `chmod 1XXX directory`
  - Relative Mode: `chmod o+t directory`
  - `ls -ld directory` => drwxrwxrw**t**
    - **T** means the lack of execute permission on the directory

### Umask
- `usmask` allows you to view ir set the base or the default permissions given when a new file is created in Linux
- `umask` => listing the current usmak value
- `umask 0022` => setting the umask value **for the current session for the current user**
  - for permanent umask value, put it inside the user's `.bashrc`

- It is considered that the default cration permissions are `0666` for files and `0777` for directories
- When we create a new file or directory the umask value is subtracted from the default creatin permissions
  - Eg In case of a 0022 umask value, a new directiry will has 0777-0022=0755 permissions
  - Eg In case of a 0022 umask value, a new file will has 0666-0022=0644 permissions

### Understanding File Attributes (lsattr, chattr)
- The attributes define the properties of the files
- Each file attribute can have one of teh two states:
  - `set` => the corresponding letter
    - `e` => indicates that the file is using extents for mapping the blocks on disk
    - `a` => the file is append only
    - `A` => no access time updates when the file is modified
    - `i` => immutable aka cannot be modified, renamed or deleted, permission cannot be modofoed, also we can not create a hardlink to reference it
  - `cleared` => `-`
- `ls -l` does not list the file attributes
- `lsattr` => to list the attributes of the files and directories within the current directory
- `sudo chattr +a filename` => the file become append only (not even root is an exception to this rule)
- `sudo chattr -a filename` => the file is not append only anymore
- `sudo chattr -R +i dirname` => set recursively every file immutable in the directory

## Processes
- Tasks are a synonym for processes
- A running instance of a program is called a **process** and it runs in its own memory space. Each time you execute a command, a new process strats
- A process is an active entity as opposed to a program, which is considered to be a passive entry
- A new process is created only when running an executeable file (not when running Shell builtin commands)
- In Linux, all the proceses in the operating system are created when anoteher process executes `fork()` system call
  - there is an exception, which is the first process, that starts when the system is booting
    - that is called init or systemd and has the process id of 1
- The process that used the for system call is the **parent process** and the created process is its **child**
- When a process terminates its execution the operating system releases most of the resources and information releted to that process
- Process properties:
  - *PID (Process ID)* - a unique positive integer number
  - *User*
  - *Group*
  - *Priority* / *Nice*
- Type of Processes:
  - *Parent*
  - *Child*
  - *Daemon* => is a process that runs in the background and are not interactive; have no controlling terminal
    - their name usually ends with **d**
  - *Zombie (defunct)* => a terminated process whose data has not been collected
    - Normally zombie processes removed quickly from the memory
  - *Orphan* => when a parent process terminates before its child process
    - Eg we close the terminal while still running some processes in it
      - There processes get the **hangup signal** and gets terminated

- **Threads** can coexist within the same process and they share resources such as memory within the process
  - Subprocesses that run in the same memory context of a single process and make the application responsive

### Listing Processes (ps, pgrep, pstree)
- Any user can see information about the running processes
- `ps` => displaying the processes running in the current terminal
  - **PID** is the process id
  - **TTY** is the name of the controlling terminal
  - **TIME** is the cumulative CPU time of the process shown in minutes and seconds
  - **CMD** is the name of the command that was used to start the process
- `ps -e` => all processes that are running
- `ps -f` => (detailed) full status information
- `ps -ef` => display all processes with detailed informations
  - **UID** is the user that is running the process
  - **PID** is the process id
  - **PPID** is the parent process id
  - **C**
  - **STIME** is the starting time of the process
  - **TTY** is the name of the controlling terminal
    - `?` means that the process is not attached to any terminal (probably a system service or daemon)
  - **TIME** is the cumulative CPU time of the process shown in minutes and seconds
  - **CMD** is the name of the command that was used to start the process
- `ps -aux` => display all processes with more detailed informations
  - **%CPU** is the cpu utilization of the process expressed as a percentage
  - **%MEM** is how much memory the process is using expressed as a percentage
  - **VSZ** is the virtual memory size of the process in kb
    - epresents the total amount of memory that a process can access. This includes swapped-out memory, allocated but unused memory, and memory from shared libraries.
  - **RSS** is the size of the psysical memory that the process is using
    - it indicated how much memory is allocated to each process
    - does not include swapped out memory, but includes memory from shared libraries as long as they are in the memory
    - include all stack and heap memory
  - **STAT** indicates the state of the process using a code
    - `S` for sleeping
    - `R` for running
    - `Z` for zombie
    - `T` for stopped
    - `I` for idle kernel thread
    - `<` indicated high priority
    - `N` indicated low priority
- `ps -aux --sort=%mem` => sorting the output by memory usage (ASC)
- `ps -aux --sort=-%mem` => sorting the output by memory usage (DESC)
- `ps -aux -u username` => listing the processes for a specific user
- `ps -ef | grep processname` => checking whether a process is running
- `pgrep preocessname` => short form checking whether a process is running, returns the process id
- `pgrep -l preocessname` => same as above, but also returns the process name
- `pgrep -l -u username preocessname` => same as above, but only list matches that are owned by the specified user
- `pstree` => displaying a hierarchical tree structure of all running processes

### Dynamic Real-Time View of Processes (top)
- `top` => starting top
- `top` shortcuts while running:
  - `h` for getting help
  - `space` for manual refresh
  - `d` for setting refresh delay in seconds
  - `q` for quitting top
  - `u` for displaying processes for the user
  - `m` for changing the display for the memory
  - `t` for changing the CPU displays to simple ASCII graphs
  - `1` for individual statistics for each CPU
  - `x` for highlighting the sorting column
  - `y` for highlighting the running process in the column list
  - `b` for toggling between bold and text highlighting
  - `<` for moving the sorting column to the left
  - `>` for moving the sorting column to the rights
  - `B` for sortig by memory
  - `P` for sorting by processor
  - `R` for reversing the sort order
  - `e` for changing the resource measure (b/kb/mb/gb)
  - `F` for entering the Field Management screen
  - `W` for saving top settings
  - use up and down arrows to navigate

- **load average** for the past 1, 5 and 15 minutes
  - for a healthy system these values shoul be less than 1

- Eg `top -d 1 -n 3 -b > top_processes.txt` => running top in batch mode (3 refreshes, 1 second delay)
- Eg `sudo apt update && sudo apt install htop` => Interactive process viewer (top alternative)
- `htop`

### Signals and Killing processes (kill, pkill, killall, pidof)
- **!!Extremly powerful commands, potential misuse can bring servers down!!**

- A **signal** is an asynchronous notification sent to a process that determines how the process should behave when it is delivered
- The process can decide to ignore some signals
- Non priviledged users can send signals only to their own processes
- root can send signals to anyone
- `Ctrl + c` == **SIGINT (2)** == INTERRUPT
- **SIGHUP (1)** => used to reload a process
- **SIGKILL (9)** => used to immediate kill a process (hard kill)
  - if a process ignores the TERM signal, we can try to send **SIGKILL (9)** signal to it
- `kill` => sends a signal to a proces or to a group of processes, causing them to act according to that signal
  - the default signal is **SIGTERM (15)** (soft kill)
- `kill -l` => listing all possible signals
- `kill -2 PID` => sending an interrupt signal to the process with the specified PID

- `pidof firefox` => Prints all pids of processes related to firefox
- `kill -INT PID1 PID2 PID3` => Sending interrupt sugnal to the given processes
- `kill -SIGINT $(pidof firefox)` => same as above but in one step
- `sudo kill -1 $(pidof sshd)` => sending HUP (restart) signal to the ssh daemon
- `killall -15 process_name` => sending SIGTERM to all processes with a particular name
  - does not accept partial name, you hava to specify exact process_names
- `pkill process_name` => same as `killall` but also works with partial process names

### Foreground and Background processes (nohup)
- **Foreground processes** are started by the user, and while they are running the user can not start another process from the same terminal
- **Background processes** are non-interactive and are started or executed by the system services or by the users
  - while they are running, we can start other processes within the same terminal
  - to start a background process, add an `&` to the end of the command
    - Eg `sleep 20 &` => starting sleep as a background process
  - a background process' output is redirected to the same terminal where it was started
  - it is common to redirect the output of a background process to a file
    - Eg `ifconfig > output.txt 2> errors.txt &`
    - Eg `ifconfig > /dev/null 2>&1 &` => we are not interested in its output or errors
  - when we start a background process, a [job id] and a PID is printed
  - if we press `enter` again and the process is already finished successfully `[job id] Done` will be printed
  - the job id is local to the current shell (besause the jobs are maintained by the current shell session) and the pid is local to the system kernel
  - if we close (or logout or disconnect) terminal of a foreground or a background process, then the process will terminate
  - `nohup command &` => to start a background process that wont terminate if we close its terminal
    - when the terminal is closed, the init (or systemd) process will inherit the nohuppped processes
    - the outoput will be redirected to the `nohup.out` file
### Job Control (jobs, fg, bg)
- `jobs` => displaying the started background processes (jobs) with their job id and with their status
- `jobs -l` => same as above, but prints the PID aswell
- `fg %jobid` => bringing a background running process to the foreground
- `Ctrl + Z` => suspending the execution of a foreground process
  - prints the [job id] status and the process name
  - `bg %jobid`=> resuming a suspended foregorund process in the background
  - `fg %jobid` => resuming a suspended foregorund process in the foreground

## Networking

### Getting information about the Network Interfaces (ip, ifconfig, route)
- `sudo apt update && sudo apt install net-tools` => to install ifconfig and route
- `ifconfig -a` => display a list of all network interfaces (both enabled and disabled) and the associated IP addresses
- `ip address show` or `ip a` => same as above
- `ip -4 address` => to list only IPv4 IP addresses
- `ip -6 address` => to list only IPv6 IP addresses
- `ifconfig` => display a list of all enabled network interfaces and the associated IP addresses

- `ifconfig enp0s3` => displaying info about a specific interface
- `ip addr show dev enp0s3` => same as above

- `route` => listing the default gateway
  - `G` flag in the `Flags` column indicates the default gateway
- `route -n` => display the names in numberis format
- `resolvectl status` => listing the current DNS SErver

### Configuring the Network on the fly (ifconfig, ip, route)
- `sudo ifconfig interdace_name down` => disabling an interface
  - Eg `ifconfig enp0s3 down`
- `sudo ip link set interdace_name down` => same as above
- `sudo ifconfig interdace_name up` => enabling a disabled an interface
- `sudo ip link set interdace_name up` => same as above
- `sudo ifconfig interface_name ip_address/network_mask up` => configuring a new ip address for an interface (after system restart, this setting will be lost; for permanent configuration use netplan)
- with `ip` the same as above is a two step process:
  - `sudo ip address del exisiting_ip_address/network_mask dev interface_name` => deleting the existing ip address
  - `sudo ip address add new_ip_address/network_mask dev interface_name` => adding the new ip address
- Changing the default gateway
  - If there is a default gateway already configured, then first we have to remove it
    - `sudo route del default gw ip_address`
    - `sudo ip route del default` => same as above
  - `sudo route add default gw new_ip_address`
  - `sudo ip route add default via new_ip_address` => same as above
- Changing the MAC address of an interface
  1. `sudo ifconfig interface_name down` => disabling the interface
  2. `sudo ifconfig interface_name hw ether new_mac_address` => configuring the new MAC address
  3. `sudo ifcondig interface_name up` => enabling the interface
- Changing the MAC address of an interface with the `ip` command
  1. `sudo ip link ser dev interface_name address new_mac_address`

### Setting Up Static IP on Ubuntu (netplan)
- Typically laptops and desktops have their ip assigned dynamically by a DHCP server which is in most cases a router
- A sevrerrequires a static configuration to avoid the single point of failure of using a DHCP server
- Configured in yaml files in the `/etc/netplan` directory
  - [Netplan examples](https://github.com/canonical/netplan/tree/main/examples)
 - Steps:
   1. Stop the NetworkManager:
     - `sudo systemctl stop NetworkManager`
  2. Disable the NetworkManager:
     - `sudo systemctl disable NetworkManager` => disable it, so it wont start after a system restart
  3. Check NetworkManager's status:
    - `sudo systemctl status NetworkManager` => should be `Avtive: inactive (dead)`
  4. Check whether is will restart after reboot:
    - `sudo systemctl is-enabled NetworkManager` => should be: `disabled`
  5. Create a yaml file in `/etc/netplan`
    - If there is a yaml (always use 2 spaces to indent) file already, remove it first
    - `sudo vim /etc/netplan/01-netconfig.yaml`
``` yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: false
      addresses:
        - 192.168.0.20/24
      gatway4: "192.168.0.1"
      nameservers:
        addresses:
          - "8.8.8.8"
          - "8.8.4.4"
```
  6. Apply the changes:
    - `sudo netplan apply`
  7. Verify the changes:
    - `ifconfig`
    - `route -n`

### Testing and Troubleshooting Network Connectivity

- `ping [options] destination_ip_address` => sending ICMP echo request packets to the specified destination IP and waits for a reply
  - Eg `ping ubuntu.com`
- Options:
  - `-n` => without reverse DNS lookup
  - `-c number` => specifying the number of sent packets
  - `-i number` => repeat frequency time, Eg `ping -i 0.4 -c 5 google.com` => sending 5 requests with the frequency of 0.4 second to google.com
    - only the superuser can set smaller than 0.2 second interval
  - `-q` => displaying only a summary
- Guidelines:
  - if `icmp_seq` is out of order, there may be some routing problems
  - the time less then 30 ms is excellent
  - the time between 30 ms and 50 ms is average but still ok
  - the time between 50 ms and 100 ms is somehow slow response
  - the time greater than 100 ms is slow response (running real time applications such as voice or video over ip may be problematic)

- **Troubleshooting connectivity issues**
  1. Ping the default gateway of the LAN
    1. `route -n`
    2. `ping ip_address`
      - If the ping is not working, we have a problem in out own lan
        - maybe we are not authenticated to the wireless access point
        - maybe we dont have the correct ip address set
        - maybe the router is not correctly configured
  2. Ping a public IP address on the internet (Eg public dns server of google: 8.8.8.8; or from coudflare: 1.1.1.1)
    - `ping 8.8.8.8`
      - If it does not work, there is an internet connecticity issue
        - check whether the router is properly configured
        - complain at the ISP
  3. Ping a stable internet domain (Eg google.com)
    - `ping google.com`
      - if its not working, we have a dns issue
        - check whetherwe are using the correct dns server and there is nothing that is filtering the packets
      - maybechange the dns server to 8.8.8.8 and check again

###  SSH (Secure Shell)
- The **SSH** protocol is used for:
  - Secure Remote Management of Servers, Routers, other Networking Devices
  - Network File Copy: `rsync`, `scp`, `sftp`, `winscp`
  - Tuneling, SSH Port Forwarding
- **sshd** is the server (daemon) and `ssh` or `putty` is the clinet

- Installation:
  - Ubuntu: `sudo apt update && sudo apt install openssh-server openssh-clinet`
  - CentOS: `sudo dnf install openssh-server openssh-client`
  - Checking its status: `sudo systemctl status ssh`

- Service Stop | Restart | Start: `sudo systemctl start | restart | stop ssh`
- Check whether it is enable to start at boot time: `sudo systemctl is-enabled ssh`
- Enable | Disable auto booting: `sudo systemctl enable | disable ssh`

- Server config file: `/etc/ssh/sshd_config`
- Client config: `/etc/ssh/ssh_config`

- `ssh username@server_address` => connecting from a client using ssh
  - `exit` or `Ctrl + D` => disconnecting
  - Options
    - `-p number` => Specifying the port

### Troubleshooting SSH
- If cannot connect to the SSH server
  1. Check whether the SSH daemon is running on the server
    - `sudo systemctl status ssh`
  2. Try to restart or start the daemon
- If getting `WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!`
  - Youhave to double check, whether you are connecting to the right server
  - Maybe the server's IP or MAC address has been changed
    - if yes, remove the server key from the known hosts file manually (`~/.ssh/known_hosts`)
- Check whether the port 22 is open on the server
  - `telnet ip_address port` (from client)
- Check whether there is a firewall on the server that is dropping the packets
  - `sudo iptables  -vnL` (from server)
- Try to run the SSH client in verbose mode with the `-v` option
  - It is possible to add multiple verbose options to increase verbositbility. Eg `-vv` or `-vvv`
- Check the server logs
  - `sudo tail -f /var/logs/auth.slog`

### Securing the OpenSSH Server (sshd)
- The default installaton of SSH is not secure
- The server config file is located at: `/etc/ssh/sshd_config` (you have to edit it manually and restart the server to apply the changes)
  - it is recommendend to backup it before modifying it
  - for the config options check `man sshd_config`
- Recommendations for securing the server:
  1. Use a non-standard port for the server (dont forget to allow it through the firewall)
  2. Disable direct root login
    - `PermitRootLogin no`
  3. Disable password authentication entirely if possible (and enable public key authentication)
    - If not possible,use strong passwords
       - lengthat least 10 characters
       - containing letters, digits and special characters
       - do not use dictionary words orcombination ofsuch words (nomatter the language)
  4. Limit users SSH access (by default all users can login remotely)
    - `AllowUsers` with a list of allowed users separated by a space
      - Filter ssh access at the firewall level. Only accept connctions to the ssh port only from the ip addresses of the allowed user's computers
      - Maybe permit the entire network if the source IP changes or is dynamic
  5. Use SSH version 2
  6. Configure an idle timeout interval.
    - The interval in seconds after which if no data has been reveived from the client, the ssh daemon will request a responsefrom the client. The idle user will be logged out.
    - `ClientAliveInterval 300`
    - `ClientAliveCountMax 0`
  6. Set the maximum number of authentication attempts permitted per connection
    - `MaxAuthTries`
  7. Specifies the maximum number of concurrent unauthanticated connections to the SSH daemon
    - `MaxStartups`
  8. The server disconnects after a specified time if the user has not successfully logged in
    - `LoginGraceTime`
  9. Always use the latest version of OpenSSH

### Copying Files over the Network (scp)
- **Be cautious, because scp can overwrite existing files without any warning**
- `sftp` is a more complex option with more features, but also runs slower
- the `:` symbol means remote
- `scp` => secure file copy over a network (require ssh access)
  - `ssh usename@server` => checking ssh access
- Copy a file from local to remote:
  - `scp -P 22 filename username@serverip:~`
  - `scp -P 22 filename username@serverip:~/new_filename` => same as above, but with a new filename
- Copy a directory from local to remote:
  - `scp -r -P 22 dirname/ username@serverip:~`
  - `scp -rp -P 22 dirname/ username@serverip:~` => same as above, plus preservers the mod and access time
- Copy a file from remote to local:
  - `scp username@serverop:/filepath local_filepath`
- Copy a directory from remote to local:
  - `scp -r username@serverop:/dir_path local_dirpath/`
- Copy a file from remote to remote:
  - `scp user_source@source_ip:source_path target_user@target_ip:target_path`

### Synchronizing Files and Directories using `rsync`
- useful for backups
- `rsync -av source_dir target_dir`
  - `-a` => archive mode:
    - copy directories recursively
    - preserve symlinks
    - preserve owner and group
  - `-v` => verbose mode aka prints everything it does
  - `-q` => quiet mode aka the opposite of verbose
  - Eg `rsync -av /etc/ ~/atc-backup` => copying `etc` directry into `~/atc-backup`
  - Eg `rsync -av /etc ~/atc-backup` => copying the contents of `etc` directry into `~/atc-backup`
- if we run it multiple times, it will only copy the files that has been changed since last run (so it is more efficient than `cp`)
- if we want `rsync` to remove a removed file from the target, we have to use the `--delete` option
- To exclude files and directories use the `--exclude-from` option
  - `echo "movie.mkv" > exclude_files.txt`
  - Eg `rsync -av --exclude-files='./exclude_files.txt' my_project/ backup/`
  - Eg `rsync -av --exclude='*.png' my_project/ backup/`
    - It is possible to specify `--exclude` multiple times

### Using `rsync` over the Network
- ssh access is necesary
  - Eg `sudo rsync -av -e ssh /etc/ student@192.168.0.20:~/etc-backup/` => from local to remote
  - Eg `sudo rsync -av -e 'ssh -p 22' /etc/ student@192.168.0.20:~/etc-backup/` => specifying port
  - Eg `sudo rsync -av -e ssh student@192.168.0.20:~/my_project/ .` => from remote to local

### using `wget`
- For downloading files from HTTP, HTTPS and FTP servers
  - Eg `wget http://example.com/movie.mpg`
  - Eg `wget -P dir_path/ http://example.com/movie.mpg` => download into a specified directory
  - Eg `wget --limit-rate=100k http://example.com/movie.mpg` => limiting bandwidth to 100KB/s
  - Eg `wget -c http://example.com/movie.mpg` => resuming an interrupted download
  - Eg `wget -b http://example.com/movie.mpg` => putting the download in the background
    - To check the progress: `tail -f wget-log`
    - To cancel the download: `pkill wget`
  - Eg `wget --miror --convert-links --adjuct-extension --page-requisites --no-parent https://example.com` => to mirror a website locally
    - `--miror` => makes the download recursive
    - `--convert-links` => convert links into relative paths
    - `--adjust-extension` => add suitable extensions to the file names
    - `--page-requisites` => also download things like CSS style sheets and images to properly display the page offline
    - `--no-parent` => not to ascend to the parent directory as well (useful to restrict the download only to part of the site)
    - `wget -mkEpnp https://example.com` => sortened version of the above

### Checking for Listening Ports (netstat, ss, lsof, telnet, nmap)
- `sudo netstat -tupan` => listing all open ports
- `sudo netstat -tupan | grep :22` => checking whether port 22 is opened
- `sudo ss -tupan` => same as above
- `sudo lsof` => listing all open files by any process
- `sudo lsof -u username` => listing all open files by processes of a specific user
- `sudo lsof -u ^username` => listing all open files by processes of not a specific user (`^` is negation)
- `sudo lsof -c nginx` => listing all open files by a specific processes (nginx in this case)
- `sudo lsof -iTCP -sTCP:LISTEN`=> listing all files that have opened TCP ports in the listen state
- `sudo lsof -iTCP -sTCP:LISTEN -nP`=> same as above + see both ports and hostnames in numberic format
- `sudo lsof -iTCP:22 -sTCP:LISTEN -nP` => listing which file has opened port 22
- `telnet ip_address port` => checking whether a specific port is open on a remote machine
- **!!!SCAN ONLY YOUR OWN HOSTS AND NETWORKS!!!**
- `nmap` => professional remote port scanner
  - `sudo apt install nmap`
  - `sudo nmap ip_address` => scanning the most used ports and displaying a summary
  - `sudo nmap ip_address -sV` => same as above + version

## Software Management
### DPKG (Debian and Ubuntu Based Distros)
- Eg: Debian, Mint, MX, Kali
- `deb` is the installation package format
- `dpkg` is a low lever package management tool
  - the `dpkg` database contains the list of the installed software on the current system
  - does not know about repositories and does not solve dependencies (like apt)
  - `dpkg --info installer.deb` => displaying information about the installer
  - `sudo dpkg -i installer.deb` => running the installer
  - `dpkg --get-selections` => listing all installed packages om the system
  - `dpkg-query -l` => same as above + package version, architecture and the short description
    - Eg `dpkg-query -l | grep chrome` => same as above filtered to chrome
  - `dpkg -L package_name` => listing all files installed from a package
    - Eg `dpkg -L google-chrome-stable` => `google-chrome-stable` is from the output of `dpkg-query -l | grep chrome`
  - `dpkg -S /bin/ls` => listing what package a specific file belongs to (Eg in case a file got corrupted and we want ot reinstall the package)
    - `/bin/ls` is from the output of `which -a ls`
  - `sudo dpkg -r package_name` => uninstall an installed package (config files will remain)
    - Eg `sudo dpkg -r google-chrome-stable`
  - `sudo dpkg -P package_name` => uninstall an installed package and remove the config files

### `Apt` - Advanced Package Tool
- `apt` is the recommended way to deal with packages on a debian based system
- In the newest versions of Ubuntu the `apt-get` and `apt-cache` tools were meged into a single command called `apt`
- Unline `dpkg`, `apt` does not understand `.deb` files. It works with packages that are doewnlloaded from repositories and calls `dpkg` directly after downloading the `.deb` archives
- An **APT repository** is a web server which containes a collection of packages with metadata that is readable by the `apt` tool
- A special kind of repository is hosted on servers like Lauchpad are **PPAs** (Personal Package Archives) that are packages maintained by not official *Ubuntu* developers
- `apt` uses an index or a local database that holds records of available packages from the repositories enabled in the system
- `sudo apt update` => updating the local package index (aka pulling the latest changes from the apt repos)
  - It is recommended to always run this before installing or updating packages
  - Note that this command does not install or update any software on the computer
- `sudo apt install package_name` => installing a package
  - Eg `sudo apt install apache2`
- `sudo apt install package_name1 package_name2 package_name3` => installing multiple packages
- `sudo apt install full_path_to_a_local_deb_file` => installing from a local deb file (full path needed)
- `sudo apt list --upgradable` => getting the list of upgradable packages
- `sudo apt install package_name_to_upgrade` => if the package is already installed, `install` will upgrade it to the latest version
- `sudo apt full-upgrade` => upgrading the whole system in one step
- `sudo apt full-upgrade -y` => same as above, but automatically says yes to all questions during the process (useful in scripts)
- `sudo apt remove package_name_to_remove` => removing the specified package
  - this may leave some configuration files behind
- `sudo apt purge package_name_to_remove` => removing the specified package including all configuration files
- `sudo apt autoremove` => removing all unused dependencies (`remove` and `purge` don't remove package dependencies)
- `sudo apt clean` => removing the saved deb files from the cache directory (`var/cache/apt/archives`)
  - removes every deb file from that directory
- `sudo apt list` => listing all available packages (there are tens of thousands)
- `sudo apt list | grep package_name` => checking whether a specific package is available
- `sudo apt search "phrase"` => finding packages whose decription contains a word or a phrase
  - Eg `sudo apt search "transparent proxy"`
- `sudo apt list --installed` => getting the list of all installed packages
- `sudo apt show package_name` => getting information about a package, including its dependencies, download size, description
- `synaptic` => a GUI based package manager

### Compiling Programs from Source Code vs Package Manager
- Source Compilation Pros:
  - You can compile applications with certain options which may be missing or disabled in the standard distribution package
  - Access to the latest version of an application
  - It's possible to have multiple versions of the same program installed
- Source Compilation Cons:
  - The package manager will be completely unaware of the changes you have made. It wont be possible to update or remove the application using the package manager
  - If you are not careful when compiling to install the program in a separate location you can break the system
  - It is not the easiest job
  - It is not possible to use `systemctl` with them
    - to start them we have to run the binary manually (to strat a server: `sudo ./binary &`)
    - to stop them we have to kill their process

### Compiling C Programs
0. Read the documentation or readme in the source directory!
1. Install the prerequisites: gcc (gnu c compiler), g++ (gnu c++ compiler), make
  - Ubuntu: `sudo apt update && sudo apt install build-essential`
  - CentOS: `sudo dnf group install "Development Tools"`
2. Download the source files from the official website
  - `wget -c tarball_url`
3. Check the inegrity of the tarball (hash or digital signature)
4. Extract the archive and move into the resulting directory
  - `tar -xzvf tarball_path`
5. Run: `./configure --help` and set the required compilation options
  - Never procead until the `./configure` script runs without any errors
  - Never run it with sudo
  - For programs that are manually compiled and not controlled by the package manager it is recommended to install into a new directory inside `/opt/` directory
    - When we have to remove the application, we need only to remove its directory inside `/opt/`
  - always use the `--prefix` option to never overwrite a program with the same name
6. Run: `make` => compiling (need a `Makefile`)
  - In case of any errors try to solve it, run `make clean` and `make` again
7. Run: `sudo make install` => creates the directory where the bunar will be installed and copies the binaries into it
8. At this point it is appropriate to remove the downloaded source files

## System Administration
### Task Automation and Scheduling Using Cron (crontab)
- `cron` runs as a daemon and is used to automate repetitive tasks like:
  - backups
  - monitoring disk space usage
  - updateing the system with the lastest application versions
  - sending emails
- Cron jobs are intended for servers or machines that are running continously
- If the system is down when the cron job is sceduled to run, the task is lost (wont start when the machine starts)
- **Crontab** has three meanings:
  - the text file that contains the user's cron jobs is called the user's **crontab**
    - on ubuntu: `/var/spool/cron/crontabs/`
  - the name of the commad that is used to manage the crontab files
  - there is a configuration file for the system wide cron jobs called **crontab**
    - located in `/etc/`
- there aretwo types of cron jobs:
  - system wide crontabs are run by the root.
    - To use them you have to move your sripts into the corresponding directory:
      - `/etc/cron.daily/`
      - `/etc/cron.hourly/`
      - `/etc/cron.monthly/`
      - `/etc/cron.weekly/`
  - individual user has a crontab file, which sort for cron table, where all cron jobs of that user are specified

- `crontab -l` => displaying the contents of the current user's crontab file
- `crontab -e` => editing the current user's crontab file
- format: minute hour(in 24 hours time format 0-23) day_of_month month day_of_week(integer between 0-7, where 0 == 7 == sunday) command
  - `*` triggers every possible value
- the minimum time unit used in cron is minute
- **Always use an absolute path of the command to execute, because cron has its own path variable that may differ from the current user's**
- root can set some restrictions regards to which users have access to their crontab files:
  - `/etc/cron.allow` and `/etc/cron.deny` (for more info check `man crontab`)
- [Online crontab helper tool1: Crontab Guru](https://crontab.guru)
- [Online crontab helper tool2: Crontab Generator](https://crontab-generator.org)
- Examples:
  - `0 6 * * * /root/backup.sh` => running a backup script every day at 6am
  - `0 6 * * 0 /root/backup.sh` => running a backup script every sunday at 6am
  - `* * * * * /root/check_space.sh` => monitoring free disk space every minute
  - `0 4,6,10 * * * /root/task.sh` => running a task at 4, 6 and 10 am (comma separated list)
  - `0 9-17 * * 1-5 /root/task.sh` => running a task on weekdays between 9 and 5 pm once per hour (using a range of values)
  - `*/3 * * * * /root/task.sh` => running a task in every 3 minutes (with `/` values repeated over a ceratin interval)
  - `10 4,21 */3 * * /root/task.sh` => running a task every 3 days at 4:10 and at 21:10
  - `@yearly /root/task.sh` => Yearly will run the specified command once a year on the 1st of january at midnight
  - `@monthly /root/task.sh` => Monthly runs the specified script once a month on the first day of the month at midnight
  - `@weekly /root/task.sh` => Weekly runs the specified script once a week on Sunday at midnight
  - `@daily /root/task.sh` => Daily runs the specified script once a day at midnight
  - `@hourly /root/task.sh` => Hourly runs the specified script once an hour at the beginning of the hour
  - `@reboot /root/task.sh` => Runs the specified task at boot time
  - `*/2 * * * * date >> /tmp/date_and_time.txt` => appending the current date and time into a file in every 2 minutes
- `tail -f /var/log/syslog` => checking cron runs
  - On CentOS: `tail -f /var/log/cron`
- `crontab -r` => removing the current users crontab file
- `sudo crontab -e -u username` => root can edit, list or remove other users cropntabs with the `-u` option
- `less /etc/crontab` => specifies when exactly root level system wide crone jobs will run

### Scheduling Tasks Using Anacron (anacron)
- `anacron` is similar to `cron`, just used on systems that are not up all the time
- if a task is scheduled in `anacron` during a downtime, then the task will be executed after the next system boot
- `anacron` is run by root, so the tasks will have root privileges
- execution frequency is expressed in days, not in minutes
- `/etc/anacrontab` is the file that specifies anacron jobs
  - format: **days** (1 == every day, 7 == every 7 deys) **delay_in_minutes**(how long anacron will wait before executing the job (helps keeping the system not being overloaded)) **job_identifier**(unique for each job) **executed_command**
  - for all anacron jobs a `/var/spool/anacron/job_identifier` is created (job timestamp file), that contains a single line that indicates the last time when this job was executed
- Eg `2 1 backup /root/backup.sh` => running in every 2 day delayed with 1 minute
- `sudo anacron -T` => checking `/etc/anacrontab` file for any syntax errors
  - no returned value means no error
- `sudo anacron -d` => running anacron inthe foreground (not in the default detached mode), so we see all printed messages (useful for debugging)

### Mounting and Unmounting filesystems (df, mount, unmount, fdisk, gparted)
- If we want to access a filesystem that is on another partition or dist, first we have to mount it or logically attach it to an existing directory
- `mount` => listing the currently attached file systems
- `mount -l -t ext4` => listing only ext4 type partitions
- `mount -l -t vfat` => listing only vfat (fat32) type partitions
- On ubuntu usb sticks will automatically be mounted at `/media/current_username/usbstickname/`
  - usually a device file that represents the hardware device is mounted at `/media/` such as `/dev/sdb`
  - `sudo fdisk -l` => lisrting the name of the device files
  - `dmesg` => same as above
  - `lsblk` => listing all block devices
- Having the name of a device file, we can mount it in any directory that already exists
- `sudo mount name_of_the_device mountpoint`
  - Eg `sudo mount /dev/sdb ~/Desktop/usb` => mounting a usb stick
- It is possible to mount the same device at different plances
- `sudo mount -o ro name_of_the_device mountpoint` => read only mounting
- `sudo mount -o rw,remount name_of_the_device mountpoint` => remounting in read/write mode (useful to make a read only mount into writeable withount unmounting)
  - Eg `sudo mount -o rw,remount /dev/sdb /home/student/Desktop/usb/`
- The mount command automatically detect the filesyste type. However some file system types are not automatically recognised.
  - `sudo mount -t vfat /dev/sdb ~/Desktop/usb` => specifying the file system type
- `sudo umount mountpoint` => unomunting a disk or a partition (works for only unused partitions (close all opened files or directories from that partition))
  - Eg `sudo umount ~/Desktop/usb`
- `sudo umount -l mountpoint` => (lazy) unmounts a busy filesystem as soon as it's not busy anymore
- Mounting an ISO (OS installer) file:
  1. Create a mount point:
    - `mkdir ~/iso`
  2. Mount the image:
    - `sudo mount /path_to_isofile ~/iso -o loop`
- `sudo fdisk` => standard utility for managing disks and partitions
  - **Always make backups before working with disks and partitions!**
- `gparted` => is a free GUI application to manage disks and partitions
  - `sudo apt install gparted`
  - `sudo gparted`

### Working with devicefiles (dd)
- `dd` is a utility for copying and converting files
- `dd` can be used to read and write from/to special device files
  - useful for backing up the boot sector od a hard drive
  - useful for cloning a disk or partition to another one
  - useful for creating a bootable usb stick
- devices are represented as special device files
  - most of them are located in `/dev`
- `sudo dd if=/dev/sdb of=/home/username/backup-usb.img status=progress`
  - `-if` => input file
  - `-of` => output file
  - in case of a restore, change the values of `-if` and `-of`
- **`dd` is copying all blocks, !!even the unused ones!!**
- the destination should be at least the same size as the source
- Creating a bootable usb stick:
  1. Find out the name of the device file for the usb drive:
    - `sudo lsblk`
  2. Unmount the usb drive if its mounted:
    - `sudo umount /media/student/950C-D952/`
  3. Formatting the usb disk :
    - `sudo mkfs.vfat /dev/sdb`
  4. Copying the iso to the usb stick:
    - `sudo dd if=/home/student/Downloads/linux....iso of=/dev/sdb bs=4M status=progress`
  5. Use the bootable usb stick

### Getting System Hardware Information (lwhw, lscpu, lsusb, lspci, dmidecode, hdparm)
- `sudo lwhw | less` => displaying a detailed overview of the system's hardware
- `sudo lwhw -json | less` => same as above, but with json format
- `sudo lwhw -html > hw.html` => same as above, but with html format
- `sudo lwhw -short | less` => displaying a short summary overview of the system's hardware
- `sudo inxi -Fx` => displaying a detailed overview of the system's hardware
  - not available on all linux distros
- `sudo lscpu` => displaying information about the CPU
- `sudo lscpu -J` => displaying information about the CPU, in json
- `sudo lshw -C cpu` => same as above but with another format
- `sudo dmidecode -t memory` => listing all memory modules with their capacity
- `sudo dmidecode -t memory | grep -i size` => listing only the memory sizes
- `sudo lspci` => listing all pci busses and details about the devices connected to them
- `sudo lsusb` => listing usb controllers and details about the devices connected to them
- `sudo lshw -C disk` => displaying information about the hard disks
- `sudo lshw -C disk -short` => displaying short summary information about the hard disks
- `sudo lsblk` => displaying information about all block devices
- `sudo fdisk -l` => displaying detailed information about all block devices
- `sudo hdparm` => getting or setting SATA drive parameters
- `sudo hdparm -i /dev/sda` => getting information about a SATA drive called `/dev/sda`
- `sudo hdparm -I /dev/sda` => getting detailed information about a SATA drive called `/dev/sda`
- `sudo hdparm -t --direct /dev/sda` => testing the read speed of a drive
- `sudp iw list | less` => showing information about the wireless devices
- `sudo uname -r` => displaying the version of the running kernel
- `sudo apt install acpi`
- `sudo acpi -bi` => getting teh battery status of a Devices

### Service Management (systemd and systemctl)
- Most modern Linux distributions are using `systemd` as the default init system and service manager
- It replaced the old `sysvinit` script system, but it's backward compatible with It
- `systemd` starts with **PID 1** as the forst process, then takes over and continues to mount the host's file systems and starts services
- `systemd` starts the services in paralell

- Statistics:
  - `systemd-analyze` => showing the boot process time, and other boot related statistics
  - `systemd-analyze blame` => listing all running units ordered by the time they took to initialize
- Linux boot process:
  1. System powers up
  2. The bootloader (GRUB) loads the kernel
  3. The kernel loads an initial ram disk that losds the system drives and looks for the root file system
  4. The kernel starts systemd initialization system
  5. systemd starts with *PID 1* as the first process
  6. systemd takes over and mounts the host's file systems and start services
- `ps -ef | less` => listing the running processes
  - here systemd is displayed as init for backward compatibility (`man init`)
- Systemd introduces the concepts of systemd units:
  - service unit
  - mount unit
  - socket unit
  - slice unit
- Units are defined in unit configuration files, which include information about the unit type and its behavior
- For example for service management tasks, the unit file contains instructions how to start, stop or restart the service
- `systemctl` => controlling the systemd system and service manager

#### Managing Services with `systemctl`
- `sudo systemctl status nginx.service` => checking nginx.service status (active (running))
- `sudo systemctl status nginx` => same as above (we can leave the .service suffix)
- `sudo systemctl stop nginx` => stopping nginx service
- `sudo systemctl status nginx` => checking nginx status (inactive (dead))
- `sudo systemctl start nginx` => starting a service
- `sudo systemctl restart nginx` => restarting a service
  - in Linux a server configuration is read once, when the server starts
  - after configuration changes, the server must restart for the configuration changes to take effect
- If an application is able to reload its configuartion files without restarting, issue the `reload` command:
  - `sudo systemctl reload nginx`
- If we are unsure whether the application is capable of reloading, issue the `reload-or-restart` option
  - `sudo systemctl reload-or-restart nginx` => trying to reload, if it is not possible then restart
- `sudo systemctl enable nginx` => configuring a service to start at boot time
  - this does not strat the service, the service will only start after the next system boot
- `sudo systemctl is-enabled nginx` => checking whether a service is enabled to start at boot time
- `sudo systemctl disable nginx` => c onfiguring a service to **NOT** start at boot time
- `sudo systemctl mask nginx` => preventing a service from being started (or enabled) automatically or manually
- `sudo systemctl unmask nginx` => enabling the service to be started or enabled again
- `sudo systemctl list-untis` => listing all actice untis that the systemd knows about
- `sudo systemctl list-untis --all` => listing all untis that the systemd has loaded, regardless of wheter they are currently actice or not

## Bash Shell Scripting

### Bash Aliases
- A bash alias is a shortcut to a command
- `alias` => listing all aliases on the system
```
alias ls=`ls --color=auto`
```
- `\ls` => running the original unaliased `ls`
- `alias alias_name="command to run"` => creating a new alias
  - Eg `alias c="clear"` => creating an alias that clears the screen
  - this alias is not permanent
  - to make them permanent, you have to declare them in the `~/.bash_profile` or in the `~/.bashrc`
    - `source ~/.bashrc` => activating the modifications in the current shell
- `unalias alias_name` => removing an alias
- it is useful to create aliases for frequently used `ssh` connections
- it is useful to create aliases for fully upgrading the system
  - `alias update="sudo apt update && sudop apt dist-upgrade -y && sudo apt clean"`

### Bash Shell Scripting
- `echo $0` => printing which shell isrunning
- `cat /etc/shells` => getting the list of all installed shells
- Each user can have a different default shell
- A shell script is basically and executeable text file that contains shell commands and other specific structures and components
- Common usage for shell scripts:
  - Monitoring the system
  - Data backup and restoring
  - Creating an email based alert system when something happens
  - User Administration
  - Security
  - Auditing
- By convention shell scripts have the `.sh` extension

### Bash Shebang
- For executable scripts the system expects in the forst line a so called **shebang**, that indicates which program to run as interpreter with the script file as its argument
- Without shebang, the users default shell will be used to run the script
- Shebang: `#!path_to_the_interpreter`
  - Eg: `#!/bin/bash`
  - Eg: `#!/usr/bin/python3` => it is possible to create scripts that will be run by python

### Comments
- `# This is a comment in bash`
- After a `#` character everythong is ignored by the interpreter
- There are no multiline comments in bash

### Running scripts
- `./script.sh` => running a shell script
  - the script is executed in a subshell
  - In this case it is mandatory for the script to have execute permission
- `name_of_the_interpreter script_name` => another way to run a shell script
  - Eg `bash script.sh`
  - In this case it is not mandatory for the script to have execute permission
  - This way of running a script will also overwrite the shebang directive
- `source script_name` => running a scripts
  - In this case it is not mandatory for the script to have execute permission
  - the `source` command reads and executes commands from the file specified as its argumnent in the current shell environment
  - the script is executed in the current shell
  - `. script_name` => same as above

### Variables in bash
- A variable is a name for a memory location
- `variable_name=value` => creatibg a new variable
  - Eg `os=Linux`
  - Eg `age=30`
  - Works both in a terminal or in a script
  - Space is not allowed before or after the `=`
  - If the value is a string that contains spaces, then enclose it between `"` characters
    - `distro="MX Linux"`
- Variable naming conventions:
  - Names should be descriptive and must remind you of the value they hold
  - Can't start with a number
  - Can't contain spaces or other special characters (except `_`)
    - Eg `server_name="Apache 2.4"`
  - Environment or shell variables that are introduced by the operating system, shell startup scripts or by the shell itself are all in caps
    - To prevent our own variables from conflicting with the above variables, use lower case variable names
- `$variable_name` => accessing the value of a variable
  - Eg `echo $os`
  - It is possible to reference variable values inside strings defined within `""`
    - `echo "Hi. This is the value of the os variable: $os"`
    - With `'` this wont work
  - Escaping with `\` also works with any character with special meaning:
    - `echo "The value of \$os is $os"`
  - It is possible to create new values basedon existing ones:
    - `my_distro="$os $distro"`
- `set | less` => listing all shell variables and functions
- `unset variable_name` => undefining or removing a variable
  - Eg `unset os`
  - **Has only effect in the current shell and in its child shells!!**, But in other independent shells the value will remain

- Declaring a read only variable (you can not unset it or modify it)
  - `declare -r variable_name=value`
    - we can use it as usual, but we cant modify its value

``` bash
#!/bin/bash
filename="/etc/passwd"
echo "Number of lines:"
wc -l $filename
echo "#################"
echo "First 5 lines:"
head -n $filename
echo "#################"
echo "Last 7 lines:"
tail -n 7 $filename
```
### Environment Variables
1. **Environment variables**
  - Defined for the current shell and are inherited by any child shells or processes
    - Eg `export MY_VAR=10`
  - Ususally named fully upper cased
  - They are used to pass information to processes that are spawned from the current shell
  - Displaying all defined environment variables: `env` or `printenv`
    - Displaying all available variables (environment, shell and the ones that are created by the user using the `set` command)
    - Variables declared without any keyword wont be displayed (Eg `my_var=10`)
    - `printenv variable_name` => printing the value of a specific environment variable
  - Eg `echo $PATH`

2. **Shell variables**
  - Are contained exclusively within the shell in which they were set or defined
    - Eg `my_var=10`
    - Eg `set my_var=10`
  - Displayed using `set`

- User configuration file: `~/.bashrc`
- System-wide configuration file (declared for all users): `/etc/bash.bashrc` and `/etc/profile` and `/etc/environment`
- Adding a new entry to PATH:
  - `export PATH=$PATH:~/scripts`

### Getting User Input
- `read` => Pausing execution and waiting for user input
- Eg `read variable_name` => Waiting for user input and storing it into variable_name
- `read -p "Enter an ip address " ip` => Providing a prompt message for the user
  - Eg `ping -c 1 $ip` => Using the provided value
- `read -s password` => Reading a password without echoing it back into the terminal

### Special Variables and Positional Arguments
- In many cases, bash scripts require argument values to provide input to the script
  - The arguments are the values provided after the script name when running it
  - The arguments are separated by spaces (aka default internal field separator)
- There are some predefined variables for this purpose, (aka positional argumants)
  - Eg `./script.sh filename1 dir1 10.0.0.1`
  - `$0` is the name of the script itself (`script.sh`)
  - `$1` is the first positional argument (`filename1`)
  - `$2` is the second positional argument (`dir1`)
  - `$3` is the last argument of the example script (`10.0.0.1`)
  - `$9` would be the ninth argument of the script and `${10}` is the tenth...
    - For positions greater than nine, the numbers must be enclosed by `{}`
  - `$#` is the number of the positional arguments
  - `$*` is a string representation of all positional arguments (seperated by space)
  - `$?` is the most recent foreground command exit status
  - If `"$1"` is a value is of type string, it is always a good practice to enclose it between `""`

### If, Elif and Else Statements
``` bash
if [ expression ] # A space is mandatory before and after the `[]`-s
then
  # Code to execute
elif [ expression ]
then
  # Code to execute
else
  # Code to execute
fi
```
- `man test` => listing all testing conditions that can be used as an expression
- `[[ expression ]]` is a new (safer) way of creating testing expression
  - Prevents word splitting on string variables that conatin spaces and you dont need to use quites
  - Also has regex matching features

### Testing Conditions for Numbers
- `INTEGER1 -eq INTEGER2` => is INTEGER1 equal to INTEGER2
- `INTEGER1 -ge INTEGER2` => is INTEGER1 greater than or equal to INTEGER2
- `INTEGER1 -gt INTEGER2` => is INTEGER1 greater than INTEGER2
- `INTEGER1 -le INTEGER2` => is INTEGER1 less than or equal to INTEGER2
- `INTEGER1 -lt INTEGER2` => is INTEGER1 less than INTEGER2
- `INTEGER1 -ne INTEGER2` => is INTEGER1 not equal to INTEGER2

### Comparing Strings in if Statements
- Two strings are equal if they have the same length and they have the same squence of characters in the same order
- `if [ "$str1" = "$str2" ];then` => Checking if `str1` is equal to `str2`
  - with using `;` it is possible to write `then` to the same line as `if`
- `if [[ "$str1" == "$str2" ]];then` => Checking if `str1` is equal to `str2`
- `if [[ "$str1" != "$str2" ]];then` => Checking if `str1` is not equal to `str2`
- `if [[ "$str1" == *"Linux"* ]];then` => Checking if `str1` conatins `Linux` as a substring
- `if [[ -z "$str1" ]];then` => Checking if `str1` is zero length
- `if [[ -n "$str1" ]];then` => Checking if `str1` is not zero length

### Multiple Conditions
- Logical OR (`||`) and AND (`&&`) operators allow you to use multiple expressions

``` bash
#!/bin/bash
read -p "Enter your age:" age
if [[ $age -lt 18 ]] && [[ $age -ge 0 ]]
then
  echo "You are a minor"
else
  echo "You are a major"
fi
```

### Command Substitution
- Running a bash command and storing its output into a variable for a later use
- There are two identical ways to perform command substitution:
  - ``` `command` ``` => writing the command between backticks
    - Eg ```now="`date`"```
  - `$(command)` => another way of command substitution
    - Eg `users="$(who)"`
    - Eg `output="$(ps-ef | grep bash)"`
    - Eg `sudo tar -czvf etc-$(date +%F_%H%M).tar.gz /etc/` => new file name for every minute

### Example: Testing Network Connections
``` bash
#!/bin/bash
output="$(ping -c 3 $1)"

if [[ "$output" == *"100% packet loss"* ]]
then
  echo "The network connection to $1 is not working."
else
  echo "The network connection to $1 is working."
fi
```

### For loops
``` bash
for item in LIST
do
  commands
done
```
- The LIST can be a series of strings separated by spaces, a range of numbers, output of a command, an array, and so on...
``` bash
#!/bin/bash
for os in Ubuntu CentOS Slackware Kali "MX Linux"
do
  echo "os is $os"
done

# printing numbers from 3 to 7 (both 3 and 7 are included)
for num in {3..7}
do
  echo "num is $num"
done

# printing numbers from 10 to 100 (both 10 and 100 are included) and incrementing by 5
for num in {10..100..5}
do
  echo "num is $num"
done

# iterating over the output of a command
# `./*` means any file in the current directory
for item in ./*
do
  if [[ -f "$item" ]]
  then
    echo "Displaying the contents of $item"
    sleep 1
    cat $item
    echo "###############"
  fi
done

for file in *.txt
do
  mv "$file" "renamed_by_script_$file"
done

# C style for loop (this is not commonly used in bash)
for ((i=0;i<=50;i++))
do
  echo "i => $i"
done
```
- If a string element contains a space, we have to enclose it within `""` characters

### While loops
``` bash
while CONDITION
do
  COMMANDS
done
```
- The set of cpmmands are executed as long as the given condition evaluates to true
``` bash
#!/bin/bash
i=0

while [[ $i -lt 10 ]]
do
  echo "i is $i"
  ((i++)) # same as: let i=i+1
done

# infinite loop
while true
do
  echo "running forever"
  sleep 1
done

# One liner
while true; do echo "hi there"; sleep 1; done
```
- When using arithmetic operations do it inside double parenthesis `(())`
  - Eg `c=$((a+b))` (same as `let c=a+b`)

### Case statement
- Case statement allows us to test strings and numbers
``` bash
case EXPRESSION in
  PATTERN_1)
    STATEMENTS
    ;;
  PATTERN_2)
    STATEMENTS
    ;;
  *)
    STATEMENTS
    ;;
esac
```
``` bash
#!/bin/bash

echp -n "Enter your favprite pet:"
read PET

case "$PET" in
  dog)
    echo "your favorite pet is the dog"
    ;;
  cat|Cat)
    echo "you like cats"
    ;;
  fish|"African turtle")
    echo "fish or zurtles are great"
    ;;
  *)
    echo "Your favorite pet is unknown"
    ;;
esac
```

### Functions
- Compared to other programming languages, bash functions are limited
- In bash () are for decoration, it is not used for arguments
``` bash
# declaring a function with the function keyword
function print_something () {
  echo "something"
}

# daclaring a function without the function keyword
display_something () {
  echo "something"
}

print_something # calling the function
display_something # in bash calling a function is done without ()-s
```
- Arguments sent to functions with using Positional Arguments
``` bash
create_files () {
  echo "Creating $1"
  touch $1
  chmod 400 $1
  echo "Creating $2"
  touch $2
  chmod 600 $2
  return 10
}

create_files aa.txt bb.txt
echo $? # this will print out 10
```
- Bash functions dont allow to return values
  - Using the `return` keyword will set the status of the last command exexuted inside the function (`$?`)
    - `0` value indicates success
    - any non zero value indicates an error
``` bash
function lines_in_file () {
  grep -c "$1" "$2"
}

n=$(lines_in_file "usb" "/var/log/dmesg") # simulating a returned value with command substitution
```

### Variable scope in functions
- In bash by default all variables are global
  - aka they are visible everywhere in the script
- Creating a variable inside a function that is local to the function (use the `local` keyword):
  - `local variable_name=value`
  - It is a good practice to create only local variables inside functions

### Creating Bash Menus (select)
``` bash
select ITEM in LIST
do
  COMMANDS
done
```
- ITEM is a user defined variable and the LIST is a series of strings, numbers or output of commands

``` bash
#!/bin/bash
PS3="This is the new prompt"
select COUNTRY in Germany France USA "United Kingdom" # prints an indexed option select list
do
  echo "COUNTRY is $COUNTRY" # variable that contains the user selected list item value
  echo "REPLY is $REPLY" # predefined variable that contains the user selected item index
  break
done
```
- The select loop is continues to execute until the `break` statement is reached
  - or until the user terminates the script (Ctrl + C)
- The default prompt is `#?`
  - To modify it change the value of the `PC3` variable

### Bash Arrays
- Variables can only store one piece of data at a time
- Bash provides one dimensional indexed and associated darrays
- Arrays can store multiple different values at the same time

``` bash
# Creating a numerically indexed array
ages=(20 22 40 38)

echo $ages # Prints the first item of the array

echo ${ages[@]} # Printing the whole array
echo ${ages[*]} # Almost same as above
echo ${!ages[*]} # Printing the array indexes
echo ${#ages[*]} # Printing the number of elements in the array
echo ${ages[0]} # Printing the first elemet of the array
echo ${ages[1]} # Printing the second elemet of the array
echo ${ages[1000]} # Trying to access a nonexisting element wont give us an error (returns "")
echo ${ages[-1]} # Printing the last elemet of the array
echo ${ages[-2]} # Printing the second last elemet of the array

numbers[0]=100 # Creating a new array with one element
numbers[1]=101 # Adding a new element to the array
numbers[1]=200 # Changing the value of an element

declare -a names # declaring an array explicitly
names[0]="Dan"
names[10]="Andrei" # It is ok, if array indexes are not consecutive
unset names[10] # Deleting an array element (creates a gap in the array)

years=(2018 2019 2020)
years+=(2021) # Adding a new element to the end of the array
years+=(2022 2023) # Adding more new elements to the end of the array

## Slicing an array (slicing is not modifying the original array)
echo ${years[@]:2} # Printing all elements starting from index 2
echo ${years[@]:2:4} # Printing four elements starting from index 2
```
- Associative arrays contain key value pairs and are similar to dictionaries, maps or hashes
  - A key can be any string value
``` bash
declare -A userdata # Creating an associative array
userdata[username]="scott" # Adding an element to the array
userdata[password]="Welcome1"
userdata[uid]=1010
userdata[uid]=1011 # Changing the value of an element

unset userdata[password] # Removing an eleemnt from an array

echo ${userdata[username]} # Accessing an array element
echo ${userdata[@]} # Printing all values of the array
echo ${!userdata[@]} # Printing all keys of the array
userdata!ó+=([shell]="Bash" [admin]=False)

## Creating an unmutable associative array
# adding a new eleemtn or modifying an existing one is not possible
declare -r -A SUPERSTARS=([Germqany]="Boney M" [USA]="Bon Jovi" [England]="Goldie")
```

### Using the Readarray Command
- `readarray array_name` converts whatever it reads from the standard input into an indexed array
  - stops appending array elements when `Ctrl + C` is pressed
- `readarray months< <(cat months.txt)` # each line of the file will be an eleement of the array
  - redirecting the contents ofa file to `readarray`
- `readarray users< <(cut -d: -f1 /etc/passwd)` # Creating an array that contains all users of the system
- `readarray -t files< <(ls /etc/*)` # Creating an array of all files of `/etc/`

### Iterating Over Arrays
``` bash
readarray -t files< <(ls /etc/*)

for f in "${files[@]}"
do
  if [[ -f $f && -r $f ]]
  then
    cat $f
  fi
done
```
## SSH Public Key Authentication
### SSH Public Key Authentication (PKA)
- **PKA** or **Public Key Authentication** is an authentication method that uses a key pair for authentication instead of password which is the default method
- **Pros:**
  - increased sucurity
  - authentication from within scripts or automation tools (automated backups, updates, network automation)
- In **PKA** there are two types of keys generated:
  - **Private key** (It stays on the SSH Client)
    - **Passphrase** protects the use ofthe private key.
    - If passphrase is configured, every private kay read requires to provide the passphrase
  - **Public key** (It stays on the SSH Server)
- Requirements:
  - ssh client that supports RSA authentication
  - a private and public key pair (for each user)
  - ssh server that supports SSH PKA
- **!!It is recommended to disable password authentication on the SSH server!!**
### Generating SSH Key Pair on Windows
- Use Putty key generator
  1. Type of key: `RSA`
  2. Number ofbits in a generated key: `2048` (this is the minimum recommended size)
  3. Generate (Move the mouse to generate randomness)
  4. Add a comment to the key (Helps to not mix upkeys later)
  5. Add passphrase if needed
  6. Save the key (the public key should have `.pub` extension,the private: `.ppk`)

### Generating SSH Key Pair on Linux
- Use `ssh-keygen`
  1. `ssh-keygen -b 2048 -t rsa -C "linux user Jan 05 2025"`
  2. You will prompted to select a different location if needed
  3. You will prompted to set a passphrase if needed
  4. By default the key will be in `~/.ssh` (as `id_rsa` and `id_rsa.pub`)
  5. Set proper permisions for the private key:
    - `chmod 400 ¨/.ssh/id_rsa`

### Configuring SSH Public Key Authentication on Linux
#### Windows
1. Get the public key
  - Open the private key with Putty key generator and copy the public key from the GUI
2. Access the Linux machine with the user that we want to authenticate with PKA
3. Create `~/.ssh/autorized_keys` file and paste to private key into that file
4. Check whether the ssh daemon is running: `systemctl status ssh`
5. Try the connection:
  1. Connection -> SSH -> Auth -> Browse Button (Private key file for authentication) -> Select the private key
  2. Session -> Enter IP address, Port -> Give the session a name -> Save
  3. Open -> Specify the user name
  4. Profit

#### Linux
1. Get the public key
  - Check the public key `cat ~/.ssh/id_rsa.pub`
2. Copy the public key using `scp`
  - `scp -P 22 ~/.ssh/id_rsa.pub username@server_ip:~`
    - OR `ssh-copy-id -i ~/.ssh/id_rsa.pub username@server_ip`
      - Copy the public key to the server and append it to `~/.ssh/authorized_keys`
3. On the server `cat id_rsa.pub >> ~/.ssh/authorized_keys`
  - **Always append the new key to the end of the file. There might be other keys in the file!!!**
4. Check the `/authorized_keys` `cat ~/.ssh/authorized_keys`
5. Try to connect with `ssh`
  - You wont be prompted providing a password
6. In case of error try verbose mode: `ssh -v username@server_ip`
