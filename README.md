# 16S-Report-Prep

## nf-core/ampliseq pipeline
* [Link to the pipeline github repository](https://github.com/nf-core/ampliseq)
* It is a bioinformatics analysis pipeline used for amplicon sequencing, supporting denoising of any amplicon and, currently, taxonomic assignment of 16S, ITS and 18S amplicons. 
* Supported is paired-end Illumina or single-end Illumina, PacBio and IonTorrent data. 
* Default is the analysis of 16S rRNA gene amplicons sequenced paired-end with Illumina.
* The pipeline is built using Nextflow.
* It runs with Conda, Docker, Podman,Shifter, Charliecloud and Singularity.
* It can run on the AWS cloud infrastructure.
* Command for running the pipeline:
  ```
  nextflow run nf-core/ampliseq -profile <docker/singularity/podman/shifter/charliecloud/conda/institute> --input "path to data" --FW_primer "forward primer sequence" --RV_primer "reverse primer sequence" --metadata "Path to metadata file""
  ```
![Image of how it runs and output expected](https://github.com/nf-core/ampliseq/blob/master/docs/images/ampliseq_workflow.png)


## MBBU 16S-Accreditation
* This is a workflow for 16SrRNA analysis.
* There are pipelines for Dada2 and Qiime and can be found [here](https://github.com/mbbu/16S_Accreditation/blob/main/Dada2_report.md)
* The Dada2 pipeline is written in R, while the Qiime pipeline is built with Nextflow.

### DADA2 MBBU 16S-Accreditation pipeline

* The following packages are required:
1. DADA2
2.	phyloseq
3.	dplyr
4.	vegan
5.	phangorn
6.	ggplot2
7.	scales
8.	grid
9.	reshape2
10.	profvis
11.	DECIPHER
12.	Rcolorbrewer

* Steps in the pipeline:
![DADA2 MBBU 16S-Accreditation pipeline](https://github.com/mbbu/Reviewing-16s-Analysis-Workflows/blob/main/MBBU-16S-Accreditation-Dada2-Pipeline-Steps%20(2).png)

### QIIME MMBU 16S-Accreditation Pipeline

* The analysis pipeline follows the following order:
1. Quality check of raw reads
2. Trimming of adapters from reads
3. Merging/Stitching
4. Filtering and Primer removal
5. Orientation
6. Dereplication
7. Chimera detection
8. Clustering OTUs
9. Phylogeny
10. Taxonomy
11. Alpha diversity and Beta diversity

* It is summarized as follows:
![QIIME MMBU 16S-Accreditation Pipeline](![image](https://user-images.githubusercontent.com/91982522/149777440-1efe7a27-8034-492e-944d-d9edaa7b35ed.png)
