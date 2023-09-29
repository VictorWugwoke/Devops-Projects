 # SHELL  SCRIPTING HANDS ON PROJECT.
 ## INTRODUCTION TO SHELL SCRIPTING AND USER INPUT
  #### Dfinition
Shell scripting refers to the process of writing and executing a series of commands in a shell (command-line) to automate tasks or perform a sequence of operations. A shell script is a text file containing a set of commands that are interpreted and executed by the shell.
### Pre-requisites 

1. Operating system
2. Bash shell (Bourne Again Shell)
3. Text editor (visual studio code)
4. Basic command line knowledge
5. Basic Programming Concepts
6. command line tools
7. Script Execution Permissions
8. Debugging Tools 

### Shell Scripting Syntax Elements.

* On my terminal I created a folder (directory) and named it practice_shell_scripting with the following command below:

`mkdir practice_shell_scripting`

* inside the Directory that I created, I created a file and named it myscript.sh by using the follwing command :

`touch myscript.sh`

Note: I used .sh to save the file because thats the extension that helps the operating system to identify that the file is ment to be executed by shell interpreter. 

* So because I need to run this file so I went ahead to modify the rights and permisions of the file I created to make it executable by using the following command below:

`chmod +x myscript.sh`

![Alt text](<mkdir chom.jpg>)

Using my VsCode text editor I opened the file .

# 1
### Variables:
In bash scripting, variables are used to store and manipulate data. They act as placeholders that can hold different values, such as numbers, strings, arrays or objects, throughout the execution of a script. You assign values to the variables using the = operator, and access their values using the variable name preceded by a $ sign.

#### Example:
 Assigning value to a variable:
`Name="John"`

Retrieving value from a variable: 
`echo $Name`
![Alt text](<Variable 1.jpg>)
![Alt text](<Variable 2.jpg>)

# 2
**Control Flow** : Control flow in bash refers to the order in which commands and statements are executed. Bash provides control flow statement like if-else, for loops, while loops, and case statements to control the flow of execution in your scripts. These statements allow you to make decisions, iterate over list, and execute different commands based on conditions. 

#### Example
using if-else to execute script based on a conditions

`#!/bin/bash`

`#Example script to check if a number is positive, negative, or zero`

`read -p "Enter a number: " num`

`if [ $num -gt 0 ]; `

`then `

    `echo "The number is positive"`

`elif [ $num -lt 0 ]; `

`then `

    `echo "The number is negative"`

`else `

    ` echo "the number is zero"`

`fi `

![Alt text](<elif statement.jpg>)
![Alt text](<elif statement 2.jpg>)

The piece of code prompts you to type a number and prints a statement stating the number is positive or negative.

### Example: 
Iterating through a list using a for loop

`#!/bin/bash`

`#Example script to print numbers from 1 to 5 using a for loop`

`for (( i=1; i<=5; i++ ))`

`do `

      echo $i

`done`

![Alt text](<for loop.jpg>)

# 3
### Command substitution: 
is a feature in bash scripting tha allows the output of a command to be used as a value or argument in another command or assignment. It is denoted by enclosing the command within `$() ` or backticks`(``)`.

**Example:** Using backtick for command substitution :

`current_date='date +%Y-%m-%d'`

**Example:** Using $() syntax for command substitution

`current_date=$(date +%Y-%m-%d) `

# 4
**Input and Output :** Bash provides various ways to handle input and output. You can use the readcommand to accept user input, and output text to console using echho command. Additionally, you can redirect input and output using operators like >(output to a file),<(input from a file), and | (pipe the output of one command as iput to another).

**Example:** Accept user input 

`echo "Enter your name: "`

`read Name`

     `echo "Welcome $Name!`

![Alt text](<user input.jpg>)

**Example** Output text to the terminal

`echo "Hello World"`

**Example** output result of a command into a file 

`echo "hello World" > index.txt`

![Alt text](<output into another.jpg>)

**Example:** Pass the content of a file as input to a command  

`grep "pattern" < iput.txt`


**Example:** Pass the result of a command as input to another command 

`echo "hello world" | grep "pattern"`

# 5
**Functions:** Bash allows you to define and use functions to group realated commands together. Functions provide a way to modularize your code and make it more reusable. You cabn define functions keyword or simply by decvlaring the function name followed by parantheses.

