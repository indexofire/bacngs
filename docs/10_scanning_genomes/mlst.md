# MLST scanning

MLST在过去被用来快速构建菌群关系，研究物种进化和演变方向等具有很大的作用。随着基因组时代的到来，它仍能发挥巨大的作用。


## 对拼接数据进行扫描

比如我们要对 Bacillus cereus lato sero 蜡样芽胞杆菌血清群 MLST 数据进行扫描，可以用以下命令获得结果。

```
$ mlst --scheme bcereus *.fasta > result.mlst
$ cat result.mlst
```


## 对短序列数据进行扫描

短序列数据要通过比对软件与参考序列比对后获得匹配结果，

```
$ srst2 --input_pe s1_1.fastq.gz s1_2.fastq.gz \
> --mlst_db ../Bacillus_cereus.fasta \
> --mlst_definitions ../bcereus.txt \
> --mlst_delimiter _ \
> --output s1 \
> --threads 40
```
