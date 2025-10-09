# RNA-seq Analysis Tutorial (Galaxy Platform)
### Using *Pochonia chlamydosporia* RNA-seq Data (BioProject [PRJNA741387](https://www.ncbi.nlm.nih.gov/bioproject/?term=PRJNA741387))

## Summary

This tutorial walks you through:
- Importing and processing real RNA-seq data.
- Performing QC, trimming, and quantification.
- Running differential expression analysis and interpreting results.

You’ll finish with a clear view of how *P. chlamydosporia* responds to chitosan and nematode cues at the transcriptome level — all within Galaxy’s user-friendly, reproducible environment.

---

## Learning objectives

By the end of this exercise, you should be able to:

1. Import public RNA-seq data from NCBI SRA into Galaxy.
2. Perform quality control and trimming of Illumina paired-end reads.
3. Quantify transcript abundance or align reads to a reference genome.
4. Identify differentially expressed genes using DESeq2.
5. Visualize and interpret results in the context of the experiment.

---

## Background

This dataset comes from **Suarez-Fernandez et al. (2021)**, who investigated how **chitosan** and **nematode egg** exposure affect gene expression in the fungus *Pochonia chlamydosporia*, a biological control agent of plant-parasitic nematodes.

- **Organism:** *Pochonia chlamydosporia*
- **Treatments:**  
  - *Pc* — Control  
  - *PcQ* — Chitosan  
  - *PcRKN* — Nematode eggs  
  - *PcRKNQ* — Chitosan + Nematode eggs
- **Platform:** Illumina NovaSeq (paired-end, 150 bp)
- **BioProject:** [PRJNA741387](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA741387)

For this tutorial, we will analyse a subset of **four samples** (one replicate per condition).

| Condition | SRR Accession | Label |
|------------|---------------|-------|
| Control | SRR14923947 | Pc |
| Chitosan | SRR14923949 | PcQ |
| Nematode eggs | SRR14923950 | PcRKN |
| Eggs + Chitosan | SRR14923951 | PcRKNQ |

---

## What you’ll need

