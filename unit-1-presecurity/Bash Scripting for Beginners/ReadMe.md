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

- How to use variables and accept user input

- How to use conditional statements and loops

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
- ### → Add a specific permission for a specific class on the system.

We do that by running the ```chmod``` command, specifying the class for which we want to add or remove a permission, followed by the file name, and then pressing Enter. If you are the owner of the file you can change all permission bits for the `owner`, `group`, and `others` without `sudo`. However, you generally cannot change the file’s owner or group without elevated privileges


```bash
chmod u+x script.sh
```

- ### → Add or remove permissions for all classes on the system with one command.

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

#Also this mean

bash /home/username/script.sh

#OR

bash /$HOME/script.sh

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
A variable is a named container used to store data, such as text or a number, so it can be used later.

## How to create variables
We can create a variable by using the syntax ```variable_name=value```. And to print a variable’s value, add``` $ ```before the ```variable_name```to reference it.
```bash
#!/bin/bash
# A simple variable example
hello=Moro
name=Dimi
echo $hello $name
```
Output:

```bash
Moro Dimi
```
- ### Variables Naming Rules:
A variable name can contain:
- 1 - Upper/Lowercase letters:``` a-z or A-Z```
- 2 - Numbers:``` 0-9```
- 3 - Underscores:``` _```

 A variable name cannot:
- 1 - Start with a number
- 2 - Contain spaces
- 3 - Contain special characters ```-  +  =  .  ,  /  \  @  #  !  $  %  ^  &  *  (  )  [  ]  {  }  :  ;  ?  '  "  <  >  |```


# There are 3 types of variables
- ## Shell variables
- ## Environment variable
- ## Special variables

## Shell variables
A shell variable is a variable created and managed by the current shell. When created in a script, it is available only within that script's scope while it is running.

And there are two types of this variable.

- ### 1 - Script-level variable
- ### 2 - Function-level local variable

## Script-level variable
A script-level variable is a variable set anywhere in a script that remains accessible to all parts of the script, including functions, unless explicitly overridden (changed) or unset (removed).

```bash
#!/bin/bash

#Script-level variable
name="Granhilde"
echo "Terve $name"
```
Output:

```bash
Terve Granhilde
```

## Function-level local variable
A function-level local variable is a variable created inside a function using the  `local`  keyword.
It is only accessible within that function and does not affect a variable with the same name outside that function.
```bash
#!/bin/bash

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
It is named block of commands that you can create once and execute whenever you need it.

Instead of writing the same commands multiple times, you put them inside a function and execute them by calling the function name.

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

Environment variables have global scope, so they are accessible across the system and can also be accessed inside scripts and they are inherited by child processes.

- ### What is parent & child process?
To simplify this topic if i open the terminal the shell I opened is a process and it's a parent process.

When I execute a command inside it, the execution process is called a child process.

for example we have the command ```sh``` opens a subshell.

A subshell is a child process inside the parent process, which runs inside the currently running shell.

If i created a variable inside the parent shell and opened a sub shell which is child shell and called that variable i will get noting.

But if i called an environment variable inside a sub shell i will get output because the Environment variables are inherited by child processes.

<img width="600" height="600" alt="download" src="https://github.com/user-attachments/assets/6adec49e-8b84-4d29-a387-f4ce866f5cba" />

The ```export``` command converts a``` shell variable ```into an ```environment variable```. This makes the variable available to ```child processes``` started by the``` current shell```. It does not make the variable ```system-wide```.

- To make an environment variable available to all users, an administrator can define it in a``` system-wide configuration file```. Common files include

- ``` /etc/environment``` a system-wide configuration file used to define environment variables for all users. The system reads these assignments and makes the variables available as environment variables, so``` export ```is not required 

- ``` /etc/profile``` a system-wide shell configuration file. It is read when users start a login shell and can contain ```shell commands```,``` aliases```,``` functions```, and ```exported environment variables```.


Environment variables are used to configure and customize the behavior of the shell and other programs. They are usually created with the```  export```  command and inherited by child processes.

And often defined in configuration files such as```  ~/.bashrc``` .

- The```  ~/.bashrc ``` file is a Bash configuration file for the ``` current user``` . Bash reads this file when an```  interactive terminal starts``` . And it can contain variables, aliases, functions, and other shell settings.

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
./script.sh hello
```

