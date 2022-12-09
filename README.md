#ALX SIMPLE SHELL PROJECT
Project to be done in teams of 2 people (your team: Nnenna Udefi, Lawrence Tsekohol)
##PROJECT WAS DONE USING
C language, Shell and Betty Linter
##DESCRIPTION
Shell is a UNIX command line interpreter that provides a command line user interface for Unix-like operating systems. It gathers input from you and executes programs based on that input.
##Tasks
### 0. Betty would be proud
Files: README.md, AUTHORS, man_1_simple_shell, help_files
###1. Simple shell 0.1
mandatory
Write a UNIX command line interpreter.

Usage: simple_shell
Your Shell should:

* Display a prompt and wait for the user to type a command. A command line always ends with a new line.
* The prompt is displayed again each time a command has been executed.
* The command lines are simple, no semicolons, no pipes, no redirections or any other advanced features.
* The command lines are made only of one word. No arguments will be passed to programs.
* If an executable cannot be found, print an error message and display the prompt again.
* Handle errors.
* You have to handle the “end of file” condition (Ctrl+D)
You don’t have to:

* use the PATH
* implement built-ins
* handle special characters : ", ', `, \, *, &, #
be able to move the cursor
* handle commands with arguments
execve will be the core part of your Shell, don’t forget to pass the environ to it…
File: shell_loop.c
### 2. Simple shell 0.2
* Handle command lines with arguments
File: main.c
### 3. Simple shell 0.3
* Handle the PATH
* fork must npt be called if the command doesnt't exist
### Simple shell 0.4
* Implement the exit built-in, that exits the shell
* Usage: exit
* You don’t have to handle any argument to the built-in exit
File: builtin.c
### 5. Simple shell 1.0
mandatory
Simple shell 0.4 +

* Implement the env built-in, that prints the current environment
File: getenv.c, getinfo.c
### 6. Simple shell 0.1.1
#advanced
Simple shell 0.1 +

* Write your own getline function
* Use a buffer to read many chars at once and call the least possible the read system call
* You will need to use static variables
* You are not allowed to use getline
You don’t have to:

* be able to move the cursor
File: getLine.c, getenv.c

###7. Simple shell 0.2.1
#advanced
Simple shell 0.2 +

You are not allowed to use strtok
File: string2.c
### 8. Simple shell 0.4.1
#advanced
Simple shell 0.4 +

* handle arguments for the built-in exit
Usage: exit status, where status is an integer used to exit the shell
File: builtin.c
### 9. setenv, unsetenv
#advanced
Simple shell 1.0 +

Implement the setenv and unsetenv builtin commands

setenv
* Initialize a new environment variable, or modify an existing one
* Command syntax: setenv VARIABLE VALUE
Should print something on stderr on failure
unsetenv
* Remove an environment variable
Command syntax: unsetenv VARIABLE
* Should print something on stderr on failure
File: environ.c
### 10. cd
#advanced
Simple shell 1.0 +

Implement the builtin command cd:

Changes the current directory of the process.
* Command syntax: cd [DIRECTORY]
* If no argument is given to cd the command must be interpreted like cd $HOME
* You have to handle the command cd -
* You have to update the environment variable PWD when you change directory
man chdir, man getcwd
File: builtin.c

### 11. ;
#advanced
Simple shell 1.0 +

* Handle the commands separator ;
### 12. && and ||
#advanced
Simple shell 1.0 +

* Handle the && and || shell logical operators
### 13. alias
#advanced
Simple shell 1.0 +

Implement the alias builtin command
Usage: alias [name[='value'] ...]
* alias: Prints a list of all aliases, one per line, in the form name='value'
* alias name [name2 ...]: Prints the aliases name, name2, etc 1 per line, in the form name='value'
* alias name='value' [...]: Defines an alias for each name whose value is given. If name is already an alias, replaces its value with value
File: builtin1.c

### 14. Variables
#advanced
Simple shell 1.0 +

* Handle variables replacement
* Handle the $? variable
* Handle the $$ variable
File: vars.c
### 15. Comments
#advanced
Simple shell 1.0 +
* Handle comments (#)
File: Helper1.c
### 16. File as input
#advanced
Simple shell 1.0 +

Usage: simple_shell [filename]
* Your shell can take a file as a command line argument
* The file contains all the commands that your shell should run before exiting
* The file should contain one command per line
* In this mode, the shell should not print a prompt and should not read from stdin
## Invocation
Usage: hsh [filename]
To invoke hsh, compile all .c files in the repository and run the resulting executable.

hsh can be invoked both interactively and non-interactively. If hsh is invoked with standard input not connected to a terminal , it reads and executes received commands in order.

Example:

$ echo "echo 'hello'" | ./hsh
'hello'
$
If hsh is invoked with standard input connected to a terminal (determined by isatty(3)), an interactive shell is opened. When executing interactively, hsh displays the prompt $ when it is ready to read a command.

Example:

$./hsh
$
Alternatively, if command line arguments are supplied upon invocation, hsh treats the first argument as a file from which to r ead commands. The supplied file should contain one command per line. hsh runs each of the commands contained in the file in or der before exiting.

Example:

$ cat test
echo 'hello'
$ ./hsh test
'hello'
$
### How hsh works
* Prints a prompt and waits for a command from the user
* Creates a child process in which the command is checked
* Checks for built-ins, aliases in the PATH, and local executable programs
* The child process is replaced by the command, which accepts arguments
* When the command is done, the program returns to the parent process and prints the prompt
* The program is ready to receive a new command
* To exit: press Ctrl-D or enter "exit" (with or without a status)
* Works also in non interactive mode
