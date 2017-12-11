# Shell

以 Bash 为例介绍一些生物信息学常用的 shell 命令。

## 循环

循环是常用的功能，往往被用来批量处理数据。循环在终端下直接运行 oneline shell 脚本或者写 shell 程序常会用到。最常用的循环 loop 方式是用 for 来执行。

```
$ for i in *.fastq.gz; do bwa aln ref.fasta $i > $i.sai; done
```

测序时常用流水号做为样品名称，比如 miseq 测序结果数据常常如下：

```
1_S1_R1_L001.fastq.gz   1_S1_R2_L001.fastq.gz
2_S2_R1_L001.fastq.gz   2_S2_R2_L001.fastq.gz
3_S3_R1_L001.fastq.gz   3_S3_R2_L001.fastq.gz
...
12_S12_R1_L001.fastq.gz 12_S12_R2_L001.fastq.gz
```

用 for 循环遍历的写法1-12可以是

```
$ for i in 1 2 3 4 5 6 7 8 9 10 11 12; do COMMAND; done
$ for i in {1..12}; do COMMAND; done

# 从1-12,间隔3输出，结果i为1,4,7,10
$ for i in {1..12..3}; do COMMAND; done
```

对于同一种文件格式，可以用正则表达来过滤

```
$ for i in 1.fq 2.fq 3.fq 4.fq; do COMMAND; done
$ for i in *.fq; do COMMAND; done
```

```
$ for i in $(COMMAND); do COMMAND; done
```

shell 还可以写成类似C语言的循环方式：

```
$ for ((i=1;i<=10;i++)); do COMMAND; done
```
