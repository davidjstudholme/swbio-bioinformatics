# Assembling a bacterial genome sequence - exploiting long reads

Previously, we assembled the genome sequence of the bacterial strain _Xanthomonas campestris_ pv. _fici_ NCPPB 2372.
We assembled the genome sequence from about a million pairs of short Illumina sequence reads.
This produced a draft-quality genome sequence that was, unfortunately, fragmented into hundreds of contigs.

But, take a look at the genome sequence for this bacterium on the NCBI webpage at https://www.ncbi.nlm.nih.gov/datasets/genome/GCA_041463625.1/.  

Notice that the sequence has been fully assembled such that there are not hundreds of contigs - there are only three contigs:

| Description  | Accession number | Length (bp) |
| -----------  | ---------------- | ----------- |
|   Chromosome |   CP167216.1     |  4,918,520  |	
|  Plasmid p22 |   CP167218.1	    |	    22,244  |
|  Plasmid p43 |   CP167217.1	    |	    43,254  |

This begs the question: why is this genome assembly so much better than the one that we generated?
The answer is that to achieve this much better assembly, I used a combination of short (Illumina) reads
plus long (Oxford Nanopore) reads.

To acheive this, I used a tool called Unicycler, which encompasses the SPAdes assembly tool, but also includes several other clever
steps to optimise the assembly and to exploit the additional information contained in the long reads.

If you are interested in knowing more, please see this [tutorial about using Unicycler in Galaxy](https://training.galaxyproject.org/topics/assembly/tutorials/unicycler-assembly/tutorial.html).
We do not have time to complete that process today, but feel free to try it on Thursday or Friday if you wish.



In the following exercise, we will experience the value of using long sequencing reads to improve the genome assembly.

### Hands on: get the long sequence reads

The long Oxford Nanopore sequence reads for this bacterial genome are in the Sequence Read Archive (SRA)
under accession number [SRR30037665](https://trace.ncbi.nlm.nih.gov/Traces/?view=run_browser&acc=SRR30037665&display=metadata).

Note that the average length of these reads is 6904 bp, and there is a lot of cariation, with some reads being much longer.

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







