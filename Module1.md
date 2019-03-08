<h2>Module 1</h2>

<h3>The plan</h3>

* [Create directory and practice moving around. Knowing more about a function](#module1_dir)
* [Download files from repositories](https://biocorecrg.github.io/advanced_linux_2019/download)
* [Manipulate files, piping, parsing, reformatting](https://biocorecrg.github.io/advanced_linux_2019/parsing)
* [Sequence file formats: Fasta and fastq](https://biocorecrg.github.io/advanced_linux_2019/bioformat)
* [Bed format and regular expressions](https://biocorecrg.github.io/advanced_linux_2019/regex)

<a name="module1_dir"></a>
<h3>Create directory and practice moving around</h3>

To create file and folders in linux is quite simple. You can use a number of programs for creating an empty file (**touch**) or an empty directory (**mkdir**)

```{bash}
touch my_beautiful_file.txt
mkdir my_beautiful_folder
```

To display the list of files and folder we can use the command **ls**

```{bash}
ls

my_beautiful_file.txt  my_beautiful_folder
```

To change the name of a file (or a directory) you can use the command **mv** while for copying the file you can use **cp**. Adding the option **-r** (recursive) to **cp** allows to copy a whole folder and its content. 

```{bash}
mv my_beautiful_file.txt my_ugly_file.txt
mv my_beautiful_folder my_ugly_folder

cp my_ugly_file.txt my_beautiful_file.txt
cp my_ugly_folder -r my_beautiful_folder
```
If you omit the **-r** option the system will complain

```{bash}
cp my_ugly_folder my_other_folder

cp: omitting directory ‘my_ugly_folder’
```

You can use **mv** also for moving a file (or a directory) inside a folder. Also **cp** will allow you to make a copy inside a folder.

```{bash}
mv my_beautiful_file.txt my_beautiful_folder
cp my_ugly_file.txt my_ugly_folder

ls

my_beautiful_folder  my_ugly_file.txt  my_ugly_folder
```

For entering in a folder we can use the tool **cd**

```{bash}
cd my_ugly_folder

ls

my_ugly_file.txt
```

For going out we can move one level out 
```{bash}
cd ../

ls

my_beautiful_folder  my_ugly_file.txt  my_ugly_folder
```

Sometimes we get lost and would like to know where we are. We can use the command **pwd**

<img src="pics/lost.jpg" width="400"/>

We can write to a file using the character **>**, that means output redirection.

```{bash}
echo "ATGTACTGACTGCATGCATGCCATGCA" > my_dna.txt
```

And display the content of the file using the program **cat**

```{bash}
echo "ATGTACTGACTGCATGCATGCCATGCA" > my_dna.txt
```

We can write to a file using the character **>**, that means output redirection.

```{bash}
cat my_dna.txt

ATGTACTGACTGCATGCATGCCATGCA
```

To convert this sequence to a RNA one we can just replace the **T** base with **U** by using the program **sed**. The sintax of this program is the following ```s/<TO BE REPLACED>/<TO REPLACE>```. You can add a **g** at the end if you want to replace every character found.

```{bash}

sed s/T/U/g my_dna.txt > my_rna.txt

cat my_rna.txt

AUGUACUGACUGCAUGCAUGCCAUGCA
```

Every command has a manual, you can read it by using the program **man** with the name of the tool.

```{bash}
man ls

LS(1)                                                                   User Commands                                                                  LS(1)

NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...

DESCRIPTION
       List information about the FILEs (the current directory by default).  Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

       Mandatory arguments to long options are mandatory for short options too.

       -a, --all
              do not ignore entries starting with .

       -A, --almost-all
              do not list implied . and ..

       --author
              with -l, print the author of each file

       -b, --escape
              print C-style escapes for nongraphic characters
 Manual page ls(1) line 1 (press h for help or q to quit)
```

<h3>Next Session</h3>

[Download files from repositories](https://biocorecrg.github.io/advanced_linux_2019/download)


