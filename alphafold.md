
# AI-Enabled Prediction of protein structures


## 1. Background

Protein structure prediction aims to determine the three-dimensional conformation of a protein from its amino acid sequence. Traditionally, this has relied on **homology modeling**, **threading**, or **ab initio** methods.  
Recent advances in **AI and deep learning** have revolutionized the field, achieving near-experimental accuracy for many proteins.

### Key AI Tools

| Tool | Developer | Core Method | Access |
|------|------------|-------------|--------|
| **AlphaFold2** | DeepMind (2021) | Transformer-based neural network trained on protein databases | Available via Google Colab, AlphaFold DB, or local installation |
| **ESMFold** | Meta AI (2022) | Large language model (ESM-2) trained on protein sequences | Accessible through the ESMFold web interface or API |

---

## 2. Learning Outcomes

After completing this exercise, you should be able to:

- Explain the main principles of AI-driven protein structure prediction.
- Use an online AI-based tool to predict the structure of a given protein sequence.
- Visualize and assess the predicted model.
- Discuss limitations and ethical considerations of AI-based predictions.

---

## 3. Prerequisites

- Basic understanding of protein structure (primary–quaternary levels)
- Familiarity with FASTA format
- Internet access and a web browser

Optional: Python environment with Biopython and PyMOL or ChimeraX for local visualization.

---

## 4. Exercise Steps

### Step 1. Choose a Protein Sequence

Obtain a short amino acid sequence (100–300 residues).  
Options:
- Retrieve a known protein (e.g., human lysozyme) from **UniProt**.
- Use your own research sequence.

Save the sequence in FASTA format (e.g., `example.fasta`).

Example:

```
>Example_protein
MKLFWLLFTIGFCWAQYEVQEKGGLTTEKDELQDKA...
```


---

### Step 2. Predict the Structure Using ESMFold

1. Go to the **ESMFold** web interface: [https://esmatlas.com/resources?action=fold](https://esmatlas.com/resources?action=fold)
2. Paste your sequence into the input box.
3. Submit the prediction and wait for the results.
4. Download the **PDB** file of the predicted model.

Alternative: If you prefer AlphaFold2, try **ColabFold**:  
[https://colab.research.google.com/github/sokrypton/ColabFold](https://colab.research.google.com/github/sokrypton/ColabFold)

---

### Step 3. Visualize the Predicted Structure

Use an online or local molecular viewer such as:

- **Mol\*** (https://molstar.org/viewer)
- **PyMOL** (`pymol example.pdb`)
- **ChimeraX** (`open example.pdb`)

Inspect:
- Secondary structures (helices, sheets)
- Fold motifs
- Predicted Local Distance Difference Test (**pLDDT**) confidence scores

---

### Step 4. Interpret the Model

Discuss:
- What does the model’s confidence tell you?
- Does the predicted fold match known homologous structures?
- How might inaccuracies affect downstream applications (e.g., docking or mutagenesis studies)?

Optional: Compare your model to a known structure using the **Protein Data Bank (PDB)** or tools like **DALI** or **TM-align**.

---

## 5. Discussion Questions

1. What types of data were used to train AlphaFold2 and ESMFold?
2. How do attention mechanisms and multiple sequence alignments contribute to accuracy?
3. What are potential limitations or ethical issues in relying on AI-predicted structures?
4. How might these tools change experimental structural biology workflows?

---

## 6. Extension (Optional)

- Try predicting a **mutant version** of your protein and compare its structure.
- Explore **protein–protein complex prediction** using **AlphaFold-Multimer**.
- Visualize confidence regions with color mapping in PyMOL or ChimeraX.

---

## 7. References & Further Reading

- Jumper et al. (2021). *Highly accurate protein structure prediction with AlphaFold.* **Nature**, 596, 583–589.  
- Baek et al. (2021). *Accurate prediction of protein structures and interactions using a three-track neural network.* **Science**, 373(6557), 871–876.  
- Lin et al. (2023). *Language models of protein sequences enable evolutionary-scale structure prediction.* **Science**, 379(6637), 1123–1130.  
- AlphaFold Protein Structure Database: [https://alphafold.ebi.ac.uk/](https://alphafold.ebi.ac.uk/)  
- ESM Atlas: [https://esmatlas.com/](https://esmatlas.com/)
- [AlphaFold: A practical guide](https://www.ebi.ac.uk/training/online/courses/alphafold/accessing-and-predicting-protein-structures-with-alphafold/choosing-how-to-access-alphafold/) by Paulyna Gabriela Magana Gomez and Oleg Kovalevskiy.


---



