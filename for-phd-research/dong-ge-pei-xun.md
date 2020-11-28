# SPAdes assembly-东哥培训

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

Step5 run the below command line in Linux

`spades.py -t 36 -k 21,33,55,77 --careful -1 /beegfs/home/qnz/spades_test/H13_R1.fq.gz -2 /beegfs/home/qnz/spades_test/H13_R2.fq.gz -o ./out`

{% hint style="info" %}
-t, --threads &lt;int&gt; number of threads to use \(default: number of CPUs\)

-k, --kmer &lt;int&gt; k-mer length \(default: 21, must be odd\)

--careful, Tries to reduce the number of mismatches and short indels
{% endhint %}

Step6 upload the files

把文件传到系统里

毛师妹多个数据，附带了郑老师的perl脚本。

师妹自己写了vim XXX.sh，用了for ...循环，然后粘贴最后一句perl脚本的in put ，同样可以运行。相当于把perl转换成了shell脚本。

郑老师脚本的最后一句：

```perl
spades.py -t 36 -k 21,33,55,77 --careful -1 $r1 -2 $r2 -o $out
```

改了下，直接在Linux中运行

Step7 run commond lines

#### Try-1

```text
 spades.py -t 36 -k 21,33,55,77 --careful -1 /beegfs/home/qnz/spades_test/H13_R1.fq.gz -2 /beegfs/home/qnz/spades_test/H13_R2.fq.gz -o ./out
```

#### Try-2 \(-k is different\)

```text
spades.py -t 36 -k 21,33,55,77,99,119,127 --careful -1 /beegfs/home/qnz/spades_test/H13_R1.fq.gz -2 /beegfs/home/qnz/spades_test/H13_R2.fq.gz -o ../out_2
```

Step N deactivate the new env

 `conda deactivate` 



#### References

https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html

https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3342519/









