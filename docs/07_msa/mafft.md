# Mafft 构建多重序列比对





## 基本用法

```
$ mafft --auto input > output
```


## 基于 web 在线的 Mafft 工具

对于个人电脑上无法开展 mafft 比对，比如无 Linux 环境或者大量序列的比对等，可以通过在线 mafft 工具来实现多重序列比对。

* [CBRC Mafft Server](https://mafft.cbrc.jp/alignment/server/large.html)
* [EBI Mafft Server](https://www.ebi.ac.uk/Tools/msa/mafft/)
* [GenomeJP Mafft Server](http://www.genome.jp/tools-bin/mafft)
* [MyHits Mafft Server](https://myhits.isb-sib.ch/cgi-bin/mafft)
* [T-REX Mafft Server](http://www.trex.uqam.ca/index.php?action=mafft)
* [MPI Mafft Server](https://toolkit.tuebingen.mpg.de/#/tools/mafft)



## 新增序列

当你需要新增序列到原来已经比对好的结果中时，如果重新计算所有序列则会浪费大量时间，mafft 提供了 --add，--addfull 参数来实现添加新序列到原比对中。


## 结果输出

输出的比对结果默认是 fasta 格式的，如果想输出 clustal 格式，可以加上参数`--clustalout`。

## Reference

1. [Mafft Official Site]()
2.
