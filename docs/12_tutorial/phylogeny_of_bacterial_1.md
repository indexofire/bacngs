# Bacterial Genomic SNP Calling Workflow

```
# 将多个数据分别存放到样品名称的文件夹中去
$ for i in $(awk -F'L001' '{gsub("_$", "", $1); print $1}' < (ls data/*.fastq.gz) | sort | uniq ); do mkdir $(basename $i); mkdir $(basename $i)/raw; cp $i*.fastq.gz $(basename $i)/raw/. ; done

# 去除低质量序列
$ for i in $(ls -d *); do sickle pe -f $i/raw/*_R1_001.fastq.gz -r $i/raw/*_R2_001.fastq.gz -t sanger -o trim/${i}_R1.fastq.gz -p trim/${i}_R2.fastq.gz -s single.fastq.gz -q 20 -l 10; done

# 序列比对到参考基因组
$ bwa index ref.fasta
$ for i in $(ls -d *); do bwa mem -M ref.fasta $i/trim/${i}_R1.fastq.gz $i/trim/${i}_R2.fastq.gz 
```



## Reference

1. http://userweb.eng.gla.ac.uk/cosmika.goswami/snp_calling/SNPCalling.html
2. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4493402/
