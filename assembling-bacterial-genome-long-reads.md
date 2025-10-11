# Assembling a bacterial genome sequence - exploiting long reads

Previously, we assembled the genome sequence of the bacterial strain _Xanthomonas campestris_ pv. _fici_ NCPPB 2372.
We assembled the genome sequence from about a million pairs of short Illumina sequence reads.
This produced a draft-quality genome sequence that was, unfortunately, fragmented into hundreds of contigs.


### The workflow for assembling long reads

![Workflow for long reads](<assembly/Screenshot 2025-10-03 at 16.19.16.png>)

In the following exercise, we will do assembly of only long reads, using an assembly tools called Flye.
Flye is specifically designed to assemble long reads (such as Oxford Nanopore) rather than short reads (such as Illumina).

It can be advantageous to combine short reads plus long reads in the assembly.
If you are interested in knowing more about such a hybrid approach to assembly,
please see this [tutorial about using Unicycler in Galaxy](https://training.galaxyproject.org/topics/assembly/tutorials/unicycler-assembly/tutorial.html).

### Hands on: get the long sequence reads

The long Oxford Nanopore sequence reads for this bacterial genome are in the Sequence Read Archive (SRA)
under accession number [SRR30037665](https://trace.ncbi.nlm.nih.gov/Traces/?view=run_browser&acc=SRR30037665&display=metadata).

Note that the average length of these reads is 6904 bp, and there is a lot of variation, with some reads being much longer. There are
more than 155 thousand reads.

See image: [Summary stats for SRR30037665 at SRA](<assembly/Screenshot 2025-10-02 at 16.47.47.png>).


- Use the [Download and Extract Reads in FASTQ](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fiuc%2Fsra_tools%2Ffastq_dump%2F3.1.1%2Bgalaxy1&version=latest) tool to get SRR30037665 data. ([Image: Getting the data](<assembly/Screenshot 2025-10-02 at 16.22.11.png>))
- For "select input type", choose "SRR accession".
- For "Accession", insert "SRR30037665".
- Press **Run Tool**.

Now we have the long reads in the Galaxy history. You can view the sequence reads in Galaxy.
See image: ([SRR30037665 long reads in Galaxy](<assembly/Screenshot 2025-10-02 at 16.52.51.png>)). Feel free to edit the name of the dataset from "Single-end data (fastq-dump)" to something more informative like "SRR30037665 long ONT reads".


### Filter the long reads, using Filtlong

- For "Input FASTQ", choose the SRR30037665 long reads.
- For "Keep percentage", enter "90".
- For "Min. length", enter "1000".
- Press **Run Tool**

See image: [Running Filtlong in Galaxy](<assembly/Screenshot 2025-10-02 at 19.52.20.png>).

Optionally, you could now use FastQC to assess the quality of the long reads before and after filtering.


|                   Quality scores before QC                                        |    Quality scores after QC              |
|   ------------------------------------------------------------------------------  |   ------------------------------------- |
| ![assembly/ont-reads-before-filtlong.png](assembly/ont-reads-before-filtlong.png) | ![assembly/ont-reads-after-filtlong.png](assembly/ont-reads-after-filtlong.png) |

|                   Read lengths  before QC                                        |    Read lengths after QC              |
|   ------------------------------------------------------------------------------  |   ------------------------------------- |
| ![assembly/lengths-before.png](assembly/lengths-before.png) |   ![assembly/lengths-after.png](assembly/lengths-after.png) | 






### Assemble the filtered long reads, using Flye

- Find the [Flye tool in Galaxy](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fbgruening%2Fflye%2Fflye%2F2.9.6%2Bgalaxy0&version=latest).
- For "Input reads", select the filtered long reads.
- For "Mode", select "Nanopore HQ".
- For all other parameters and options, leave the default settings.
- Click on **Run Tool**
 
See image: [Running Flye in Galaxy](<assembly/Screenshot 2025-10-02 at 21.25.53.png>).

Flye will generate four outputs:

- Consensus - this is the assembled genome sequence
- Assembly graph
- Graphical fragment assembly
- Assembly info	

Notice that we have now succeeded in assemblign the genome into just three circular contigs, that correspond to the chromosome and two plasmids:

![Screenshot of assembly info](<assembly/Screenshot 2025-10-02 at 21.33.56.png>)

We can visualise the graphical fragment assembly using Bandage. This helps to illustrate the massive improvement in assembly using long reads versus short reads.


|                 Assembly graph from long reads                                                              |   Assembly graph from short reads              |
| ----------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| ![Assembly graph from long reads](<assembly/Galaxy82-[Bandage Image on data 63_ Assembly Graph Image].jpg>) | ![Assembly graph from short reads](<assembly/Galaxy28-[Bandage Image on data 25_ Assembly Graph Image].jpg>) |


### Annotate the Flye-assembled genome sequence with Bakta

![annotation/Galaxy86-[Bakta on data 61_ Plot of the annotation].svg](<annotation/Galaxy86-[Bakta on data 61_ Plot of the annotation].svg>)


### Visualise the Bakta annotation in genome viewer



## Step 8: Visualise the genome assembly

The GFF3-formatted annotation is useful, because we can view this in an interactive genome browser such as the [Integrative Genome Browser (IGV)](https://igv.org/):

![Viewing the assembled and annotated genome sequence in IGV](<annotation/igv-app.svg>)

See image: [Viewing the assembled and annotated genome sequence in IGV](<annotation/igv-app.svg>).

To acheieve this, we first need to download the assembled genome sequence from Galaxy:

- Locate the relevant dataset in your Galaxy history. It will be the the FASTA file generated as output from Flye. [Image](<>).
- Click on the "disk" icon to download this FASTA file onto your local computer. [Image](<>).
- The file will probably appear in your Download folder and will be called something like `Galaxy14-[Flye on data 5_ consensus].fasta`.

We also need the Bakta annotation of this assembled genome sequence:

- Locate the relevant dataset. It will be a GFF3 file generated as output from Flye. [Image](<>).
- Click on the "disk" icon to download this GFF3 file onto your local computer. [Image](<>).
- The file will probably appear in your Download folder and will be called something like `Galaxy19-[Bakta on data 14_ Annotation and sequences (GFF3)].gff3`.

Now, you can load these files into IGV:

- Navigate to the IGV web application at [https://igv.org/app/](https://igv.org/app/).
- Use the **Genome->Local File** menu item to upload the assembled genome (FASTA file).
- Use the **Tracks->Local File** menu item to upload the assembled genome (GFF3 file).


## Optional Step 9: Visualising the reads aligned against the assembly

If you have time, it can be interesting to align the original sequence reads against the assembled genome sequence. 
This allows us to check for consistency between the final assembly versus the raw data from which it was inferred.

Optionally, you can follow this procedure:

- In Galaxy, use [BowTie2](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fdevteam%2Fbowtie2%2Fbowtie2%2F2.5.4%2Bgalaxy0&version=latest) to align the Illumina sequence reads against the assembled genome sequence.
- 










