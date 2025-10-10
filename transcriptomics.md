# 🧬 RNA-seq Analysis of *Xanthomonas oryzae*

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

We will work with **downsampled data** (a few hundred thousand reads per sample) to make the analysis quick and manageable for classroom use.

---

## Hands on: Step 1 — Import the provided RNA-seq data into Galaxy

You will import **two samples** (paired-end FASTQ files):

| Condition | Read 1 (R1) | Read 2 (R2) |
|------------|-------------|-------------|
| Control | [🔗 Zenodo link for R1](https://zenodo.org/record/XXXXX/files/Xoo_control_R1.fastq.gz) | [🔗 Zenodo link for R2](https://zenodo.org/record/XXXXX/files/Xoo_control_R2.fastq.gz) |
| Treatment | [🔗 Zenodo link for R1](https://zenodo.org/record/YYYYY/files/Xoo_treatment_R1.fastq.gz) | [🔗 Zenodo link for R2](https://zenodo.org/record/YYYYY/files/Xoo_treatment_R2.fastq.gz) |

### To import the data in Galaxy:
1. Go to [your Galaxy server](https://usegalaxy.eu) (or your course instance).  
2. From the top menu, choose **“Upload Data.”**
3. Click the **“Paste/Fetch Data”** tab.  
4. Paste the four Zenodo URLs listed above into the box (one per line).  
5. Click **“Start.”**
6. Wait until all datasets turn green (completed).  
7. Rename the datasets for clarity (e.g. `control_R1`, `control_R2`, `treatment_R1`, `treatment_R2`).
8. Build a **paired dataset collection**:
   - Select all four FASTQs  
   - Click **“Build List of Dataset Pairs”**  
   - Pair R1/R2 correctly and name the collection, e.g. `Xoo_downsampled_reads`.

---

## Hands on: Step 2 — Quality control
Run **FastQC** on the paired-end collection.

- Tool: **FastQC**  
- Input: Your paired-end dataset collection  
- Output: Inspect the HTML reports for quality, GC content, adapter contamination, etc.  
- Optional: Run **MultiQC** to summarize results.

---

## Hands on: Step 3 — Map reads to the reference genome

1. Get the *Xanthomonas oryzae* pv. *oryzae* reference genome (FASTA) and annotation (GFF/GTF).  
   - You can import them from Galaxy’s **“Reference Data”** section or from ENA/NCBI:
     - Genome: [NCBI link, e.g. `GCF_000007615.1`](https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_000007615.1/)
     - Annotation: Corresponding GFF3 file.
2. Run **HISAT2** (or another aligner such as Bowtie2 or STAR):
   - Input: The paired-end collection  
   - Reference genome: *Xoo* FASTA  
   - Output: BAM alignment files  

---

## Hands on: Step 4 — Count reads per gene

Use **featureCounts** to summarize aligned reads per gene.

- Input: BAM files  
- Annotation: GFF3 file  
- Output: Gene count matrix  

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

### Credits

- Data re-used from [BioProject PRJNA261679](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA261679)
- Original study: Kim, S., Cho, Y. J., Song, E. S., Lee, S. H., Kim, J. G., & Kang, L. W. (2016). Time-resolved pathogenic gene expression analysis of the plant pathogen *Xanthomonas oryzae* pv. *oryzae*. *BMC Genomics*, **17**, 345. https://doi.org/10.1186/s12864-016-2657-7.
- Prepared for the Graduate Bioinformatics Workshop, [University/Year].

---

