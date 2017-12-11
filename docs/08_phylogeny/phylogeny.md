# Phylogeny

## Model

1. GTR: General Time Reversible
2. HKY:







#### 计算进化树各个节点的距离：

1. Dendropy

```python
import dendropy
from dendropy import treecalc

tree = dendropy.Tree.get_from_path("input.nex", "nexus")
pdm = treecalc.PatristicDistanceMatrix(tree)
for i, t1 in enumerate(tree.taxon_set):
    for t2 in tree.taxon_set[i+1:]:
        print("Distance between '%s' and '%s': %s" % (t1.label, t2.label, pdm(t1, t2)))
```

2. ape

```R
> library(ape)
> tree<-read.tree("file.tre")
> PatristicDistMatrix<-cophenetic(tree)
```
