# Assembling a bacterial genome sequence - exploiting long reads

Previously, we assembled a bacterial genome sequence from about a million pairs of short sequence reads.
This produced a draft-quality genome sequence that was, unfortunately, fragmented into hundreds of contigs.

In the following exercise, we will experience the value of using long sequencing reads to improve the genome assembly.


### Hands on: copy the Galaxy history to create a new Galaxy history

In this exercise, we are going to assemble the genome sequence from the same bacterial strain as previously. 
Previously, we downloaded the short sequence reads and performed some quality control on them. We will re-use those
short reads in addition to the long reads. So, let's save some time by re-using the short-read data.

1. Use the "Copy this history" function to make a copy of the history. ([Image: "Copy this history"](<assembly/Screenshot 2025-10-02 at 09.56.25.png>))
2. Choose a suitable name for this new history (e.g. "SWBio Bacterial genome assembly long reads"). ([Image: Choose a name](<assembly/Screenshot 2025-10-02 at 16.20.41.png>))
3. Now you can see the new history in the Galaxy website. ([Image: New Galaxy history](<assembly/Screenshot 2025-10-02 at 16.21.12.png>))

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

### Assemble the short reads + long reads, using SPAdes

Just like we did previously, we are going to use SPAdes as the tool for _de-novo_ genome assembly. This time we will input long reads in addition to the short reads that we inputted previously.

- Find [SPAdes in Galaxy](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fnml%2Fspades%2Fspades%2F4.2.0%2Bgalaxy0&version=latest).
- For "Operation mode", choose "Assembly and error correction".
- For "Single-end or paired-end short-reads", choose "Paired-end: list of dataset pairs".
- For "FASTA/FASTQ file(s): collection", choose the SRR15305418 TrimGalore results that you prepared earlier (i.e. short reads after QC).
- Click on "Additional read files", and under "Nanopore reads", select the SRR30037665 long reads.
- Under "Pipeline options", activate the "Isolate" option.
- Press **Run Tool**.

See image: [Running SPAdes with short + long reads](<assembly/Screenshot 2025-10-02 at 17.07.58.png>).

  





