# Somatic_Mutation
TUMOR-ONLY SOMATIC MUTATION PIPELINE

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

```
