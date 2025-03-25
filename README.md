# Somatic_Mutation
Somatic mutation analysis pipeline for tumor-only samples

```
Pipeline Overview

Goal: Detect somatic mutations (SNVs, indels, CNVs) in tumor samples without a matched normal control.
Challenge: Higher risk of false positives (germline variants may be misclassified as somatic).
Solution: Use population databases (e.g., gnomAD, onckoKB, Clinvar, Cosmic) and stringent filters to mitigate noise.

Key Tools:

GATK Mutect2: Primary variant caller	Tumor-only mode (--tumor-sample) with --panel-of-normals (PoN).
Control-FREEC: 	Copy number variation (CNV) detection	Uses BAM file and reference genome.
Strelka: Small variant caller (SNVs/indels)	Complementary to Mutect2 for sensitivity.
SnpEff:	Variant annotation	Adds functional impact (e.g., missense, nonsense).
VEP (Ensembl):	Additional annotation	ClinVar, COSMIC, etc.
BCFtools: 	Filtering & post-processing	Removes low-quality variants.


"""
TUMOR-ONLY SOMATIC MUTATION PIPELINE
------------------------------------
Input: Tumor BAM/FASTQ (no matched normal)
Output: Filtered somatic variants (VCF), CNV calls, annotated results

Steps:
1. Preprocessing:
   - Trim: cutadapt (adapters)
   - Align: bwa-mem → BAM
   - Clean: GATK MarkDuplicates + BQSR

2. Variant Calling:
   - SNVs/Indels: 
     * GATK Mutect2 (--tumor-only + PoN)
     * Strelka2 (cross-validation)
   - CNVs: Control-FREEC (GC correction)

3. Filtering:
   - Remove germline variants (gnomAD/1000G)
   - Filter low-confidence calls (GATK FilterMutectCalls)
   - Merge calls (BCFtools)

4. Annotation:
   - Functional impact: SnpEff (missense/nonsense)
   - Clinical relevance: VEP (ClinVar/COSMIC)

5. Output:
   - VCF: High-confidence somatic variants
   - Plots: CNV profiles (Control-FREEC)
   - Report: MultiQC summary

Key Databases:
- Panel of Normals (PoN)
- gnomAD/OncoKB/ClinVar/COSMIC
"""

```
