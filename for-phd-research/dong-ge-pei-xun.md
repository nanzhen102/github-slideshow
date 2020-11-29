---
description: >-
  Use SLURM to run a job. Submit a job in a certain Conda env that contains
  every software you need.
---

# SPAdes assembly-a phage genome-circle

细菌基因组拼接，毛+王，SPAdes噬菌体

噬菌体基因组拼接，彭+乔，

需要改参数

这是单菌，娜姐给的要改的perl的是宏基因组

Bankevich A, Nurk S, Antipov D, et al. SPAdes: a new genome assembly algorithm and its applications to single-cell sequencing\[J\]. Journal of computational biology, 2012, 19\(5\): 455-477.

R1，R2代表双端测序的结果

SPAdes \(St. Petersburg genome assembler\) is a genome assembly algorithm which was designed for single cell and multi-cells bacterial data sets. However, it might not be suitable for large genomes projects.

| **SPAdes pipeline** | **Functions** |
| :--- | :--- |
| BayesHammer  | read error correction tool for Illumina reads |
| IonHammer | read error correction tool for IonTorrent data |
| SPAdes | iterative short-read genome assembly module |
| MismatchCorrector | improves mismatch and short indel rates in resulting contigs and scaffolds |

Step1 create a new env

`conda create --name spades`

Step2 activate the new env

`conda activate spades`

Step3 verify the env

`conda env list` 

```text
(spades) [nanzhen@admin ~]$ conda env list
# conda environments:
#
                         /beegfs/home/nanzhen/VirSorter2/db/conda_envs/1dbde381
base                     /beegfs/home/nanzhen/miniconda3
spades                *  /beegfs/home/nanzhen/miniconda3/envs/spades
vs2                      /beegfs/home/nanzhen/miniconda3/envs/vs2

```

Step4 install SPAdes in the new env

`conda install -c bioconda spades`

\(Step5 run the below command line in Linux\)

`spades.py -t 36 -k 21,33,55,77 --careful -1 /beegfs/home/qnz/spades_test/H13_R1.fq.gz -2 /beegfs/home/qnz/spades_test/H13_R2.fq.gz -o ./out`

{% hint style="info" %}
`spades.py`  就是主要的提交脚本

-t, --threads &lt;int&gt; number of threads to use \(default: number of CPUs\)

-k, --kmer &lt;int&gt; k-mer length \(default: 21, must be odd\)

--careful, Tries to reduce the number of mismatches and short indels

`-1` `-2` 分别指定双端测序的R1和R2端序列文件
{% endhint %}

Step5 upload the files

把文件传到系统里

毛师妹多个数据，附带了郑老师的perl脚本。

师妹自己写了vim XXX.sh，用了for ...循环，然后粘贴最后一句perl脚本的in put ，同样可以运行。相当于把perl转换成了shell脚本。

郑老师脚本的最后一句：

```perl
spades.py -t 36 -k 21,33,55,77 --careful -1 $r1 -2 $r2 -o $out
```

改了下，直接在Linux中运行

Step6 run commond lines

#### Try-1

```text
 spades.py -t 36 -k 21,33,55,77 --careful -1 /beegfs/home/qnz/spades_test/H13_R1.fq.gz -2 /beegfs/home/qnz/spades_test/H13_R2.fq.gz -o ./out_1
```

#### Try-2 \(-k is different\)

```text
spades.py -t 36 -k 21,33,55,77,99,119,127 --careful -1 /beegfs/home/qnz/spades_test/H13_R1.fq.gz -2 /beegfs/home/qnz/spades_test/H13_R2.fq.gz -o ./out_2
```

Step7 check output files

`contig.fasta` 代表contig组装的结果

`scaffolds.fasta` 代表scaffold的结果

如contig.fasta里，会含有多个 contig，&gt;开头，length是长度，cov是深度。

Step8 evaluate the quality of assembly results - assembly-stats software

in spades env

`conda install -c bioconda assembly-stats` 

`cd /beegfs/home/qnz/spades_test/out_2` 

`assembly-stats contigs.fasta` 

output:

```text
(spades) [nanzhen@admin out_2]$  assembly-stats contigs.fasta
stats for contigs.fasta
sum = 4414476, n = 787, ave = 5609.25, largest = 1090207
N50 = 803942, n = 3
N60 = 803942, n = 3
N70 = 663511, n = 4
N80 = 663511, n = 4
N90 = 42727, n = 7
N100 = 128, n = 787
N_count = 0
Gaps = 0
```

> largest大于1M，肯定不是噬菌体，不符合噬菌体的基因大小，常100Kb左右。
>
> 选取contigs中的一个进行NCBI上的BLAST比对，
>
> 确实，是宿主污染。实验提取时候的问题。

Step9 check the length of each contig

`grep ">" contigs.fasta | less` 

`q` 

Step10 the longest contig - write a script to extract it

{% tabs %}
{% tab title="Method1" %}
```python
seq = open("/Users/nanzhen/Desktop/contigs.fasta")
seq_longestcontig = open("/Users/nanzhen/Desktop/contigs_longest.fasta", 'w')

str = ''

for line in seq:
	if line[0] == ">" and str =="":
		line_1 = line
	elif line[0] != ">":
		str = str + line
	elif line[0] == ">" and str != "":
		if "160931" in line_1:
			seq_longestcontig.write(line_1 + str)
		line_1 = line
		str = ""

seq.close()
seq_longestcontig.close()
```
{% endtab %}

{% tab title="Method2-simple" %}
use biopython

