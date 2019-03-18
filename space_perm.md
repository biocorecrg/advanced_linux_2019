<h2>Space in volumes and permissions</h2>

<h3>Volume sizes and disk space</h3>

When we deal with analyzing valuable data we should consider different problems:
* Consuming too much disk space
* Consuming too much memory
* Corrupting / deleting files

Check the size of a file with :
* **ls -lh**: 
	* **l**: list.
	* **h**: human readable.

```{bash}
ls -lh Escherichia_coli_bl21_gold_de3_plyss_ag_.ASM2366v1.pep.all.fa 
```

Get a summary of the disk usage size of a directory:
* **du -sh**: 
	* **du** stands for **D**isk **U**sage.
	* **s**: summarize.
	* **h**: human readable format.

```{bash}
du -sh my_beautiful_folder/

3.5K	my_beautiful_folder/
```

Display disk usage of all the files and directories:
* ** du -ah**:
	* **a**: all.

```{bash}
du -ah my_beautiful_folder/
```


* For CRG users, remember that page where you can check the space occupied in your group (and all folders!):
  + https://accounting.linux.crg.es/addons/storage/insight/login.php

* Reduce the space by:
  + Compressing files.
  + Using programs such as **zcat** or **gunzip -c** to extract information of zipped files on the fly instead of extracting the data.
  + Creating **symbolic links** instead of copying files and folders.

```{bash}
# compress files using gzip:
gzip Escherichia_coli_bl21_gold_de3_plyss_ag_.ASM2366v1.pep.all.fa

# show the content of a gzipped file without uncompressing it:
zcat SRR6466185_1.fastq.gz | head
gunzip -c SRR6466185_1.fastq.gz | head

# link files instead of copying them

mkdir test_links
cd test_links

# ln for linking, -s for symbolic link: first comes the file to link, then where to link it!
ln -s ../SRR6466185_1.fastq.gz .
# give the copy of the file another name:
ln -s ../SRR6466185_2.fastq.gz ./sample2_SRR6466185_1.fastq.gz

cd ..
```

Show the system disk space statistics (file system disk space usage):
* **df -h**. 
	* **df** stands for: **D**isk **F**ilesystem.
	* **h**: human readable.

```{bash}
df -h

Filesystem                              Size  Used Avail Use% Mounted on
/dev/sda3                                20G  8.1G   11G  44% /
devtmpfs                                 63G     0   63G   0% /dev
tmpfs                                    63G     0   63G   0% /dev/shm
...
```

<h3>Permissions</h3>

Create a small file:

```{bash}
echo "my file" > test.txt
```

* Each file has particular permissions that restrict their access to the users. <br>

**ls -l** shows those permissions:

```{bash}
ls -l test.txt
-rw-r--r-- 1 sbonnin Bioinformatics_Unit 5 Mar 14 16:29 test.txt
```
Here is the owner is **sbonnin** and the group it belongs to is **Bioinformatics_Unit**.<br>

The first field here contains **10 ticks**:

* tick 1: 
	* **d**: directory
	* **-**: regular file
	* **l**: symbolic link (1 field) 
* ticks 2-4: permissions of the **owner** (3 fields)
* ticks 5-7: permissions of the **group** (3 fields)
* ticks 8-10: permissions of **any other user** (3 fields)

|Owner|Group|Any user|
| :---:  | :---:  | :---:  |
| rw- | r-- | r-- |

* What kind of permissions are we talking about?
	* **r**: read
	* **w**: write
	* **x**: execute

* In the latter example:
  + **sbonnin** can **read** and **write** the file, but NOT execute it.
  + Members of **Bioinformatics_Unit** can only **read** the file.
  + All other users can only **read** the file.

* **chmod** controls the changes of permissions:

```
chmod [who][+,-,=][permissions] filename
```

* Add **writing** permissions to the **group**:

```{bash}
chmod g+w test.txt

ls -l test.txt

-rw-rw-r-- 1 sbonnin Bioinformatics_Unit 5 Mar 14 16:29 test.txt
```

* Add **writing** permissions to the **all other users**:

```{bash}
chmod o+w test.txt 

ls -l test.txt

-rw-rw-rw- 1 sbonnin Bioinformatics_Unit 5 Mar 14 16:29 test.txt
```

* Remove writing permissions to all **but the owner**:

```{bash}
chmod og-w test.txt 

ls -l test.txt

-rw-r--r-- 1 sbonnin Bioinformatics_Unit 5 Mar 14 16:29 test.txt
```

* Remove all permissions to all **but the owner**:

```{bash}
chmod og-rw test.txt

-rw------- 1 sbonnin Bioinformatics_Unit 5 Mar 14 16:29 test.txt
```

* Preserve the file from any modification **even by yourself** using **a** (= all):

```{bash}
chmod a-w test.txt 

-r-------- 1 sbonnin Bioinformatics_Unit 5 Mar 14 16:29 test.txt

# Try to overwrite the content of test.txt:

echo "test" > test.txt
-bash: test.txt: Permission denied

# Try to remove test.txt:

rm test.txt
rm: remove write-protected regular file ‘test.txt’?
```

* Control whether a file or folder is **executable**:

```{bash}
chmod -x my_ugly_folder/

# try to enter the folder:
cd my_ugly_folder/
-bash: cd: my_ugly_folder/: Permission denied
```

* A user that don't have the **executing** rights can't access the directory !

* Apply permission changes **recursively**, i.e. to all files inside a directory:

```{bash}
chmod -R +x my_ugly_folder/
```

<h4>Use binary or octal notation for file permissions</h4>

<br>
* Each tick in the first field refers to:
	* a type of permission: read, write, execute.
	* a user type: owner, group, all others.

Each tick can be replaced by **0** (does not have that permission) or **1** (has that permission): this creates a **binary** number at each **user type**, that can be converted into an **octal** number.<br>

Hence, each **octal** number represents a set of permissions:

| Binary | Octal | Permission |
| :----: | :----: | :----: |
| 000 |	0 | - - - |
| 001 |	1 | - - x |
| 010 |	2 | - w - |
| 011 |	3 | - w x |
| 100 |	4 | r - - |
| 101 |	5 | r - x |
| 110 |	6 | r w - |
| 111 |	7 | r w x |

<br>

* Set the permissions of **my_expression.txt** (from Module 1) so that:
  + the owner can: read, write and execute.
  + the group can: read and write.
  + the other users don't have any permission.

```{bash}
chmod 760 my_expression.txt
# 7 for the owner
# 6 for the group
# 0 for other users
```


<h3>Next Session</h3>

[Variables and "For" Loops](https://biocorecrg.github.io/advanced_linux_2019/var_for)

