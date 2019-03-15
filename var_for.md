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
mylist=`ls -l`

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

* Calculations on variables:

```{bash}
# create the variable "num" that contains the number 2
num=2

# add 1 to "num"
echo $((num + 1))

# same as:
echo $(echo $nextnum+1 | bc)

# same as:
echo `echo $num+1 | bc`

# divide by 3:
echo `echo $num/3 | bc`

# show 4 decimals:
echo "scale=4; $((num))/3" | bc

```

A few built-in variables exist:

| Variable | Returns: |
| :---: | :---: |
| $USER | the user name |
| $HOME | the path of the home directory |
| $HOSTNAME | the hostname of the machine you are currently connected to |
| $RANDOM | a different random number each time it is accessed |

```{bash}
echo my user name is $USER, I work on the machine $HOSTNAME and my home directory path is $HOME.
```

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

<h4>Exercise</h4>

* Write a **for loop** and use your knowledge of **variables** to retrieve the **fasta** sequences of the following proteins from the Uniprot website:
  + Q9Y6G1, Q9NS00, Q9GZY8, O75843, Q3L8U1, P49810, P01584, O00182, Q02224, Q13547

  + Note: for one protein only (e.g. O94907 gene DKK1):
```{bash}
wget https://www.uniprot.org/uniprot/O94907.fasta
```

* Now for each of these proteins, write a **for loop** to :
  + create a **folder per protein** (using the protein name)
  + move the fasta files of each protein into the appropriate folder
  + (optional): change the name of the fasta file to add up the name of the corresponding gene (e.g. O94907_DKK1.fasta). Note: the name of the gene is found in the header of each fasta file.
  + you will need: **cd**, **mkdir**, **mv**, **basename**, **cut**, **grep**.

```{bash}
for protein in Q9Y6G1 Q9NS00 Q9GZY8 O75843 Q3L8U1 P49810 P01584 O00182 Q02224 Q13547
do
wget https://www.uniprot.org/uniprot/${protein}.fasta
done
```

```{bash}
for protein in Q9Y6G1 Q9NS00 Q9GZY8 O75843 Q3L8U1 P49810 P01584 O00182 Q02224 Q13547
do
mkdir $protein
mv ${protein}.fasta $protein
cd $protein
genename=$(grep ">" ${protein}.fasta | cut -d"|" -f3 | cut -d"_" -f1)
mv ${protein}.fasta `basename $protein .fastq`_${genename}.fasta
cd ..
done
```


[Back to the home page](https://biocorecrg.github.io/advanced_linux_2019)

