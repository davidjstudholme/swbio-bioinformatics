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

Here is an overview of the Galaxy workflow:

![Galaxy workflow for RNA-seq exercise](<rna-seq/Screenshot 2025-10-10 202711.jpg>)

View image: [Galaxy workflow for RNA-seq exercise](<rna-seq/Screenshot 2025-10-10 202711.jpg>).


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
I used [this tool in Galaxy](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fiuc%2Fseqtk%2Fseqtk_sample%2F1.5%2Bgalaxy0&version=latest)
to do the downsampling.
Note that we also not including replicates in this analysis, to save time and avoid complexity.
When performing research, it would be necessary to include several replicates of the treatmenet and the control.

- The data are from: [BioProject PRJNA261679](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA261679)
- Original study: Kim, S., Cho, Y. J., Song, E. S., Lee, S. H., Kim, J. G., & Kang, L. W. (2016). Time-resolved pathogenic gene expression analysis of the plant pathogen *Xanthomonas oryzae* pv. *oryzae*. *BMC Genomics*, **17**, 345. [https://doi.org/10.1186/s12864-016-2657-7](https://doi.org/10.1186/s12864-016-2657-7).

---

## Step 1: Import the provided RNA-seq data into Galaxy

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
   - Give the collection a suitable name, e.g. `RNA-seq paired reads`. [Image](<rna-seq/Screenshot 2025-10-10 114827.jpg>) and press the **Build** button.
   - The new collection will appear in your Galaxy history, looking something like this [image](<rna-seq/Screenshot 2025-10-10 114917.jpg>).

     
---

## Step 2: Quality control
Run **FastQC** on the paired-end collection.

- Tool: [FastQC](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fdevteam%2Ffastqc%2Ffastqc%2F0.74%2Bgalaxy1&version=latest)  
- Input: Your paired-end dataset collection. [Image](<rna-seq/Screenshot 2025-10-10 115047.jpg>).  
- Output: Inspect the HTML reports for quality, GC content, adapter contamination, etc.  
- Run **fastp** to filter-out poor data. [Image](<rna-seq/Screenshot 2025-10-10 120653.jpg>).
   - Input: Collection of paired RNA-seq sequencing reads.
   - Use the default settings for all other options.
   - Output: a new collection called something like `fastp on collection 9: Paired-end output`. This contains the trimmed, filtered, paired reads.

---

## Step 3: Align RNA-seq reads against a reference genome

For this step, we first need to obtain the *Xanthomonas oryzae* pv. *oryzae* reference genome (in FASTA format).
The file can be obtained from the the NCBI, via their FTP site, with this URL:

```
https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/007/385/GCA_000007385.1_ASM738v1/GCA_000007385.1_ASM738v1_genomic.fna.gz
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

Now we have BAM files that contain the RNA-seq reads against the reference genome sequence. Optionally, at this point, we could visualise the alignments
using a genome browser such as [IGV](https://igv.org/). 

---

## Step 4: Count reads per gene

Now that we have aligned the RNA-seq reads against the reference genome, next we need to quantify the results.
The amount of reads aligned to a gene is a correlated with the abundance of the corresponding transcript in the biological sample.
Our aim is to identify genes that are differentially expressed between the control versus the treated samples.
Therefore, for each gene in the reference genome, we will count how many control-sample reads are aligned and how many treated-sample reads are aligned.
That will enable us to compare the two samples and identify genes that show differences in control versus treated.

To acheive this, we will use a tool called
[featureCounts](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fiuc%2Ffeaturecounts%2Ffeaturecounts%2F2.1.1%2Bgalaxy0&version=latest).

In addition to the alignments of reads against the referece genome, we also need a file that specifies the coordinates of every gene on the reference genome.
That file is in GFF3 format and can be obtained from the NCBI's FTP site at this URL:

```
https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/007/385/GCA_000007385.1_ASM738v1/GCA_000007385.1_ASM738v1_genomic.gff.gz
```

1. Upload the GFF3 file from NCBI into Galaxy (using Galaxy's **Upload** button).
   - The GFF3 file will appear in your Galaxy history. [Image](<rna-seq/Screenshot 2025-10-10 130904.jpg>).
   - Optionally, you can rename the GFF file in your Galaxy history
2. Run featureCounts. [Image](<rna-seq/Screenshot 2025-10-10 131439.jpg>).
   - Alignment files: BAM files  output from BowTie2
   - Gene annotation file: GFF3 file that you uploaded in the previous step.
   - Output: Gene count matrices.
   - GFF feature type filter: "CDS".
   - GFF gene identifier: "locus_tag".
  
After running featureCounts, your Galaxy history will contain two new files containing the read-counts for each gene.
One file is for "control" and one is for "treatment". 
You can see the contents of one of the two files in this [image](<rna-seq/Screenshot 2025-10-10 132421.jpg>).
Remember that we want to *compare the two*. So, we need to somehow combine the two matrices into one.
There are many ways that we could acheive this.
One way is to use the [Join two datasets](https://usegalaxy.eu/?tool_id=join1&version=latest) tool in Galaxy.

- Click on the **Upload** button.
- Click on **Paste / Fetch data**.
- Insert the URL for the GFF3 file and press **Start**.
- When the file turns green, you can press **Close**.


After running featureCounts, you will have two tables of results.
One consists of read-counts for the control and the other table has read-counts for the treatment.

3. To compare treatment versus control, we need to combine the two tables into one:
   - In the history, enable viwing of hidden datasets by clicking on the "crossed eye" icon. 
   - Tick the boxes for the two datasets that are the matrices generated by featureCounts. [Image](<rna-seq/Screenshot 2025-10-10 142254.jpg>).
   - Click on the drop-down menu that says "2 of x selected".
   - Click on  **Unhide** in the drop-down menu. [Image](<rna-seq/Screenshot 2025-10-10 142152.jpg>).
   - Once you have unhidden those two datasets, run [Join two datasets](https://usegalaxy.eu/?tool_id=join1&version=latest):
      - For **Join** and **with**, Select the two matrix datasets. [Image](<rna-seq/Screenshot 2025-10-10 142152.jpg>)
      - For **Using column**, select "Column 1" for both.
      - Press **Run Tool**.
   - This will generate a new matrix dataset in your Galaxy history.

---

## Step 5: Identify differentially expressed genes

We now have a matrix that enumerates the numbers of aligned reads against each gene in the treatment and in the control.
If you view that matrix in Galaxy, it will look something like this [image](<rna-seq/Screenshot 2025-10-10 143014.jpg>).

Now we need to examine this matrix and identify which genes are different in their coverage-by-reads.

If we were doing this for real research then we would use an automated tool such as
[DESeq2](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fiuc%2Fdeseq2%2Fdeseq2%2F2.11.40.8%2Bgalaxy0&version=latest) or
[edgeR](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fiuc%2Fedger%2Fedger%2F3.36.0%2Bgalaxy5&version=latest) or
[Salmon](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fbgruening%2Fsalmon%2Fsalmon%2F1.10.1%2Bgalaxy2&version=latest).
Those tools contain fairly sophisticated models of the expected data and its inherent nose and biases. They are able to consider multiple replicates
of each treatment and thereby infer statistical significance of any observed differences.

If you are seriously interested in performing RNA-seq analysis yourself as part of your PhD project, then I recommend that you explore those tools further.
Also, see the Galaxy training materials available [here](https://training.galaxyproject.org/training-material/topics/transcriptomics/).

However, for most of us here, it will be sufficient today to take a much-simplified approach to illustrate the basic prinicples.
Here, I will illustrate the steps using a MS Excel spreadsheet. But, you could perform the steps in a different platform, such as R.

- Use the "disk" icon to download the matrix. [Image](<rna-seq/Screenshot 2025-10-10 171505.jpg>).
- This will download a file into your Download folder, called something like `Galaxy47-[Join two Datasets on data 40 and data 42].tabular`. [Image](<rna-seq/Screenshot 2025-10-10 171740.jpg>).
- Rename the file to something more sensible, like `read-counts.tsv`. [Image](<rna-seq/Screenshot 2025-10-10 172221.jpg>).
- Now import the file into your favourite spreadsheet software, e.g. MS Excel. [Image](<rna-seq/Screenshot 2025-10-10 172612.jpg>).
- Now that the data are imported, note that the third column is redundant [Before deletion](<rna-seq/Screenshot 2025-10-10 172718.jpg>); so, delete that column. [After deletion](<rna-seq/Screenshot 2025-10-10 172917.jpg>)
- In the final column, add the formula: `=LOG([@treatment]/[@control])`. [Image](<rna-seq/Screenshot 2025-10-10 173032.jpg>).
- Now we can see log-ratios for all genes. [Image](<rna-seq/Screenshot 2025-10-10 173101.jpg>).
- Sort the data on the log-ratio column. 
- Re-name the columns and format the cells in the final column so it looks something like this [image](<rna-seq/Screenshot 2025-10-10 173624.jpg>).
- Now, the most-differentially expressed genes are to be found at the top and the bottom of the spreadsheet.
- Another way of looking at this is as a histogram showing the frequency distribution of the log-ratio. The differentially expressed genes are in the tails. [Image](<rna-seq/Screenshot 2025-10-10 174412.jpg>).
- Alternatively, you could plot the numbers of counts for control versus treatment, and identify the genes that diverge from the correlation. [Image](<rna-seq/Screenshot 2025-10-10 174103.jpg>).
  
---

## Step 6: Interpretation

- Which genes are significantly upregulated in the treatment condition?  
- Do any correspond to known virulence factors, secretion systems, or regulatory proteins?  
- Explore functions using gene names or cross-referencing with databases such those found at NCBI or KEGG or UniProt.

You can interactively explore the data by visualing the BAM-formatted alignments in the IGV genome browser:

- Download the two BAM files and there accompanying index files from your Galaxy history. [Image](<rna-seq/Screenshot 2025-10-10 192109.jpg>).
- The four files should now be in your Downloads folder. [Image](<rna-seq/Screenshot 2025-10-10 192306.jpg>).
- Rename the files to something more informative and simple (`control.bam`, etc.). [Image](<rna-seq/Screenshot 2025-10-10 192652.jpg>).
- Download the reference genome sequence and the GFF3 annotation from the NCBI FTP site (see URLs above). [Image](<rna-seq/Screenshot 2025-10-10 192954.jpg>).
- Navigate your web-brower to [https://igv.org/app/](https://igv.org/app/) to open the IGV web application.
- Use the **Genome->Local File** menu item to load the FASTA-formatted reference genome sequence into IGV.
- Use the **Tracks->Local File** menu item to load the GFF3-formatted annotation into IGV.
- Use the **Tracks->Local File** menu item to load the two BAM files and their accomapnying BAI files. [Image](<rna-seq/Screenshot 2025-10-10 193255.jpg>).
- Use the zoom tool near the top-right of the IGV page to zoom in on any part of the genome. It should look something like this [image](<rna-seq/Screenshot 2025-10-10 193518.jpg>). Check that you undertsnad what you are looking at. Ask, if you are unsure.
- Choose some differentially expressed genes from the spreadhseet. [Image](<rna-seq/Screenshot 2025-10-10 193713.jpg>).
- Try to locate those genes in the IGV browser and notice the differening abundances of RNA-seq reads at those genes. E.g. see this [image](<rna-seq/Screenshot 2025-10-10 194211.jpg>).
   - Gene _fecA_ clearly shows more abundant mRNA in the treatment than in the control. Locus tag XOO0901 corresponds to gene _fecA_.
   - You can find out more about XOO0901 / _fecA_ at [https://www.ncbi.nlm.nih.gov/protein/?term=XOO0901](https://www.ncbi.nlm.nih.gov/protein/?term=XOO0901).
   - Gene _glpQ_ clearly shows more abundant mRNA in the treatment than in the control. Locus tag XOO0902 corresponds to gene _glpQ_.
   - You can find out more about XOO0902 / _glpQ_ at  [https://www.ncbi.nlm.nih.gov/protein/?term=XOO0902](https://www.ncbi.nlm.nih.gov/protein/?term=XOO0902).
- Further examples of differentially expressed genes can be seen in the example below.
   - Can you find a gene whose transcription is _increased_ in the treatment versus the control?
   - Can you find a gene whose transcription is _decreased_ in the treatment versus the control?

![Example DEGs visualised in IGV](<rna-seq/Screenshot 2025-10-10 194555.jpg>)

View image: [Example DEGs visualised in IGV](<rna-seq/Screenshot 2025-10-10 194555.jpg>).


## Summary

You have successfully:
- Imported RNA-seq data from Zenodo into Galaxy.  
- Performed read QC and alignment.  
- Quantified gene expression.
- Identified differentially expressed genes between two bacterial conditions.
- Visualised and examined examples of differentially expressed genes in the IGV browser.

## ⚠️ Disclaimer — Interpreting results without replicates

In this exercise, we are working with **only one RNA-seq sample per condition** (one control and one treatment).  
This simplified setup makes the workflow fast and easy to follow, but it also means that:

- We **cannot estimate biological variability**,  
- and therefore **cannot perform valid statistical testing** for differential expression.

In real research, **biological replicates** (typically three or more per condition) are essential.  
Replicates allow tools such as **DESeq2** and **edgeR** to model natural variation in gene expression and to identify genes that are *significantly* differentially expressed rather than simply showing random differences.

Because we have no replicates here, any comparison between the two samples is **descriptive only**.  
We can look at read counts and fold changes to see which genes *appear* more or less expressed, but these differences cannot be interpreted as statistically significant.

### A note on normalization

Raw read counts are influenced by factors such as:
- total sequencing depth (number of reads per sample), and  
- gene length (longer genes naturally produce more reads).

To make counts comparable across samples, RNA-seq analyses normally include a **normalization** step.  
Different tools use different methods:
- DESeq2: median of ratios (size-factor normalization)  
- edgeR: trimmed mean of M-values (TMM)  
- TPM/RPKM: length and library-size normalization for exploratory analysis  

In this simplified example, we are inspecting **raw featureCounts output**.  
If the two libraries have very different total read depths, fold changes may be misleading. In this example, we started with the same numer of sequence reads (2,000,000) for both samples; so, we can get away without normalising in this case.

**Conclusion:**  
This session demonstrates *how* RNA-seq data are processed and compared, not *how to make statistically valid biological conclusions*.  
The concepts you learn here — mapping, counting, combining, and interpreting data — are the foundation for more rigorous analyses once replicates and normalization are added.

---

# Further information about RNA-seq analysis
For a more in-depth and realistic tutorial on analysing RNA-seq data in Galaxy, please see:

- [Reference-based trascriptomics tutorial](<https://training.galaxyproject.org/training-material/topics/transcriptomics/tutorials/ref-based/tutorial.html>)
- [Transcriptomics tutorial](<https://gallantries.github.io/video-library/modules/transcriptomics>)


