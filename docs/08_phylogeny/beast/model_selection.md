# 选择模型

Bayesian 计算需要选择各种模型，比如序列进化的模型，分子种模型等等。那么在分析中如何选择模型，哪一种模型更适合我们的数据？这里就要用一些成熟的统计学原理进行模型选择和比较。

模型和参数会产生2个极端即过拟合和低拟合。

过拟合：参数众多，模型复杂
低拟合：参数太少，模型简单

原则1：不要把参数的各种组合结果进行比较。
原则2：比较与假设相关或者感兴趣的模型。


HME: harmonic mean estimator(Newton and Raftery, 1994)
AICM: Akaike's information criteration(AICM, Raftery et al., 2007)
PS: path sampling(Lartillot and Philippe, 2006)
SS: stepping-stone sampling(Xie et al., 2011)

SS, PS > AICM > HME

HME 和 AICM 在 tracer 中提供的评估计算功能，但是 SS 和 PS tracer 中没有相应功能。要在 beauti 中的 MCMC 模块的 Marginal Likelihood estimation(MLE)中选择设置 PS 和 SS。

用 PS 和 SS 生成的结果中，选择最高的 log marginal Likelihood 的那个模型。Bayers Factor(BF) 是一种相对 log marginal Likelihood 的概念，它的计算公式：

ln(BF) = ln(marginal Likelihood(modelA)) - ln(marginal Likelihood(modelB))

如果 ln(BF) = -530 - (-540) = 10 ，说明 modelA 比 modelB 更合适。软件生成的是 log 值，一般都是一个很小的数，因此 log 后一般为负数。

beauti 生成 xml 文件中关于 PS/SS 分析的部分是：

```
<beast>
    <steppingStoneSamplingAnalysis fileName="MLE-1.bsp.log MLE-2.bsp.log">
        <likelihoodColumn name="pathLikelihood.delta"/>
        <thetaColumn name="pathLikelihood.theta"/>      
    </steppingStoneSamplingAnalysis>
</beast>
```


## Reference
1. BAYESIAN MODEL TESTING - Guy Baele, Rega Institute, Department of Microbiology and Immunology, K.U. Leuven, Belgium.
2. [什么是Bayesian Factor BF](http://bayesfactor.blogspot.ca/2014/02/the-bayesfactor-package-this-blog-is.html)
3. http://beast.community/model_selection_1