#!/bin/bash

`# Define a function to greet the user`

    greet() {
        `echo "Hello, $1! Nice to meet you."`
    }

`# call the greet function and pass the name as an argument`

`greet "john"`

![Alt text](<greet function.jpg>)


## Shell Scripting continues
**step 1 :** Since I have previously created a folder which i named **practice_shell_scripting** on my terminal using the command :

`mkdir practice_shell_scripting.`

 This will hold all the script that I will write in this project.

 **Step 2 :** I also created a file in **Practice_shell_scripting** directory that I named **myscrip.sh** by the using the command :

 `touch myscript.sh`

 **step 3 :** Inside of that **myscript.sh** file I will write the block of code below:

` #!/bin/bash`

`# prompt the user for their name`

`read -p "Enter your name: " Name`

`# Display a greeting with the entered name` 

   ` echo "Hello, $Name! Nice to meet you."`

simple explanation of the code block: The script prompts for your name. As you type your name, it displays the text *hello(your name)! nice to meet you*. Also` #!/bin/bash` helps you specify the type of bash interpreter to be used to execute the script.

**Step 4:** Save your file

**Step 5** Run the command `sudo chmod +x myscript.sh` this makes the file executable. (*note that i have previously done this before*)
 **Step 6:** Run the script using the command:
 
 ` ./myscript.sh`

The out put:
  ![Alt text](<prompt user input.jpg>)

  ## Directory Manipulation and Navigation
  This script will display the current directory, creatye a new director called "my_directory", change to that directory, create two files inside it, list the files, move back one level up, remove the "my_directory" and its contents, and finally list the files in the current directory again.

To achieve this i will perform the following steps:

  **Step 1:** I will create a file named *navigating-linux-filesystem.sh*

  **Step 2:** I will write the code block below inside my file:


 ` #!/bin/bash`

`# Display current directory`

`echo "Current directory: $PWD"`

`# Create a new directory`

`echo "Creating a new directory..."`

    mkdir my_directory

`echo "New directory created."`

`# Change to new directory`

`echo "Changing to the new directory..."`

    cd my_directory

`echo "Current directory: $PWD"`

`# Create some files`

`echo "Creating files..."`

    touch file1.txt

    touch file2.txt

`echo "Files created."`

`# List the files in the current directory`

`echo "Files in the current directory:"`

       ls 

`# Move one level up`

`echo "Moving one level up..."`

       cd..

`echo "Current directory: $PWD"`

`# Remove the new directory and its contents`
`echo "Removing the new directory..."`

    rm -rf my_directory
`echo "Directory removed"`

`#List the files in the current directory again `

`echo "Files in the current directory:"`

      ls 
![Alt text](<Directory manipulation 2.jpg>)
![Alt text](<Directory manipulation 3.jpg>)

**Step 3:** i will run the command `Sudo chmod +x` `navigating-linux-filesystem.sh` to set execution permission on the file

**Step 4:** Finally I will then run my script using this command `./navigating-linux-filesystem.sh`

![Alt text](<Directory manipulation.jpg>)

## File Operation and Sorting
In this section I will be writing a simple shell script that focuses on File operations.

This script creates three files (file1.txt, file2.txt,and file3.txt), displays the files in their current order, sorts them alphabetically, saves the sorted files in **sorted_files_sorted_alphabetically.txt** and finally displays the contents of the final sorted file. 

To achieve thsi i will have to follow the following steps: 

**Step 1:** I will open my terminal and create a file called **sorting.sh** using the command `touch sorting.sh`

**Step 2:** I will write the following code block inside the file as below :

`#!/bin/bash`

`# Create three files`
`echo "Creating files..."`

`echo "This is file3." > file3.txt`

`echo "This is file1." > file1.txt`

`echo "This is file2." > file2.txt`

`echo "Files created."`

`# Display the files in thier current order` 

`echo "Files in thier current order:"`

    ls

`# Sort the files alphabetically` 

`echo "Sorting files alphabetically..."`

    ls | sort > sorted_files.txt
`echo "Files sorted."`

`# Display the sorted files `

`echo "Sorted files:"`

      cat sorted_files.txt

