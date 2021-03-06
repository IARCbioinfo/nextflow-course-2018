# Using the IARC nextflow bioinformatics pipelines course 2018

![nextflow](https://www.nextflow.io/img/nextflow2014_no-bg.png)

The aim of this course is to enable participants to use the bioinformatics pipelines developed at IARC using nextflow.

## Description of the course

__Learning objectives__  
After completing this course, participants will be able to use the IARC nextflow bioinformatics pipelines and more specifically:
- set pipeline parameters and configuration
- execute, resume and debug pipelines,
- trace and visualise pipeline execution,
- run the pipelines on workstation or on a high performance computing cluster,
- use github and Docker/Singularity containers to run reproducible analyses,
- understand the basis concepts of the nextflow language used to describe the pipelines.

Please note that the development of pipelines will only be very briefly covered in this course.

## Agenda and slides

__Wednesday 23 May__ ([slides](slides/day1.pdf))  
09:00-10:00	Introduction to bioinformatics pipelines, nextflow, docker, Github and the IARC organization  
10:00-10:30	Practical application: running your first pipeline  
10:30-11:00	Break  
11:00-11-30 The hidden structure of nextflow: work folder and configuration  
11:30-12:30	Practical application: configuring, crashing, resuming and debugging pipelines

__Thursday 24 May__  ([slides](slides/day2.pdf))  
09:00-09:30	Introduction to HPC clusters and running pipelines on a cluster.  
09:30-10:30	Practical application: trace and visualise pipeline execution with log files.  
10:30-11:00 Break  
11:00-11h30 Introduction to the nextflow language: understanding what the pipelines are doing  
11:30-12:30	Practical application: advanced usages toward reproducibility (choosing a container, Github releases and branches, modifying a pipeline etc.)

## Gitter Chat

A [![Join the chat at https://gitter.im/IARCbioinfo/nextflow-course-2018](https://badges.gitter.im/IARCbioinfo/nextflow-course-2018.svg)](https://gitter.im/IARCbioinfo/nextflow-course-2018?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge) is open for the course. This will allow participants to discuss on their projects but also to ask any question regarding the course.

## Laptop setup

Laptops use Ubuntu 16.04.

Nextflow is already installed and in `~/bin`, which is in your `PATH`.

Docker is already installed. If you are curious, here is how to install it on Docker [website](https://docs.docker.com/install/linux/docker-ce/ubuntu/).

If you need a good text editor, [Atom](https://atom.io) is also installed.

## Demo commands

```
nextflow run iarcbioinfo/nf_coverage_demo -with-docker --bam_folder data_test/BAM/BAM_multiple/ --bed data_test/BED/TP53_exon2_11.bed
```

```
nextflow run iarcbioinfo/platypus-nf -with-docker --input_folder data_test/BAM/ --ref data_test/REF/17.fasta
```

```
nextflow run iarcbioinfo/RNAseq-nf -with-docker --input_folder data_test/BAM/BAM_multiple/ --output_folder BAM_realigned --ref_folder data_test/REF --gtf data_test/REF/TP53_small.gtf --bed data_test/BED/TP53_small.bed --mem 4
```

## Config

Config files examples are in the config folder in this repository. Note that adding `-with-trace` in your `nextflow run` command is equivalent to have a configuration file containing:
```
trace {
    enabled = true
}
```
or:
```
trace.enabled = true
```
One example of each possibility is given (`nextflow.config_1` and `nextflow.config_2`). You will also find the configuration file I propose to use on IARC Jupiter cluster.

## IARC Jupiter cluster
Create a symlink to singularity
```
ln -s  /appli57/singularity/singularity-2.4.5/bin/singularity /home/username/bin/
```

Add in your `~/.bash_profile`
```
export NXF_JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk.x86_64/jre/
export NXF_TEMP=/data/tmp

export SINGULARITY_CACHEDIR=/data/username/.singularity
export SINGULARITY_LOCALCACHEDIR=/data/tmp/
```

Change your `~/.nextflow/config` with the one on the config folder in this repository.

Check cluster usage using `bhosts` or your own jobs using `bjobs`. You can also run our script to check what the others are doing: `/appli57/scripts/bjobs_monitor.r`.

## Useful links

- IARC bioinformatics [GitHub organization](https://github.com/IARCbioinfo)
- [Docker](https://www.docker.com) and [DockerHub](https://hub.docker.com). See my short [docker tutorial](https://github.com/IARCbioinfo/SBG-CGC_course2018/blob/master/demo_code/docker_demo.md) here if you want to know more about it. IARC bioinformatics [DockerHub page](https://hub.docker.com/u/iarcbioinfo/).
- [Singularity](https://singularity.lbl.gov) and the [PLOS one paper](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0177459) presenting it.
- Nextflow ressources:
  - Nextflow [website](https://www.nextflow.io/index.html)
  - Nextflow [documentation](https://www.nextflow.io/docs/latest/index.html)
  - Nextflow [releases on GitHub](https://github.com/nextflow-io/nextflow/releases) with changelogs
  - Nextflow [issues on GitHub](https://github.com/nextflow-io/nextflow/issues)
  - Nextflow [![Gitter](https://badges.gitter.im/IARCbioinfo/nextflow-course-2018.svg)](https://gitter.im/nextflow-io/nextflow?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
  - Nextflow [blog](https://www.nextflow.io/blog.html)
  - Nextflow [google group](https://groups.google.com/forum/#!forum/nextflow)
  - Nextflow [twitter](https://twitter.com/nextflowio)
  - A curated list of [Nextflow pipelines](https://github.com/nextflow-io/awesome-nextflow)
  - [nf-core](http://nf-co.re): an emerging effort to collect high quality pipelines
  - Nextflow paper: Di Tommaso P, Chatzou M, Floden EW, Barja PP, Palumbo E, Notredame C. Nextflow enables reproducible computational workflows. _Nat Biotechnol._ 2017 Apr 11;35(4):316-319. [doi: 10.1038/nbt.3820](https://www.nature.com/articles/nbt.3820). PubMed PMID: 28398311.
  - Another paper by nextflow folks about the impact of Docker on performance: https://peerj.com/articles/1273/
- Dataflow programming on [wikipedia](https://en.wikipedia.org/wiki/Dataflow_programming)
- Scientific workflow system on [wikipedia](https://en.wikipedia.org/wiki/Scientific_workflow_system)
- A [paper in PLOS Comp. Bio.](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1004947) about using GitHub efficiently to manage your bioinformatics projects

## Tips and tricks