- Access to [Galaxy Main](https://usegalaxy.org) (create a free account).  
- Basic understanding of RNA-seq experimental design.  
- The following Galaxy tools will be used:
  - **Faster Download and Extract Reads in FASTQ** (from NCBI SRA)
  - **FastQC**
  - **MultiQC**
  - **fastp** (or *Trim Galore!*)
  - **Salmon quant** (alignment-free quantification)
  - **DESeq2** (differential expression)
  - *(optional)* **Heatmap**, **Volcano plot**, or **GOseq**

---

### Hands on: Import the data

To ensure that things run quickly and smoothly, I have prepared a subset of the RNA-seq data for use in this computer practical.
If we used the entire original dataset, some steps would take a lot longer to run.

The FASTQ-formatted files, containing the RNA-seq sequence reads, can be found at Zenodo:

```
https://zenodo.org/records/17301354/files/Pc.1.fq.gz
https://zenodo.org/records/17301354/files/Pc.2.fq.gz
https://zenodo.org/records/17301354/files/PcQ.1.fq.gz
https://zenodo.org/records/17301354/files/PcQ.2.fq.gz
https://zenodo.org/records/17301354/files/PcRKN.1.fq.gz
https://zenodo.org/records/17301354/files/PcRKN.2.fq.gz
https://zenodo.org/records/17301354/files/PcRKNQ.1.fq.gz
https://zenodo.org/records/17301354/files/PcRKNQ.2.fq.gz
```

You will now upload these files directly from Zenodo into Galaxy:

- Click on the **Upload** button, near the top-left of the Galaxy web page. (See the [Upload button](<rna-seq/Screenshot 2025-10-09 at 15.06.15.png>).)
- Select "Paste / Fetch data" (See the [Paste / Fecth data button](<rna-seq/Screenshot 2025-10-09 at 14.55.30.png>).)
- Paste the Zenodo web links. (See the [pasted web links](<rna-seq/Screenshot 2025-10-09 at 14.55.30.png>).)
- Press **Start**. (See the [Start button](<rna-seq/Screenshot 2025-10-09 at 14.55.30.png>).)
- Press **Close**. (See the [Close button](<rna-seq/Screenshot 2025-10-09 at 14.57.58.png>).)

The FASTQ files will appear in your Galaxy history:

See image: [Galaxy history, showing FASTQ files](<rna-seq/Screenshot 2025-10-09 at 15.13.19.png>).


---

## Hands on: Quality control

1. Run [FastQC](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fdevteam%2Ffastqc%2Ffastqc%2F0.74%2Bgalaxy1&version=latest) on all FASTQ files.
See image: [Running FastQC on all the FASTQ files](<rna-seq/Screenshot 2025-10-09 at 15.19.36.png>). 

2. Use [MultiQC](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fiuc%2Fmultiqc%2Fmultiqc%2F1.27%2Bgalaxy3&version=latest) to aggregate the FastQC reports.
See image: [Running MultiQC on the FastQC results](<rna-seq/Screenshot 2025-10-09 at 15.45.54.png>).


   

**Questions:**
- Are there adapters present?
- Are the read qualities good across all cycles?
- Are there major differences between samples?

---

## Hands on: Trimming

1. Use [fastp](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fiuc%2Ffastp%2Ffastp%2F1.0.1%2Bgalaxy2&version=latest):
- See image: [Runnning fastp in Galaxy](<rna-seq/Screenshot 2025-10-09 at 16.05.36.png>).
- Select the 
- Output: trimmed reads.
- Options:
  - Detect adapters automatically.
  - Minimum length = 30 bp.
2. Run **FastQC** + **MultiQC** again on the trimmed reads.
3. Confirm that adapter content and low-quality bases are reduced.

Note that we could have used [TrimGalore](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fbgruening%2Ftrim_galore%2Ftrim_galore%2F0.6.10%2Bgalaxy0&version=latest)
instead of fastp; there is always more than one tool to choose from!

---

## Step 4: Quantify transcript abundance with Salmon

> For simplicity and speed, we’ll use *alignment-free* quantification.

1. Obtain the *P. chlamydosporia* transcriptome FASTA file:
- Download from https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/411/695/GCA_000411695.3_PcB1v3/GCA_000411695.3_PcB1v3_rna_from_genomic.fna.gz.
- https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/411/695/GCA_000411695.3_PcB1v3/GCA_000411695.3_PcB1v3_genomic.fna.gz
- Upload to Galaxy.
2. Use **Salmon index** to build a transcriptome index (only once).
3. Run **Salmon quant** for each sample:
- Input: trimmed read pairs.
- Select the index you built.
- Library type: *Automatic detection*.
- Output: quantification directory for each sample.

You should now have four quantification outputs, one per sample.

---

## Step 5: Differential expression analysis (DESeq2)

1. Create a **sample annotation table** as a small tabular file and upload it:
```

sample	condition
Pc	control
PcQ	chitosan
PcRKN	eggs
PcRKNQ	eggs_chitosan

```
2. Open the **DESeq2** tool in Galaxy.
- Input type: Salmon quantifications.
- Design factor: `condition`.
- Run contrasts:
  - `PcQ` vs `Pc` (effect of chitosan)
  - `PcRKN` vs `Pc` (effect of eggs)
  - `PcRKNQ` vs `Pc` (combined treatment)
3. Review outputs:
- **MA plot** (log2 fold change vs. mean expression)
- **PCA plot**
- **Results table** with log2 fold changes and adjusted p-values.

---

## Step 6: Visualize and interpret

- Use **Heatmap** or **Volcano plot** tools in Galaxy to visualize top genes.
- Export DE gene tables and visualize in Excel or R if desired.
- (Optional) Run **GOseq** or **clusterProfiler** for GO enrichment analysis.

**Questions for discussion:**
1. How do the samples cluster in the PCA plot?
2. Which treatment has the strongest transcriptional response?
3. Are redox-related or cell wall–related genes among the upregulated ones?
4. How many genes are significantly different at FDR < 0.05?

---

## Step 7: Report your findings

Prepare a short report including:

1. A brief summary of the workflow.
2. Screenshots of the PCA and volcano plots.
3. A table of the top 10 upregulated and downregulated genes.
4. Interpretation of biological meaning (1–2 paragraphs).

---

## Instructor notes

- Use only four samples for a ~2-hour session. The full dataset (10 runs) can be assigned for independent practice.
- Provide a shared Galaxy history or workflow that students can import:
- **Get Data → fastp → FastQC/MultiQC → Salmon → DESeq2**
- You may pre-upload the *P. chlamydosporia* reference FASTA and GTF to save time.
- Optionally demonstrate how to **share histories** and **export workflows** in Galaxy.

---

## References

- **BioProject:** [PRJNA741387](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA741387)  
- **Publication:** Suárez-Fernández, M., et al. (2021). *Chitosan modulates Pochonia chlamydosporia gene expression during its parasitic relationship with root-knot nematodes.* *Frontiers in Microbiology*, 12:722845.  
- **Galaxy Training:** [RNA-seq reads to differential expression](https://training.galaxyproject.org/training-material/topics/transcriptomics/tutorials/rna-seq-counts-to-genes/tutorial.html)

