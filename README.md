# Protocol

#### Date: **Dec** 10, 2020

#### Author: Nanzhen Qiao

#### Status: Version 1.0

#### Project: The analysis of prophage in pig gut microbiome 

\*\*\*\*

### 1. Conda

**Background**

Conda is an open source package management system and environment management system for installing multiple versions of software packages and their dependencies and switching easily between them. It works on Linux, OS X and Windows, and was created for Python programs but can package and distribute any software.

Conda allows users to create separate environments containing files, packages, and their dependencies that will not interact with other environments. When users begin using Conda, they already have a default environment named base. Users put programs into separate environments rather than their base environment.

**Installation**

`conda install -c anaconda conda` in XShell/Terminal/FinalShell/your lab server to install conda package

`conda info` to verify if Conda is successfully installed

`conda update conda` to update Conda to the current version

`conda info -e` to verify your current environment

### 2. Virsorter

**Background**

VirSorter2 applies a multi-classifier, expert-guided approach to detect diverse DNA and RNA virus genomes. It is used to identify prophages in complete microbial genomes.

VirSorter2 can identify viral signal in assembled sequence \(contigs\) as short as 3kb, while providing near-perfect identification \(&gt;95% Recall and 100% Precision\) on contigs of at least 10kb.

**Installation**

`conda create --name virsorter` to create a new environment for virsorter

`conda activate virsorter` to activate the new environment

`conda install -c bioconda virsorter=2` to install virsorter

**Run**

> Note:
>
> Before starting this step, please check the job scheduling system for your lab server.
>
> e.g. Slurm,
>
> Slurm is an open source, fault-tolerant, and highly scalable cluster management and job scheduling system for large and small Linux clusters.
>
> The `sbatch` command is a bash script used to specify the resources you need to run your jobs, such as the number of nodes you want to run your job. Then, Slurm schedules your job based on the availability of the resources you’ve specified.

`vim virsorter2.sh` to create a vim file

press `I` key to start editor

type the following command lines

```text
#!/bin/sh
#SBATCH -J nanzhen_virsorter2
#SBATCH -c 30
#SBATCH -p normal
​
for i in `ls /beegfs/home/qnz/scaffold`
do
virsorter run -w ${i} -i /beegfs/home/qnz/scaffold/${i} -j 30
done
```

> Note:
>
> `-J nanzhen_virsorter2` is a name of the job that you want to run
>
> `-c 30` , you can change the `30` according to your lab server
>
> `-p normal` , you can change the `normal` according to your lab server
>
> `/beegfs/home/qnz/scaffold/` is the path that you store your scaffold files on the lab server

press `Esc` key to stop editor

type `:wq` to save and close the vim file

`sbatch virsorter2.sh` to submit the job

`squeeze -u qnz` to check the status of the running job

**Check output files**

use `mkdir` command to create a new folder named `visorter_output_hu_weilan`

use `mv` command to move all outfiles into this folder

`cd visorter_output_hu_weilan` to go to this folder

`ls` to view all output files

`cd file_name.fa` to one of the output files

`less final-viral-combined.fa` to view identified viral sequences \(full sequences identified as viral \(identified with suffix \|\|full\), partial sequences identified as viral \(identified with suffix \|\|{i}\_partial\)\)

type `Q`key to quit the `less` command

`less final-viral-score.tsv` to view a table that can be used for further screening of results

type `Q`key to quit the `less` command

**Remove redundancy \(Test Run\)**

`mkdir test_20201210` to create a new folder

`cp -r W2P21_scaffold.fa test_20201210` to copy files and paste to the new folder

`cd test_20201210` to the new folder

`grep -c "scaffold_*" /beegfs/home/qnz/1_prophage_virsorter/visorter_output_hu_weilan/test_20201210/W2P21_scaffold.fa/final-viral-combined.fa` to calculate the number of contigs

`conda install -c bioconda pullseq` to install pullseq

`pullseq -i final-viral-combined.fa -m 5000 > test_5000.fa` to delete contigs whose length &lt;= 5000bp

`conda install -c bioconda drep` to install drep

to install dependency-1-Mash

to install dependency-2-MUMmer

\*\*\*\*

