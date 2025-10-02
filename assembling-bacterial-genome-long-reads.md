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
under accession number SRR30037665.

- Use the [Download and Extract Reads in FASTQ] tool to get SRR30037665 data. ([Image: Getting the data](<assembly/Screenshot 2025-10-02 at 16.22.11.png>))
- 







