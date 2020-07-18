## THE COMMAND LINE

### Basics And Navigation

**Home directory**

    ~

**Present working directory**

By default, `pwd` will list the “logical” path of your current directory. This means it will treat symlinked paths as if they were the actual paths.

If we want to see the actual physical path, with all of the symlinks resolved, we can use the `-P` flag, `pwd -P`.

**List files and directories**

By default, `ls` will operate in the current directory that you’re in. However, you may want to find out what files are in another directory, without first leaving your current directory. The `ls` command will let you pass it a path to work on, `ls /usr/local/`.

All files:

    ls -a

Long form listinng:

    ls -l

Human readable sizes:

    ls -lh

Sorting by size:

    ls -lhS

Sorting by last modified:

    ls -lt

Reverse sort:

    ls -lr

**Change directories**

Navigate to path:

    cd ~/Documents 

Navigating up:
   
    cd ..

Navigate to home directory:

    cd

**Creating directories**

    mkdir foo
    
Create nested directories:

    mkdir -p a/b/c 

**Copying Files**

`cp` source_file_path destination_file_path

`cp` will allows you to list several files you would like to copy. When you do this, however, the last argument _must_ be a directory, and the original file names of the source files will be used as the names of the new files in the target directory.

    cp a.txt b.txt foo

 Force overwriting of a file:

    cp -f a.txt b.txt

 Confirm overwriting of a file:

    cp -i a.txt b.txt

**Deleting Files**

 List files that were deleted:

    rm -v a.txt

**Moving Files**

    mv -v source_file_path destination_file_path

**Input/Output**

In the following example, we “pipe” the output of the `ls` command to the input of the `grep` command to find all the files in my home directory that contain an underscore, `_`.

    ls -a ~ | grep _
    
Writing to a file:
    
    ls -a ~ | grep _ > underscores.txt
    

### Ack/Ag

Searching large code bases is something that most of us do on a daily basis. Whether it be to refactor some code, or to simply find where a variable, class, or method has been implemented. Good searching tools are the lifeblood of development.

This query is run recursively against the current directory:

    ag search_term

Path to search against:

    ag search_term foo/

Search for any occurrence of the word readme at the end of a line:

    ag readme$

Result set is now presented as just a list of files:

    ag search_term -l

Case insensitive search:

    ag search_term -l -i

Limit our search results to filenames that contain the word action:

    ag search_term -l -G action

Search for files that end with ec:

    ag search_term -l -G ec$

If we aren’t interested in seeing any results from the foo/lib directory:

    ag search_term -l --ignore-dir=foo/lib 

Despite its name, the **–ignore-dir** flag will also let us filter out particular files, not just directories:

    ag search_term -l --ignore-dir="*txt"

Both Ack and Ag will expect standard input as a source for searching. This means we don’t need to just search files, but we can use other commands to provide the data we’ll search over.

For example, we can use the `ps` command to get a list of all of the processes running on our machine, and then search for a specific command using either Ack or Ag.

We search through all of the running processes to find one that contains the term **forego**:

    ps -e | ag forego 

Ag is significantly faster than Ack.  

### cURL

**Basics**  

Print the response of the web page to the console:

    curl http-server.com/hello    

See more information about the response:

    curl -i http-server.com/hello 

**Following Redirects**

There are times when we are trying to download a resource from a server, but instead of the resource we requested, the server returns a status code of **302**. The **302** response may also include a message that the resource has moved:

    curl -L http-server.com/hello

**Downloading Files**

    curl -O http-server.com/assets/image.png

    curl -o hello_image.ong http-server.com/assets/image.png

**Changing HTTP Request Method**

POST request:

    curl -X POST http-server.com/echo

PUT request:

    curl -X PUT http-server.com/echo

Send paramerters:
    
    curl -X POST "http-server.com/echo?fname=foo&lname=bar"

