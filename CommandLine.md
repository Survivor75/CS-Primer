THE COMMAND LINE

Basics And Navigation

Home directory

~

Present working directory

By default, pwd will list the “logical” path of your current directory. This means it will treat symlinked paths as if they were the actual paths. 
If we want to see the actual physical path, with all of the symlinks resolved, we can use the -P flag, pwd -P.

List files and directories

By default, ls will operate in the current directory that you’re in. However, you may want to find out what files are in another directory, without first leaving your current directory. The ls command will let you pass it a path to work on, ls /usr/local/.

ls -a   (all files)
ls -l   (long form listinng)
ls -lh  (human readable sizes)
ls -lhS (sorting by size)
ls -lt  (sorting by last modified)
ls -lr  (reverse sort)

Change directories

cd ~/Documents (navigate to path)
cd ..          (navigating up)
cd             (navigate to home directory)

Creating directories

mkdir foo
mkdir -p a/b/c (create nested directories)

Copying Files

cp source_file_path destination_file_path

cp will allows you to list several files you would like to copy. When you do this, however, the last argument must be a directory, and the original file names of the source files will be used as the names of the new files in the target directory.

cp a.txt b.txt foo

cp -f a.txt b.txt (force overwriting of a file)
cp -i a.txt b.txt (confirm overwriting of a file)

Deleting Files

rm -v a.txt (list files that were deleted)

Moving Files

mv -v source_file_path destination_file_path

Input/Output

| (redirecting output)
In the following example, we “pipe” the output of the ls command to the input of the grep command to find all the files in my home directory that contain an underscore, _.

ls -a ~ | grep _

> (writing to a file)
ls -a ~ | grep _ > underscores.txt

< (reading from a file)
ls -a ~ | grep _ 

Ack/Ag

Searching large code bases is something that most of us do on a daily basis. Whether it be to refactor some code, or to simply find where a variable, class, or method has been implemented. Good searching tools are the lifeblood of development.

ag search_term       (this query is run recursively against the current directory)
ag search_term foo/  (path to search against)
ag readme$           (search for any occurrence of the word readme at the end of a line)
ag search_term -l    (result set is now presented as just a list of files)
ag search_term -l -i (case insensitive search)

ag search_term -l -G action (limit our search results to filenames that contain the word action)

ag search_term -l -G ec$ (search for files that end with ec)

ag search_term -l --ignore-dir=foo/lib (if we aren’t interested in seeing any results from the foo/lib directory)
ag search_term -l --ignore-dir="*txt" (Despite its name, the –ignore-dir flag will also let us filter out particular files, not just directories)

Both Ack and Ag will expect standard input as a source for searching. This means we don’t need to just search files, but we can use other commands to provide the data we’ll search over.
For example, we can use the ps command to get a list of all of the processes running on our machine, and then search for a specific command using either Ack or Ag.

ps -e | ag forego(we search through all of the running processes to find one that contains the term forego)

Ag is significantly faster than Ack.

cURL

Basics

curl http-server.com/hello    (prints the response of the web page to the console)
curl -i http-server.com/hello (see more information about the response)

Following Redirects

There are times when we are trying to download a resource from a server, but instead of the resource we requested, the server returns a status code of 302. The 302 response may also include a message that the resource has moved.

curl -L http-server.com/hello (follow redirects)

Downloading Files

curl -O http-server.com/assets/image.png                 ( the results will be saved into a file named image.jpg)
curl -o hello_image.ong http-server.com/assets/image.png (custom file name)

Changing HTTP Request Method

curl -X POST http-server.com/echo (post request)
curl -X PUT http-server.com/echo  (put request)

curl -X POST "http-server.com/echo?fname=foo&lname=bar"    (send parameters)
curl -X POST -d "fname=foo&lname=bar" http-server.com/echo (send request body)
curl -X POST -d "{\"fname\":\"foo\"}" http-server.com/echo (send request body as json)

Setting Headers

curl -X POST -d "{\"fname\":\"foo\"}" http-server.com/echo -H "Accept: application/json" -H "Auth: 12345" (append headers)

Basic HTTP Auth

curl -X POST -u "user:password" http-server.com/login -H "Accept: application/json" (basic auth)

Find

Basics

find PATH_TO_SEARCH OPTIONS_TO_USE PATTERN_TO_SEARCH_FOR

find . -name foo.txt
find . -name \*foo.txt

Searching Paths

find . -path \*session\*         (find any files whose path contains the word session)
find . -path \*session\* -type f (find only files whose path contains the word session)
find . -path \*session\* -type d (find only directories whose path contains the word session)

And/Or Expression

find . -path \*session\* -type f -name \*mem\*         (find only files whose path name contains session and whose file name contains mem)
find . \( -name \*.gemspec -or -name \*.jpg \) -type f (find files whose name either ends in .gemspec or in .jpg)


Not Matching Query

find . -not -path \*t\* -type f (find all of the files in our directory that don’t contain the letter t somewhere in their path)

Find By Last Modified Time

find . -mtime -1 (find files who have been modified in the last day)
find . -mmin -5  (files that have been modified in the last 5 minutes)

Find By File Size

find . -size +200k (search for files whose size is greater than 200 kilobytes)

Performing Operations

find ./guides -type f -name \*.yml -print -delete (find all of the files whose name ends with .yml and delete them from our repository)

Grep

grep is a tool for searching files for search terms.

Basics

grep Pack README.md      ( search for the term Pack in the README.md file)
grep "r..y" README.md    (search the README.md file for any lines that contain the letter r followed by any two characters, then followed by the letter y)
grep -c python README.md (count the number of times a pattern is found in a file)
grep -n python README.md (displaying line numbers)
grep -i python README.md (case insensitive search)

Searching Multiple Files

grep python README.md RELEASE_DOC (search specific files)
grep python *.md                  (search specific files in the current directory by giving it a pattern)
grep -R “foo” .
grep -R --include="*.yml" "foo" . (search for the term foo in yml files)

Searching From Standard Output

ps -e | grep forego (grep to search for the process that matched the pattern, forego)

Ps

Basics

ps (when the ps command is run without any arguments, it will return results for the processes that belong to the current user)

Column	Definition
PID	The process ID of the process.
TTY1	The controlling terminal for the process.
TIME	The cumulative CPU time the process has used since the process started. The format for this time is [ dd-]hh:mm:ss.
CMD	The name of the command that is running


Display User-Oriented Output

ps u (display common useful information, such as CPU and memory usage)

Column	Definition
USER	The user that the process is running under.
%CPU	The percentage of time the process has used the CPU since the process started.
%MEM	The percentage of real memory used by this process.
VSZ	Indicates, as a decimal integer, the size in kilobytes of the process in virtual memory.
RSS	The real-memory size of the process (in 1 KB units).
STAT	The status of the process.
STARTED	When the process was started.

Display All Processes

ps -e


Display Processes By User

ps -U root

Customize Displayed Output

ps -U root

Sorting

ps -m -O %mem -u root (sort by memory usage)
ps -r -O %cpu -u root (sort by cpu usage)

Cal

Cat

Kill

Man

Tail

Tree