Here, hello is an argument passed to ```script.sh```.

Inside the script:
```bash
#!/bin/bash
echo "First argument: $1"
echo "Second argument: $2"
```
We will use arguments more later when we learn how to make decisions with```if statements.```

But before we get there, we need to learn how to make our scripts more interactive and useful, we need a way for the script to receive input and make decisions based on that input.

That’s why we’re going to dive into.

# User Input (READ)
The read command allows a script to receive information typed by the user while the script is running and stores that input in a variable.
```bash
#!/bin/bash

echo "What is your name?"
read name  # Stores user input in the variable 'name'

echo "Hello, $name!"
```
If we look at that command, we can see that I included ```echo``` for the text I want to display. However, if I want to develop a program and insert ```echo``` on every line where I want something to appear on the screen, the code will become longer, and troubleshooting will become more difficult. I may also fall into something called``` hard-coding```.

That is why the ```read``` command provides a solution. We can add options to it, and each option performs a ```specific function```, making our code cleaner and easier to read.

For example, we can use the``` -p``` option to display a ```prompt```.

```bash
#!/bin/bash

read -p "What is your name?: " name
echo "Hello $name."

```
output:

```bash

What is your name?: Kyber
Hello  Kyber
```

We have another option. For example, if I want to enter a password and do not want a stalker to look at my screen and see what I am typing.

we can use the silent option ```-s``` to hide the user’s input from being displayed on the screen.

We can also combine the options together.

```bash
#!/bin/bash

read -s -p "Enter your password: " password

echo "Password received."

```
output:

```bash
Enter your password:
Password received.
```

What if we create a program that reads Windows file paths and needs to use the backslash (\)? 

By default, the read command treats the backslash as an escape character, so it may not display the backslashes correctly.

We can use the ```-r ```option to prevent this from happening.


```bash
#!/bin/bash

read -r -p "Enter a windows path: " path
echo "You entered: $path"

```
output:

```bash
Enter a path: C:\Users\Kyber
You entered: C:\Users\Kyber
```
What if we want to set a time limit for the prompt and give the user a specific amount of time to enter their input? 

If the input is not received within that time, the prompt will close. 

We can use the ```-t ``` Time out option to do this.

```bash
#!/bin/bash

read -t 5 -s -p "Enter your password within 5 seconds : " password

echo "Password received."

```
output:

```bash
Enter your password within 5 seconds:
Password received.
```

What if we want the user to enter text and be able to edit it before confirming it?

For example, the user can use the arrow keys to move through the text and edit it

In that case, we use the``` -e ```option.

```bash
#!/bin/bash

read -e -p "Enter a command: " command
echo "You entered: $command"

```
output:

```bash
Enter a command: ls -l
You entered: ls -l
```

We can also provides initial text that appears automatically in the input area. The user can edit this text before pressing ```Enter```.

In that case, we use the``` -i ```option and The``` -i ```option must be used together with``` -e```, because``` -e``` enables keyboard editing.


```bash
#!/bin/bash

read -e -i "Hello" -p "Edit the message: " message

echo "Final message: $message"

#command will be displayed as Edit the message: Hello
```
output:

```bash
Edit the message: Hello, Dimi
Final message: Hello, Dimi
```

We can also tell the prompt to stop reading input from the user after they press a specific key. 

By default, read stops when the user presses Enter, but we can change this behavior. 

To do that, we use the ```-d``` option.

```bash
#!/bin/bash

read -d "," -p "Enter text followed by a comma: " text
echo
echo "You entered: $text"
```
output:

```bash
Enter text followed by a comma: Hello,←
You entered: Hello
```