Send request body:
    
    curl -X POST -d "fname=foo&lname=bar" http-server.com/echo 
    
    curl -X POST -d "{\"fname\":\"foo\"}" http-server.com/echo

**Setting Headers**

    curl -X POST -d "{\"fname\":\"foo\"}" http-server.com/echo -H "Accept: application/json" -H "Auth: 12345"

**Basic HTTP Auth**

    curl -X POST -u "user:password" http-server.com/login -H "Accept: application/json"

### Find

**Basics**

    find PATH_TO_SEARCH OPTIONS_TO_USE PATTERN_TO_SEARCH_FOR

    find . -name foo.txt
    
    find . -name \*foo.txt

**Searching Paths**

Find any files whose path contains the word session:

    find . -path \*session\*

Find only files whose path contains the word session:

    find . -path \*session\* -type f

Find only directories whose path contains the word session:

    find . -path \*session\* -type d

**And/Or Expression**

Find only files whose path name contains session and whose file name contains mem:

    find . -path \*session\* -type f -name \*mem\*

Find files whose name either ends in .gemspec or in .jpg:

    find . \( -name \*.gemspec -or -name \*.jpg \) -type f

**Not Matching Query**

Find all of the files in our directory that don’t contain the letter t somewhere in their path:

    find . -not -path \*t\* -type f

**Find By Last Modified Time**

Find files who have been modified in the last day:

    find . -mtime -1 

Files that have been modified in the last 5 minutes:

    find . -mmin -5  

**Find By File Size**

Search for files whose size is greater than 200 kilobytes:

    find . -size +200k

**Performing Operations**

Find all of the files whose name ends with .yml and delete them from our repository:

    find ./guides -type f -name \*.yml -print -delete 

### Grep

grep is a tool for searching files for search terms.

**Basics**

Search for the term Pack in the README.md file:

    grep Pack README.md      

Search the README.md file for any lines that contain the letter r followed by any two characters, then followed by the letter y:

    grep "r..y" README.md    

Count the number of times a pattern is found in a file:

    grep -c python README.md 

**Displaying line numbers.**

    grep -n python README.md

**Case insensitive search.**

    grep -i python README.md 

**Searching Multiple Files**

Search specific files:

    grep python README.md RELEASE_DOC

Search specific files in the current directory by giving it a pattern:

    grep python *.md
    
    grep -R “foo” .
    
Search for the term foo in .yml files:

    grep -R --include="*.yml" "foo" . 

**Searching From Standard Output**

Use grep to search for the process that matched the pattern, forego:

    ps -e | grep forego 

### Ps

**Basics**

When the ps command is run without any arguments, it will return results for the processes that belong to the current user:
   
    ps 

**Display User-Oriented Output**

    ps u 

**Display All Processes**

    ps -e

**Display Processes By User**

    ps -U root

**Sorting**

Sort by memory usage:

    ps -m -O %mem -u root

Sort by cpu usage:

    ps -r -O %cpu -u root

### Kill

The `kill` command is, unfortunately, poorly named. Its name would imply that its sole purpose is that of mischief, when in reality its purpose is to simply send messages to processes. A few of these signals will forcefully terminate a process. Others will simply tell the process to shutdown when it is ready.

    kill 12345

  **Forcefully Terminate A Process**

      kill -9 12345

### Tree

 Using the  `tree`  command, you can recursively list the contents of a directory in a tree-like format.  This is handy when you want to get a high-level view of all the directories and files inside of a project for example.

By default,  `tree`  will list all of the directories and files in a given directory, but it also comes with many flags that will alter the level of detail you get back.

### Wc

The `wc` command provides two really useful functions, it will both count the number of words in a file, as well as the number of lines in a file.

**Count Words In A File**

If we want to count the number of words in a file we can use the `-w` flag:

    wc -w /usr/share/dict/web2a

**Count Lines In A File**

To count the number of lines in a file we can use the `-l` flag:

    wc -l /usr/share/dict/web2a

