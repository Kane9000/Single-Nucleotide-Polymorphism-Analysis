# Single-Nucleotide-Polymorphism-Analysis
## Introduction

In this study Plasmodium falciparum parasites were cultured in normal growth media or media containing antimalarial drugs to induce drug resistance. Whole genome sequencing was conducted on each line of parasites to find single nucleotide polymorphisms in genes that may assist the parasite's ability to resist the effects of the antimalarial drug Tafenoquine.

Traditionally, a SNP matrix is generated and after removing "junk" genes and results are parsed line by line to find a changes in genes that occured in the drug resistant lines compared to the control lines. 

This method is challenging because there are over a twenty two million base pairs in the Plasmodium falciparum genome and even after filtering out unrelated genes and base pairs with no changes there are still hundreds of thousands of lines to manually check.

In this study, open source gene annotation and impact prediction software was utilised to filter significant changes in the type of mutations in each gene. 

This method allows the quantification of predictive Low, Moderate and High Impact modifications induced by Tafenoqiune in each gene to compare significant changes between the control lines and the drug resistant lines of parasites.


## Methods

Whole Genome Sequencing

DNA from sixteen isolates of P.falciparum from parental, control and treatment lines were isolated for whole genome sequencing using Illumina Novaseq sequence production. Sequence files were generated in a FASTQ format containing 150bp reads using the Illumina DRAGEN BCL Convert 07.021.624.3.10.8 pipeline by the Australian Genome Research Facility Ltd., Melbourne, Australia.

Data Preprocessing

Raw sequence data was aligned to a reference genome using bwa mem 0.7.17. Reads were mapped to the P.falciparum 3D7 v61 reference genome available from https://plasmodb.org/. Further bioinformatic preprocessing was conducted using the broad institute Genome Analysis Tool Kit GATK-4.4.0.0 package. Sequences were preprocessed using samtools fixmate, Picard MarkDuplicates and  SetNmMdAndUqTags to fill in coordinates, remove duplicates and recalibrate tags, respectively. GATK Base Quality Score Recalibration was then applied using variants from the Pf crosses 1.0 release as the set of known sites from malariagen.net.

Variant Discovery

GATK HaplotypeCaller was used to identify SNPs and indels variations and generated a single VCF file for each sample. Subsequent annotations were conducted with SnpEff 5.2a and SnpSift allowed us to filter the predicted effects of genetic variants. Variants were sorted by either ‘High’ or ‘Moderate’ impact and manually manipulated in Jupyter Notebooks using the python programming language. 

Data interpretation

SNP matrix

A high and moderate impact SNP matrix was created using only the highest impacting effect from each variant. Duplicate variants in the parental, control and drug resistant lines were removed. Unrelated genes “VAR”, “RIF” and “Stevor” were then removed. Lastly, only variants that were unique to drug resistant lines were retained for further investigation. Data contained in folders SnpSift_High_Impact & SnpSift_Moderate_Impact.

Variant Impact and Effect counts

SnpEff generated a table of genes and counts of predicted impacts and effects. For each gene and each impact or effect, a t-test was conducted to compare the control group to the treatment lines. Statistically significant changes in variant impact or effect counts were recorded. Data contained in SnpEff_BigData. 

Types of effects and impact description https://pcingola.github.io/SnpEff/snpeff/inputoutput/

Impact	Meaning	Example
HIGH	The variant is assumed to have high (disruptive) impact in the protein, probably causing protein truncation, loss of function or triggering nonsense mediated decay.	stop_gained, frameshift_variant
MODERATE	A non-disruptive variant that might change protein effectiveness.	missense_variant, inframe_deletion
LOW	Assumed to be mostly harmless or unlikely to change protein behavior.	synonymous_variant
MODIFIER	Usually non-coding variants or variants affecting non-coding genes, where predictions are difficult or there is no evidence of impact.	exon_variant, downstream_gene_variant


## Results and Discussion
In this study, the most interesting effects are the High impact effects which would cause a change in function of the gene product.

Using the method decribed above, a list of 49 genes were generated which had significant changes in high impact mutations compared to the control line of parasite for further investigation. 

![image](https://github.com/user-attachments/assets/f1e3843f-b30a-4162-a089-14a976029a00)

A search of these genes a Plasmodium Informatic Resource database (plasmodb.org) shows that many of these genes are involved in the regulation of DNA replication and other cellular signaling pathways. 

![goCloud (1)](https://github.com/user-attachments/assets/57bb459b-d8ab-47f1-95dc-000f0bdb7ca0)


## Conclusions

In this study, the impact of Tafenoqiune on cultures of Plasmodium falciparum were determined using gene annotation and prediction software. Genes with significant changes in high impact mutations compared to the control line of parasites were filtered for further investigation.



