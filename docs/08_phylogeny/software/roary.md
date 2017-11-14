# Roary

## Roary 介绍

## 使用方法

### 1.

首先将所有要分析的gff格式的基因组文件放置到gff文件夹中，运行 roary 获得 Pangenome 分析，主要可以获得基因的分布情况。加上 `-e --mafft` 参数，可以调用 mafft 获得核心基因序列的多重比对结果。`-p 40` 为分析时条用的 threads 数量，根据计算机CPU具体情况设定。

``` bash
# 生成核心基因，并对核心基因序列用mafft进行多重序列比对
# -e --mafft 表示用 mafft 进行序列比对
# -cd 100 表示100%菌株都需要携带的基因才算为核心基因，如果菌株中一旦存在距离
# 较远的或者混杂了非目的物种的菌株基因组，最终的核心基因数量可能会非常小，所以
# 要谨慎使用，为了避免不同物种构建 core-genome，可以用参数
# -k /path/to/Kraken_database/ 使用karaken来分析reads的物种偏向。该参数默认值
# 为 99, 即99%菌株携带的基因即为核心基因。
# -p 40线程进行计算
$ roary -e --mafft -cd 100 -p 40 gff/*.gff

# 如果菌株数量过多，或者菌株草图中contigs数量太多，会导致矩阵过于庞大
```

### 2. 结果文件

在当前文件夹下可以生成相应的结果文件：

accessory_binary_genes.fa
accessory_binary_genes.fa.newick
accessory_graph.dot
accessory.header.embl
accessory.tab
blast_identity_frequency.Rtab
clustered_proteins
core_accessory_graph.dot
core_accessory.header.embl
core_accessory.tab
core_alignment_header.embl
core_gene_alignment.aln
core_gene_alignment.aln.reduced
gene_presence_absence.csv
gene_presence_absence.Rtab
number_of_conserved_genes.Rtab
number_of_genes_in_pan_genome.Rtab
number_of_new_genes.Rtab
number_of_unique_genes.Rtab
pan_genome_reference.fa
RAxML_bootstrap.raxml
RAxML_info.raxml
summary_statistics.txt

!!! note "summary_statistics.txt"
    test
