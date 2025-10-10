# RNA-seq Analysis of *Xanthomonas oryzae*

## Learning goals
In this exercise, you will perform a complete RNA-seq analysis comparing *Xanthomonas oryzae* pv. *oryzae* under two conditions to identify differentially expressed genes.

You will:

1. Import the provided RNA-seq data into Galaxy  
2. Perform quality control (FastQC)  
3. Map reads to the reference genome  
4. Quantify gene expression  
5. Identify differentially expressed genes  
6. Interpret the results in a biological context  

---

## Biological background

*Xanthomonas oryzae* pv. *oryzae* (Xoo) is a bacterial pathogen that causes bacterial blight of rice.  
In this study, RNA-seq was used to compare gene expression under two laboratory conditions that mimic different stages of infection or environmental stimuli.

Specifically, the bacteria were grown in liquid media and treated by adding plant extract to mimic the conditions of being in contact with the host plant, thus
inducing virulence genes.
A plant extract was prepared by grinding the leaves of a Xoo-susceptible rice cultivar (Milyang23) in liquid nitrogen.
The negative control consisted of bacteria grown in the same liquid medium, but without the addition of plant extract.

The original datasets are large and numerous. We will work with **downsampled data**
(two million read-pairs per sample) to make the analysis quick and manageable for classroom use.
Note that we also not including replicates in this analysis, to save time and avoid complexity.
When performing research, it would be necessary to include several replicates of the treatmenet and the control.

