# Bash Scripting Summary
a simple and fast summary of bash scripting components

### Bash Comments:
Bash ignores everything written on the line after the hash mark `#` (except shebang).<br>we can use comments in top of our scripts to show details of them.

```
#author: KoroushPub
#created/modified: Aug,2022
#Description: what your script do?
#Usage: how to use it?
```

### shebang `#!`
tell the Linux OS which interpreter to use to parse the rest of the file ,for bash scripting we always use `#!/bin/bash`<br>
note that must be the first line in the Linux shell.

## EXPANSIONS

### parameter expansion
Simple Syntax:  `$parameter`<br>
Advanced Syntax:  `${parameter}`



| Syntax      | Description |
| ----------- | ----------- |
| `${#parameter}`       | isplay how many characters the variable’s value contains       |
| `${parameter^}`   | onvert the first character of the parameter to uppercase        |
| `${parameter^^}`|Convert all characters of the parameter to uppercase|
|`${parameter,}`|Convert the first character of the parameter to lowercase|
|`${parameter,,}`|Convert all characters of the parameter to lowercase|
|`${parameter : offset : length}`|The shell will expand the value of the parameter starting at character number defined by “offset” and expand up to a length of “length”|


### brace expansion
Syntax: `{, or ..}`

| Syntax      | Description |
| ----------- | ----------- |
| `{a,b,c,d,1,2,3}`       | a b c d 1 2 3       |
| `{a..z}`   |a b c d e f g h i j k l m n o p q r s t u v w x y z        |
| `{1..10}`| 1 2 3 4 5 6 7 8 9 10 |
|`note{01..10}`|note01 note02 note03 note04 note05 note06 note07 note08 note09 note10|

### arithmetic expansion
Syntax: `$(( expression ))`

### tilde expansion
Syntax: `~`

### command substitution
Syntax: `$(command)`

## PARAMETER TYPES

### Variables
Syntax: `variable=value`


### Positional Parameters

Example:<br>
`./script alex 25`<br>

```
#!/bin/bash
echo "hello $1 happy birthday you are $2 now!"
```

### Special Parameters

| Syntax      | Description |
| ----------- | ----------- |
| `$#`       | Stores the number of command line arguments provided to the script       |
| `$0`   |Stores the script name        |
| `$?`| Gives the exit code returned by the most recent command |
|`$@`|Expands to each positional parameter as its own word with subsequent word splitting|

## Arrays
use to store multiple different values at the same time.<br>
Syntax: `array=(item1 item2 item3 .. itemX)`<br>
note: in array we use spaces to separate values within an array

### Array Modification

| Operation      | Description |
| ----------- | ----------- |
| `array[0]=value`       | Changes the element value of the array. |
| `array+=(value)`   | Appends the value to the end of array.   |
| `array+=(item1 item2 item3)`| Appends multi items to the array. |
|`unset array[number]`|Removes the specified element from the array.|

### Array Expansion

| Expansion      | Description |
| ----------- | ----------- |
| `${array}`       | show the first element of an array |
| `${array[@]}`   |show all elements of an array        |
| `${!array[@]}`| show all index number of elements of an array |
|`${array[@]:offset:length}`|start with the first offset element, and continue the `:length` of the array|



## comparison operators
list of comparison operators for numbers you can use within bash scripts:

| Syntax      | Description |
| ----------- | ----------- |
| `-eq`       | Equal       |
| `-ne`   |Less than or equal    |
| `-lt`| Less than |
|`-ge`|Greater than or equal|
| `-gt`| Greater than |
|`-ge`|Greater than or equal|
|`-z`|in null|
|`-n`|not null|

operators for comparing strings:

| Syntax      | Description |
| ----------- | ----------- |
| `=`       | Equal       |
| `!=`   |Not Equal    |

operators for file checking:

| Syntax      | Description |
| ----------- | ----------- |
| `-e`       | True if file entry exists |
| `-f`   |True if file entry exists and is a regular file    |
| `-d`|True if file entry exists and is a directory |
|`-x`|True if file entry exists and is executable by the current user|


# Script Logic

### select
`Select` command is a very useful bash command for bash menu creation.

You can define a custom prompt for the select loop inside a shell script, using the PS3 environment variable, as explained below.

```
PS3="choose your item: "
select item in door bed chair;
do
echo "you selected chair"
break
done
```

### if,elif,else
The if statement starts with the if keyword followed by the conditional expression and the then keyword. The statement ends with the fi keyword.

```
num=12
if [ "$num" -ge 10 ];
then
        echo "$num is greater then ten!"
elif [ "$num" -lt 10 ];
then
        echo "$num is less thenn ten!"
else
        echo "$num is ten."
fi
```

### case
The bash case statement is generally used to simplify complex conditionals when you have multiple different choices.

note: `*)` is used as a “default” case, and is used to hold
commands that should run if no other cases match.

```
color=blue

case "$color" in
        red)echo "the color is red";;
        blue)echo "the color is blue";;
        *)echo "other things ...";;
esac

```
### while
while loop is a control flow statement that allows code or commands to be executed repeatedly based on a given condition.<br>
note: You must ensure that the condition you provide the while
loop does become false at some point to avoid infinite
loops!

```
num=14

while [ "$num" -gt 10 ];
do
echo "ur number is $num"
num=$(($num-1))
done
```
### while_read
read each line of the file or output command we provided.

file
```
while read line;
do
        echo $line
done < "$HOME/file.txt"
```
command output
```
while read line;
do
        echo "$line"
done < <(ls -l $HOME)
```

### for
the bash for loop is a bash programming language statement which allows code to be repeatedly executed.

```
for num in {1..10};
do
        echo ${num}
done
```
# Tips
### making your scripts accessible from any folder:<br>

Edit your ~/.profile file to add a custom folder to your PATH:<br>
`export PATH="$PATH:/path/to/script_directory`<br>

Reload the ~/.profile file:<br>
`source ~/.profile`

### checking syntax errors with `shellcheck`
install: `sudo apt install shellcheck`<br>
usage: `shellcheck <script>`
