# Bash Scripting for Beginners
<img width="1200" height="670" alt="bash" src="https://github.com/user-attachments/assets/171772d4-a65c-451a-acc9-240bda83967e" />


Shell scripting is an important part of process automation in Linux. Scripting helps you write a sequence of commands in a file and then execute them.

This saves you time because you don't have to write certain commands again and again. You can perform daily tasks efficiently and even schedule them for automatic execution.


The applications and uses of scripting are numerous, so let's dive in.

In this article, you will learn:

- What is a bash shell?

- What is a bash script and how do you identify it?

- How to create your first bash script and execute it.

- The basic syntax of shell scripting.

- How to see a system's scheduled scripts.

- How to automate scripts by scheduling via cron jobs.

The best way to learn is by practicing. I highly encourage you to follow along here [kyberkernel parrot ](https://github.com/KyberKernel/cyber-course-portfolio/tree/main/unit-1-presecurity/Parrot%20OS%20Live%20USB%20With%20Encrypted%20Persistence%2C%20and%20Nuke%20Password). You can access a running Linux shell within minutes.


# Introduction to the Bash Shell
The Linux command line is provided by a program called the shell. Over the years, the shell program has evolved to cater to various options.

Different users can be configured to use different shells. But most users prefer to stick with the current default shell. The default shell for many Linux distros is the GNU Bash

When you first launch the shell, it uses a startup script located in /home/user/.bashrc file which allows you to customize the behavior of the shell.

When a shell is used interactively, it displays a $ when it is waiting for a command from the user. This is called the shell prompt.
```bash
[username@host ~]$
```


If shell is running as root, the prompt is changed to #. The superuser shell prompt looks like this:

```bash
[root@host ~]#
```


Bash is very powerful as it can simplify certain operations that are hard to accomplish efficiently with a GUI. Remember that most servers do not have a GUI, and it is best to learn to use the powers of a command line interface (CLI).

# What is a Bash Script?

bash script is a series of commands written in a file. These are read and executed by the Bash interpreter. The interpreter executes line by line. Anything you'd normally type into the terminal can go in a script, plus you get variables, loops, conditions, etc. Bash is both the shell you're typing into and a scripting language in its own right.

### How Do You Identify a Bash Script?

File extension of ```.sh```

By naming conventions, bash scripts end with a ```.sh``` However, bash scripts can run perfectly fine without the``` .sh ```extension. it's just a convention so people know it's a shell script.

### Scripts start and identified with a shebang.

```bash
#!/bin/bash
```

Shebang is a combination of bash``` # ```and bang``` ! ```followed by the bash shell path. That first line tells the system which interpreter to run the file with and If you skip it and you are using bash script file, the script can still work cuz the terminal use the bash interpreter to execute the files by default.

## There are three ways to execute a Bash script file
- ### Executing the file from its location after adding execute permission.

Navigate to the script file location. I’ll use the home folder as an example here : ```/home/user/script.sh```
Open the terminal. By default, it should open in your home folder, which you can identify by looking for the``` ~ ```symbol```[username@host ~]$```. If you do not see it for some reason, use the``` cd ```command without any additional options. This will take you to your home folder.

Then create a script file there using the text editor  ```nano ```, which is the default text editor in most Linux distributions.

```bash
nano script.sh
```
Then nano will open an empty text file. On the first line, write the shebang. On the second line, write the simple echo command, followed by double quotation marks containing: `Hello, welcome to the script`.

To save the file, press `Ctrl + X`, then `Y`, and press `Enter`.

```bash
#!/bin/bash
echo "Hello, welcome to the script"
```
Now check the file’s permissions by running the command.

```bash
ls -l
```

You will find the script file with the following permissions: `-rw-rw-r--`.
Each group of three characters represents someone on the system. The first three are for the `User`, the second three are for the `Group`, and the third three are for` Others`.

<img width="450" height="300" alt="1-file-permission-767x474-2923469870" src="https://github.com/user-attachments/assets/039b3f86-0793-4b78-b7d8-65f00e334e39" />

To execute the file, you need to have execute permission. There are two ways to add execute permission.
- ### Add a specific permission for a specific class on the system.

We do that by running the ```chmod``` command, specifying the class for which we want to add or remove a permission, followed by the file name, and then pressing Enter. If you are the owner of the file you can change all permission bits for the `owner`, `group`, and `others` without `sudo`. However, you generally cannot change the file’s owner or group without elevated privileges


```bash
chmod u+x script.sh
```

- ### Add or remove permissions for all classes on the system with one command.

We do that by running the ```chmod``` command Followed by numbers that are translated into specific permissions, and then followed by the file name, and then pressing Enter.
Here is an example of adding execute permission for the owner class while keeping the other classes’ default permissions unchanged.


```bash
chmod 764 script.sh
```

And here is a cheatsheet of the permissions and the numbers that represent them.

<img width="600" height="300" alt="chmod-reference-table-354684197" src="https://github.com/user-attachments/assets/115bfbfe-003b-43e3-8ea3-4cf6ba6f296b" />


So, based on what we wrote, we gave execute permission to the owner, kept read and write permissions for the group, and kept read permission for others `-rwxrw-r--`

Now, to execute the script, we navigate to its location and press Enter. Since the script is in the home folder and we are already in the home folder, we run the command like this:

```bash
./script.sh
```

The ```./``` represents the location where I am currently and I am currently in ```/home/user/``` . and You can verify where you at on the system by running the command  ```pwd ```

The script will run, and you will see on the screen```Hello, welcome to the script```

- ### Executing the file from its location without execute permission.

As we know by now, the terminal uses the Bash interpreter to execute files by default. We can execute the script by simply calling the interpreter, followed by the file we want it to execute. The interpreter reads the file and then executes it, so you need to have read permission to perform this step.

```bash
bash script.sh
```

- ### Executing the script by typing only its name.

Before I tell you how to do that we need to understand how the shell searches for and executes commands. 

The shell uses the ```environment variable ``` ```$PATH``` that stores a list of directories where the shell looks for executable commands.

External commands are binary executable files that run from their locations. Built-in commands are built directly into the shell itself.

Think of the shell as a helper that receives the commands you type and finds the correct program to run.

Imagine you type:

```bash
ls
```

The shell does something like this:

It asks, Is ```ls``` one of my built-in commands?

If not, it looks at ```$PATH```.

- ```$PATH``` is like a list of folders``` /usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games ```to list yours you can run the command 

```bash
echo $PATH
```

The shell searches those folders one by one:

```bash
/usr/local/bin/ls
/usr/bin/ls
/bin/ls
```
When it finds the ls program, it runs it.

If it cannot find it, you see:

```bash
command not found
```

So, to run a simple command like ```ls```, you do not need to write its location every time, such as``` /usr/bin/ls```. You can just type``` ls```, and the command will execute.

This happens because the location of``` ls``` is included in the``` $PATH```variable.

And just like that you can also include your script’s location in the```$PATH ```variable, and the shell will execute it as soon as you type the script’s name.

To do that, we need to be abit careful here and modify ```$PATH ```only for the current user, not for the entire Linux distribution.

We will modify the ```.bashrc ```file and add our directory to the ```$PATH``` list so that the shell will look there for executables and execute our script.

To do that, let’s first store our script into a directory so Let’s create that directory and move our script into it.

```bash
mkdir scripts
```

And to move our script there we use the command ```mv```
- The command ```mv``` has two main use cases
- 1- Move a file or directory to another location ```mv SOURCE DESTINATION```
- 2- Rename a file or directory ```mv CurrentName NewName```

```bash
mv script.sh scripts
```
Now let’s modify our ```.bashrc``` file.
run the command ```ls -a``` to list everything, Open your Bash configuration file by using ```nano```

```bash
nano .bashrc
```

Add this line at the bottom 

```bash
export PATH="$HOME/scripts:$PATH"
```
- ```export``` makes a shell variable available to child processes started by the parent shell.

Save and exit Nano
Press `Ctrl+O`
Press `Enter`
Press `Ctrl+X`
Reload `.bashrc`

```bash
source .bashrc
```
Now you can run your script by simply typing its name in the terminal

```bash
script.sh
```
- Remember, you need to have execute permission to execute the script this way

# The Basic Syntax of Bash Scripting
Just like any other programming language, bash scripting follows a set of rules to create programs understandable by the computer. In this section, we will study the syntax of bash scripting.

- # Variables
## How to create variables
We can create a variable by using the syntax ```variable_name=value```. To get the value of the variable, add``` $ ```before the variable.
```bash
#!/bin/bash
# A simple variable example
hello=Moro
name=Dimi
echo $hello $name
```
- variables Naming rules:
- 1 - They can contain letters:``` a-z or A-Z```
- 2 - They can contain numbers:``` 0-9```
- 3 - They can contain underscores:``` _```
- What You Can't Do
- 1 - They cannot contain hyphens:``` -```
- 2 - They cannot start with a number

# There are 3 types of variables
- ## Shell variables
- ## Environment variable
- ## Special variables

## Shell variables
A shell variable is a variable created and managed by the current shell. When created in a script, it is available to that script while it is running. It is not automatically passed to child processes unless it is exported.
And there are two types of this variable.

- ### 1 - Script-level variable
- ### 2 - Function-level local variable

## Script-level variable
A script-level variable is a variable set anywhere in the script (outside a function, or inside one without `local`), and it can be used by other parts of the script, including functions.

## Function-level local variable
A function-level local variable is a variable created inside a function using the  `local` keyword.
It is only accessible within that function and does not affect a variable with the same name outside that function.
```bash
#Script-level variable
name="Granhilde"

#Function
kyber() { 
#Function-level Local Variable
    local name="Justia" 
    echo "Moikka $name"
}
#Calling the Function by its name
kyber
#Calling the Script-level variable by using $
echo "Terve $name"
```
Output:

```bash
Moikka Justia
Terve Granhilde
```
- ### → What is the function ?
It is named block of commands that you can create once and execute (call) whenever you need it.

Instead of writing the same commands multiple times, you put them inside a function and call the function by its name.

Basic syntax
```bash
function_name() {
    # commands
}
```
For example:
```bash
kyber() {
    echo "Moikka!"
}
```
Here:

```kyber``` → the function name
```()``` → indicates that you are creating a function
```{ ... }``` → contains the commands that belong to the function.

The function doesn't execute when you create it, You execute it by calling its name:
```bash
kyber
```
Output
```bash
Moikka!
```
- Why we use or need functions?

Functions are useful for

→ Reusing code

→ Organizing a script

→ Avoiding repetition

→ Making scripts easier to read and maintain

## Environment variables
Environment variables are variables within the system environment. They are used to configure the system’s behavior and allow users to customize their systems.

Environment variables have global scope, so they are accessible across the system and can also be accessed inside scripts.

Shell variables are accessible only within the script. They are accessible only within the scope where they were created.

If I create a variable in the parent process, I cannot access it from a child process, even if that child process was created by the parent process.

- ### What is parent & child process?
To simplify this topic if i open the terminal the shell I opened is a process and it's a parent process.

When I execute a command inside it, the execution process is called a child process.

for example we have the command ```sh``` opens a subshell.

A subshell is a child process inside the parent process, which runs inside the currently running shell.

If i created a variable inside the parent shell and opened a sub shell which is child shell and called that variable i will get noting.

But if i called an environment variable inside a sub shell i will get output because the Environment variables are inherited by child processes.

<img width="600" height="600" alt="download" src="https://github.com/user-attachments/assets/6adec49e-8b84-4d29-a387-f4ce866f5cba" />

The ```export``` command exports a variable as an environment variable and makes it available to child processes. In other words, by using the ```export``` command, I make my shell variable accessible to child processes.

Environment variables use the export command and are accessible throughout the system. Their purpose is to configure and customize the system. Most of the time, they are defined in configuration files.

The purpose of shell variables is to be used inside a script, making the script more usable and easier to develop.

The ```export``` command makes a variable accessible to the parent and child processes of the process where I used the command. It does not make the variable ```system-wide```.

The ```Bash``` configuration file is ```.bashrc```, and it is used by the ```Bash shell ```for the ```current user```.

Variables can be used to call and execute programs that exist on the system. For example, if I want to call the``` Wireshark ``` program from the terminal, I can call it from it's path ```/usr/bin/wireshark```.

Or call it by just typing its name ``` Wireshark ``` and the word ``` Wireshark ``` is a variable define as ```WIRESHARK=/usr/bin/wireshark``` and the shell will use the ```Environment variables``` ```$PATH``` to search for and execute commands inside the ```$PATH``` directory's.

Environment variables are usually written in uppercase letters, such as ABCDEFG.

Examples of some Environment variables


```bash
$PATH	Where Bash looks for commands
$HOME	Your home directory
$USER	Your username
$SHELL	Your default shell
$PWD	Your current directory
$OLDPWD	Your previous directory
$HOSTNAME	Your computer's hostname
$TERM	Your terminal type
$LANG	Your language/locale
$EDITOR	Your preferred text editor
$TMPDIR	Directory for temporary files
$SHLVL	Current Bash nesting level
$BASH_VERSION	Your Bash version
```

## Special variables

Special variables are built-in Bash variables that automatically contain useful information about the current shell, script, arguments, processes, or the result of commands.

You don't normally create these variables yourself, the Bash sets their values automatically.

And there are two types of this variable.

- ### 1 - Special variables
- ### 2 - Positional Parameters

## Special variables

Bash, special variables are built-in variables that give you information about the shell, script, arguments, processes, and command results.

Examples of Special variables
```bash
$0	Name/path of the script
$#	Number of arguments
$@	All arguments, treated as separate arguments
$*	All arguments, treated as one string when quoted
$?	Exit status of the last command
$$	Process ID (PID) of the current Bash process
```

## Positional Parameters

Positional parameters allow you to pass arguments to a Bash script and access them inside the script.

Examples of Positional Parameters
```bash
$1, $2, $3...	First, second, third, etc. arguments

```
```bash
./script.sh varia vantaa

#Inside the script:

#!/bin/bash

echo "Script name: $0"
echo "First argument: $1"
echo "Second argument: $2"
echo "Number of arguments: $#"
echo "All arguments: $@"
echo "Process ID: $$"
echo "Exit status: $?"

```

Output:

```bash
Script name: ./script.sh
First argument: varia
Second argument: vantaa
Number of arguments: 2
All arguments: varia vantaa
Process ID: 12343
Exit status: 0

```
What happened?

When you ran:

```./script.sh varia vantaa```

Bash assigned:
```bash
$0  → ./script.sh
$1  → varia
$2  → vantaa
$#  → 2
$@  → varia vantaa
$$  → 12343
$?  → 0
```
The important idea is:
```bash
./script.sh varia vantaa
             ↑     ↑
            $1    $2
```
So the arguments you give to the script become positional parameters.

- ## What is the arguments?

Arguments are values passed to a command or script when it is executed.

allow scripts to receive information from the user when the script starts. 

Bash provides positional parameters such as $1, $2, $3, etc.

For example:
```bash
./script.sh hello world
```

Here, hello is an argument passed to script.sh.

Inside the script:
```bash
#!/bin/bash
echo "First argument: $1"
echo "Second argument: $2"
```
We will use arguments more later when we learn how to make decisions with```if statements.```
But before we get there, we need to learn how to make our scripts more interactive and useful, we need a way for the script to receive input and make decisions based on that input.

That’s why we’re now going to dive into User Input and While Loops then into Conditional Statements
```bash
read
   ↓
while loops
   ↓
if / elif / else
   ↓
case
```
# User Input and While Loops







