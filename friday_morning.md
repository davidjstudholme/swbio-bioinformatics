# Purpose: question your findings

On Thursday you generated results; this morning you become the reviewer of those results.

Don't assume  just because a tool ran successfully that it has produced a valid answer!

# A critical-analysis checklist (09:30–10:00)
Five questions to ask of any bioinformatics result:
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

# Apply the checklist to the mini-project (10:00–11:00)
Revisit your results and identify at least one limitation, uncertainty or potential source of error.

## For RNA-seq projects	For genome assembly projects
Are the sample identities and treatment labels correct?	Is the read dataset appropriate for the organism and assembly method?
Is there sufficient biological replication for the intended comparison?	Are the assembly metrics consistent with expectations?
Do QC and PCA reveal problematic samples or batch effects?	Are there signs of contamination or incompleteness?
Are fold changes and statistical evidence both considered?	Could repeats, heterozygosity or mixed material explain fragmentation?
Are gene annotations and functional claims supported?	Is the assembly suitable for the intended downstream use?
Then ask them to write a short critical appraisal of their preliminary result.


# Peer review (11:15–12:00)
Each student explains their biological question, shows their figure, and describes their main limitation. Their partner acts as a constructive reviewer and asks:
- What evidence supports your conclusion?
- What alternative explanation could there be?
- What additional analysis would strengthen your interpretation?

# Decide what to do next (12:00–12:30)
Make a short priority list:
- One thing to check or improve.
- One additional analysis that would be useful.
- One limitation they will explicitly acknowledge.
 
The **deliverable**: a critical appraisal and a revised interpretation of their findings.
