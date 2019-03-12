<h2>Space in volumes and permissions</h2>

When we deal with analyzing valuable data we should consider different problems:
* Consuming too much disk space
* Consuming too much memory
* Corrupting / deleting files

To check the space occupied by each file we can use **ls** with the option **-lh** but to check the amount of data occupied in a folder we have to use **du** (estimate file space usage) with the option "human readable" and "summarize"

```{bash}
du -hs my_beautiful_folder/

3.5K	my_beautiful_folder/

du -hs 
86M	.
```

To reduce the space we must consider using compressed files as much is possible and extract the information of the fly using **zcat** or programs able to read the compressed files. We should be only careful not to fill the RAM when you are making some complex sorting / parsing operation. In that case can be useful to have intermediate files that can be deleted after the next step. 

Another tool that can be useful for knowing how much space is avaible to you is **df** (report file system disk space usage).

```{bash}
df -h

Filesystem                              Size  Used Avail Use% Mounted on
/dev/sda3                                20G  8.1G   11G  44% /
devtmpfs                                 63G     0   63G   0% /dev
tmpfs                                    63G     0   63G   0% /dev/shm
...
```

In Linux each file has particular permissions that restrict their acess to the users. When you list a file with **ls -l** we can see them:

```{bash}
ls -al README
-rw-r--r-- 1 lcozzuto Bioinformatics_Unit 4923 Mar  6 18:59 README
```

|Owner|Group|Any user|
| :---:  | :---:  | :---:  |
|-rw-|r--|r--|

In this particular case the owner has the right to **read** and **write** the file, while the user belonging to the same group can only **read** as any other user.

We can change this behaviour by using the program **chmod**.


```{bash}
chmod g+w README 

ls -al README

-rw-rw-r-- 1 lcozzuto Bioinformatics_Unit 4923 Mar  6 18:59 README
```

In this way we add **(+)** the possiblity to **write** to the file to the users of the same group. We can extend this to **others**

```{bash}
chmod o+w README 

ls -al README

-rw-rw-rw- 1 lcozzuto Bioinformatics_Unit 4923 Mar  6 18:59 README
```

Or to restrict **(-)** to only the owner.

```{bash}
chmod og-w README 

ls -al README

-rw-r--r-- 1 lcozzuto Bioinformatics_Unit 4923 Mar  6 18:59 README
```

Sometimes you don't want either you to touch that file so you can restrict you too (**user**) or in general **anyone**

```{bash}
chmod a-w README 

ls -al README

-r--r--r-- 1 lcozzuto Bioinformatics_Unit 4923 Mar  6 18:59 README

echo "aaaa" > README
-bash: README: Permission denied

```

Be careful you can still delete the file but you should have a warning.

In addition to **reading** and **writing** you have also **executing** that is important for programs and directories. A directory that is non executable by an user is not accessible.

```{bash}
chmod -x my_ugly_folder/

cd my_ugly_folder/
-bash: cd: my_ugly_folder/: Permission denied
```







<h3>Next Session</h3>

[Variables and "For" Loops](https://biocorecrg.github.io/advanced_linux_2019/var_for)

