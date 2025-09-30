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

![Getting the data from SRA](<assembly/Screenshot 2025-09-30 at 15.36.23.png>)

### Hands on: perform quality control using TrimGalore
 
- In Galaxy, find the [TrimGalore tool](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fbgruening%2Ftrim_galore%2Ftrim_galore%2F0.6.10%2Bgalaxy0&version=latest).
- For "Is this library paired- or single-end?", choose "Paired collection".
- For "Select a paired collection", select the SRR15305418 paired sequence reads that you obtained earlier.
- Press the **Run Tool** button.

![Running TrimGalore](<assembly/Screenshot 2025-09-30 at 15.39.31.png>)

TrimGalore removes poor-quality sequence reads and trims poor-quality ends from otherwise high-quality reads.

TrimGalore results appear in the Galaxy history.

![TrimGalore results in history](<assembly/Screenshot 2025-09-30 at 15.50.46.png>)


### Hands on: check the quality of the sequence data before and after applying filtering + trimming

We will use FastQC and MultiQC to assess the quality of the sequence reads data (which is in FASTQ format).

- Find the [FastQC tool](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fdevteam%2Ffastqc%2Ffastqc%2F0.74%2Bgalaxy1&version=latest) in Galaxy.


![Running FastQC on original data](<assembly/Screenshot 2025-09-30 at 15.54.42.png>)

- Do the same for the post-TrimGalore data too.

![Running FastQC on post-TrimGalore data](<assembly/Screenshot 2025-09-30 at 15.55.35.png>)

FastQC generates various output files. You may need to click on the "eye" icon to display hidden files, in order to see all the FastQC output.

![Results from FastQC](<assembly/Screenshot 2025-09-30 at 16.13.04.png>)

You can now explore and view the FastQC output directly, if you wish. Alternatively, load the FastQC output into MultiQC.