**Piping Input To WC**

Count the occurrences of the phrase “FOO” in the code:

    ag FOO | wc -l


### Disk

**fdisk**

`fdisk` is the most commonly used command to check the partitions on a disk. The fdisk command can display the partitions and details like file system type. However it does not report the size of each partitions.

    sudo fdisk -l

Each device is reported separately with details about size, seconds, id and individual partitions.

**sfdisk**

`sfdisk` is another utility with a purpose similar to fdisk, but with more features. It can display the size of each partition in MB.

    sudo sfdisk -l -uM

**df**

`df` is not a partitioning utility, but prints out details about only mounted file systems. The list generated by df even includes file systems that are not real disk partitions.

    df -h

The general syntax for the  `df`  command is as follows:

    df [OPTIONS] FILESYSTEM

When used without any argument, the `df` command will display information about all mounted file systems.

    df

```
Filesystem     1K-blocks      Used Available Use% Mounted on
dev              8172848         0   8172848   0% /dev
run              8218640      1696   8216944   1% /run
/dev/nvme0n1p3 222284728 183057872  27865672  87% /
tmpfs            8218640    150256   8068384   2% /dev/shm
tmpfs            8218640         0   8218640   0% /sys/fs/cgroup
tmpfs            8218640        24   8218616   1% /tmp
/dev/nvme0n1p1    523248    107912    415336  21% /boot
/dev/sda1      480588496 172832632 283320260  38% /data
tmpfs            1643728        40   1643688   1% /run/user/1000
```

Each line includes the following columns:

-   “Filesystem” - The name of the filesystem.
-   “1K-blocks” - The size of the filesystem in 1K blocks.
-   “Used” - The used space in 1K blocks.
-   “Available” - The available space in 1K blocks.
-   “Use%” - The percentage of used space.
-   “Mounted on” the directory on which the filesystem is mounted.

To display information only for a specific file system, pass its name or the mount point to the  `df`  command.

For example, to show the space available on the file system mounted to the system root directory (`/`), you can use either  `df /dev/nvme0n1p3`  or  `df /`.

```
df /
```

```
Filesystem     1K-blocks      Used Available Use% Mounted on
/dev/nvme0n1p3 222284728 183057872  27865672  87% /

```

**Show Disk Space Usage in Human Readable Format**

By default, the  `df`  command shows the disk space in 1-kilobyte blocks and the size of used and available disk space in kilobytes.

To display information about disk drives in human-readable format (kilobytes, megabytes, gigabytes and so on), invoke the  `df`  command with the  `-h`  option:

```
df -h
```

```
Filesystem      Size  Used Avail Use% Mounted on
dev             7.8G     0  7.8G   0% /dev
run             7.9G  1.8M  7.9G   1% /run
/dev/nvme0n1p3  212G  176G   27G  88% /
tmpfs           7.9G  145M  7.7G   2% /dev/shm
tmpfs           7.9G     0  7.9G   0% /sys/fs/cgroup
tmpfs           7.9G   24K  7.9G   1% /tmp
/dev/nvme0n1p1  511M  106M  406M  21% /boot
/dev/sda1       459G  165G  271G  38% /data
tmpfs           1.6G   16K  1.6G   1% /run/user/1000

```

**File System Types**

The  `-T`  option tells  `df`  to display file system types:

```
df -t
```

The output includes an additional column named “Type” showing the type of the filesystem:

```
Filesystem     Type     1K-blocks      Used Available Use% Mounted on
dev            devtmpfs   8172848         0   8172848   0% /dev
run            tmpfs      8218640      1744   8216896   1% /run
/dev/nvme0n1p3 ext4     222284728 183666100  27257444  88% /
tmpfs          tmpfs      8218640    383076   7835564   5% /dev/shm
tmpfs          tmpfs      8218640         0   8218640   0% /sys/fs/cgroup
tmpfs          tmpfs      8218640        24   8218616   1% /tmp
/dev/nvme0n1p1 vfat        523248    107912    415336  21% /boot
/dev/sda1      ext4     480588496 172832632 283320260  38% /data
tmpfs          tmpfs      1643728        40   1643688   1% /run/user/1000

```