a package in python
{% endtab %}

{% tab title="files" %}
{% file src="../.gitbook/assets/contigs.fasta" caption="contigs.fasta" %}
{% endtab %}

{% tab title="output file" %}
{% file src="../.gitbook/assets/contigs\_longest \(4\).fasta" caption="contigs\_longest.fasta" %}
{% endtab %}
{% endtabs %}

Step11 the longest contig - if it is a circular DNA

\(my python version is 3.8, create a new env to change it to 3.6）

`conda create -n circle-map python=3.6` to create a new env

`conda activate circle-map` to activate the new env

`python --version` to check the python version in the new env

`conda list` to know what packages are installed in a Conda environment

`conda install -c bioconda circle-map` to install circle-map

文件为什么都保存到默认文件夹里的。。。可以提前设置保存在某一个文件夹里吗

`conda install -c bioconda bwa` to install bwq package

`conda install -c bioconda samtools` to install samtools package

follow this tutorial and **use SLURM to run a job!!!!!** ❗ ****❗ ****❗ ****❗ ****❗\*\*\*\*

**Submit a job in a certain Conda env that contains every software you need**  ❗ ****❗ ****❗ ****❗ ****❗\*\*\*\*

{% embed url="https://github.com/iprada/Circle-Map/wiki/Tutorial:-Identification-of-circular-DNA-using-Circle-Map-Realign" %}

`vim circle-map_nanzhen.sh` 

type the following command lines

```text
#!/bin/sh
#SBATCH -J circlemap_nanzhen
#SBATCH -c 30
#SBATCH -p normal


# Step 1: preparing and downloading the data
wget https://raw.githubusercontent.com/iprada/Circle-Map/master/tutorial/unknown_circle_reads_1.fastq
wget https://raw.githubusercontent.com/iprada/Circle-Map/master/tutorial/unknown_circle_reads_2.fastq
wget http://hgdownload.soe.ucsc.edu/goldenPath/hg38/bigZips/hg38.fa.gz
gunzip -d hg38.fa.gz
bwa index hg38.fa
samtools faidx hg38.fa

# Step 2: Alignment of the reads to the reference genome
bwa mem -q hg38.fa unknown_circle_reads_1.fastq unknown_circle_reads_2.fastq > unknown_circle.sam

# Step 3: Preparing the files for Circle-Map
samtools sort -n -o qname_unknown_circle.bam unknown_circle.sam
samtools sort -o sorted_unknown_circle.bam unknown_circle.sam
Circle-Map ReadExtractor -i qname_unknown_circle.bam -o circular_read_candidates.bam
samtools sort -o sort_circular_read_candidates.bam circular_read_candidates.bam
samtools index sort_circular_read_candidates.bam
samtools index sorted_unknown_circle.bam

# Step 4: Detecting the circular DNA
Circle-Map Realign -i sort_circular_read_candidates.bam -qbam qname_unknown_circle.bam -sbam sorted_unknown_circle.bam -fasta hg38.fa -o my_unknown_circle.bed

```

`sbatch circle-map_nanzhen.sh` 

{% hint style="info" %}
为什么所有的都在PD排队？？可以通过调节`-c` 来插队吗？smp还有挺多盒，normal最多的只有6个了。

可以的，把盒`-c` 调成5个试试。插队成功！

```text
             60197    normal 20140308      lxd  R      15:39      1 node7 
             60198    normal 20131015      lxd  R      11:00      1 node6 
             60199    normal 20140306      lxd  R      10:02      1 node6 
             60200    normal 20131005      lxd  R       6:45      1 node6 
             60201    normal 20131129      lxd  R       4:28      1 node8 
             60202    normal 20140306      lxd  R       2:34      1 node6 
             61059    normal circlema      qnz  R       0:06      1 node8 
```
{% endhint %}

`squeue -u qnz` to know all current jobs for a User

`sacct -j 61059 --format=JobID,JobName,MaxRSS,Elapsed` to get additional information of a completed job. This includes run time, memory used, etc. 

```text
(base) [qnz@admin ~]$ sacct -j 61058 --format=JobID,JobName,MaxRSS,Elapsed
       JobID    JobName     MaxRSS    Elapsed 
------------ ---------- ---------- ---------- 
61059        circlemap+              00:41:05 
61059.batch       batch       944K   00:41:05 
61059.extern     extern          0   00:41:05 
```

Step12 Error - check Errors

in an `slurm-job#.out` file,  'ImportError: Bio.Alphabet has been removed from Biopython. In many cases, the alphabet can simply be ignored and removed from scripts. In a few cases, you may need to specify the \`\`molecule\_type\`\` as an annotation on a SeqRecord for your script to work correctly. Please see https://biopython.org/wiki/Alphabet for more information.'

Google the error, perhaps it is due to the biopython version, it should be 1.68 rather than 1.78.

`conda list` in the new env to check the version of python and biopython

`conda install python=2` to install python2, no need to delete python3

`conda install -c montilab biopython=1.68` to install biopython1.68

`sbatch` the job again, the job \# is  61063











Step13 the second and third long contigs - BLAST to see what it belongs to







最长或者次长的那条挑出来，看是否能成环。





#### References

https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html

https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3342519/

https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-019-3160-3





{% hint style="info" %}
Geneious Prime software 

彭师妹从文献中发现这个软件，很快就得到能否成环的结果。

功能极其强大，但是要求的内存也多。但是，对于此phage数据，即使随机选择序列，也组装得到类似长度的contig，说明，没有必要测序深度这么深。
{% endhint %}



