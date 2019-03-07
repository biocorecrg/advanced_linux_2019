<a name="module1_parsing"></a>
<h3>Manipulate files, piping, parsing, reformatting</h3>

Parsing a file means extracting meaningful parts from a data source. In few words if you have table and are interested only in a number of columnes, extracting those columnes can be an example of **parsing**. In our case, for example, we can extract the name of our sequences by using again the program **grep** and redirecting the output to a new file.

```{bash}
grep ">" Escherichia_coli_bl21_gold_de3_plyss_ag_.ASM2366v1.pep.all.fa > seq_names.txt

more seq_names.txt

>ACT27082 pep supercontig:ASM2366v1:CP001665:347:1750:1 gene:ECBD_0001 transcript:ACT27082 gene_biotype:protein_coding transcript_biotype:protein_coding descrip
tion:chromosomal replication initiator protein DnaA
>ACT27083 pep supercontig:ASM2366v1:CP001665:1755:2855:1 gene:ECBD_0002 transcript:ACT27083 gene_biotype:protein_coding transcript_biotype:protein_coding descri
ption:DNA polymerase III, beta subunit
>ACT27084 pep supercontig:ASM2366v1:CP001665:2855:3928:1 gene:ECBD_0003 transcript:ACT27084 gene_biotype:protein_coding transcript_biotype:protein_coding descri
ption:DNA replication and repair protein RecF
>ACT27085 pep supercontig:ASM2366v1:CP001665:3957:6371:1 gene:ECBD_0004 transcript:ACT27085 gene_biotype:protein_coding transcript_biotype:protein_coding descri
ption:DNA gyrase, B subunit
```

We can also **pipe** the results of a program (via Standard output) to a new program (via Standard input) by using the character 
```|```, the program **head** allows to extract the first N rows (indicated by the parameter **-n**). Tail, instead allows to get the latest N rows.

```{bash}
grep ">" -c Escherichia_coli_bl21_gold_de3_plyss_ag_.ASM2366v1.pep.all.fa
4228

grep ">" Escherichia_coli_bl21_gold_de3_plyss_ag_.ASM2366v1.pep.all.fa | head -n 3 
>ACT27082 pep supercontig:ASM2366v1:CP001665:347:1750:1 gene:ECBD_0001 transcript:ACT27082 gene_biotype:protein_coding transcript_biotype:protein_coding description:chromosomal replication initiator protein DnaA
>ACT27083 pep supercontig:ASM2366v1:CP001665:1755:2855:1 gene:ECBD_0002 transcript:ACT27083 gene_biotype:protein_coding transcript_biotype:protein_coding description:DNA polymerase III, beta subunit
>ACT27084 pep supercontig:ASM2366v1:CP001665:2855:3928:1 gene:ECBD_0003 transcript:ACT27084 gene_biotype:protein_coding transcript_biotype:protein_coding description:DNA replication and repair protein RecF

grep ">" Escherichia_coli_bl21_gold_de3_plyss_ag_.ASM2366v1.pep.all.fa | tail -n 3 
>ACT31307 pep supercontig:ASM2366v1:CP001665:4569941:4570198:-1 gene:ECBD_4328 transcript:ACT31307 gene_biotype:protein_coding transcript_biotype:protein_coding description:protein of unknown function DUF37
>ACT31308 pep supercontig:ASM2366v1:CP001665:4570162:4570488:-1 gene:ECBD_4329 transcript:ACT31308 gene_biotype:protein_coding transcript_biotype:protein_coding description:ribonuclease P protein component
>ACT31309 pep supercontig:ASM2366v1:CP001665:4570538:4570678:-1 gene:ECBD_4330 transcript:ACT31309 gene_biotype:protein_coding transcript_biotype:protein_coding description:ribosomal protein L34
```
Now let's try to extract only the identifiers from the sequence names. As we can see they are located just before a **space**. So we can slice the first column using the space as delimiter using the program **cut** and the option **-d " "**.

```{bash}
cut -f 1 -d " " seq_names.txt |head -n 5 
>ACT27082
>ACT27083
>ACT27084
>ACT27085
>ACT27086
```
We still have the character **>** from the fasta file. For removing it we can use the program **tr** with the option **-d** (delete).

```{bash}
cut -f 1 -d " " seq_names.txt | tr -d ">" | head -n 5 
ACT27082
ACT27083
ACT27084
ACT27085
ACT27086
```
Going back to the genome file, we can use a combination of **grep** and **wc** to count the number of bases. The option **-v** of **Grep** will remove the row with the indicated character. The option **-m** of **wc** tool allows to count only the characters, while **-l** gives you the nnumber of lines. 

```{bash}
grep -v ">" Escherichia_coli_bl21_gold_de3_plyss_ag_.ASM2366v1.dna.toplevel.fa| wc -m
4647121

grep -v ">" Escherichia_coli_bl21_gold_de3_plyss_ag_.ASM2366v1.dna.toplevel.fa| wc -l
76183
```




