# Bash Scripting – TryHackMe

This folder contains my hands-on exercises and notes from the Bash Scripting room on TryHackMe. It focuses on scripting fundamentals, automation, and practical command-line usage to enhance system administration skills.

## Introduction

Bash is a scripting language available on most Linux distributions and MacOS. Shell scripts are sequences of Bash commands in a file, used to automate tasks and perform more complex operations than single-line commands.  

**Key concepts explored in this room include:**
- Bash syntax  
- Variables  
- Parameters and arguments  
- Arrays  
- Conditionals


## First Script

**This section introduces creating and running your first Bash script, including basic commands and execution workflow.**

### Concepts Learned:
- Bash scripts are files containing a sequence of Bash commands.
- Scripts start with a shebang (#!/bin/bash) to indicate the interpreter.
- You can include both Bash commands and regular Linux commands in a script.
### Implementation:
- *Create a script file, e.g., first_script.sh.*
- *Script contents:*
  #!/bin/bash
  echo "Hello World"
  ls
  whoami
  id
- *Make the script executable:*
  chmod +x first_script.sh
- *Run the script:*
  ./first_script.sh

### Notes:
- echo outputs text to the terminal, similar to Python’s print.
- Any Linux command can be executed within a Bash script if formatted correctly.
- Always include #!/bin/bash at the top of your scripts.



## Variables

**This section introduces variables in Bash, how to assign and use them, and basic debugging techniques.**

### Concepts Learned:
- Variables store values that can be reused throughout a script.
- Variable names cannot contain spaces and must not have spaces around = when assigning values.
- Access variable values using $ before the variable name.
- Multiple variables can be used in the same statement.
- 
### Implementation / Example:
- **Assign a value to a variable:**
   name="Harish"
- **Use the variable:**
   echo $name
- **Output:**
    Harish
- **Combine variables:**
   first="Harish"
    second="R"
    echo $first $second
- **Output:**
   Harish R
- **Debugging:**
- **Run script with debug mode to trace execution:**
    bash -x ./script.sh
- **Insert set -x and set +x in the script to debug specific sections:**
   set -x
   echo $name
   set +x
- **Debugging shows which commands are executed successfully and highlights errors for easy correction.**

### Notes:
- Variables simplify updating values across a script without changing multiple lines.
- Regular use of debugging improves problem-solving and error detection skills.


## Parameters

**This section covers passing and using parameters in Bash scripts, including command-line arguments and interactive input.**

### Concepts Learned:
- Parameters are variables passed to scripts from the command line.
- $1, $2, … represent the first, second, etc., arguments.
- read can be used for interactive user input instead of command-line arguments.
- Combining parameters with variables allows dynamic and reusable scripts.

### Implementation / Example:

**Using command-line arguments:**
echo "Hello $1"
**Run with:**
./example.sh Alex
**Output:**
Hello Abishek
Accessing the second argument:
echo "Hello $2"
**Run with:**
./example.sh Abishek J
**Output:**
  J
**Interactive input with read:**
echo "Enter your name:"
read name
echo "Hello $name"
**Combine multiple parameters for dynamic output:**
read name age job
echo "My name is $name, I am $age years old, and I work as a $job."
**Output:**
  My name is Abishek, I am 21 years old, and I work as a penetration Tester
### Notes:
- Parameters make scripts flexible and reusable.
- read allows for interactive scripts, useful for input validation and dynamic behavior.
- Practice by creating scripts that accept multiple arguments or interactive input to reinforce understanding.



## Arrays

**This section covers creating, accessing, modifying, and deleting arrays in Bash scripts.**

### Concepts Learned:

Arrays store multiple pieces of data in a single variable.

Each element in an array has an index, starting at 0.

Array elements can be accessed, modified, or removed individually.

### Implementation / Example:

**Declare an array:**

fruits=('apple' 'banana' 'cherry' 'date')
**Print all elements:**
echo "${fruits[@]}"
**Output:**
apple banana cherry date
**Access a single element by index:**
echo "${fruits[2]}"
**Output:**
cherry
**Modify an element:**
fruits[1]='blueberry'
echo "${fruits[@]}"
**Output:**
apple blueberry cherry date
**Remove an element using unset:**
unset fruits[0]
echo "${fruits[@]}"
**Output:**
blueberry cherry date


### Notes:
- Arrays allow for storing related data efficiently.
- Indexing starts at 0.
- [@] is used to reference all elements, while [index] references a specific element.
- unset removes an element but does not reindex the array.
- Practice by using arrays to store multiple pieces of information for small projects, like a multi-person biography maker.




### Conditionals

**This section covers using if statements and relational operators to control the flow of Bash scripts.**

## Concepts Learned:
- Execute code based on a condition being true or false.
- Use relational operators to compare numbers and strings.
- Combine multiple conditions for complex logic.

## Implementation / Example:
**Basic if syntax:**
count=10
if [ $count -eq 10 ]; then
    echo "They are equal"
else
    echo "They are not equal"
fi

**Output (if count=10):**
They are equal

**Common Relational Operators:**
*Operator	Description*
  -eq	Equal to
  -ne	Not equal to
  -gt	Greater than
  -lt	Less than
  -ge	Greater than or equal
  -le	Less than or equal

**File Checks & Combined Conditions**
- Check file existence and permissions using -f and -w.
- Use logical combinations in conditional statements.

**Check if a file exists and is writable:**
  file=$1
  if [ -f "$file" ] && [ -w "$file" ]; then
    echo "hello" >> "$file"
  else
      touch "$file"
      echo "hello" >> "$file"
  fi

**Run script:**
  ./example.sh myfile.txt
  cat myfile.txt
**Output:**
  hello


## Notes:
- -f checks if a file exists.
- -w checks if a file is writable.
- Logical AND (&&) allows checking multiple conditions simultaneously.
- if/else statements are essential for controlling script behavior dynamically.
- Practice by expanding projects: combine parameter input, file checks, and logical operators.


# Key Takeaways
- Bash is a versatile scripting language that simplifies task automation and system administration.
- Variables and parameters allow scripts to be dynamic and reusable.
- Arrays are powerful for handling multiple data elements efficiently.
- Conditionals enable decision-making and error handling within scripts.
- Debugging tools (bash -x, set -x) are essential for identifying and fixing issues quickly.
- Practicing small scripts and projects builds confidence and strengthens understanding.
- Combining Bash with Linux commands extends the capabilities of scripts for real-world tasks.


