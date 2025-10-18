# Exploring AI-predicted protein structures

**Objective:** Introduce students to AI-predicted protein structures using the AlphaFold Protein Structure Database and practice interpretation, visualization, and structural analysis.

---

## 1. Background

Protein structure prediction seeks to determine the 3D conformation of a protein from its amino acid sequence.  
Recent breakthroughs in **AI and deep learning**—notably **AlphaFold2** (DeepMind) and related models—have achieved near-experimental accuracy for many proteins.

### Key AI Tools

| Tool | Developer | Core Method | Access |
|------|------------|-------------|--------|
| **AlphaFold2** | DeepMind (2021) | Transformer-based deep learning using evolutionary information | Available via ColabFold (Google Colab), local installation, or AlphaFold DB |
| **ESMFold** | Meta AI (2022) | Protein language model trained on massive sequence datasets | Currently unreliable for browser-based folding (2025) |

The AlphaFold Protein Structure Database contains **millions of predicted structures** for proteins across multiple species. These predictions include **per-residue confidence scores (pLDDT)**.  
This exercise focuses on **structure visualization, interpretation, and comparative analysis** using precomputed structures, avoiding ab initio prediction.

---

## 2. Learning Outcomes

After completing the exercise, you should be able to:

- Retrieve AI-predicted protein structures from the AlphaFold Database.  
- Visualize protein 3D structures in web-based or local tools.  
- Interpret confidence metrics (pLDDT) and relate them to structural features.  
- Compare predicted structures with experimentally determined structures from the PDB.

---

## 3. Prerequisites

- Familiarity with protein sequences and FASTA format.  
- Basic understanding of secondary and tertiary structure.  
- Internet access; no special accounts required.  

Optional: Local molecular visualization tools (PyMOL, ChimeraX) for advanced analysis.

---

## 4. Exercise steps

### Step 1: Select a protein

- Pick a protein of interest. Options include:
  - Human proteins (UniProt ID, e.g., **P69905** for hemoglobin alpha).  
  - Bacterial or viral proteins (UniProt ID or gene name).  
- Note the **UniProt accession** and species.

---

### Step 2: Query the AlphaFold database

1. Go to [https://alphafold.ebi.ac.uk/](https://alphafold.ebi.ac.uk/)  
2. Enter the **UniProt ID or gene name** in the search bar.  
3. Browse the results and select the relevant protein entry.

---

### Step 3: Explore the predicted structure

- View the structure in the embedded **Mol\*** viewer.  
- Observe:
  - **Secondary structure elements**: α-helices, β-sheets, loops.  
  - **Confidence scores (pLDDT)**: color-coded (blue = high confidence, orange/yellow = low).  
  - Domains and predicted fold.

---

### Step 4: Analyze and compare

1. Identify **high- and low-confidence regions**.  
2. Optional: Download the PDB file for local analysis in **PyMOL** or **ChimeraX**.  
3. Compare the predicted structure to any **known experimental structures** in the PDB (if available):
   - Use **RCSB PDB**: [https://www.rcsb.org/](https://www.rcsb.org/)  
   - Use structural alignment tools like **TM-align** or **DALI** to quantify similarity.
4. Discuss:
   - Do predicted folds match experimentally determined structures?  
   - Are flexible loops and low-confidence regions consistent with expected disorder?

---

### Step 5: Optional comparative exploration

- Pick homologs from other species and compare AlphaFold structures to explore **conservation of fold**.  
- Identify residues that are **highly conserved and well-predicted** versus variable and low-confidence.

---

## 5. Discussion questions

1. How reliable are AI-predicted structures for regions with low sequence conservation?  
2. How do confidence scores (pLDDT) relate to experimental uncertainty or disorder?  
3. What insights can structural comparisons across species provide?  
4. How could these predicted structures inform experimental design (mutagenesis, docking, etc.)?

---


## 7. References

- AlphaFold Protein Structure Database: [https://alphafold.ebi.ac.uk/](https://alphafold.ebi.ac.uk/)  
- Jumper et al. (2021). *Highly accurate protein structure prediction with AlphaFold.* **Nature**, 596, 583–589.  
- Tunyasuvunakool et al. (2021). *Highly accurate protein structure prediction for the human proteome.* **Nature**, 596, 590–596.

---

## 8. Optional Extension: *Ab initio* structure prediction

If you want to explore **de novo prediction** (predicting a structure directly from sequence):

1. **ColabFold (AlphaFold2)**
   - Google Colab notebook: [https://colab.research.google.com/github/sokrypton/ColabFold](https://colab.research.google.com/github/sokrypton/ColabFold)  
   - Enter your protein sequence and run the notebook.  
   - Produces predicted 3D structures and per-residue confidence scores.  
   - **Note:** Requires a Google account and may take 10–20 minutes per protein.

2. **ESMFold (Meta AI)**
   - Uses a protein language model to predict structures from sequence.  
   - Web interface: [https://esmatlas.com/resources?action=fold](https://esmatlas.com/resources?action=fold)  
   - **Caveat:** Browser interface may be unreliable; download or local execution may be more stable.

**Tip:** This optional extension is for students interested in running predictions themselves, but it is not required to complete the main database-based exercise.
This is useful if you are investigating a protein for which no prediction has been deposited in the AlphaFold database. And example is the prediction of structures for druggable proteins of the Mpox virus. See:
Sahu, A., Gaur, M., Mahanandia, N. C., Subudhi, E., Swain, R. P., & Subudhi, B. B. (2023). Identification of core therapeutic targets for Monkeypox virus and repurposing potential of drugs against them: An *in silico* approach. *Computers in Biology and Medicine*, 161, 106971. [https://doi.org/10.1016/j.compbiomed.2023.106971](https://doi.org/10.1016/j.compbiomed.2023.106971).

---
