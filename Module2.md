<h2>Module 2</h2>

<h3>The plan</h3>

* [Tabular files](#module2_tab)
* [GTF files](#module2_gtf)
* [Space in volumes](#module2_space)
* [Permissions](#module2_perm)
* [Variables](#module2_var)
* ["For" Loops](#module2_loops)
* [Introduction to VIM text editor](#module2_vim)

<a name="module2_tab"></a>
<h3>Tabular files</h3>

A general tabular file (or tab separated text) is a table which columnes are separated by the character **\t**. A easy way to obtain this format is exporting a spreadsheet (like the excel file) in TSV.

<img src="images/exporting_excel.png" width="800"/>

You can download that file here <a href="my_expression.txt.zip">Download File</a> or via command line:

```{bash}
wget https://biocorecrg.github.io/advanced_linux_2019/my_expression.txt.zip

unzip my_expression.txt.zip 

more my_expression.txt

ids	baseMean	log2FoldChange	lfcSE	stat	pvalue	padj	gene.name	gene.type
ENSMUSG00000027009.18	6367.702449	-5.403229286	0.164511219	-32.84413864	1.3811E-236	3.1294E-232	Itga4	protein_coding
ENSMUSG00000030730.12	6085.911781	-6.880702974	0.224575305	-30.63873367	3.7337E-206	4.2301E-202	Atp2a1	protein_coding
ENSMUSG00000020393.16	3811.600859	-3.392964274	0.113074912	-30.00634011	8.1118E-198	6.1268E-194	Kremen1	protein_coding
ENSMUSG00000031962.6	5177.660551	-6.5722255	0.224972968	-29.21340091	1.3105E-187	7.4238E-184	Cdh15	protein_coding
ENSMUSG00000034648.9	7607.79254	-5.034267672	0.17328645	-29.05170986	1.4641E-185	6.6352E-182	Lrrn1	protein_coding
ENSMUSG00000049641.14	901.8440812	-7.022597773	0.246253844	-28.51771841	7.0643E-179	2.6678E-175	Vgll2	protein_coding
ENSMUSG00000050315.13	877.4673602	-4.465899309	0.157998266	-28.26549573	9.1813E-176	2.972E-172	Synpo2	protein_coding
ENSMUSG00000063659.11	2505.765754	-3.799372346	0.134497081	-28.2487347	1.4752E-175	4.1783E-172	Zbtb18	protein_coding

```

<a name="module2_gtf"></a>
<h3>GTF files</h3>

The **G**eneral **T**ransfer **F**ormat (GTF) format contains annotation of features and consists of one line per feature, each containing 9 columns of data.
<br>
GTF files can be downloaded for example from ENSEMBL, where each correspond to a specific version/update of the annotation.<br>
The annotation from the latest version of the annotation is in the [ENSEMBL main page](http://www.ensembl.org/Homo_sapiens/Info/Index) (for *Homo sapiens*).
<br>
Previous versions of the annotation are found in the [archives](http://www.ensembl.org/Homo_sapiens/Info/Index).

* Download the GTF file in ENSEMBL release 94 for *Homo sapiens*:

```{bash}
# -o: name of the output file
curl -o Homo_sapiens.GRCh38.94.chr.gtf.gz ftp://ftp.ensembl.org/pub/release-94/gtf/homo_sapiens/Homo_sapiens.GRCh38.94.chr.gtf.gz
```

The name of the ENSEMBL gtf file is composed of:
* <species>: The systematic name of the species. (here, Homo_sapiens)
* <assembly>: The assembly build name. (here, GRCh38)
* <version>: The version of Ensembl from which the data was exported. (here, 94)

* Let's check the file:
	* No need to uncompress the file: **zcat** allows to view the content of a compressed file without actually uncompressing it !

```{bash}
# Display the first 10 rows
zcat Homo_sapiens.GRCh38.94.chr.gtf.gz | head
# Check number of rows
zcat Homo_sapiens.GRCh38.94.chr.gtf.gz | wc -l
# Browse the whole file
zcat Homo_sapiens.GRCh38.94.chr.gtf.gz | less
```

* Fields:

| Column number | Column name | Details |
| :----: | :----: | :----: |
| 1 | seqname | name of the chromosome or scaffold; chromosome names can be given with or without the 'chr' prefix. |
| 2 | source | name of the program that generated this feature, or the data source (database or project name) |
| 3 | feature | feature type name, e.g. Gene, Variation, Similarity |
| 4 | start | Start position of the feature, with sequence numbering starting at 1. |
| 5 | end | End position of the feature, with sequence numbering starting at 1. |
| 6 | score | A floating point value. |
| 7 | strand | defined as + (forward) or - (reverse). |
| 8 | frame | One of '0', '1' or '2'. '0' indicates that the first base of the feature is the first base of a codon, '1' that the second base is the first base of a codon, and so on.. |
| 9 | attribute | A semicolon-separated list of tag-value pairs, providing additional information about each feature. |

* Check chromosome names
```{bash}
# Remove rows starting with "#": grep (-v keeps only what doesn't match)
# Retrieve the first column only: cut (-f to specify the field)
# Keep the unique occurences in column 1: uniq
zcat Homo_sapiens.GRCh38.94.chr.gtf.gz | grep -v "#" | cut -f1 | uniq
```

* How many gene features are present in this file ?
```{bash}
zcat Homo_sapiens.GRCh38.94.chr.gtf.gz | awk '$3=="gene"' | wc -l
```

* Extract gene names:
```{bash}
zcat Homo_sapiens.GRCh38.94.chr.gtf.gz | awk '$3=="gene" {print $10}' | sed 's/"//g' | sed 's/;//g' > gene_names_Homo_sapiens.GRCh38.94.txt
```

* Create a BED file out of the genes from the GTF:
```{bash}
zcat Homo_sapiens.GRCh38.94.chr.gtf.gz | awk '$3=="gene" {print $1"\t"$4"\t"$5"\t.\t.\t"$7}' | sed 's/"//g' | sed 's/;//g' > genes_Homo_sapiens.GRCh38.94.bed
```

<a name="module2_space"></a>
<h3>Space in volumes</h3>

<a name="module2_perm"></a>
<h3>Permissions</h3>

<a name="module2_var"></a>
<h3>Variables</h3>

<a name="module2_loops"></a>
<h3>"For" loops</h3>

<a name="module2_vim"></a>
<h3>VIM text editor</h3>
