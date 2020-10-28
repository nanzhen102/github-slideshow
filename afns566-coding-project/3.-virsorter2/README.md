# 3. VirSorter2

#### 3.1 Introduction

VirSorter2 applies a multi-classifier, expert-guided approach to detect diverse DNA and RNA virus genomes.

#### 3.2 Installation 

Two methods to install VirSorter2.

{% tabs %}
{% tab title="Simple method" %}
Run`conda install -c bioconda virsorter=2` to install this package with Conda.
{% endtab %}

{% tab title="Recommended method " %}
Follow the four steps below to install a development version.

1. Run `conda create -n vs2 -c bioconda -c conda-forge python=3 scikit-learn=0.22.1 imbalanced-learn pandas seaborn hmmer prodigal screed ruamel.yaml snakemake=5.16.0 click` to create an environment named "vs2"  and install other packages.
2. Run `conda activate vs2` to activate the environment.
3. Run `git clone https://github.com/jiarong/VirSorter2.git` to clone all documents.
4. Run `cd VirSorter2` to change to the dictionary named "VirSorter2", run `pip install -e .`to final install it.  

> `-e` is short for `--editable`, and `.` refers to the current working directory, so together, it means to install the current directory \(i.e. your project\) in editable mode.
{% endtab %}
{% endtabs %}

#### 3.3 Test run \(only one input file\)

**Step 1.** Fetch testing data

```text
wget -O test.fa https://raw.githubusercontent.com/jiarong/VirSorter2/master/test/8seq.fa 
```

**Step 2.** Run classification with 4 threads \(-j\) and test-out as output directory \(-w\)

```text
virsorter run -w test.out -i test.fa -j 4
```

**Step 3.** Check results

```text
ls test.out
```

#### 3.4 Officially run \(multiple input files\)

Step 1. ****Learn Vim.

{% page-ref page="vim.md" %}

Step 2. ****Learn Shell.

{% page-ref page="shell-jiao-ben.md" %}

Step 3. ****Learn for loop.

{% page-ref page="3.-loops-for-while-and-until.md" %}

Step 4. ****Learn Slurm.

{% page-ref page="4.-slurm.md" %}

Step 5. Run `vim virsorter2_nanzhen_1.sh`.

Step 6. Type the following command lines.

```text
#!/bin/sh
#SBATCH -J nanzhen_virsorter2
#SBATCH -c 30
#SBATCH -p normal

for i in `ls /beegfs/home/qnz/scaffold`
do
virsorter run -w ${i} -i /beegfs/home/qnz/scaffold/${i} -j 30
done

```

Step 7. Run `conda activate vs2`.

Step 8. Run `sbatch virsor2_nanzhen_1.sh`.

```text
(vs2) [nanzhen@admin ~]$ sbatch virsorter2_nanzhen_1.sh
>>> Submitted batch job 45693
```

Step 9. Run `squeue` .

```text
(vs2) [nanzhen@admin ~]$ squeue
>>>              JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
>>>              42222    normal nnnnnnnn      nnn  R 1-08:24:37      1 node4 
>>>              45693    normal nanzhen_      qnz  R       1:03      1 node3 

```

or run `squeue -u qnz`

waiting......



#### 3.5 References

* https://github.com/jiarong/VirSorter2
* https://peerj.com/articles/985/ 

