# 16S-Report-Prep

## nf-core/ampliseq pipeline
* A bioinformatics analysis pipeline used for amplicon sequencing, supporting denoising of any amplicon and, currently, taxonomic assignment of 16S, ITS and 18S amplicons. 
* Supported is paired-end Illumina or single-end Illumina, PacBio and IonTorrent data. 
* Default is the analysis of 16S rRNA gene amplicons sequenced paired-end with Illumina.
* The pipeline is built using Nextflow.
* It runs with Conda, Docker, Podman,Shifter, Charliecloud and Singularity.
* It can run on the AWS cloud infrastructure.
* [Link to the pipeline github repository](https://github.com/nf-core/ampliseq)
* Command for running the pipeline:
  ```
  nextflow run nf-core/ampliseq -profile <docker/singularity/podman/shifter/charliecloud/conda/institute> --input "path to data" --FW_primer "forward primer sequence" --RV_primer "reverse primer sequence" --metadata "Path to metadata file""
  ```
![Image of how it runs and output expected](https://github.com/nf-core/ampliseq/blob/master/docs/images/ampliseq_workflow.png)
