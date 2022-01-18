# 16S-Report-Prep
## Introduction
16S rRNA is a gene that encodes the RNA component of the small subunit(30S subunit) of ribosomes in bacteria and archaea. It is called "the molecular fossil" of bacteria because of being highly conserved and specific. This makes it the most widely used gene marker for genus and species identification, as well as taxonomic significance. The gene is about 1500bp and is composed of both conserved regions and variable regions. The conserved region is shared while the variable regions have differences among different bacteria and therefore providing information on the specificity of the genus and the species. 

The gene is used in microbiome analysis. Analysis pipelines have been developed and improved over the years and include QIIME and DADA2 pipelines. As our internship project, we reviewed some of the existing pipelines and came up with a conclusion on the best among the following:
- https://github.com/nf-core/ampliseq 
- https://h3abionet.github.io/H3ABionet-SOPs/16s-rRNA-1-0.html
- https://github.com/h3abionet/TADA
- https://github.com/mbbu/16S_Accreditation
- https://github.com/h3abionet/h3abionet16S

## H3ABionet-SOPs/16s-rRNA-1-0.html
* This only provides an analysis workflow with tools and databases summarised [here](https://github.com/h3abionet/H3ABionet-SOPs/blob/master/pages/genomics_analysis/16s-rRNA/16s-rRNA.md).
* It is an SOP that refers both to QIIME and QIIME2.
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
       <td>Qiime, Visualization, functional analysis</td>
       <td>dada2</td>
       <td>Qiime</td>
       <td>dada2</td>
   </tr>
    <tr>
       <td>Last updated</td>
       <td>2 months</td>
       <td>3 months</td>
       <td>8 months</td>
       <td>8 months</td>
   </tr>
   <tr>
       <td>Documentation</td>
       <td>Well documented</td>
       <td>Well documented</td>
       <td>Lack setup instructions</td>
       <td>Not well documented</td>
   </tr>
    <tr>
       <td>Gaps</td>
       <td>None</td>
       <td>Test data, Functional analysis, visualization</td>
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
|---------|-------------|
