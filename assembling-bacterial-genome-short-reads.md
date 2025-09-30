# Assembling a bacterial genome sequence

In this exercise, we are going to perform _de-novo_ assembly of a bacterial genome from short sequence reads. There are many different tools that we could use for genome assembly.
We will use a very commonly-used software tool called SPAdes.

SPAdes can assemble genome sequences from short reads only or it can assemble from a combination of short reads + long reads. Here, we are going to use only short reads.

### The dataset

- We will use a sequencing dataset that has been deposited in the Sequence Read Archive (SRA) under accession number SRR15305418.
- You can find information about this dataset on the SRA website [here](https://trace.ncbi.nlm.nih.gov/Traces/?view=run_browser&acc=SRR15305418&display=metadata).
- The data come from genome sequencing of the bacterial plant-pathogen *Xanthomonas campestris* pv. *fici* strain NCPPB 2372.
- The data consists of 1.1 million pairs of 151-bp sequence reads.
  
### Hands on:  Getting the data into Galaxy

- In Galaxy, create a new history. Give it a relevant name such as "Bacterial genome assembly short reads".
- Find the "Download and Extract Reads in FASTQ format from NCBI SRA" tool in Galaxy [here](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fiuc%2Fsra_tools%2Ffastq_dump%2F3.1.1%2Bgalaxy1&version=latest).
- For "select input type", choose "SRR accession".
- For "Accession", choose "SRR15305418".
- For "Select output format", choose "gzip compressed fastq".
- Press the **Run Tool** button.


### Hands on: check the quality of the data
 
Optionally, we could filter-out poor-quality sequence reads and/or trim poor-quality parts of reads.




