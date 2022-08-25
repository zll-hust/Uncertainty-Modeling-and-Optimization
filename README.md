# Uncertainty Modeling and Optimization

## Before Reading

This is my note (in Chinese) for Robust Optimization, including a brief introduction to Stochastic Programming and Chance-Constraint Programming. The notes include two parts. Part 1 is the introduction of some basic theories of RO, including classical (static) RO, Adaptive RO, Distributionally RO, ADRO, and some preliminary knowledge, such as Lagrange dual, conic programming. Part 2 introduces some applications of RO in different OR scenarios. 

In these notes, I try to derive the results of the theorems step by step. However, since I'm not good at mathematics, the derivation may not strict enough. Luckily, my object is to apply the modeling methods to some OR problems, so a quick understanding may also be useful for beginners like me. Remarkably, I didn't learn any course about convex optimization, although it plays an important role in RO. So, I think these notes will be helpful, especially for undergraduates majoring in management or engineering but not mathematics.

Besides, although my notes are not good enough, the references are strongly recommended.

The notes are also updated in my blog in CSDN([Part 1](https://blog.csdn.net/zll_hust/article/details/123988838?spm=1001.2014.3001.5501), [Part 2](https://blog.csdn.net/zll_hust/article/details/124230862?spm=1001.2014.3001.5501)) and my WeChat Official Account.

The notes will be continuously supplemented if I have any leisure. Here is the Chinese preface.

## 前言

已经很久没有写过类似学科知识分享的内容了。之前提到过多次，最近一段时间在学习不确定性问题的处理。虽然学习很不连贯，导致效率一直不高，但也算读过/看过一些资料，对这方面有了大概的了解。感觉自己自主推倒/复习不够，根基很浅，为了巩固学过的一些知识，决定做一点小笔记，在做的过程中复习学过的内容，也顺带与大家分享。

“不确定性优化”这个词应该是没有的。我这样叫，是因为我打算介绍的内容基本上用于处理不确定性问题。这个范围是很广的，因为优化本身是很广的概念，我也不能够、不打算做/学/写这么多内容。所以我改成了“建模与优化”，旨在介绍以优化应用为目的的建模方法，以及一些基本的处理方法。

无需多说，在现实生活中，很多东西都是不确定的。客户的需求，行驶的时间，投资收益率。我们通常用参数的期望来估计其真实值，这在很多情况下会对结果造成巨大的影响。轻则使得目标函数变差，比如错误估计了开会迟到扣工资，重则使得解不可行，比如错过了整个会议，领导让你走人。因此，如何更精确地处理不确定性问题，是很重要的。

简单来说，不确定性的建模方法主要是随机规划(stochastic programming/optimization, 简称SO)，鲁棒优化(robust optimization, 简称RO)和机会约束(chance-constraints programming, 简称CCP)。SO和CPP是传统的处理方法，已经有很多很多年的研究。他们主要基于已知分布的随机变量，这在现实中往往是很难得到的。此外，SO比较多的使用期望这一概念，因此结果往往是平均情况下的，不能反应极端情况的结果。RO主要是这个世纪发展的一门技术，无需多说，近几年在优化领域，无论是OR还是ML都产生了很大的影响。他的目的是为了放松“已知概率分布”的条件，并得到一个鲁棒性够强的解，而不是平均意义上的解。当然，对应的问题就是，由于解需要在任何情况下都可行，所以解的质量可能在大多数情况下不够好，也就是过于conservative(保守)。深究下去，SO也有Apriori paradigm和reoptimization，RO也有classical RO，Distributionally RO，Adaptive/Adjustable RO，ADRO等多种框架。不同的建模范式各有特点。

虽然叫不确定性，但我暂时比较想写/学的内容还是RO相关的，因为SO目前的知识已经够我用了，CCP则暂时不想研究。因此，我只会花一点内容简单介绍SO和CCP，留坑以后再填。因为未来不一定更新，所以暂时决定在近几天边学边写，多写一点内容。

回到作者本身，我是管理学出身，本科没有凸优化、随机过程等课程，只学过皮毛的线性规划，数学基础很差。但是，RO本身是一门很严谨的内容，因为他在一定程度上挑战了一般的线性规划框架，并且涉及概率论，推导的过程自然需要很严谨。学RO的目的如果真的想推导公式，那是比较难的。好在，作者是做algorithm的，我们的目的是应用。所以，我的内容也会很不严谨，以理解为目的，并添加一些应用的内容，比如RO在facility location，portfolio，vehicle-routing等方面的应用，作为学习的实例。不过对应的，作者基础差的好处就是，介绍到内容可能会详细一些。在文章中，对我自己也不确定的内容，我会尽量用<>标出，或者用文字说明。此外，我也会尽量详细地列出知识的来源，因为在我的学习过程中，很多文献/课程/资料都起到很大的作用。有什么问题也希望大家指出。

大家一起学习，一起进步！

## About Me

Hang Zhou, an undergraduate student of Huazhong University of Science & Technology, major in Management Science. Now I'm working for certainty/uncertainty operations research algorithm design.
