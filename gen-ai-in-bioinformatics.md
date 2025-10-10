
- Nguyen, E., Poli, M., Durrant, M. G., Kang, B., Katrekar, D., Li, D. B., Bartie, L. J.,
Thomas, A. W., King, S. H., Brixi, G., Sullivan, J., Ng, M. Y., Lewis, A., Lou, A., Ermon, S.,
Baccus, S. A., Hernandez-Boussard, T., Ré, C., Hsu, P. D., & Hie, B. L. (2024).
**Sequence modeling and design from molecular to genome scale with Evo**. *Science*, 386, eado9336.
https://doi.org/10.1126/science.ado9336
- Theodoris C. V. (2024). **Learning the language of DNA**. _Science_, 386, 729–730. https://doi.org/10.1126/science.adt3007
- [Evo Designer](https://arcinstitute.org/tools/evo/evo-designer)
- [SynGenome](https://arcinstitute.org/tools/syngenome) - autocomplete a genome sequence!
- [Pretraining a Large Language Model (LLM) from Scratch on DNA Sequences](https://training.galaxyproject.org/training-material/topics/statistics/tutorials/genomic-llm-pretraining/tutorial.html)


# Evo Designer Tutorial Exercise  

**Tool:** [Evo Designer (Arc Institute)](https://arcinstitute.org/tools/evo/evo-designer)

---

## 1. Overview

Evo Designer is an interactive interface for **Evo 2**, a large generative model trained on billions of natural DNA sequences.  
It can generate, extend, and evaluate DNA sequences, providing insight into how machine learning models understand genomic information.

In this exercise, you will:
- Explore the **generation** of new DNA sequences from prompts.
- **Extend** existing sequences.
- **Evaluate** natural and synthetic DNA with Evo’s scoring features.
- **Interpret** the results and reflect on their biological meaning.

---

## 2. Learning Objectives

By the end of this tutorial, you should be able to:

1. Use Evo Designer to generate DNA sequences from text or organism prompts.  
2. Extend partial DNA sequences and inspect predicted annotations.  
3. Score a DNA sequence to visualize model confidence (entropy / perplexity).  
4. Compare outputs across different prompts and analyze patterns.  
5. Critically discuss the possibilities and limits of generative DNA modeling.

---

## 3. Getting Started

1. Open Evo Designer in a browser:  
   ➜ [https://arcinstitute.org/tools/evo/evo-designer](https://arcinstitute.org/tools/evo/evo-designer)

2. Familiarize yourself with the interface:
   - **Mode selector:** choose “Generate,” “Continue,” or “Score.”
   - **Prompt options:** choose by organism or enter your own text.
   - **Visualization panels:** view DNA sequences, annotations, entropy plots, and predicted protein structures.

3. Work individually or in pairs. Keep notes of your prompts, outputs, and observations.

---

## 4. Exercises

### **Exercise 1 – Generate a DNA Sequence**
- In “Generate” mode, choose **an organism** (e.g. *E. coli*, *Human*, *Saccharomyces cerevisiae*) and a gene name or short description.
- Click *Generate* and observe:
  - The resulting DNA sequence length.
  - Any predicted coding regions.
  - GC content (approximate visually or copy to another tool).
  - If available, predicted 3D protein structure.

**Questions:**
- How plausible does the sequence look (e.g. open reading frames, start/stop codons)?
- What features might make it look “natural” or not?

---

### **Exercise 2 – Continue a Known Sequence**
- Switch to “Continue” mode.
- Paste the first ~200 bp of a known gene (e.g. *lacZ*, *gapdh*, or another of your choice).
- Generate a continuation.

**Questions:**
- Does the continuation maintain the correct reading frame?
- How similar or different is the GC content from the original fragment?
- What do you notice about entropy patterns at the junction between the input and generated region?

---

### **Exercise 3 – Score a Sequence**
- In “Score” mode, paste two sequences:
  1. A natural gene sequence (from NCBI or another database).
  2. A randomized or “scrambled” sequence of similar length.

- Observe the entropy/perplexity plots.

**Questions:**
- Are coding regions associated with lower entropy?
- How does the model’s confidence differ between natural and random sequences?

---

### **Exercise 4 – Compare Prompts**
- Generate sequences using two different prompts, such as:
  - *E. coli gyrA*
  - *Haloferax volcanii secY*

**Questions:**
- How do GC content, annotations, or predicted structures differ?
- What might these differences suggest about the model’s learned representation of species-specific patterns?

---

### **Exercise 5 (Optional) – Explore Model Creativity**
- Try to “steer” the generation:
  - Provide partial sequences.
  - Combine multiple ideas in one prompt (e.g. *E. coli enzyme for antibiotic resistance*).
  - Generate several outputs and compare diversity.

**Questions:**
- How consistent are the results?
- Do the sequences vary substantially between runs?


---

## Discussion and Reflection

Discuss with fellow students and instructors:
- How “design” and “prediction” differ in biological modeling.  
- What kinds of tasks might be suitable for generative DNA tools.  
- What ethical or safety considerations should apply to sequence generation.

---


### Key Takeaway

> Evo Designer illustrates how large language models trained on biological sequences can generate plausible genetic material—but **interpretation and validation remain essential.**  
> Use this exercise to practice critical thinking at the intersection of AI and biology.
