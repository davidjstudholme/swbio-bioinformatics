Friday morning (09:30–12:30): Critical analysis of results
Purpose: teach students to question their own findings.
I would make this session explicitly different from Thursday afternoon. On Thursday they generate results; on Friday morning they become reviewers of those results.
This is particularly important because students often assume that a tool has produced a valid answer simply because it ran successfully.
Part 1 — A critical-analysis checklist (09:30–10:00)
Introduce a common set of questions:
Five questions to ask of any bioinformatics result
1. Did the analysis work technically?
Were there errors, warnings, poor QC metrics or unexpected outputs?


2. Is the dataset suitable?
Are the samples, metadata and reference appropriate for the question?


3. Are the assumptions reasonable?
Does the analysis account for biological replication, confounding, reference quality or other relevant limitations?


4. Is the result convincing?
Is it consistent, sufficiently supported, and robust to obvious sources of uncertainty?


5. Does it answer the biological question?
What can legitimately be concluded, and what remains uncertain?



Part 2 — Apply the checklist to the mini-project (10:00–11:00)
Students revisit their own results and identify at least one limitation, uncertainty or potential source of error.
You could give them a project-specific checklist:
For RNA-seq projects	For genome assembly projects
Are the sample identities and treatment labels correct?	Is the read dataset appropriate for the organism and assembly method?
Is there sufficient biological replication for the intended comparison?	Are the assembly metrics consistent with expectations?
Do QC and PCA reveal problematic samples or batch effects?	Are there signs of contamination or incompleteness?
Are fold changes and statistical evidence both considered?	Could repeats, heterozygosity or mixed material explain fragmentation?
Are gene annotations and functional claims supported?	Is the assembly suitable for the intended downstream use?
Then ask them to write a short critical appraisal of their preliminary result.
Part 3 — Peer review (11:15–12:00)
Pair students, preferably with people doing different project types.
Each student explains their biological question, shows their figure, and describes their main limitation. Their partner acts as a constructive reviewer and asks:
- What evidence supports your conclusion?
- What alternative explanation could there be?
- What additional analysis would strengthen your interpretation?
This works particularly well for a mixed cohort because it forces students to explain their analysis in language that a non-specialist can understand.
Part 4 — Decide what to do next (12:00–12:30)
Students make a short priority list:
- One thing to check or improve.
- One additional analysis that would be useful.
- One limitation they will explicitly acknowledge.
The deliverable: a critical appraisal and a revised interpretation of their findings.
One particularly useful teaching opportunity
Your Gyrodactylus kobayashii RNA-seq mini-project contains an explicit complication: the available information does not establish which sample corresponds to which treatment. SWBio Bioinformatics coursework task 2025.docx

I would use this deliberately as an example of why critical evaluation matters. Students should recognise that they cannot responsibly assign treatment-specific biological meaning to expression differences without reliable sample metadata.
That is a much better lesson than simply giving everyone a dataset that works perfectly.