What if we want to stores multiple input values in an indexed array. Each value is assigned an index number, starting from 0, so we can access the values individually.

In that case, we use the``` -a ```option.


```bash
#!/bin/bash

read -a names -p "Enter three names: "
echo "First name: ${names[0]}"
echo "Second name: ${names[1]}"
echo "Third name: ${names[2]}"
```
output:

```bash
Enter three names: Dimi Roni Karita
First name: Dimi
Second name: Roni
Third name: Karita

#The values must be separated by spaces. The first value is stored at index 0, the second at index 1, and the third at index 2
```
Here is a quick list of some of the most commonly used options in Bash scripting with the read command.
```bash

-p	Displays a prompt before waiting for the user’s input.
-s	Hides the user’s input while they are typing. It is commonly used for passwords.
-r	Prevents backslashes (\) from being treated as escape characters. It is recommended when reading ordinary text.
-t	Sets a time limit, in seconds, for entering input.
-a	Stores the input as separate elements in an indexed array.
-e	Enables keyboard editing while entering input. It allows features such as using the arrow keys to move through the text.
-i	Provides initial text that the user can edit. It must be used with -e.
-d	Uses a specified character as the delimiter instead of Enter. The input ends when that character is entered.
-u	Reads input from a specific file descriptor instead of standard input.
-n	Reads a specific number of characters and continues immediately after that number is entered.
```

And finally what if we want to ask the user whether they really want to do something and give them the choice of Y or N?

If we want the action to be taken immediately after they press a key, without pressing``` Enter```

we can use the``` -n ```option the the number of inputs we want to insert.

```bash
#!/bin/bash

read -n 1 -p "Do you want to continue? (Y/N): " answer

if [[ "$answer" == "Y" || "$answer" == "y" ]]; then
    echo "Continuing..."
else
    echo "Exiting..."
fi
```
output:

```bash
Do you want to continue? (Y/N): Y
Continuing...

Do you want to continue? (Y/N): N
Exiting...
```


As we can see in the last example, we used something called a logical choice, in other words, an ```if statement```.

# What is ```if statement```?
The if statement in Bash is used to execute a block of code only if a certain condition is``` true```.

It’s the most basic way to make decisions in shell scripting.

```bash
if [ condition ]; then
    # Code to run if condition is true
fi
```
If I want to add more than one condition, I can use``` elif ```and ```else```, and the command will look like this:

```bash
if [ condition ]; then
    # Code to execute if the condition is true
elif [ condition2 ]; then
    # Code to execute if the second condition is true
else
    # Code to execute if all conditions are false
fi
```

If the condition after ```if ```is true, Bash executes the code under ```then```.

If the condition is``` false```, Bash checks the condition after``` elif```. You can use multiple``` elif``` statements if you want to check more conditions.

If all the conditions are``` false```, Bash executes the code under ```else```.

The ```fi``` keyword marks the end of the ```if``` statement.

### Let’s talk about comparison operators in Bash, which are used to compare values.

There are three main types:

- String comparisons
- Numeric comparisons
- File comparisons

## String comparisons

string comparisons are used to check if two strings are equal, not equal, empty, or match a pattern. They are essential for decision-making in scripts.

### String Comparison Operators

```bash

# Equality
=   # Equal to
==  # Equal to (preferred in [[ ]])
!=  # Not equal to

# Less Than
<   # Less than (lexicographical)
<=  # Less than or equal to (lexicographical)

# Greater Than
>   # Greater than (lexicographical)
>=  # Greater than or equal to (lexicographical)

# Empty/Non-empty Check
-z   # Is empty?
-n   # Is not empty?

```
## Numeric comparisons

Numeric comparisons are used to check if numbers are equal, not equal, greater, less, etc... and They are essential for decision-making in scripts.

### Numeric comparisons Operators

```bash
# Equality
-eq   # Equal to (=)
-ne   # Not equal to (!=)

# Less Than
-lt   # Less than (<)
-le   # Less than or equal to (<=)

# Greater Than
-gt   # Greater than (>)
-ge   # Greater than or equal to (>=)

```

