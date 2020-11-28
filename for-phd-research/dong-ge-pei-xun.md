# 东哥培训

细菌基因组拼接，毛+王，SPAdes噬菌体

噬菌体基因组拼接，彭+乔，

需要改参数

这是单菌，要改的perl的是宏基因组

Bankevich A, Nurk S, Antipov D, et al. SPAdes: a new genome assembly algorithm and its applications to single-cell sequencing\[J\]. Journal of computational biology, 2012, 19\(5\): 455-477.

R1，R2代表双端测序的结果

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





Step N deactivate the new env

 `conda deactivate` 





#### References

https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html

https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3342519/









