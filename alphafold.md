# Tutorial Exercise: AI-Enabled Prediction of Protein Structures

**Objective:** Introduce students to AI-based approaches for predicting protein 3D structures, using **AlphaFold2** through the **ColabFold** platform.

---

## 1. Background

Protein structure prediction seeks to determine the 3D conformation of a protein from its amino acid sequence.  
Recent breakthroughs in **AI and deep learning**—notably **AlphaFold2** (DeepMind) and related models—have achieved near-experimental accuracy for many proteins.

### Key AI Tools

| Tool | Developer | Core Method | Access |
|------|------------|-------------|--------|
| **AlphaFold2** | DeepMind (2021) | Transformer-based deep learning using evolutionary information | Available via ColabFold (Google Colab), local installation, or AlphaFold DB |
| **ESMFold** | Meta AI (2022) | Protein language model trained on massive sequence datasets | Currently unreliable for browser-based folding (2025) |

---

## 2. Learning Outcomes

After completing this exercise, you should be able to:

- Explain the main principles of AI-driven protein structure prediction.  
- Use **ColabFold** to predict a 3D structure from an amino acid sequence.  
- Visualize and assess the predicted model’s confidence.  
- Discuss strengths and limitations of AI-based predictions.

---

## 3. Prerequisites

- Basic knowledge of protein structure (primary to quaternary).  
- Familiarity with the FASTA sequence format.  
- Internet access and a Google account (for Google Colab).  

Optional: Local visualization software such as **PyMOL** or **ChimeraX**.

---

## 4. Exercise Steps

### Step 1. Choose a Protein Sequence

Select a short amino acid sequence (100–300 residues).

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

### Step 2. Predict the Structure Using ColabFold (AlphaFold2)

1. Go to **ColabFold on Google Colab**:  
   👉 [https://colab.research.google.com/github/sokrypton/ColabFold](https://colab.research.google.com/github/sokrypton/ColabFold)
2. Open the notebook titled **AlphaFold2 (ColabFold)**.  
3. Log in with your Google account.  
4. In the notebook:
   - Run the setup cell to install dependencies.  
   - In the sequence input cell, paste your FASTA sequence (with header line).  
   - Choose the default settings for model type and number of recycles.  
5. From the Colab menu, select **Runtime → Run all**.  
6. Wait for the notebook to finish (≈10–20 min).  
7. Download the **PDB** structure file and view the automatically generated confidence plots.

---

### Step 3. Visualize the Predicted Structure

Use one of the following tools:

- **Mol\*** online viewer: [https://molstar.org/viewer](https://molstar.org/viewer)  
- **PyMOL**:  
  ```bash
  pymol example.pdb
  ```
- **ChimeraX**:  
  ```bash
  open example.pdb
  ```

Inspect:
- Secondary structures (α-helices, β-sheets).  
- Fold motifs and domains.  
- **pLDDT** confidence coloring (blue = high confidence; yellow/orange = low).

---

### Step 4. Interpret the Model

Discuss:
- What do high vs. low **pLDDT** values indicate?  
- Does the fold resemble known protein families?  
- How might low-confidence regions correspond to intrinsic disorder or flexible loops?  
- How would inaccuracies affect downstream modeling (e.g., docking, mutagenesis)?

Optional: Compare your model to a known structure using tools like **DALI** or **TM-align**.

---

## 5. Discussion Questions

1. What are the main innovations that allow AlphaFold2 to achieve high accuracy?  
2. How does ColabFold differ from the original AlphaFold2 implementation?  
3. What biological insights can be gained from pLDDT confidence values?  
4. What ethical or practical issues arise from relying solely on AI-predicted structures?

---

## 6. Extension (Optional)

- Predict a **mutant** version of your protein and compare its structure.  
- Use **AlphaFold-Multimer** (available in ColabFold) to predict a **protein–protein complex**.  
- Visualize confidence regions with color mapping in PyMOL or ChimeraX.

---

## 7. References & Further Reading

- Jumper et al. (2021). *Highly accurate protein structure prediction with AlphaFold.* **Nature**, 596, 583–589.  
- Baek et al. (2021). *Accurate prediction of protein structures and interactions using a three-track neural network.* **Science**, 373(6557), 871–876.  
- ColabFold documentation: [https://github.com/sokrypton/ColabFold](https://github.com/sokrypton/ColabFold)  
- AlphaFold Protein Structure Database: [https://alphafold.ebi.ac.uk/](https://alphafold.ebi.ac.uk/)

---
