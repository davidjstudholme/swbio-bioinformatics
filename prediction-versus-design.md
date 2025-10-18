## Reflection: How Do “Design” and “Prediction” Differ in Biological Modeling?

In biology, **design** and **prediction** sound similar but involve fundamentally different modes of reasoning and responsibility.

---

### Prediction

**Goal:** *To infer or anticipate what already exists or will occur in nature.*

- **Example tasks:**  
  - Predicting a protein’s 3D structure from its sequence (e.g. AlphaFold, ESMFold).  
  - Predicting the effect of a mutation on enzyme activity.  
  - Predicting gene expression from promoter strength.

- **Nature of the task:**  
  - Model acts as an *interpreter* of natural data.  
  - Success is measured by *accuracy* — how well predictions match experimental or known outcomes.  
  - Mistakes are informative but low-risk: they reveal where the model’s understanding is limited.

---

### Design

**Goal:** *To create something new that may not exist in nature.*

- **Example tasks:**  
  - Designing a new enzyme, regulatory sequence, or entire gene.  
  - Engineering minimal genomes or synthetic circuits.  
  - Using generative models (like Evo 2) to invent plausible but novel sequences.

- **Nature of the task:**  
  - Model acts as a *creator* or *generator*.  
  - Success is measured by *function* and *safety* — does the design work, and is it appropriate to use?  
  - Mistakes carry higher stakes: a design that “looks natural” might still fail, behave unpredictably, or pose risks.

---

### Comparing the Two

| Aspect | Prediction | Design |
|--------|-------------|--------|
| **Purpose** | Understand or anticipate biological behavior | Create new biological entities |
| **Data relationship** | Fits patterns in existing data | Intentionally explores beyond known data |
| **Evaluation** | Accuracy vs ground truth | Performance and safety of the output |
| **Risk profile** | Low — interpretive errors | High — functional and ethical consequences |
| **Role of human judgment** | Evaluate correctness | Define goals, constraints, and responsibility |

---

### 💭 Why It Matters

As tools like **Evo 2** blur the boundary between prediction and design, it’s important to ask:

- When does *suggesting a plausible sequence* become *designing a biological construct*?  
- What additional validation or containment steps are ethically required for generated DNA?  
- How should scientific responsibility evolve as AI systems begin to propose biological solutions rather than just describe them?

---

### Discussion Prompt

> **Question:**  
> If Evo 2 generates a plausible coding sequence that encodes a new protein fold, is that a *prediction* of something nature could have evolved, or a *design* of something entirely new?  
> 
> **Follow-up:**  
> How would you test or regulate such a sequence before considering real-world synthesis?

---

**Takeaway:**  
> Prediction models *map the world as it is*.  
> Design models *imagine worlds that could be* — and that difference carries both creative power and ethical weight.
