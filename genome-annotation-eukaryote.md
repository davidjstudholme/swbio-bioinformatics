Previously, we obtained a fungal genome sequence and then masked its repeat sequences using RepeatModeller + RepeatMasker.

Now, we will use that masked genome sequence as the input for genome annotation. In other words, we will search the genome for features such as protein-coding genes.

### Hands on: run Braker3 on the masked fungal genome sequence

- Search for Braker3 in the Galaxy Tool search box. That will take you to [here](https://usegalaxy.eu/?tool_id=toolshed.g2.bx.psu.edu%2Frepos%2Fgenouest%2Fbraker3%2Fbraker3%2F3.0.8%2Bgalaxy2&version=latest).
- For "Genome sequence is soft-masked" select "Yes".
- For "Species name", optionally insert "Cyberlindnera fabianii".
- For "RNA-seq mapped to genome to train Augustus/GeneMark", choose "Nothing selected". (No RNA-seq data is availabke for this species.)
- For "Proteins to map to genome", choose XXXXX.
- For "Fungal genome", choose "Yes".
- For "Output format", choose "GFF3".