- The data are from: [BioProject PRJNA261679](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA261679)
- Original study: Kim, S., Cho, Y. J., Song, E. S., Lee, S. H., Kim, J. G., & Kang, L. W. (2016). Time-resolved pathogenic gene expression analysis of the plant pathogen *Xanthomonas oryzae* pv. *oryzae*. *BMC Genomics*, **17**, 345. [https://doi.org/10.1186/s12864-016-2657-7](https://doi.org/10.1186/s12864-016-2657-7).

---

## Hands on: Step 1 — Import the provided RNA-seq data into Galaxy

You will import **two samples** (paired-end FASTQ files):

| Condition | Read 1 (R1) | Read 2 (R2) |
|------------|-------------|-------------|
| Control (without_15) | [🔗 Link for R1](https://zenodo.org/records/17311933/files/without_15.SRR1582666.subsampled_1.fq.gz) | [🔗 Link for R2](https://zenodo.org/records/17311933/files/without_15.SRR1582666.subsampled_2.fq.gz) |
| Treatment (M23_15) | [🔗 Link for R1](https://zenodo.org/records/17311933/files/M23_15.SRR1582659.subsampled_1.fq.gz) | [🔗 Link for R2](https://zenodo.org/records/17311933/files/M23_15.SRR1582659.subsampled_2.fq.gz) |

To facilitate copy-and-paste, here are those links:

```
https://zenodo.org/records/17311933/files/without_15.SRR1582666.subsampled_1.fq.gz
https://zenodo.org/records/17311933/files/without_15.SRR1582666.subsampled_2.fq.gz
https://zenodo.org/records/17311933/files/M23_15.SRR1582659.subsampled_1.fq.gz
https://zenodo.org/records/17311933/files/M23_15.SRR1582659.subsampled_2.fq.gz
```

### To import the data in Galaxy:
1. Go to the [Galaxy webserver](https://usegalaxy.eu).  
2. From the Galaxy menu, on the left of the page, choose **“Upload”**.
3. Click the **“Paste/Fetch Data”** tab and paste the four Zenodo URLs listed above into the box (one per line). [Image](<rna-seq/Screenshot 2025-10-10 112850.jpg>).  
5. Click **“Start.”**
6. Wait until all datasets turn green (completed). [Image](<rna-seq/Screenshot 2025-10-10 112925.jpg>).
7. The four files will appear in your Galaxy history. [Image](<rna-seq/Screenshot 2025-10-10 114212.jpg>).
8. Rename the datasets for clarity (e.g. `control_R1`, `control_R2`, `treatment_R1`, `treatment_R2`). [Image](<rna-seq/Screenshot 2025-10-10 114409.jpg>).
9. Build a **paired dataset collection**:
   - Select all four FASTQs. [Image](<rna-seq/Screenshot 2025-10-10 114613.jpg>).
   - Click **“Build List of Dataset Pairs”**.
   - Check that the datasets are paired correctly, as in this [image](<rna-seq/Screenshot 2025-10-10 114641.jpg>).  
   - Give the collection a suitable name, e.g. `RNA-seq paired reads`. [Image](<rna-seq/Screenshot 2025-10-10 114827.jpg>) and press **Build**.
   - The new collection will appear in your Galaxy history, looking something like this [image](<rna-seq/Screenshot 2025-10-10 114917.jpg>).
---

## Hands on: Step 2 — Quality control
Run **FastQC** on the paired-end collection.

- Tool: [FastQC](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fdevteam%2Ffastqc%2Ffastqc%2F0.74%2Bgalaxy1&version=latest)  
- Input: Your paired-end dataset collection. [Image](<rna-seq/Screenshot 2025-10-10 115047.jpg>).  
- Output: Inspect the HTML reports for quality, GC content, adapter contamination, etc.  
- Run **fastp** to filter-out poor data. [Image](<rna-seq/Screenshot 2025-10-10 120653.jpg>).
   - Input: Collection of paired RNA-seq sequencing reads.
   - Use the default settings for all other options.
   - Output: a new collection called something like `fastp on collection 9: Paired-end output`. This contains the trimmed, filtered, paired reads.

---

## Hands on: Step 3 — Align RNA-seq reads against a reference genome

For this step, we first need to obtain the *Xanthomonas oryzae* pv. *oryzae* reference genome (in FASTA format).
The file can be obtained from the the NCBI, via their FTP site, with this URL:

```
https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/007/385/GCA_000007385.1_ASM738v1/GCA_000007385.1_ASM738v1_genomic.fna.gz`
```

1. Get the reference genome sequence from NCBI, into Galaxy ([image](<rna-seq/Screenshot 2025-10-10 121604.jpg>)):
   - Click on the **Upload** button near the top-left of the Galaxy page.
   - Click on **Paste / Fetch data**.
   - Copy and paste the URL (see above) into the box.
   - Press **Start**.
   - The reference genome sequence will appear in your Galaxy history. You can view it like in this [image](<rna-seq/Screenshot 2025-10-10 122133.jpg>).
   - Optionally, you could edit the name of the reference genome dataset, like in this [image](<rna-seq/Screenshot 2025-10-10 122223.jpg>).
2. Run [BowTie2](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fdevteam%2Fbowtie2%2Fbowtie2%2F2.5.4%2Bgalaxy0&version=latest):
   - Input: The paired-end collection of sequence reads output from fastp. [Image](<rna-seq/Screenshot 2025-10-10 122353.jpg>).  
   - Reference genome: The FASTA-formatted *Xoo* reference genome that you uploaded to Galaxy in the previous step.   
   - Output: BAM alignment files  

---

## Hands on: Step 4 — Count reads per gene

Use [featureCounts](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fiuc%2Ffeaturecounts%2Ffeaturecounts%2F2.1.1%2Bgalaxy0&version=latest)
to summarize aligned reads per gene.

- Input: BAM files  
- Annotation: GFF3 file
- Output: Gene count matrix  

```
https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/007/385/GCA_000007385.1_ASM738v1/GCA_000007385.1_ASM738v1_genomic.gff.gz
```

- Click on the **Upload** button.
- Click on **Paste / Fetch data**.
- Insert the URL for the GFF3 file and press **Start**.
- When the file turns green, you can press **Close**.


After running featureCounts, you will have two tables of results.
One consists of read-counts for the control and the other table has read-counts for the treatment.

To compare treatment versus control, we need to combine the two tables into one.

Use the [Join two datasets](https://usegalaxy.eu/?tool_id=join1&version=latest) tool.






---

## Hands on: Step 5 — Identify differentially expressed genes

Use **DESeq2** (or **edgeR**) for differential expression analysis.

- Input: featureCounts matrix  
- Factor: “Condition” (Control vs. Treatment)  
- Output: Table of differentially expressed genes  

Inspect:
- `log2FoldChange`
- `padj` (adjusted p-value)
- Volcano plot or MA plot (optional)

---

## Hands on: Step 6 — Interpretation

- Which genes are significantly upregulated in the treatment condition?  
- Do any correspond to known virulence factors, secretion systems, or regulatory proteins?  
- Explore functions using gene names or cross-referencing with databases such as KEGG or UniProt.

---

## Hands on: Optional clean-up

When finished:
- Delete intermediate datasets (e.g., raw FastQC reports, intermediate BAMs).  
- Keep your `featureCounts` table and DESeq2 results for interpretation.  

---

## Summary

You have successfully:
- Imported RNA-seq data from Zenodo into Galaxy  
- Performed read QC and alignment  
- Quantified gene expression  
- Identified differentially expressed genes between two bacterial conditions  

This workflow mirrors a real research scenario, simplified for clarity and speed.

---


