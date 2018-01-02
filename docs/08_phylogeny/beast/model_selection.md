# 选择模型

Bayesian 计算需要选择各种模型，比如序列进化的模型，分子种模型等等。那么在分析中如何选择模型，哪一种模型更适合我们的数据？这里就要用一些成熟的统计学原理进行模型选择和比较。

模型和参数会产生2个极端即过拟合和低拟合。r

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


1. Model Selection 模型选择：哪个模型是最适合分析自己DNA数据的模型？
2. Model Plausibility 模型可信性评估：我如何知道选择的模型给出的结果是可信的？

#### Model Selection

本质上说，所有的模型都是错误的，只有一部分是有用的。（George E.P. Box）

使用统计学方法为系统发育推理选择适当的序列进化模型已经较好的被完善了，并且现有文献（Sullivan and Joyce，2005）提供了足够强大的支撑。模型越复杂，越适合实际的数据。但是当模型复杂到一定程度时，结果所需的成本也是必须要考虑的问题。更复杂的模型需要估计更多的参数，而样本数据包含信息量是有限的。使用过于简单化的进化模型忽略了在自然界中发生的基本重要过程，可能会导致结果出现系统性误差（偏差），而使用过于复杂的模型会导致随机误差（方差膨胀）。事实上所有的模型选择方法都在试图找到平衡这两个相互竞争的误差来源的“最佳逼近模型”（Burnham, Anderson，1998），但是它们通常基于不同的理论基础。这些理论基础（及其相关的模型选择标准）有：

1. LRT: Frequentist Hypothesis Testing(Likelihood Ratio Test)
2. AIC: Information Theory(Akaike's an Information Criterion)
3. DT/R: Decision Theory(Decision Theoretic Risk)
4. BIC: Mix of Bayesian motivation and information theory(Bayesian Information Criterion)
5. BF: Bayesian Model Selection(Bayes Factors)
6. PP: Bayesian Hypothesis Testing or Model Averaging(Posterior Probabilities)

各种模拟研究表明，至少在贝叶斯框架中，适度的过度参数化通常会导致比适度的参数缺失更小的推理误差（Huelsenbeck, Rannala，2004; Lemmon, Moriarty，2004; Brown, Lemmon，2007）。这并不意味着严重的超参数化比适度的参数化要好。因此，如果两个模型似乎根据一个或多个模型选择标准大致相同，并且不能获得模型平均的估计值，那么通常会更好错在复杂的一面。

#### Model Plausibility

虽然模型选择标准的目标是选择一个最佳逼近一组候选模型中的自然过程的模型，但它们不能保证所选择的模型足以提供无偏差的推论。 当所有的候选模型都有一套共同的假设时尤其如此。 例如，许多核苷酸替代模型都假设这一点

1. 位点是相互独立的
2. 变化进程在一个序列中是均匀的
3. 变化进程在树上是均匀的
4. 密码子结构并不重要
5. 所有基因共享相同的树形拓扑

如果所有候选模型都假设了这些条件，那么模型选择标准就不可能说明这些假设在经验数据中被强烈违反了。因此，询问所选模型是否“足够好”是一个好主意。回答这个问题的一个直观的，高度灵活的，并且未被充分利用的方法是执行预测模拟。在频率分析中，这通常称为参数自举(parametric bootstrapping)，在贝叶斯的情况下称为后验预测模拟(posterior predictive simulation)。这两种方法的逻辑很简单。如果所选择的模型提供了对自然界的充分近似，在假设模型下模拟的数据应该“看起来”与经验数据非常相似。频率主义和贝叶斯方法的唯一区别在于，参数自举包括模拟来自树和模型参数的ML估计的许多数据集，而后验预测模拟从后验分布中绘制树和参数值用于模拟。

评估模型充分性的预测模拟成功的关键是量化数据集“外观”的方式。 存在几乎无限的潜在的测试统计数据用于评估“外观”，但是在系统发育的开发或测试中已经进行了相当少的工作。 这里有几个建议：

1. The multinomial likelihood (Goldman, 1993a; Huelsenbeck et al., 2001; Bollback, 2002)
2. Chi-squared statistic for homogeneity of nucleotide frequencies (Huelsenbeck et al., 2001)
3. Frequency of invariant sites (Goldman, 1993b)
4. Number of unique site patterns (Goldman, 1993b)
5. Number of “parallel” sites (Goldman, 1993b)

不幸的是，这些统计数据很少用于评估模型充分性的经验分析。如果原始研究的作者使用模型充分性的预测性评估，他们可能会谨慎对待其结果。最后，请记住，拒绝基于预测模拟的模型的合理性并不能保证系统发育估计是错误的。同样，不拒绝模型的合理性并不能保证系统发育估计是正确的。预测模拟只能直接告诉我们模型是否可以重述数据的某些特征。然而，如果两组研究（A和B）支持不同的树形拓扑结构，并且A组的分析一致地失败了模型似真性测试，而B组的研究没有，那么在A处理结果似乎比B更谨慎。





## Reference
1. BAYESIAN MODEL TESTING - Guy Baele, Rega Institute, Department of Microbiology and Immunology, K.U. Leuven, Belgium.
2. [什么是Bayesian Factor BF](http://bayesfactor.blogspot.ca/2014/02/the-bayesfactor-package-this-blog-is.html)
3. http://beast.community/model_selection_1
4. http://treethinkers.org/tutorials/model-selection/
