---
description: This step should be done before VirSorter2.
---

# 4. assembly + Bin

{% hint style="info" %}
run `module load Metagenomics/lxd` to use the metagenomic assembly software

**DO NOT need to reinstall software.**
{% endhint %}

#### 4.1 Introduction

scaffold file

metagenomic, DNA



#### 4.2 Convert Perl script to Shell script.  

```javascript
#!/usr/bin/perl -w
use strict;
my %ids;
my @gz = glob("*.gz");
my %reads;

foreach (@gz) {
    if (/(ERR\d+)_\d+\.fastq\.gz/) {
	    $reads{$_} = "1";
		$ids{$1} = "1";
	}
}

foreach (%ids) {
    my $r11 = $_ . "_1.fastq.gz";
	my $r22 = $_ . "_2.fastq.gz";
	# my $r1 = $_ . ".ff.1.fastq.gz";
    my $r1 = $r11;
    my $r2 = $r22;
	# my $r2 = $_ . ".ff.2.fastq.gz";
	my $out = $_ . "_out";
	if (exists $reads{$r11}) {
	    if (exists $reads{$r22}) { 
			# system("fastp --in1 $r11 --in2 $r22 --out1 $r1 --out2 $r2 -l 50 -w 24");
			system("megahit --k-list 27,37,51,71,87 -1 $r1 -2 $r2 -t 72 -o $out");
			system("reformat.sh -Xmx20g threads=72 in=$out/final.contigs.fa out=$out/final.contigs-2000.fasta fastaminlen=2000");
			system("bowtie2-build $out/final.contigs-2000.fasta $out/final.contigs-2000");
			system("bowtie2 -x $out/final.contigs-2000 -1 $r1 -2 $r2 -p 72 --very-sensitive-local -S $out/final.contigs-2000.sam");
			system("samtools view -@ 72 -S -b $out/final.contigs-2000.sam > $out/final.contigs-2000.bam");
			system("samtools sort -m 2056M -o $out/final.contigs-2000.sorted.bam -@ 72 $out/final.contigs-2000.bam");
			system("java -jar /mnt/public/home/zjs/tools/picard/build/libs/picard.jar MarkDuplicates REMOVE_DUPLICATES=true READ_NAME_REGEX=null MAX_FILE_HANDLES_FOR_READ_ENDS_MAP=3000 I=$out/final.contigs-2000.sorted.bam O=$out/final.contigs-2000.sorted.dep.bam M=$out/final.contigs-2000.sorted.dep.metrics.txt");
			my $depth = $out . "/" . "final.contigs-2000" . ".depth.txt";
			my $pairs = $out . "/" . "final.contigs-2000" . ".paired.txt";
			system("jgi_summarize_bam_contig_depths --outputDepth $depth --pairedContigs $pairs --minContigLength 2000 --minContigDepth 1 $out/final.contigs-2000.sorted.dep.bam");
			my $bin = $out . "/" . "bins";
			my $fa = $_ . ".bin";
			my $bin_out = $bin . "/" . $fa;
			system("mkdir $bin");
			system("metabat2 -i $out/final.contigs-2000.fasta -t 72 -a $depth -o $bin_out");
			my $ch_out = $out . "/" . $out . "_checkm";
			system("mkdir $ch_out");
			system("checkm lineage_wf -f $ch_out/checkM-SCG-single.txt -t 72 --pplacer_threads 10 -x fa $bin $ch_out");
			system("rm $out/final.contigs-2000.sam $out/final.contigs-2000.bam $out/final.contigs-2000.sorted.bam $out/final.contigs-2000.sorted.dep.bam $r1 $r2");
			system("mv $r11 finished/");
			system("mv $r22 finished/");
		}
	}
}

time nohup checkm lineage_wf -f checkM-SCG-single.txt -t 72 --pplacer_threads 10 -x fasta ./part2 ./output2
```



#### 4.3 Run 



