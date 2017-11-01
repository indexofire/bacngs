# Assembly 数据的进化树构建

传统的细菌基因组测序结果构建进化树，一般参用reads比对到reference genome上后，获得各个样本的snp位点序列，通过将所有序列连锁后可以获得所要分析的样本的SNP序列，以此序列构建进化树。

对于输入数据为已经拼接完成的assembly序列，就要采用其他的方法获得snp位点了。比如用kmer（ksnp3）的方法获取snp位点，也可以获得core-genes，将核心基因的序列比对获得相应的SNP位点。

基于assembly数据构建进化树的工具往往开发较早，出现在NGS发展之前，一般来说缺少多线程的支持。

## 1. 数据准备

从 NCBI Assembly 数据库下载 gff 格式的数据。对于基因组测序reads数据，可以用spades拼接获得scaffolds.fasta后，用prokka生成gff格式的文件。将所有的gff文件放在一个目录中。

## 2. 数据质控

即使是assembly数据库中ref seq的数据，也建议进行质控后选择。对于非refseq的数据更要仔细验证后选择，否则后面分析会浪费大量精力和时间。

### 2.1 物种鉴定

```
$ kraken
```

## 3. 数据分析

### 3.1 基于core genes的分析方法

同一物种的细菌会携带核心基因组

需要注意的是细菌存在大量的recombination，如果只分析snp，那么indel等需要去除，同时要把recombination造成的snp也去除。

### 3.1.1 roary

```
$ roary -cd 100 -e --mafft -p 40 -f output *.gff
  # 参数说明:
  # -cd 100 表示只有100%的基因组均包括的基因，才做为 core genes，默认是 99%
  # -e --mafft 用mafft进行多重序列比对
  # -p 40 使用多线程
  # -f output 输出结果到output目录
```

获得的 core_gene_alignment.aln 是用mafft生成的比对文件。可用来构建进化树。

```
$ raxml -f a -p 12345 -x 12345 -#100 -s core_gene_alignment.aln -n cg -m GTRGAMMAI -T 40
```

#### 3.1.2 get_homologs

```
$
```

### 3.2 基于MUMs的分析方法

#### 3.2.1 parsnp

* reference non-free

Harvest工具中的parsnp可以用来快速鉴定同一种菌的基因组进化关系，特点是速度特别快，适合做同一种菌的近源基因组序列关系分析。如果同一种菌的菌株的序列差异较大，存在较多IS序列，会造成比对的基因组覆盖度区域过低，比如400个Bacillus cereus的菌株比对，只有1%的参考序列可以覆盖到。这种情况下就不适合使用harvest。而比如甲型副伤寒沙门菌高度保守，可以用parsnp来快速构建基因组进化图。如果覆盖度不够，应考虑使用mugsy，mauve等工具进行分析。

parsnp其精度比基于mapping的SNP分析略低，但速度快的多。

```
$ parsnp -g ref.gbk -d fna -c -x
  # 参数说明
  # -g ref.gbk 表示选择gbk格式的基因组做为参考序列
  # -d fna 表示用fna目录下的fasta格式文件做为输入数据
  # -c 表示使用fna目录下的所有基因组
  # -C 10000 表示跨越基因组10k长区域
  # -x 用phipack去除重组
```

```
$ harvestools -i parsnp.ggr -S output.snp
$ mafft --maxiterate 1000 --localpair output.snp > output.mafft
$ raxml -f a -p 12345 -x 12345 -#100 -s output.mafft -n snp -m GTRGAMMA -T 40
```

#### 3.2.2 progressMauve

* reference free

Mauve工具使用java开发的

```
$ progressMauve --output=output.xmfa *.gbk
```

#### 3.2.3 Mugsy

* reference free

mugsy这些工具由于

```
$ mugsy -p mugsy *.fasta
$ mugsyWGA -i output.xmfa
```

**参考文献：**

> [Angiuoli SV and Salzberg SL. Mugsy: Fast multiple alignment of closely related whole genomes. Bioinformatics 2011 27(3):334-4](https://www.ncbi.nlm.nih.gov/pubmed/21148543)

### 3.3 基于kmer的分析方法

#### 3.3.1 kSNP3

```
$ kSNP3
```

#### 3.3.2 andi

#### 3.3.3 
