# MLST scanning

MLST在过去被用来快速构建菌群关系，研究物种进化和演变方向等具有很大的作用。随着基因组时代的到来，它仍能发挥巨大的作用。


## MLST

```
$ mlst --scheme bcereus *.fasta > result.mlst
```


## srst2

```
$ srst2 --input_pe s1_1.fastq.gz s1_2.fastq.gz \
> --mlst_db ../Bacillus_cereus.fasta \
> --mlst_definitions ../bcereus.txt \
> --mlst_delimiter _ \
> --output s1 \
> --threads 40
```