## File comparisons

File comparison operators in Bash are used to check various file properties such as existence, type, permissions, and modification time.

These operators are typically used within conditional statements to control the flow of scripts based on file attributes.

### File comparisons Operators

```bash
-e   # Exists (file/directory/symlink)
-f   # Exists AND is a regular file (not directory/symlink/special)
-d   # Exists AND is a directory
-L   # Exists AND is a symbolic link
-h   # Exists AND is a symbolic link (same as -L)
-r   # Exists AND is readable
-w   # Exists AND is writable
-x   # Exists AND is executable
-s   # Exists AND is not empty
-k   # Exists AND has sticky bit set (directory protection)
-c   # Exists AND is a character device node
-b   # Exists AND is a block device node
-nt # File1 is newer than File2
-ot # File1 is older than File2
-ef # Both files are hard links to the same inode
```

## The``` ! ```Negation Operator

In Bash scripting, the ```! ``` symbol is used as a negation operator. It means ```“NOT” ```and reverses the result of a command or condition.

For example:
```bash
if ! [[ -f "file.txt" ]]; then
    echo "File does not exist"
fi
```
In this example ```-f "file.txt" ``` checks whether ```file.txt``` ```exists```. The ```! ```reverses the result, so the``` then ```part runs when the file ```does not exist```.

# Combining Conditions
Allow you to combine multiple conditions using AND, OR, and parentheses. These operators help you make decisions based on whether one or more tests are true.

### Combining Conditions Operators
```bash
&& means AND : both conditions must be true.
|| means OR  : at least one condition must be true.
-a means AND inside [ ].
-o means OR  inside [ ].
(  )  Parentheses are used to group conditions and control which condition is evaluated first.
```
For Example: 
```bash
if [ -n "$pass" ] && [ "$pass" = "password" ]; then
    echo "Password is valid"
fi
```
Example using parentheses
```bash
if [[ "$a" == "yes" && ( "$b" == "yes" || "$c" == "yes" ) ]]; then
    echo "Condition is true"
fi

```
This means
```bash
Condition A AND (Condition B OR Condition C)

The parentheses group these conditions

Condition B OR Condition C

That group is evaluated first. Then its result is combined with Condition A using &&.

```
As you can see in the previous example we used Double Square Brackets and thats made our script looks cleaner but before that

# What is Double Square Brackets [[ ... ]] in Bash

The double square brackets ```[[ ... ]]```, are used to test conditions in Bash. They allow you to combine multiple conditions in one test expression, making the code shorter and easier to read.

Example using Double Square Brackets
```bash
read -p "Provide your age, country, and membership: " age country membership

age=18
country="fi"
membership="premi"

if [[ ( "$age" -ge 18 && "$country" == "fi" ) || "$membership" == "premi" ]]; then
    echo "Welcome in"
else
    echo "Access denied"
fi
```
This means

(age is at least 18 AND country is fi)
OR
membership is premi

The first condition to check is the age and country if the results false then check the membership if results true then enter the site if not then print access denied 

Same Example using singel Square Brackets
```bash
if \( [ "$age" -ge 18 ] && [ "$country" = "fi" ] \) || [ "$membership" = "premi" ]; then
    echo "Welcome in"
else
    echo "Access denied"
fi

```
As you can see, the single bracket version is longer and uses more separate condition checks.
```bash
[ "$age" -ge 18 ]
[ "$country" = "fi" ]
[ "$membership" = "premi" ]
```

With double brackets, several conditions can be written inside one condition check
```bash
if [[ ( $age -ge 18 && $country == fi ) || $membership == premi ]]; then
    echo "Welcome in"
fi
```
The double brackets make the code shorter because you do not need a separate``` [ ... ] ```for every condition.

- It is safer, handles errors better, and is easier to use.

- I do not need to add quotation marks ```"$var" ```between the values.

- Logical operators are included.

