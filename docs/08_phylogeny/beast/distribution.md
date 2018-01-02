# Distribution

在 Beast 设置参数时，特别是各个 priors 的设置，经常不是用固定的某个值，而是用这个 priors 的先验概率分布。常见的分布有：

1. Normal
2. LogNormal
3. Beta
4. Uniform
5. Exponential
6. Laplace
7. Gamma
8. Inverse Gamma


## Normal Distribution

正态分布(高斯分布): N(μ, σ^2)

概率密度函数为正态分布的期望值μ决定了其位置，其标准差σ决定了分布的幅度。当μ = 0,σ = 1时的正态分布是标准正态分布。


## LogNormal Distribution


## Beta Distribution


## Uniform Distribution


## Exponential Distribution


## Laplace Distribution

## Gamma Distribution

Gamma 分布是一种连续的概率分布，在许多系统发育程序中受欢迎。 Gamma 分布流行的部分原因是在于它有一个形状移位器，可以从 exponential 到 normal 假设一系列的形状分布。 Gamma 分布具有两个参数这一事实导致了这种灵活性。 在大多数系统发育应用中，这些参数被称为形状参数 alpha 和速率参数 beta（注意速率参数 beta，参数的一些应用被 “scale参数” 替代，scale 实际上只是速率参数的倒数）。

您可以使用以下R脚本探索这两个参数对gamma分布的影响（请注意，此脚本着重绘制SIMMAP 1.5程序中gamma分布的默认参数设置的侧面值）：

```R
# Generate a plot of gamma distributions that vary the shape parameter (alpha).
> x <- seq(0, 100, length=200)
# Make probability density function for SIMMAP default gamma distribution
> simmapDefaultGamma <- dgamma(x, shape=1.25, scale=1/0.25)  
> plot(x, simmapDefaultGamma, type="l", yaxs="i", xaxs="i", ylim=c(0,0.16), xlim=c(0,100), xlab="x value", ylab="Density", main="Probability density for gamma distribution with variable alpha and beta=0.25", lwd=0)
> colors <- c("red", "black", "blue", "darkgreen", "purple", "orange")
> alphas <- c(0.1, 1.25, 2, 4, 8, 10)
> labels <- c("alpha=0.1", "alpha=1.25 (SIMMAP default)", "alpha=2", "alpha=4", "alpha=8", "alpha=10")
> for(i in 1:length(alphas)) {
    hx <- dgamma(x, shape=alphas[i], rate=1, scale=1/0.25)
    lines(x, hx, lwd=3, col=colors[i])
}
legend("topright", inset=.05, title="Probability densities",
labels, lwd=3, col=colors)
```



对于 gamma 分布的许多系统发育应用（例如，为了适应跨站点替代率的变化（ASRV）），alpha和beta参数被限制为相等的。 因为 gamma 分布的均值是 alpha/beta，所以这个约束确保了 gamma 分布的均值为1。 当 gamma 分布用作ASRV上的先验概率密度时，这是重要的，因为它保留将分支长度解释为每个位点的预期（平均）替换数量的能力。



## Inverse Gamma Distribution





## Reference

1. [The Gamma Distribution](http://en.wikipedia.org/wiki/Gamma_distribution)
2. [treethinkers Gamma Distribution](http://treethinkers.org/tutorials/the-gamma-distribution/)
