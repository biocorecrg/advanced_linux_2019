<h2>Variables and "For" loops</h2>

<h3>Variables</h3>

A variable can contain a number, a character or a string of character.<br>
It is meant to **store temporarily** a piece of information.

* Create a variable:

```{bash}
# Assign the string "hola" to the variable "myfirstvariable":
myfirstvariable="hola"
```

* Variable names can be written in:
  + uppercase
  + lowercase
  + a mixture of both

* Access the content of a variable with **$**
* Show the content of a variable with **echo**

```{bash}
# Show the content of the variable
echo $myfirstvariable
```

Store a directory path:

```{bash}
# shortcut to a directory path
pathtodir=/users/bi/sbonnin/linux_test

# list what is in that directory
ls $pathtodir

```

* Command substitution:
  * Take the output of a command and save it as the value of a variable:

```{bash}
# store the output of "ls -l" and store it in "mylist"
mylist=$(ls -l)

# Show content of "mylist"
echo $mylist
```

* Using quotes:
  + **single quotes ' '** treat each character literally.
  + **double quotes " "** can access the content of variables.

```{bash}
# create one variable:
myname=Sarah

# use this variable when creating a new one, either with single or double quotes:
mytext1='My name is $myname'
mytext2="My name is $myname"

# access the content of each variable:
echo $mytext1
My name is $myname

echo $mytext2
My name is Sarah
```

* Use curly brackets if there are ambiguities:
	* the **{ }** **isolate** the variable name

```{bash}
mynumber=1

echo $mynumber_one
echo ${mynumber}_one
```


A few built-in variables exist:

| Variable | Returns: |
| :---: | :---: |
| $USER | the user name |
| $HOME | the path of the home directory |
| $HOSTNAME | the hostname of the machine you are currently connected to |
| $RANDOM | a different random number each time it is accessed |

<h3>"For" loops</h3>

**For loop** are used to repeat certain tasks.
<br>
The basic construct is:

<img src="images/forloop.png" width="200"/>

* At each **iteration** (repetition) of the loop, VARIABLE will be assigned a value from RANGE, sequentially.

* In the example below:
  + at the first iteration, **1** is assigned to **i**
  + at the second iteration, **2** is assigned to **i**
  + and so on...

```{bash}
for i in 1 2 3 4 5
do
	echo $i
done
```

* Loop on a longer range of values:

```{bash}
# 1 to 100
for i in {1..100}
do
        echo $i
done

# 1 to 100 with steps of 5
for i in {1..100..5}
do
        echo $i
done
```

* Use a for loop to check the number of rows of all text files in a folder:

```{bash}
for i in *txt
do 
	echo $i
	wc -l $i
done
```

* Use a for loop to change the extension of files:
  + **\*txt** is looking for all files with the **.txt** extension.

```{bash}
for i in *txt
do 
        echo $i
	newname=`echo $i | sed 's/txt/tab/'`
        mv $i $newname
done
```

* Use **basename** to keep only the file name but not the path (if looping around files that are not in the current directory):

```{bash}
for i in directory/*tab
do
        echo $i
        newname=`basename $i .tab`.txt
        mv $i $newname
done
```

* Loop around **folders only**:

```{bash}
for i in */
do
        echo $i
	# enter directory
	cd $i
	# count how many items the directory contains
	ls * | wc -l
	# leave the directory (go one directory up)
	cd ..
done
```

* Loop on selected files: all text files that **DO NOT** start with "a":

```{bash}
for i in `ls *.txt | grep -v "^a"`
do
        echo $i
done
```

* Write for loop in one line with **;** (semicolon):

```{bash}
for i in */; do echo $i; cd $i; ls * | wc -l; cd ..; done
```

[Back to the home page](https://biocorecrg.github.io/advanced_linux_2019)