- I can change the order of the logic by adding parentheses``` (  ) ```around the condition I want to process first.

Okay, now we know about ``` arguments``` and ```logical operations``` in Bash, and how to insert``` user input```. We need to create an interface for the program we want to code.

To do that, we need to talk about ``` loops ```in Bash and how they work.

So, we are going to dive in loops now.

# Loops

The two main loops in Bash are the ```while loop ```and the ```for loop```.

## While loop

A ```while ```loop repeats commands while a condition is true.

When the condition becomes false, the loop stops.

```bash
while condition
do
    commands
done
```
Example:
```bash
#!/bin/bash

myvar=1

while [[ $myvar -le 10 ]]
do
    echo "$(date +"%Y-%m-%d_%H-%M-%S"): $myvar"
    myvar=$(( myvar + 1 ))
    sleep 2
done
```
Output:
```bash
2026-09-13_14-30-00: 1
2026-09-13_14-30-02: 2
2026-09-13_14-30-04: 3
2026-09-13_14-30-06: 4
2026-09-13_14-30-08: 5
2026-09-13_14-30-10: 6
2026-09-13_14-30-12: 7
2026-09-13_14-30-14: 8
2026-09-13_14-30-16: 9
2026-09-13_14-30-18: 10

```
Let’s go ahead and see what happened

As you can see, the script counts from 1 to 10. How does it work?

At the top, we have the shebang:
```bash
#!/bin/bash
```
This tells the system to use Bash to run the script

Next, we create a variable called``` myvar ```and set its value to 1:

```bash
myvar=1
```
After that, we start a while loop. We use the keyword``` while```, followed by a condition:

```bash
while [[ $myvar -le 10 ]]
```
This condition checks whether myvar is less than or equal to 10.

At the beginning, myVar is equal to 1, so the condition is true. While the condition is true, the commands inside the loop are executed.

First, the script prints the current value of myvar and the current date and time using Command Substituiton:
```bash
echo "$(date +"%Y-%m-%d_%H-%M-%S"): $myvar"
```
- ## What is Command Substituiton
- It's capture a command's output and use it as a value
```bash
current_user=$(whoami)
echo "Hello, $current_user"
echo "Today is $(date)"
```
```bash
## Date formatting
| Specifier | Meaning |
|-----------|---------|
| %Y | year (4-digit) |
| %m | month (01-12) |
| %d | day (01-31) |
| %H | hour (00-23) |
| %M | minute |
| %S | second |
| %A / %a | weekday, full / abbreviated |
| %I | hour (01-12) |
| %p | AM/PM |

date +"%Y-%m-%d_%H-%M-%S"

```
Then, it increases the value of ```myvar``` by 1 using the arithmetic calculation:
```bash
myvar=$(( myvar + 1 ))
```
For example, if myVar is 1, it becomes 2. If it is 2, it becomes 3.

- ## What is arithmetic calculation
- arithmetic calculations is a basic math operation let you work with whole numbers using operators such
```bash
+	addition
-	subtraction
*	multiplication
/	division
%	modulus
```
Useing the syntax``` $(( ... ))```:
```bash
a=5
b=2

sum=$((a + b))
difference=$((a - b))
product=$((a * b))
quotient=$((a / b))
remainder=$((a % b))

echo "$sum"        # 7
echo "$difference" # 3
echo "$product"    # 10
echo "$quotient"   # 2
echo "$remainder"  # 1

```
The script then waits for 2 seconds:
```bash
sleep 2
```
Finally, the ```done ```keyword shows that the commands inside the``` while ```loop have ended.

The loop repeats this process:

- Check whether``` myvar ```is less than or equal to``` 10```.
- Print the current value.
- Add``` 1 ```to``` myvar```.
- Wait for``` 2 seconds```.
- Repeat the loop.
When``` myvar``` is 10, the condition is still true because 10 is equal to 10.

The script prints 10 and then increases``` myvar ```to 11.

The loop runs one more time, but now the condition is false because 11 is greater than 10.

