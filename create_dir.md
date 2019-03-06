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
$ my_beautiful_file.txt  my_beautiful_folder
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
$ cp: omitting directory ‘my_ugly_folder’
```

You can use **mv** also for moving a file (or a directory) inside a folder. Also **cp** will allow you to make a copy inside a folder.

```{bash}
mv my_beautiful_file.txt my_beautiful_folder
cp my_ugly_file.txt my_ugly_folder

ls
$ my_beautiful_folder  my_ugly_file.txt  my_ugly_folder
```

For entering in a folder we can use the tool **cd**

```{bash}
cd my_ugly_folder

ls
$ my_ugly_file.txt
```

For going out we can move one level out 
```{bash}
cd ../

ls
$ my_beautiful_folder  my_ugly_file.txt  my_ugly_folder
```

<img src="pics/lost.jpg" width="400"/>

Sometimes we get lost and would like to know where we are. We can use the command **pwd**
