<a name="module1_bioformat"></a>
<h3>Biological file formats: Fasta, fastq, bed formats.</h3>


We already showed the fasta format. There is a header characterized by the presence of **>** and a number of rows containing the sequence.
The format is used for both nucleic acids and proteins.

<img src="images/fasta_format.png" width="400"/>

Another way to store sequencing data, and particularly the short reads coming from the sequencers is the **Fastq** format.
This format allows to store also the information about the quality of that particular base, i.e. the probability that that base reading was true or not.

<img src="images/fastq_format.png" width="400"/>

The format contains for rows for sequence with a header containing **@** as the first character, the sequence content, a **spacer** and the quality encoded using ASCII characters.

<img src="images/phred_quality.png" width="400"/>


