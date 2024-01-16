# Lab Report 1

## Changing Directories
`cd` stands for "change directory" and is used for navigating through the different folders in your workspace.
* Using the `cd` command with no arguments will bring you to the root directory.
For exmaple, when our working directory is /home/lecture1 and our root directory is /home, running `cd` with no arguments gives the following output:
```
[user@sahara ~/lecture1]$ cd
[user@sahara ~]$ pwd
/home
```
With the `pwd` command, we can see that we are now in the `/home` directory. When you use `cd` with no arguments (meaning without specifying a directory), it will bring you straight back to the root directory. This is not an error.


* Using the `cd` command with a directory as an argument will take you to that directory (if it exists). <br>
When our working directory is `/home`, running the command `cd lecture1` will take us to `./lecture1`:
```
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
We can see that we are now in the `lecture1` directory. When you use `cd` with a valid directory as an argument, it will make your working directory the one that you specified.

If you provide an invalid directory, the output will look like this:
```
[user@sahara ~]$ cd fakedirectory
bash: cd: fakedirectory: No such file or directory
```
This throws an error because the specified directory does not exist within the current directory. 


* Using the `cd` command with a file as an argument will throw an error, even if the file exists.      
When we are in the `/home` directory and there is a file called `hello.txt`, running `cd hello.txt` gives the following:
```
[user@sahara ~]$ ls
hello.txt  
[user@sahara ~]$ cd hello.txt
bash: cd: hello.txt: Not a directory
```
This throws an error because the `cd` command is meant for navigating through directories, and it does not know what to do with a file. 

## Listing files
The `ls` command is meant for listing out the contents of a directory.
* Running `ls` with no arguments will list out the contents of the current directory. <br>
When our current directory is `/home` and it contains a file called `hello.txt` and another directory called `lecture1`, running `ls` will show both the file and directory.
```
[user@sahara ~]$ ls
hello.txt  lecture1
```
Running `ls` with no arguments (meaning without specifying a directory) will simply print the contents of the current directory if there are any, which is not an error.

* Running `ls` with a directory as an argument will list out the contents of the specified directory. <br>
For example, when we are in the `/home` directory and we want to see the contents of the `lecture1` folder (which exists), running `ls lecture1` prints:
```
[user@sahara ~]$ ls lecture1
Hello.java  messages  README
```
`ls` with a valid directory as an argument will print out the contents of the specified folder, as shown above.  <br>
When the directory given as an argument is invalid, the following output is printed:
```
[user@sahara ~]$ ls fake-directory
ls: cannot access 'fake-directory': No such file or directory
```
This throws an error becuase there is no directory named `fake-directory`, and `ls` cannot print the contents of a non-existent directory.

* Running `ls` with a file as an argument simply prints out the file name. <br>
When our current directory is `/home` and it contains a file called `hello.txt`, running `ls hello.txt` gives:
```
[user@sahara ~]$ ls hello.txt
hello.txt
```
A file does not have any sub-contents, so `ls` simply prints the file name. This is not an error. 

Once again, providing a non-existent file name throws an error:
```
[user@sahara ~]$ ls fake-file.txt
ls: cannot access 'fake-file.txt': No such file or directory
```
Since the file does not exist, `ls` has nothing to do and throws and error.

## Displaying files
The `cat` command is used to display the contents of a file. 

* Running `cat` with no arguments does something interesting; it takes input through `stdin`, and once some input is given by the user, it prints out the input. This continues until the user exists the loop. <br>
For example, when our current directory is `/home`, running `cat` with no arguments allows us to input strings:

Any input given is immediately printed out again (even newlines; the large gap is simply a newline given by the user and a newline printed out by `cat`). This is not an error and is instead a behavior of terminal itself; running certain commands with no arguments will begin a loop that reads from `stdin`.

* Running `cat` with a directory as an argument throws an error. <br>
When our working directory is `/home` and it contains a folder called `lecture1`, running `cat lecture1` prints:

```
[user@sahara ~]$ cat lecture1
cat: lecture1: Is a directory
```
Since the purpose of `cat` is to print the contents of a file, it needs a valid file as input, and thus providing a directory throws an error.

* Running `cat` with a valid file displays the contents of the file in the terminal window. <br>
For example, when our current directory is `/home` and it contains a file named `hello.txt` with the contents "Hello everyone!", running `cat hello.txt` gives:
```
[user@sahara ~]$ cat hello.txt
Hello everyone!
```
This is because `cat` simply takes the file given as an argument and prints its contents. When the file does not exist, however, `cat` throws an error:
```
[user@sahara ~]$ cat fake-file.txt
cat: fake-file.txt: No such file or directory
```
Since `fake-file.txt` does not exist, `cat` cannot print its contents, so it throws an error.