If you want to limit listing to file systems of a specific type use the  `-t`  option followed by the type.

Here is an example showing how to list all ext4 partitions:

```
df -t ext4
```

```
Filesystem     1K-blocks      Used Available Use% Mounted on
/dev/nvme0n1p3 222284728 183666112  27257432  88% /
/dev/sda1      480588496 172832632 283320260  38% /data

```

Similar to above, the  `-x`  option allows you to limit the output to file systems that are not of a specific type:

```
df -x tmpfs
```

```
Filesystem     1K-blocks      Used Available Use% Mounted on
dev              8172848         0   8172848   0% /dev
run              8218640      1696   8216944   1% /run
/dev/nvme0n1p3 222284728 183057872  27865672  87% /
/dev/nvme0n1p1    523248    107912    415336  21% /boot
/dev/sda1      480588496 172832632 283320260  38% /data
```

**du**

The general syntax for the  `du`  command is as follows:

    du [OPTIONS] FILE

If the given `FILE` is a directory, `du` will summarize disk usage of each file and subdirectory in that directory. If no `FILE` is specified, `du` will report the disk usage of the current working directory.

Usually, you would want to display only the space occupied by the given directory in a human-readable format. To do that, use the  `-h`  option.

For example, to get the total size of the  `/var/lib`  and all of its subdirectories, you would run the following command:

    sudo du -h /var

To report only the total size of the specified directory, and not for subdirectories use the `-s` option:

    sudo du -sh /var

The `-c` option tells `du` to report a grand total. This is useful when you want to get the combined size of two or more directories.

    sudo du -csh /var/log /var/lib

**free**

The syntax for the `free` command is as follows:

    free [OPTIONS]
   
When used without any option, the `free` command will display information about the memory and swap in kibibyte. 1 kibibyte (KiB) is 1024 bytes.

    free

```
              total        used        free      shared  buff/cache   available
Mem:        8075208     3204964     1310540      551232     3559704     4198340
Swap:       2097148           0     2097148
```

Here’s what each column mean:

-   **total**  - This number represents the total amount of memory that can be used by the applications.
-   **used**  - Used memory. It is calculated as:  `used = total - free - buffers - cache`
-   **free**  - Free / Unused memory.
-   **shared**  - This column can be ignored as it has no meaning. It is here only for backward compatibility.
-   **buff/cache**  - The combined memory used by the kernel buffers and page cache and slabs. /this memory can be reclaimed at any time if needed by the applications. If you want buffers and cache to be displayed in two separate columns use the  `-w`  option.
-   **available**  - An estimate of the amount of memory that is available for starting new applications, without swapping.

### Network

**ifconfig**

`ifconfig` utility is used to configure network interface parameters.Mostly we use this command to check the IP address assigned to the system.

    ifconfig -a


**traceroute**

`traceroute` print the route packets take to network host.Destination host or IP is mandatory parameter to use this utility.

    traceroute stackoverflow.com

**dig**

`dig` (Domain Information Groper) is a flexible tool for interrogating DNS name servers. It performs  DNS lookups and displays the answers that are returned from the name servers.

    dig stackoverflow.com

**telnet**

`telnet` connect destination host:port via a telnet protocol if connection establishes means connectivity between two hosts is working fine.

    telnet stackoverflow.com 443

**nslookup**

`nslookup` is a program to query Internet domain name servers.

    nslookup stackoverflow.com


**netstat**

`netstat` command allows you a simple way to review each of your network connections and open sockets. `netstat` with head output is very helpful while performing web server troubleshooting.

**scp**

`scp` allows you to secure copy files to and from another host in the network.

