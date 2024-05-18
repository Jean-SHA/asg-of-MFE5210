# asg-of-MFE5210
factor A：momentum

Part1: what is Momentum？

股票价格的动量（Momentum）代表的是股价在一定时间内延续前期走势的现象。因子表达式：momentum=closet/closet-n-1

全球市场普遍存在动量效应。Jegadeesh和Titman(1993)最早提出动量这一概念，他们发现美国股市中，投资组合收益表现出中期价格动量效应(JT价格动量策略)。Moskowitz和Pedersen(2013)检验 动量在发达国家除股票外的市场上广泛存在，同时De等(2012)证实新兴市场同样存在显著动量效应。与海外长期的研究和经验相悖的是，在A股市场，反转因子（Reverse）要远强于动量因子，且短期反转因子表现得更显著（具体可见mom专题）。

Part2: construct the mom_factor

Assumptions：

· 回测区间：2022.1.1-2022.12.31，共计242个交易日

· 数据：A股主板股票数据，剔除st和过滤掉最近150天新上市的股票，累计732776条数据

· 回测平台：聚宽

· 不考虑交易费用

· 原始数据不进行行业中性化

构建 get_momentum_factor(dates,observing)函数获取N日动量因子，此处N=5，10，



Par4：reference

1、光大证券-多因子系列报告之二十二：再论动量因子

2、Value and Momentum Everywhere

3、中国A股市场动量效应的特征和形成机理研究