Therefore, the loop stops, and the script finishes.

In Bash, a ```while loop``` is often combined with a``` case statement ```to create an interactive menu of options.

The while loop repeatedly displays the menu and allows the user to select an option.

The ```case statement ```checks the user’s choice and executes the corresponding command.

After the command finishes, the loop returns to the menu.

It continues until the user chooses an option such as Exit, which stops the loop.

More about that later, let see the other type of loops in Bash.

# For Loops
A ```for Loop ```allows you to perform a task repeatedly for every item in a set.

compared to an``` if statement``` an ```if statement``` performs a task once if a certain set of conditions evaluates as true.

Where as a``` while loop ```performs a task or set of tasks over and over again until a particular state is reached.

A ```for Loop ```is a concept of executing a command or set of commands against each item in a set
```bash
for variable in list
do
    commands
done
```
Here is a Practical``` for loop ```example
```bash
#!/bin/bash

# Create the logfiles directory

mkdir -p logfiles

# Create example files

touch logfiles/access.log
touch logfiles/error.log
touch logfiles/system.log
touch logfiles/notes.txt

# Compress every .log file

for file in logfiles/*.log
do
    tar -czvf $file.tar.gz $file
done
```
### How the script will works?

```mkdir -p logfiles ```creates the directory if it does not already exist, and``` touch ```creates the example files.

If the files already exist, ```touch``` does not delete their contents.

The script will create this structure:
```bash
logfiles/
├── access.log
├── error.log
├── system.log
└── notes.txt
```
Then the``` For ```loop does the following:

- Looks inside the logfiles directory.
- Finds every file ending in ```.log```.
- Stores one filename in the variable file.
- Creates a compressed``` .tar.gz ```archive for that file.
- Moves to the next ```.log``` file.
- Repeats until all matching files have been processed.
- Ends when there are no more ```.log``` files.

After the loop finishes, the directory will contain:
```bash
logfiles/
├── access.log
├── access.log.tar.gz
├── error.log
├── error.log.tar.gz
├── system.log
├── system.log.tar.gz
└── notes.txt
```
### so what the purpose of the For loop ?

A for loop repeats the same action for multiple files or values automatically.

It is useful when you need to perform the same operation multiple times without writing the commands repeatedly.

And the purpose of the for loop in our example is to process every .log file automatically.

Without the loop, you would need to write one command for every file:

```bash


tar -czvf logfiles/access.log.tar.gz logfiles/access.log
tar -czvf logfiles/error.log.tar.gz logfiles/error.log
tar -czvf logfiles/system.log.tar.gz logfiles/system.log

```
This saves time, makes the script shorter, and allows the script to process any number of .log files automatically.

Let’s discuss next the`` case statement``. It’s going to be a lot of fun since we’re starting to get closer to the end of this course and becoming able to create simple Bash programs that can perform useful tasks for us.

But remember, with practice, you can do almost anything with Bash.

# Case Statements
We can use a case statement to create a sort of menu and allow the user to choose an option from that menu.

Example:

```bash
#!/bin/bash

echo "What is your favorite Linux distribution?"

echo "1. Arch Linux"
echo "2. CentOS"
echo "3. Debian"
echo "4. Linux Mint"
echo "5. Ubuntu"
echo "6. Other"

read -p "Choose an option: " distro

case "$distro" in
    1)
        echo "Arch Linux is a powerful and flexible distribution."
        ;;
    2)
        echo "CentOS is commonly used on servers."
        ;;
    3)
        echo "Debian is a community-based distribution."
        ;;
    4)
        echo "Linux Mint is user-friendly and easy to use."
        ;;
    5)
        echo "Ubuntu is popular on both servers and computers."
        ;;
    6)
        echo "You selected a distribution that is not on the list."
        ;;
    *)
        echo "You did not enter an appropriate choice."

esac
```
Now notice that we have an asterisk:
```bash
*)
    echo "You did not enter an appropriate choice."

   ```
