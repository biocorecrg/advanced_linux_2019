<h2>Module 1</h2>

<h3>The plan</h3>

* [Create directory and practice moving around](#module1_dir)
* [Download files from repositories](#module1_down)
* [Manipulate file, parsing, reformatting](#module1_pars)
* [Knowing more about a function](#module1_man)
* [Regular expressions](#module1_regex)
* [Fasta, fastq, bed formats](#module1_formats)


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

<a name="module1_down"></a>
<h3>Download files from repositories</h3>

Several institutions hosts differen kind of genomics data. For example the genome broswer **Ensembl** (https://www.ensembl.org/index.html) is also a public repository of genomes and annotation that can be freely donloaded and used for any kind of analysis.
The resource **Ensembl Bacteria** (https://bacteria.ensembl.org/index.html) contains a large number of bacterial genomes and their annotation. As an example we can browse the page corresponding to *Escherichia coli 'BL21-Gold(DE3)pLysS AG'* 


https://bacteria.ensembl.org/Escherichia_coli_bl21_gold_de3_plyss_ag_/Info/Index/

<img src="images/ensembl_escherichia.png" width="800"/>

We can click on "Download genes, cDNAs, ncRNA, proteins **FASTA**"

<img src="images/list_ensembl_escherichia.png" width="800"/>

And then on **DNA**

<img src="images/file_list_escherichia.png" width="800"/>

Then as an example we can use the copy the link address of the **README** file using the mouse right button.

<img src="images/right_click.png" width="800"/>

Then we can go back to our command line and use the program **wget** to download that file and using **CTRL+C** to pasthe the address

```{bash}
wget ftp://ftp.ensemblgenomes.org/pub/bacteria/release-42/fasta/bacteria_22_collection/escherichia_coli_bl21_gold_de3_plyss_ag_/dna/README


--2019-03-06 18:59:13--  ftp://ftp.ensemblgenomes.org/pub/bacteria/release-42/fasta/bacteria_22_collection/escherichia_coli_bl21_gold_de3_plyss_ag_/dna/README
           => ‘README’
Resolving ftp.ensemblgenomes.org (ftp.ensemblgenomes.org)... 193.62.197.94
Connecting to ftp.ensemblgenomes.org (ftp.ensemblgenomes.org)|193.62.197.94|:21... connected.
Logging in as anonymous ... Logged in!
==> SYST ... done.    ==> PWD ... done.
==> TYPE I ... done.  ==> CWD (1) /pub/bacteria/release-42/fasta/bacteria_22_collection/escherichia_coli_bl21_gold_de3_plyss_ag_/dna ... done.
==> SIZE README ... 4923
==> PASV ... done.    ==> RETR README ... done.
Length: 4923 (4.8K) (unauthoritative)

100%[======================================================================================================================>] 4,923       --.-K/s   in 0s      

2019-03-06 18:59:14 (295 MB/s) - ‘README’ saved [4923]
```

we can then use the program **more** to display part of the content of the file

```{bash}
more README


#### README ####

IMPORTANT: Please note you can download correlation data tables,
supported by Ensembl, via the highly customisable BioMart and
EnsMart data mining tools. See http://www.ensembl.org/biomart/martview or
http://www.ebi.ac.uk/biomart/ for more information.

The genome assembly represented here corresponds to  
GCA_000023665.1

#######################
Fasta DNA dumps
#######################

-----------
FILE NAMES
------------
The files are consistently named following this pattern:
   <species>.<assembly>.<sequence type>.<id type>.<id>.fa.gz

<species>:   The systematic name of the species.
<assembly>:  The assembly build name.
<sequence type>:
 * 'dna' - unmasked genomic DNA sequences.
--More--(14%)
```


<a name="module1_pars"></a>
<h3>Manipulate file, parsing, reformatting</h3>

<a name="module1_man"></a>
<h3>Knowing more about a function</h3>

<a name="module1_regex"></a>
<h3>Regular expressions</h3>

<a name="module1_formats"></a>
<h3>Fasta, fastq, bed formats</h3>