`# Remove the original files`

`echo "Removing original files..."`

     rm file1.txt file2.txt file3.txt
`echo "Original files removed."`

`# Rename the sorted file to a more descriptive name` 

`echo "Renaming sorted file..."`

    mv sorted_files.txt sorted_files_sorted_alphabetically.txt

`echo "File renamed."`

`# Display the final sorted file`

`echo "Final sorted file:"`

![Alt text](<File operations and sorting 1.jpg>)
![Alt text](<file operations and sorting 2.jpg>)

    cat sorted_files_sorted_alphabetically.txt

**step 3:** I will go ahead to set execution permission on *sorting.sh* using the following command :

`chmod +X sorting.sh`

**Step 4:** I will then run my script using the command: 

`./sorting.sh`

![Alt text](<file operations and sorting3.jpg>)

## Working with Numbers and Calculations 
This script defines two variable num1 and num2 with numeric values, performs basic arithmetic operations ( addition, subtraction, multiplication, division, and modulus), and displays the results. it also performs more complex calculations such as raising num1 to the power of 2 and calculating the square root of num2, and display those results as well.

To achieve this i will have to perform the following steps :

**Step 1:** On my terminal I will create a file and name it *calculations.sh* using the follwing command: 

`touch calculations.sh`

**Step 2:** I will write the following code block inside the file (*calculations.sh*) that I created :

`#!/bin/bash`

`# Define two variables with numeric values` 
`num1=10`

`num2=5`

`# Perform basic arithmetic operations`

`sum=$((num1 + num2))`

`difference=$((num1 - num2))`

`product=$((num1 * num2))`

`quotient=$((num1 / num2))`

`remainder=$((num1 % num2))`

`# Dispaly the results`

`echo "Number 1: $num1"`

`echo "Number 2: $num2"`

`echo "Sum: $sum"`

`echo "Difference: $difference"`

`echo "Product: $product"`

`echo "Quotient: $quotient"`

`echo "Remainder: $remainder"`

`# Perform some more complex calculations `

`power_of_2=$((num1 ** 2))`

`square_root=$(awk "BEGIN{ printf \"%.2f\", sqrt``($num2) }")`

`# Display the results`

`echo "Number 1 rasied to the power of 2:` 
`$power_of_2"`

`echo "Square root of number 2: $square_root"`

![Alt text](<working with numbers 1.jpg>)
![Alt text](<working with numbers 2.jpg>)

**Step 3:** I will have to set execution permission on *calculations.sh* using the command:

`chmod +x calculations.sh`

**Step 4:** I will go ahead to run my script using the following command :

`./calculations.sh`

![Alt text](<Working with numbers3.jpg>)

## File Backup and Timestamping
The script defines the source director and backup directory paths. it then creates a timestamp using the current date and time, and creates a backup directory using the `cp` command with the `-r` option for recursive copying. Finally, it displays a message indicating the completion of the backup process and shows the path to the backup directorywith timestamp.

I can achieve this by following this simple steps :

**Step 1:** On my terminal I open a file and name it `backup.sh` using the follwoing the command :

`touch backup.sh`

**Step 2:** I will write on the file (backup.sh) the following block of code :

`#!/bin/bash`

`# Define the source directory and backup directory`

`source_dir="/path/to/source_directory"`

`backup_dir="/path/to/backup_directory"`

`# Create a timestamp with the current date and time `

`timestamp=$(date +"%Y%m%d%H%M%S")`

`# Create a backup directory with the timestamp`

`backup_dir_with_timestamp="$backup_dir/backup_$timestamp"`

`# Create the backup directory`

` mkdir "$backup_dir_with_timestamp"`

`# Copy all files from the source directory to the backup directory`

`cp -r "$source_dir"/* "$backup_dir_with_timestamp"`

`# Display a message indicating the backup process is complete `

`echo "Backup completed. Files copied to: $backup_dir_with_timestamp"`

![Alt text](<File Backup 2.jpg>)

**Step 3:** I will have to set the execute permission on *backup.sh* using the following command :

`chmod +X backup.sh`

**Step 4:** I will go ahead to run my command with the following command :

`./backup.sh`

![Alt text](<File backups.jpg>)
