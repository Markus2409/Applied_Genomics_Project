# Applied Genomics Project – *De novo genome assembly and functional genomics of the Pelobatrachus nasutus as a phenotypic plasticity, and antimicrobial defenses model*


---

![Sequencing](https://img.shields.io/badge/Sequencing-PacBio_HiFi-blue?style=flat-square)
![Assembly](https://img.shields.io/badge/Assembly-3D--DNA+Juicebox+hifiasm-green?style=flat-square)
![Annotation](https://img.shields.io/badge/Annotation-RepeatModeler2+RepeatMasker+BRAKER2_(AUGUSTUS+STAR)+MAKER-orange?style=flat-square)
![Population](https://img.shields.io/badge/Population_Analysis-BWA--MEM2+GATK+ANGSD-yellowgreen?style=flat-square)
![Organism](https://img.shields.io/badge/Organism-Pelobatrachus_nasutus-teal?style=flat-square)
![Budget](https://img.shields.io/badge/Budget-100000€-brightgreen?style=flat-square)

---
## Introduction / State of the Art

This repository documents the **Applied Genomics Simulation Project** developed during the *Applied Genomics* course of the Master’s Degree in **Bioinformatics** (University of Bologna, 2025).  

The project was designed under an **assigned budget of €100,000**, and represents a **simulation exercise** rather than a real sequencing effort.  

The main goal was to design a **working pipeline** for the *de novo* assembly of the genome of the Malayan horned frog (*Pelobatrachus nasutus*), which as of **26th August 2025** still lacks a published nuclear reference genome.  

In addition to genome assembly, the project focused on the **annotation of genes relevant to biomedical applications** (e.g., antimicrobial peptides, skin-related genes) and the **investigation of phenotypic plasticity** (cutaneous tubercles, mucous glands, pigmentation differences) across contrasting habitats.  
## Methodological Pipeline

**Sample Collection & Ethics**  
- 1 high-quality individual sample from blood for reference genome assembly (HMW DNA).  
- 1 skin sample for RNA-seq and Hi-C assembly.  
- Skin biopsy samples from 10 individuals (5 from protected forest, 5 from fragmented habitat) for resequencing (15× each).  

> All activities were conducted in full compliance with the **Nagoya Protocol**, with prior informed consent (PIC), mutually agreed terms (MAT), and collection permits obtained from the Malaysian Government, Sarawak Forestry Department, and private landowners (Wilmar Oil Palm Plantation).
---

**DNA & RNA Extraction**  
- Genomic DNA: Qiagen Genomic-tip, QC with Qubit fluorometer and NanoDrop (A260/280 ≈ 1.8–2.0, A260/230 > 2.0), PFGE (>50 kb).  
- Total RNA (skin): Qiagen RNeasy, stored in RNAlater, RIN ≥ 7.  

---

**Genome Sequencing**  
- PacBio HiFi (30–40× coverage, 15–20 kb reads): long, high-accuracy reads.  
- Hi-C (Illumina NovaSeq PE150): chromatin conformation for scaffolding, recovered from the skin tissue sample of the reference individual.  
- RNA-seq (skin of the reference individual, 2–3 replicates, NovaSeq PE150, ~50M reads each).  
- Illumina sequencing for downstream population analysis (10 individuals, 15× each, NovaSeq PE150).  

---

**Assembly & QC**  
- *hifiasm* for contig-level assembly (Cheng et al., 2021).  
- Hi-C scaffolding with *3D-DNA* (Dudchenko et al., 2017) + *Juicebox* (Robinson et al., 2018) with manual curation.  
- QC metrics: N50 > 20 Mb, BUSCO (Tegenfeldt et al., 2025), QV ≥ 30 (Rhie et al., 2020), LAI (Ou et al., 2018).  

---

**Functional Annotation**  
- Repeat discovery: *RepeatModeler2* (Flynn et al., 2020) + masking with *RepeatMasker* (Smit et al., 2015).  
- Gene models: *BRAKER2* (Gabriel et al., 2024; Stanke et al., 2004) combines RNA-seq evidence (*STAR*, Dobin et al., 2013) with ab initio models to improve exon–intron boundary prediction (*AUGUSTUS*, Stanke et al.,2004).  
- Refinement: *MAKER* (Cantarel et al., 2008) integrating *BRAKER2* results with homology from the closely related *Leptobrachium ailaonicum* genome (Li et al., 2019).  
- Major target gene families: antimicrobial peptides (AMPs, validated through APD3, Wang et al., 2016), keratins, mucins, extracellular matrix proteins.  

---

**Population Genomics**  
- Mapping: *BWA-MEM2* (Md et al., 2019) against the reference genome.  
- Variant calling: *GATK* (der Auwera et al., 2002) in gVCF mode, joint calling.  
- Genotype likelihoods: *ANGSD* (Korneliussen et al., 2014) for allele frequencies and summary statistics.  
- Population structure: *PCAngsd* (Meisner & Albrechtsen, 2018) for PCA.  
- Differentiation: $F_{ST}$ (Wright, 1978).  
- Environmental associations: *BayPass* (Gauthier, 2025) to identify SNPs correlated with habitat (protected vs fragmented).  

---

## Budget & Estimated Costs
> The estimated costs reported in this project were obtained, whenever possible, by directly contacting the information services of **Illumina**, **PacBio**, **Qiagen** and **ThermoFisher** for updated sequencing, extraction and conservation kit prices.  
> For consumables and contingency expenses, a **general estimate** was made based on standard laboratory practices (plasticware, barcoding materials, cryogenic storage, shipping logistics), with an additional margin included to cover unexpected costs.


| **Item**                               | **Estimated Cost (€)** | **Notes** |
|----------------------------------------|------------------------|-----------|
| Fieldwork & permits                    | 4,800                  | Sampling in Gunung Gading NP & Wilmar plantation; ABS/Nagoya compliance |
| DNA extraction (HMW + resequencing)    | 3,250                  | Qiagen Genomic-tip |
| RNA extraction (skin only)             | 1,420                  | RNAlater + Qiagen RNeasy kits |
| PacBio HiFi sequencing                 | 34,780                 | 30–40× coverage, 1 HQ individual |
| Hi-C sequencing                        | 8,230                  | Hi-C libraries from fresh tissue, sequenced on Illumina NovaSeq PE150 |
| Illumina resequencing (10 ind., 15×)   | 14,650                 | Illumina NovaSeq PE150 |
| RNA-seq (skin, 2–3 replicates)         | 6,180                  | Illumina NovaSeq PE150 |
| Computational costs & Cloud storage    | 11,740                 | Assembly, annotation, population genomics analyses |
| Consumables & contingency              | 8,560                  | Tubes, barcoding, dry shipper |
| **TOTAL**                              | **93,610**             | Within the €100,000 budget |

