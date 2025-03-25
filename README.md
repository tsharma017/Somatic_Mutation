# Somatic_Mutation
somatic mutation analysis pipeline for tumor-only samples

```
Pipeline Overview

Goal: Detect somatic mutations (SNVs, indels, CNVs) in tumor samples without a matched normal control.
Challenge: Higher risk of false positives (germline variants may be misclassified as somatic).
Solution: Use population databases (e.g., gnomAD, onckoKB, Clinvar, Cosmic) and stringent filters to mitigate noise.

Key Tools & Their Roles
Tool	Purpose	Notes
GATK Mutect2: Primary variant caller	Tumor-only mode (--tumor-sample) with --panel-of-normals (PoN).
Control-FREEC: 	Copy number variation (CNV) detection	Uses BAM file and reference genome.
Strelka: Small variant caller (SNVs/indels)	Complementary to Mutect2 for sensitivity.
SnpEff:	Variant annotation	Adds functional impact (e.g., missense, nonsense).
VEP (Ensembl):	Additional annotation	ClinVar, COSMIC, etc.
BCFtools: 	Filtering & post-processing	Removes low-quality variants.

```
