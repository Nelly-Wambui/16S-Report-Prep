# 16S-Report-Prep
## Introduction
16S rRNA is a gene that encodes the RNA component of the small subunit(30S subunit) of ribosomes in bacteria and archaea. 16S is a sedimentation coefficient([Dependency Map of Proteins in the Small Ribosomal Subunit](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.0020010)). This is an essential gene required for initiating protein synthesis and the stabilizing correct codon-anticodon pairing in the A site of the ribosome during mRNA translation([The distribution, diversity, and importance of 16S rRNA gene introns in the order Thermoproteales](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4496867/)). It is called "the molecular fossil" of bacteria because of being highly conserved and specific. This makes it the most widely used gene marker for genus and species identification, as well as taxonomic significance([16S/18S/ITS Amplicon Sequencing](https://www.cd-genomics.com/16S-18S-ITS-Amplicon-Sequencing.html)). The gene is about 1500bp and is composed of both conserved regions and variable regions. The conserved region is shared while the variable regions have differences among different bacteria and therefore providing information on the specificity of the genus and the species([16S rRNA, One of the Most Important rRNAs](https://www.cd-genomics.com/blog/16s-rrna-one-of-the-most-important-rrnas/)). 

The gene is used in microbiome analysis. Analysis pipelines have been developed and improved over the years and include QIIME and DADA2 pipelines. Our internship project required us to review some of the existing pipelines and come up with a conclusion on the best among the following:
- https://github.com/nf-core/ampliseq 
- https://h3abionet.github.io/H3ABionet-SOPs/16s-rRNA-1-0.html
- https://github.com/h3abionet/TADA
- https://github.com/mbbu/16S_Accreditation
- https://github.com/h3abionet/h3abionet16S

After testing them we concluded that the nf-core/ampliseq pipeline was the best and we made changes to the 

## H3ABionet-SOPs/16s-rRNA-1-0.html
* This only provides an analysis workflow with tools and databases summarised [here](https://github.com/h3abionet/H3ABionet-SOPs/blob/master/pages/genomics_analysis/16s-rRNA/16s-rRNA.md#appendices-appendices).
* It is an SOP that refers to both QIIME and QIIME2.
* Practice dataset and metadata included in the SOP can be obtained in [this link](http://h3data.cbio.uct.ac.za/assessments/16SrRNADiversityAnalysis/practice/).
* In it are also questions on operation,run-time and output analysis that one would consider having as a criteria in reviewing workflows.
* It would be a good SOP for an individual intending to create a QIIME pipeline from scratch.

## h3abionet/TADA
* This pipeline is a Targeted Amplicon Diversity Analysis(TADA) using DADA2, implemented in Nextflow.
* The typical command for running the pipeline is:
```
nextflow run uct-cbio/16S-rDNA-dada2-pipeline --reads '*_R{1,2}.fastq.gz' --trimFor 24 --trimRev 25 --reference 'gg_13_8_train_set_97.fa.gz' -profile uct_hex
```
* The above command holds the mainly required arguments,which are:
  - **--reads** which specifies the location of your input FastQ files.
  - **--trimFor and --trimRev** that set length of R1 (--trimFor) and R2 (--trimRev) that needs to be trimmed (if no trimming is needed, then set 0).
  - **--reference** specifying the path to taxonomic database for annotation.
  - **-profile** which chooses a configuration profile amongst:
     
    `standard`  
    The default profile, used if -profile is not specified at all. Runs locally and expects all software to be installed and available on the PATH.  
    `uct_hex`  
    Designed to run on UCT's high-performance cluster (hex).  
    `none`  
    No configuration at all. Useful if you want to build your own config from scratch and want to avoid loading in the default base config profile (not recommended).
* It outputs results mostly in RDS format.

## nf-core/ampliseq pipeline
* Its current version is Ampliseq Version 2.1.1.
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
* For usage of the pipeline, refer to [this](https://nf-co.re/ampliseq/usage), and for the parameters refer to [these parameters](https://nf-co.re/ampliseq/parameters)

![Image of how it runs and output expected](https://github.com/nf-core/ampliseq/blob/master/docs/images/ampliseq_workflow.png)


## MBBU 16S-Accreditation
* This is a workflow for 16SrRNA analysis.
* The current version is Accreditation_Zenodo
* The Dada2 pipeline is written in R, while the Qiime pipeline is built with Nextflow.

### DADA2 MBBU 16S-Accreditation pipeline

* The following packages are required:
1. DADA2
2. phyloseq
3. dplyr
4. vegan
5. phangorn
6. ggplot2
7. scales
8. grid
9. reshape2
10. profvis
11. DECIPHER
12. Rcolorbrewer

* Steps in the pipeline:
![DADA2 MBBU 16S-Accreditation pipeline](https://github.com/mbbu/Reviewing-16s-Analysis-Workflows/blob/main/MBBU-16S-Accreditation-Dada2-Pipeline-Steps%20(2).png)

### QIIME MBBU 16S-Accreditation Pipeline

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
![image](https://user-images.githubusercontent.com/91982522/149777440-1efe7a27-8034-492e-944d-d9edaa7b35ed.png)

## h3abionet16S
* We had difficulties running this and due to lack of an easy set-up, we did away with it.

## Workflow Comparison
This workflow comparison is only for the pipelines that we tested and found to be running without being so cumbersome and for some without being cumbersome at all.

<table>
    <tr>
       <th>Criteria</th>
       <th>nf-core/ampliseq</th>
       <th>TADA</th>
       <th>MBBU Accreditation Qiime</th>
       <th>MBBU Accreditation dada2</th>
   </tr>
   <tr>
       <td>Runtime</td>
       <td>21 minutes</td>
       <td>46 minutes</td>
       <td>#</td>
       <td>#</td>
   </tr>
   <tr>
       <td>Setup</td>
       <td>Easy, 1 command</td>
       <td>Easy, 1 command</td>
       <td>Hard, edit configs</td>
       <td>Hard</td>
   </tr>
   <tr>
       <td>Functionality</td>
       <td>QIIME2, Visualization, functional analysis</td>
       <td>DADA2</td>
       <td>QIIME2</td>
       <td>DADA2</td>
   </tr>
    <tr>
       <td>Last updated</td>
       <td>October 2021</td>
       <td>September 2021</td>
       <td>April 2021</td>
       <td>April 2021</td>
   </tr>
   <tr>
       <td>Documentation</td>
       <td>Well documented</td>
       <td>Well documented</td>
       <td>Lacks setup instructions</td>
       <td>Not well documented</td>
   </tr>
    <tr>
       <td>Gaps</td>
       <td>None</td>
       <td>Test data, visualization</td>
       <td>Test config, functional analysis</td>
       <td>Not automated</td>
   </tr>
    <tr>
       <td>Seq</td>
       <td>16S, 18S, ITS</td>
       <td>16S, ITS</td>
       <td>16S</td>
       <td>16S</td>
   </tr>
    
</table>

| Syntax  | Description |
|---------|-------------|
| profile | argument    |
| test | 16s |
