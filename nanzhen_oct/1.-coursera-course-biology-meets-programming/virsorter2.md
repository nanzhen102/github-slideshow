# previous\_virsorter2



{% hint style="info" %}
以前的版本：

Xudong Li:

virsorter.lsf （Linux里后缀无所谓，不过bash还是常用.sh为后缀，方便识别）

```text
for file in 6_BDME192013411-1a 9_BDME192013412-1a 10_BDME192013413-1a 11_BDME192013414-1a
do
nohup wrapper_phage_contigs_sorter_iPlant.pl -f /mnt/data/home/lxd/4_salt_metagenomics/5.megahit_out/${file}/final.contigs.fa --db 1 --wdir /mnt/data/home/lxd/4_salt_metagenomics/viruses/virsorter/${file}/ --data-dir /mnt/data/home/lxd/4_salt_metagenomics/tools/virsorter-data --ncpu 15 --diamond 1>${file}.out 2>${file}.err &
done
```

最新的版本看jiarong github
{% endhint %}