The asterisk works as a catch-all option. While the script is running, the case statement compares the user’s input with the available options, such as values one through six.

If none of those options match, Bash reaches the asterisk.

This means that the user entered something other than a valid selection.

For example, they may have entered 7, 9, ABC, or 123. Since none of these values match the available options, the asterisk executes its command and displays the appropriate message.

Notice After each case option that there are two semicolons
```bash
1)
    echo "You selected option 1."
    ;;
    ↑
     ↑
 
```
The two semicolons tell Bash that the commands for that option are finished. If you have multiple commands, the semicolons should be placed after the final command.

The ``semicolons ``can be placed on the same line as the command or on a separate line. When there is only one command, it is common to place them at the end of that command.

The final case option dosent need the semicolons before ``esac``

The ``esac`` keyword marks the end of the ``case statement``.

Now let’s add a ``while ``loop to our script and create a real, working menu.
```bash
#!/bin/bash

finished=0

while [ "$finished" -ne 1 ]
do
    echo "What is your favorite Linux distribution?"
    echo "1. Arch Linux"
    echo "2. CentOS"
    echo "3. Debian"
    echo "4. Linux Mint"
    echo "5. Ubuntu"
    echo "6. Other"
    echo "7. Exit"

    read -p "Choose an option: " distro

    case "$distro" in
        1)
            echo "Arch Linux is a powerful and flexible distribution."
            ;;
        2)
            echo "CentOS is commonly used on servers."
            ;;
        3)
            echo "Debian is a community-based distribution."
            ;;
        4)
            echo "Linux Mint is user-friendly and easy to use."
            ;;
        5)
            echo "Ubuntu is popular on both servers and computers."
            ;;
        6)
            echo "You selected a distribution that is not on the list."
            ;;
        7)
            finished=1
            ;;
        *)
            echo "You did not enter an appropriate choice."
    esac

done

echo "Thank you for using this script."

```

How this script works?

- The while loop displays the menu repeatedly.

- The case statement checks the user’s choice and executes the matching command.

- When the user selects option 7, the finished variable changes from 0 to 1. 

- The while condition is then no longer true, so the loop ends.

Now, this particular script is not very useful by itself. 

However, if you use your creativity, you can create a menu-driven interface for managing a server. 

This could be especially useful for beginners who have not yet mastered all the necessary commands.

A menu-driven script could perform many different tasks. 

Instead of simply displaying an echo statement when the user selects an option, the script could:

- Update packages
- Reboot the server
- Perform data-processing tasks
- Manage files
- Run other system administration commands

For example, option 7 is used to exit the script. It does not need to display an echo statement. Instead, it can set the finished variable to 1.

# Exit Status

An exit status is a value that indicates whether a command or script completed successfully.

- 0 means success.
- Any other value indicates some kind of failure.

The special variable``` $? ```stores the exit status of the most recently executed command:

``echo $?``

You can set your own exit status using the` exit `command:
```bash
exit 0   # Success
exit 1   # Error

```
Custom exit codes are useful for identifying different types of failures, especially when debugging scripts.

For example:

```bash
if [ ! -d "$1" ]; then
    echo "Source directory does not exist"
    exit 1
fi
```
In this example,`` -d "$1" ``checks whether the first argument is a directory.

If the directory does not exist, the script displays an error message and ``exits with status code 1``.

# THE END 

## Congratulations on completing this Bash scripting course!

You now have the basic knowledge and tools needed to start creating useful Bash scripts. You have learned how to use``` variables, user input, conditional statements, loops, case statements, exit statuses, and command-line arguments```.

These concepts allow you to automate repetitive tasks, create interactive menus, process files, manage servers, and build scripts that provide real value.

This is only the beginning. Continue practicing, experiment with your own ideas, and do not be afraid to make mistakes. The more you practice, the more confident and creative you will become with Bash scripting.

### You made it to the end! 

Now it’s your turn to put your Bash skills into action. Keep practicing, stay curious, and turn your ideas into powerful scripts. 

The command line is yours to explore.
