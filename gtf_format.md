<a name="module2_gtf"></a>
<h3>GTF files</h3>

The **G**eneral **T**ransfer **F**ormat (GTF) format contains annotation of features and consists of one line per feature, each containing 9 columns of data.

GTF files can be downloaded for example from ENSEMBL, where each correspond to a specific version/update of the annotation.

The annotation from the latest version of the annotation is in the [ENSEMBL main page](http://www.ensembl.org/Homo_sapiens/Info/Index) (for *Homo sapiens*).

Previous versions of the annotation are found in the [archives](https://www.ensembl.org/info/website/archives/index.html).

* Download the GTF file in [ENSEMBL release 94](http://oct2018.archive.ensembl.org/Homo_sapiens/Info/Index) for *Homo sapiens*.


<img src="images/ensembl_archive.png" width="800"/>

The name of the ENSEMBL gtf file is composed of:
* <species>: The systematic name of the species. (here, Homo_sapiens)
* <assembly>: The assembly build name. (here, GRCh38)
* <version>: The version of Ensembl from which the data was exported. (here, 94)

<img src="images/ensembl_gtf.png" width="600"/>

We can use this time the tool **curl** and the option **-o** for indicating the output file name.

```{bash}

curl -o Homo_sapiens.GRCh38.94.chr.gtf.gz ftp://ftp.ensembl.org/pub/release-94/gtf/homo_sapiens/Homo_sapiens.GRCh38.94.chr.gtf.gz

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 41.6M  100 41.6M    0     0  19.6M      0  0:00:02  0:00:02 --:--:-- 19.6M
```

* Let's check the file:

```{bash}
zcat Homo_sapiens.GRCh38.94.chr.gtf.gz | head

#!genome-build GRCh38.p12
#!genome-version GRCh38
#!genome-date 2013-12
#!genome-build-accession NCBI:GCA_000001405.27
#!genebuild-last-updated 2018-07
1	havana	gene	11869	14409	.	+	.	gene_id "ENSG00000223972"; gene_version "5"; gene_name "DDX11L1"; gene_source "havana"; gene_biotype "transcribed_unprocessed_pseudogene";
1	havana	transcript	11869	14409	.	+	.	gene_id "ENSG00000223972"; gene_version "5"; transcript_id "ENST00000456328"; transcript_version "2"; gene_name "DDX11L1"; gene_source "havana"; gene_biotype "transcribed_unprocessed_pseudogene"; transcript_name "DDX11L1-202"; transcript_source "havana"; transcript_biotype "processed_transcript"; tag "basic"; transcript_support_level "1";
1	havana	exon	11869	12227	.	+	.	gene_id "ENSG00000223972"; gene_version "5"; transcript_id "ENST00000456328"; transcript_version "2"; exon_number "1"; gene_name "DDX11L1"; gene_source "havana"; gene_biotype "transcribed_unprocessed_pseudogene"; transcript_name "DDX11L1-202"; transcript_source "havana"; transcript_biotype "processed_transcript"; exon_id "ENSE00002234944"; exon_version "1"; tag "basic"; transcript_support_level "1";
1	havana	exon	12613	12721	.	+	.	gene_id "ENSG00000223972"; gene_version "5"; transcript_id "ENST00000456328"; transcript_version "2"; exon_number "2"; gene_name "DDX11L1"; gene_source "havana"; gene_biotype "transcribed_unprocessed_pseudogene"; transcript_name "DDX11L1-202"; transcript_source "havana"; transcript_biotype "processed_transcript"; exon_id "ENSE00003582793"; exon_version "1"; tag "basic"; transcript_support_level "1";
1	havana	exon	13221	14409	.	+	.	gene_id "ENSG00000223972"; gene_version "5"; transcript_id "ENST00000456328"; transcript_version "2"; exon_number "3"; gene_name "DDX11L1"; gene_source "havana"; gene_biotype "transcribed_unprocessed_pseudogene"; transcript_name "DDX11L1-202"; transcript_source "havana"; transcript_biotype "processed_transcript"; exon_id "ENSE00002312635"; exon_version "1"; tag "basic"; transcript_support_level "1";
```

The file is quite big. In general it has a header indicated by the first character **"#"** and one row per feature composed by 9 columnes:

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

Let's count the number of gene features we have.

```{bash}
zcat Homo_sapiens.GRCh38.94.chr.gtf.gz | awk '{if ($3=="gene") print }'| wc -l 

58676
```

<h4>Exercise</h4>
Try to calculate the total number of each features. 


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
