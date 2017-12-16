#

将细菌基因拼接，然后将reads比对到参考基因组，输出未比对的reads。再将未比对的reads比对到拼接结果上，就可以知道参考基因组上没有的序列reads拼接的contigs是那些了。


```
$ spades.py --careful -k 21,33,55,77,99,121 -1 1_R1.fastq.gz -2 1_R2.fastq.gz -o assembly -T 40
$ cp assembly/scaffolds.fasta assembly.fasta
$ bwa index ref.fasta
$ bwa mem ref.fasta 1_R1.fastq.gz 1_R2.fastq.gz | samtools -bS

$ bwa index assembly.fasta

```
