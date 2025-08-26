# Applied Genomics Project – *De novo genome assembly and functional genomics of the Pelobatrachus nasutus as a phenotypic plasticity, and antimicrobial defenses model*


---

![Sequencing](https://img.shields.io/badge/Sequencing-PacBio_HiFi-blue?style=flat-square)
![Assembly](https://img.shields.io/badge/Assembly-3D--DNA+Juicebox+hifiasm-green?style=flat-square)
![Annotation](https://img.shields.io/badge/Annotation-RepeatModeler2+RepeatMasker+BRAKER2_(AUGUSTUS+STAR)+MAKER-orange?style=flat-square)
![Population](https://img.shields.io/badge/Population_Analysis-BWA--MEM2+GATK+ANGSD-yellowgreen?style=flat-square)
![Organism](https://img.shields.io/badge/Organism-Pelobatrachus_nasutus-teal?style=flat-square)
![Budget](https://img.shields.io/badge/Budget-100000€-brightgreen?style=flat-square)

## Table of Contents

- [Introduction & State of the art](#introduction--state-of-the-art)
- [Software & Toolkits](#software--toolkits)
- [Methodological Pipeline](#methodological-pipeline)
- [Budget](#budget--estimated-costs)
- [References](#references)
- [Contacts](#contacts)
---
## Introduction & State of the art
This repository documents the **Applied Genomics Simulation Project** developed during the *Applied Genomics* course of the Master’s Degree in **Bioinformatics** (University of Bologna, 2025).  

The project was designed under an **assigned budget of €100,000**, and represents a **simulation exercise** rather than a real sequencing effort.  

The main goal was to design a **working pipeline** for the *de novo* assembly of the genome of the Malayan horned frog (*Pelobatrachus nasutus*), which as of **26th August 2025** still lacks a published nuclear reference genome.  

In addition to genome assembly, the project focused on the **annotation of genes relevant to biomedical applications** (e.g., antimicrobial peptides, skin-related genes) and the **investigation of phenotypic plasticity** (cutaneous tubercles, mucous glands, pigmentation differences) across contrasting habitats.  

This repository is also intended to provide a **concise overview of the designed pipeline, bioinformatics softwares utilized and budget estimates**, while serving as a container for **meta-information** such as figures used in the project, the presentation slides, and the final report document.
##  Software & Toolkits

| **Tool / Software**            | **Purpose**                                                                 | **Reference** |
|--------------------------------|-----------------------------------------------------------------------------|---------------|
| **hifiasm**                    | Fast haplotype-resolved *de novo* assembler optimized for PacBio HiFi reads, capable of producing phased assemblies. | [Cheng 2021](#ref-cheng2021) |
| **3D-DNA**                     | Automated scaffolding tool using Hi-C data to assemble contigs into chromosome-length scaffolds. | [Dudchenko 2017](#ref-dudchenko2017) |
| **Juicebox**                   | Interactive visualization and manual curation tool for genome assemblies using Hi-C contact maps. | [Robinson 2018](#ref-robinson2018) |
| **RepeatModeler2**             | De novo detection of transposable elements and repeats in genomic sequences. | [Flynn 2020](#ref-flynn2020) |
| **RepeatMasker**               | Uses a repeat library (e.g. from RepeatModeler2) to mask repetitive elements across the genome. | [Smit 2015](#ref-smit2015) |
| **BRAKER2** *(uses STAR + AUGUSTUS)* | Automated gene annotation pipeline combining RNA-seq alignments (**STAR**) with ab initio predictions (**AUGUSTUS**) to refine exon–intron boundaries. | [Gabriel 2024](#ref-gabriel2024); [Stanke 2004](#ref-stanke2004); [Dobin 2013](#ref-dobin2013) |
| **MAKER**                      | Annotation pipeline integrating *ab initio* predictions and homology evidence into final gene models. | [Cantarel 2008](#ref-cantarel2008) |
| **BWA-MEM2**                   | High-performance sequence aligner for mapping Illumina reads to the reference genome. | [Md 2019](#ref-md2019) |
| **GATK**                       | Toolkit for variant discovery and genotyping, using the gVCF workflow for joint calling. | [der Auwera 2002](#ref-vanderauwera2002) |
| **ANGSD**                      | Population genomics tool for calculating allele frequencies and summary statistics from NGS data. | [Korneliussen 2014](#ref-korneliussen2014) |
| **PCAngsd**                    | Performs PCA based on genotype likelihoods for low-coverage sequencing datasets. | [Meisner 2018](#ref-meisner2018) |
| **BayPass**                    | Detects SNPs associated with environmental variables or population structure. | [Gautier 2025](#ref-baypass) |



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

---
## References

- <a id="ref-donol2025"></a>Donol, C. M., Zainudin, R., & Deka, E. Q. (2025). *Morphological variation of Pelobatrachus nasutus...* **JSSM**, 20(2), 390–406. https://doi.org/10.46754/jssm.2025.02.013
- <a id="ref-kumar2017"></a>Kumar, S., Stecher, G., Suleski, M., & Hedges, S. B. (2017). TimeTree. **Mol Biol Evol**, 34(7). https://doi.org/10.1093/molbev/msx116
- <a id="ref-li2019"></a>Li, Y., Ren, Y., Zhang, D., *et al.* (2019). Mustache toad genome (Hi-C). **GigaScience**, 8(9). https://doi.org/10.1093/gigascience/giz114
- <a id="ref-kosch2025"></a>Kosch, T. A., *et al.* (2025). Comparative analysis of amphibian genomes. **Mol Ecol Resour**, 25(1). https://doi.org/10.1111/1755-0998.14025
- <a id="ref-wang2016"></a>Wang, G., Li, X., & Wang, Z. (2016). APD3 database. **Nucleic Acids Res**, 44(D1). https://doi.org/10.1093/nar/gkv1278
- <a id="ref-wright1978"></a>Wright, S. (1978). *Evolution and the Genetics of Populations*, Vol. 4. University of Chicago Press.
- <a id="ref-cheng2021"></a>Cheng, H., Concepcion, G. T., Feng, X., Zhang, H., & Li, H. (2021). hifiasm. **Nat Methods**, 18(2). https://doi.org/10.1038/s41592-020-01056-5
- <a id="ref-dudchenko2017"></a>Dudchenko, O., *et al.* (2017). 3D-DNA / Hi-C scaffolds. **Science**, 356(6333). https://doi.org/10.1126/science.aal3327
- <a id="ref-robinson2018"></a>Robinson, J. T., *et al.* (2018). Juicebox.js. **Cell Systems**, 6(2). https://doi.org/10.1016/j.cels.2018.01.001
- <a id="ref-tegenfeldt2025"></a>Tegenfeldt, F., *et al.* (2025). BUSCO/OrthoDB update. **Nucleic Acids Res**, 53. https://doi.org/10.1093/nar/gkae987
- <a id="ref-rhie2020"></a>Rhie, A., Walenz, B. P., Koren, S., & Phillippy, A. M. (2020). Merqury. **Genome Biol**, 21. https://doi.org/10.1186/s13059-020-02134-9
- <a id="ref-ou2018"></a>Ou, S., Chen, J., & Jiang, N. (2018). LAI. **Nucleic Acids Res**, 46(21). https://doi.org/10.1093/nar/gky730
- <a id="ref-flynn2020"></a>Flynn, J. M., *et al.* (2020). RepeatModeler2. **PNAS**, 117(17). https://doi.org/10.1073/pnas.1921046117
- <a id="ref-smit2015"></a>Smit, A. F. A., Hubley, R., & Green, P. (2015). RepeatMasker Open-4.0. http://www

## Contacts

For any questions, suggestions, or contributions, feel free to open an issue or contact the maintainer:

**Marco Cuscunà**  
- <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Seal_of_the_University_of_Bologna.svg/1200px-Seal_of_the_University_of_Bologna.svg.png" width="16"/> [marco.cuscuna@studio.unibo.it](mailto:marco.cuscuna@studio.unibo.it)  
- [![ORCID](https://orcid.org/sites/default/files/images/orcid_16x16.png)](https://orcid.org/0009-0008-4017-8328) `0009-0008-4017-8328`
