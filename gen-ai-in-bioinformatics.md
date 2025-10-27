# Evo Designer Tutorial Exercise  

**Tool:** [Evo Designer (Arc Institute)](https://arcinstitute.org/tools/evo/evo-designer)

---

## 1. Overview

Evo Designer is an interactive interface for **Evo 2**, a large generative model trained on billions of natural DNA sequences.  
It can generate, extend, and evaluate DNA sequences, providing insight into how machine learning models understand genomic information.

A generative AI tool such as ChatGPT generates generates new text,
based on the user-supplied prompt and its underlying large language model (LLM). That LLM has been built on text (from internet, documents, bbooks etc.).

Evo 2 is somewhat analogous to such AI chat tools.
The fundamental difference is that it generates DNA sequences instead of text. Its underlying LLM has been trained on nulceotide sequences instead of text. 

In this exercise, you will:
- Explore the **generation** of new DNA sequences from prompts.
- **Extend** existing sequences.
- **Evaluate** natural and synthetic DNA with Evo’s scoring features.
- **Interpret** the results and reflect on their biological meaning.

---

## 2. Learning Objectives

By the end of this tutorial, you should be able to:

1. Use Evo Designer 2 to generate DNA sequences from text- or organism- prompts.  
2. Extend partial DNA sequences and inspect predicted annotations iof those generated sequences.  
3. Score a DNA sequence to visualize model confidence (entropy).  
4. Compare outputs across different prompts and analyze patterns.  
5. Critically discuss the possibilities and limits of generative DNA modeling.

---

## 3. Getting Started

1. Open Evo Designer in a browser:  
   - [https://arcinstitute.org/tools/evo/evo-designer](https://arcinstitute.org/tools/evo/evo-designer)

2. Familiarize yourself with the interface:
   - **Mode selector:** you can “[Generate](<evo/Screenshot 2025-10-18 140506 generate.jpg>)” or “[Score](<evo/Screenshot 2025-10-18 140506 score.jpg>)” a sequence.
   - **Prompt options:** you can continue a sequence that you generated or that you entered.
   - **Visualization panels:** view DNA sequences, annotations, entropy plots, and predicted protein structures.
   - **Settings:** you can control several [options and parameters](<evo/Screenshot 2025-10-18 142005 settings for generate.jpg>) for sequence generation.

3. Work individually or in pairs or samll groups. Keep notes of your prompts, outputs, and observations.

---

## 4. Exercises

### **Exercise 1 – Generate a DNA Sequence** "from scratch"
- In “Generate” mode, choose [an organism](<evo/Screenshot 2025-10-18 140506 organism.jpg>) (e.g. Human)
- Click **Generate** and observe:
  - The resulting DNA sequence length.
  - Any predicted coding regions.
  - GC content (e.g. copy and paste into ).
  - If available, predicted 3D protein structure.
- Repeat this process several times to generate several DNA sequences from this species (e.g. Human).
- Repeat this process several times to generate sequences for a different species (e.g. *Mycobcaterium tuberculosis*).

| Species                      | Sequence generated | G+C content  | Protein product(s)? | 
| --------------------------   | ------------------ | ------------ | ------------------- |  
| Human                        | First attempt      |              |                     |   
| Human                        | Second attempt     |              |                     |   
| Human                        | Third attempt      |              |                     |   
| Human                        | Fourth attempt     |              |                     |   
| *Mycobacterium tuberculosis* | First attempt      |              |                     |   
| *Mycobacterium tuberculosis* | Second attempt     |              |                     |   
| *Mycobacterium tuberculosis* | Third attempt      |              |                     |   
| *Mycobacterium tuberculosis* | Fourth attempt     |              |                     | 

Note: this illustrates that genomes of different species have different charateristic nucleotide composition. This includes percentage of G+C versus A+T.   

- In “Generate” mode, choose [an organism](<evo/Screenshot 2025-10-18 140506 organism.jpg>) (e.g. *E. coli*, Human, *Saccharomyces cerevisiae*) and a gene name or short description.
- Click **Generate** and observe:
  - The resulting DNA sequence length.
  - Any predicted coding regions.
  - GC content (approximate visually or copy to another tool).
  - If available, predicted 3D protein structure. 

**Questions:**
- How plausible does the sequence look (e.g. open reading frames, start/stop codons)?
- What features might make it look “natural” or not?


---

### **Exercise 2 – Continue a known sequence**
Now, rather than generating a sequence from scratch, we are going to provide some real DNA sequence as a prompt.
The tool will then continue the sequence, by generating new sequence to follow the prompt sequence.
- Make sure that you are in "Generate" mode.
- Paste the first ~200 bp of a known gene (e.g. *lacZ*, *gapdh*, or another of your choice) or click on one of the examples (e.g. *gyrA*) to automatically insert the example sequence. See [image](<evo/Screenshot 2025-10-18 142005 settings for generate.jpg>).
- Generate a continuation, by pressing **Generate**.
- Examine the [resulting sequence](<evo/Screenshot 2025-10-18 153516 gyrA result.jpg>).
   - Perform a [BLASTX](<evo/Screenshot 2025-10-18 154037 blastx form.jpg>) search at the [NCBI BLAST website](https://blast.ncbi.nlm.nih.gov/BlastAlign.cgi) to search your generated DNA sequence against real protein sequences.
 - Perform a BLASTN search at the [NCBI BLAST website](https://blast.ncbi.nlm.nih.gov/BlastAlign.cgi) to search your generated DNA sequence against real DNA sequences.

![resulting sequence](<evo/Screenshot 2025-10-18 153516 gyrA result.jpg>)

- Notice that the first part of the sequence is the prompt, which is the actual sequence from a real *gyrA* gene, indicated in orange in tis [image](<evo/Screenshot 2025-10-18 155603 gyrA blastn.jpg>).
- Notice that the remainder of the sequence is the synthetic sequence, generated by Evo 2
(indicated in yellow in the [image](<evo/Screenshot 2025-10-18 155603 gyrA blastn.jpg>)).
This generated sequence is "fictional" and therefore does not exactly match
any sequence in the public sequence databases; but it is very similar!

**Questions:**
- Does the continuation maintain the correct reading frame?
- How similar or different is the GC content from the original fragment?
- What do you notice about entropy patterns at the junction between the input and generated region?

---

### **Exercise 3 – Score a sequence**
- In “Score” mode, paste two sequences:
  1. A natural gene sequence (from NCBI or another database or use the supplied examples such as human *actB*).
  2. A randomized or “scrambled” sequence of similar/same length. You could use [this tool](<https://www.bioinformatics.org/sms2/shuffle_dna.html>) to scramble your sequence.

- Observe the entropy plots.
- Optionally, also try BLAST searches with the "real" sequence and with the scrambled sequence. The latter should not give any signiicant hits; there is a very low probability that a  random sequence will show significant similarity to a real genome or protein.

**Questions:**
- Are coding regions associated with lower entropy?
- How does the model’s confidence differ between natural and random sequences?

#### Understanding Evo 2 entropy scoring

When you use **“Score a sequence”**, the tool calculates how *predictable* each nucleotide is according to Evo 2’s learned model of natural DNA.

This is shown as an **entropy plot** across the sequence.

####  What entropy means

Entropy measures the **uncertainty** in the model’s prediction of the next base.

| Entropy value (bits) | Model’s confidence | Biological interpretation |
|----------------------:|--------------------|----------------------------|
| **0–0.5** | Very confident | Common or conserved patterns — often within coding regions or known motifs |
| **0.5–1.5** | Moderately confident | Typical biological variation, weakly constrained regions |
| **>1.5** | Uncertain | Unusual composition, boundaries, or potentially non-natural sequence |

*(If the model had no idea, entropy would reach ~2 bits per base — since log₂(4) = 2 for four nucleotides.)*

---

#### How to read the plot

- **Low, smooth regions:** likely structured or coding DNA that fits well with natural patterns.  
- **Spikes or jumps:** may indicate boundaries (e.g. start/stop codons) or unexpected motifs.  
- **Sustained high entropy:** the model finds the region surprising — could be synthetic, random, or atypical.

**Question:**
- Can you think of any practical applications of this entropy-based scoring of DNA sequences?

---


## Discussion and reflection

Discuss with fellow students and instructors:
- How do “design” and “prediction” differ in biological modeling? Find some additional thoughts about this [here](prediction-versus-design.md). 
- What kinds of tasks might be suitable for generative DNA tools?  
- What ethical or safety considerations should apply to sequence generation? Consider for example the concerns raised about [AI-generated bacteriophages](https://arcinstitute.org/news/hie-king-first-synthetic-phage), e.g. in [this LinkedIn post](<https://www.linkedin.com/posts/elenakyria_omg-is-this-a-major-breakthrough-or-have-activity-7375059508391342080-m-LT?utm_source=share&utm_medium=member_desktop&rcm=ACoAAAMpP9MBSCze3aWU9bT36byr7i3Hx7YidPw>).

---


### Key takeaway

- Evo Designer illustrates how large language models trained on biological sequences can generate plausible genetic material, but **interpretation and validation remain essential.**  
- Use this exercise to practice critical thinking at the intersection of AI and biology.

## Further reading

# LLMs and generative AI in bioinformatics
Background information can be found in these manuscripts and web pages:

- https://www.dataiku.com/stories/detail/what-is-a-large-language-model/
- Nguyen, E., Poli, M., Durrant, M. G., Kang, B., Katrekar, D., Li, D. B., Bartie, L. J.,
Thomas, A. W., King, S. H., Brixi, G., Sullivan, J., Ng, M. Y., Lewis, A., Lou, A., Ermon, S.,
Baccus, S. A., Hernandez-Boussard, T., Ré, C., Hsu, P. D., & Hie, B. L. (2024).
**Sequence modeling and design from molecular to genome scale with Evo**. *Science*, 386, eado9336.
https://doi.org/10.1126/science.ado9336
- Theodoris C. V. (2024). **Learning the language of DNA**. _Science_, 386, 729–730. https://doi.org/10.1126/science.adt3007
- [Evo Designer](https://arcinstitute.org/tools/evo/evo-designer)
- [SynGenome](https://arcinstitute.org/tools/syngenome) - autocomplete a genome sequence!
- [Pretraining a Large Language Model (LLM) from Scratch on DNA Sequences](https://training.galaxyproject.org/training-material/topics/statistics/tutorials/genomic-llm-pretraining/tutorial.html)

