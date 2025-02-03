# Shell Scripting Notes

## Shell
- A shell is an interface to the OS that allows users to execute commands.
- Common shells include Bash, C Shell, Korn Shell, and Z Shell.
- To check the current shell:

```sh
echo $0
```

- Shell scripts are files containing a series of commands.
- The shell interprets and executes the script.
- Useful for automating tasks such as system monitoring, log file analysis, and backup management.

### Shebang
- Specifies the interpreter for the script.
- Recommended but not mandatory.

```sh
#!/bin/bash
```

## I/O Standard Input, Standard Output, and Standard Error
- **Standard Input (stdin):** Data input (usually from the keyboard).
- **Standard Output (stdout):** Normal command output.
- **Standard Error (stderr):** Error messages.

Redirecting output:
```sh
ls > output.txt  # Redirect stdout to file
ls 2> error.txt  # Redirect stderr to file
ls &> all_output.txt  # Redirect both stdout and stderr to file
cat file.txt  # Read from a file and display
```

## Variables
- Assign values using `=`.
- Use `$VAR_NAME` to reference a variable.
- Enclose values in quotes if they contain spaces.

```sh
NAME="John Doe"
echo "Hello, $NAME"
```

## Special Variables
- `$0` - Script name
- `$1, $2, ...` - Positional parameters
- `$#` - Number of arguments
- `$?` - Exit status of last command
- `$$` - Process ID of script
- `$@` - All arguments

```sh
echo "Script name: $0"
echo "First argument: $1"
echo "Number of arguments: $#"
```

## Reading Input
- Read input from the user.

```sh
echo "Enter your username:"
read USERNAME
echo "Logging in as $USERNAME..."
```

## Command Substitution
- Captures command output.

```sh
CURRENT_DATE=$(date +"%Y-%m-%d %H:%M:%S")
# $() is similar to ``
CURRENT_DATE=`date +"%Y-%m-%d %H:%M:%S"`

CURRENT_TIME=`date +"%H:%M:%S"`
echo "Current timestamp: $CURRENT_DATE current time: $CURRENT_TIME"
```

## Conditionals and Operators
- **If-else statement:**

```sh
if [ "$USERNAME" == "admin" ]; then
    echo "Welcome, Admin!"
else
    echo "Access denied."
fi
```

### Operators:
- **Arithmetic Operators:** `+ - * / %`  
  ```sh
  x=10
y=5
sum=$((x + y))
echo "Sum: $sum"
  ```

- **Comparison Operators:** `-eq, -ne, -gt, -lt, -ge, -le`
  ```sh
  if [ $x -gt $y ]; then
      echo "$x is greater than $y"
  fi
  ```

- **Logical Operators:** `&&, ||`
  ```sh
  if [ $x -gt 0 ] && [ $y -gt 0 ]; then
      echo "Both numbers are positive"
  fi
  ```

## Exit Statuses and Return Codes
- `$?` stores the exit status of the last executed command (0 = success, non-zero = failure).

```sh
ping -c 1 google.com
if [ $? -eq 0 ]; then
    echo "Internet is up."
else
    echo "No Internet connection."
fi
```

## String Test Conditionals
- Checking string conditions:

-  Using the test command `([ ])`

- check if string is empty

```sh
if [ -z "$VAR" ]; then
    echo "VAR is empty"
fi
```
- check if strings are equal

```sh
if [ "$STR1" = "$STR2" ]; then
echo "STR1 and STR2 are equal"
fi
```

- contains a sub string

```sh
string="Hello World"

if [[ "$string" == *"World"* ]]; then
  echo "String contains 'World'"
fi
```

- `[[ ]]` bash specific. Check if a string macthes a regex

```sh
if [[ $STR =~ ^[a-zA-Z]+$ ]]; then
echo "STR is a string of letters"
fi
```

## Positional Parameters, Arguments, for Loops
- Using arguments:

```sh
./script.sh arg1 arg2
```

- **For loop:**

```sh
for server in server1 server2 server3; do
    ping -c 1 $server
    echo "$server checked"
done
```

## While Loop, Infinite Loops, Shifting, Sleep
- **While loop:**

```sh
COUNT=1
while [ $COUNT -le 5 ]; do
    echo "Checking server status..."
    ((COUNT++))
    sleep 5  # Pause for 5 seconds

done
```

- **Infinite loop:**

```sh
while true; do
    echo "Monitoring logs..."
    tail -f /var/log/syslog
    sleep 5
done
```

## Case Statements
- Alternative to multiple `if-elif-else` conditions.

```sh
echo "Enter a service (nginx/apache/mysql):"
read SERVICE
case $SERVICE in
    nginx) systemctl restart nginx ;;
    apache) systemctl restart apache2 ;;
    mysql) systemctl restart mysql ;;
    *) echo "Unknown service." ;;
esac
```

## Functions
- Define and call functions.

```sh
backup_logs() {
    tar -czf backup_$(date +%Y%m%d).tar.gz /var/log
    echo "Logs backed up."
}

backup_logs
```


### environmental variables

