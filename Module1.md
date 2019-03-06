<h2>Module 1</h2>

<h3>The plan</h3>

* [Create directory and practice moving around](https://biocorecrg.github.io/advanced_linux_2019/create_dir.md)
* [Download files from repositories](#module1_down)
* [Manipulate file, parsing, reformatting](#module1_pars)
* [Knowing more about a function](#module1_man)
* [Regular expressions](#module1_regex)
* [Fasta, fastq, bed formats](#module1_formats)




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
