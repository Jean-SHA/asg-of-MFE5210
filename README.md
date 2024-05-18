# asg-of-MFE5210

Factor：momentum_5D & momentum_10D

-- Part1: what is Momentum？

股票价格的动量（Momentum）代表的是股价在一定时间内延续前期走势的现象。因子表达式：momentum=closet/closet-n-1

全球市场普遍存在动量效应。Jegadeesh和Titman(1993)最早提出动量这一概念，他们发现美国股市中，投资组合收益表现出中期价格动量效应(JT价格动量策略)。Moskowitz和Pedersen(2013)检验 动量在发达国家除股票外的市场上广泛存在，同时De等(2012)证实新兴市场同样存在显著动量效应。与海外长期的研究和经验相悖的是，在A股市场，反转因子（Reverse）要远强于动量因子，且短期反转因子表现得更显著（具体可见mom专题）。

-- Part2: construct the mom_factor

Assumptions：

· 回测区间：2022.1.1-2022.12.31，共计242个交易日

· 数据：A股主板股票数据，剔除st和过滤掉最近150天新上市的股票，累计732776条数据

· 回测平台：聚宽

· 不考虑交易费用


构建 get_momentum_factor(dates,observing)函数获取N日动量因子，此处N=5/10，通过聚宽下载对应数据保存为本地csv，随后读取为stock_data,org_ret_day为未进行行业中性化的每日收益率。N日收益率通过prod函数（每日收益率相乘）获得。函数返回值即为N日动量因子。
<img width="851" alt="image" src="https://github.com/Jean-SHA/asg-of-MFE5210/assets/128243716/a6fa3fe4-b2f0-431b-a787-cddc31ca89ed">
将对应的5日和10日动量因子保存为字典，keys为‘5D’、‘10D’，随后保存为csv/pkl形式

-- Part3: Factor Analysis
本文意图使用alphalens进行，但由于其公司倒闭停止维护alphalens，与numpy、pandas、scipy等库产生冲突，频繁报错，最后选择聚宽研究环境下进行因子分析，直接调用其中相关的因子分析函数。

参数设置：

·持仓周期5天

·分层quantiles=10

各因子分组IC Mean情况
 ------------------------------------------------------------ 
                  5D          10D
   period_5    0.013519    0.017627 
 ------------------------------------------------------------ 

ic图：

<img width="733" alt="截屏2024-05-18 下午3 41 06" src="https://github.com/Jean-SHA/asg-of-MFE5210/assets/128243716/ed9ac766-2341-4826-99ab-9716ab632fe4">

 查看因子报告：def factor_report(far):<img width="845" alt="截屏2024-05-18 下午3 44 35" src="https://github.com/Jean-SHA/asg-of-MFE5210/assets/128243716/70cc1486-5822-4b94-9f70-e5327a9c0012">

 查看持仓周期报告trans2period(fardic,period)
 
 <img width="519" alt="截屏2024-05-18 下午3 44 41" src="https://github.com/Jean-SHA/asg-of-MFE5210/assets/128243716/ec5a95d5-8c6d-4672-b1bc-120ea194d996">
 
最后发现5日动量因子夏普比率为5.37，低于10日动量因子的6.72<img width="511" alt="截屏2024-05-18 下午4 08 56" src="https://github.com/Jean-SHA/asg-of-MFE5210/assets/128243716/e2066134-1530-4be3-b58a-f60c2738f022">

关于5日动量因子：<img width="854" alt="截屏2024-05-18 下午4 10 56" src="https://github.com/Jean-SHA/asg-of-MFE5210/assets/128243716/b3fb1a5d-1d39-4c95-91b3-39a624005115">
<img width="865" alt="截屏2024-05-18 下午4 11 18" src="https://github.com/Jean-SHA/asg-of-MFE5210/assets/128243716/b8c15046-6e7f-4eba-a89d-3f84a05ef9b4">

关于10日动量因子：<img width="860" alt="截屏2024-05-18 下午4 11 11" src="https://github.com/Jean-SHA/asg-of-MFE5210/assets/128243716/312f9c6f-7bbb-4fd4-adf7-0289f1e127eb">
<img width="884" alt="截屏2024-05-18 下午4 11 25" src="https://github.com/Jean-SHA/asg-of-MFE5210/assets/128243716/ed07f3ea-8804-489d-9ce3-67452ea087ba">

动量因子的收益率图为
<img width="775" alt="截屏2024-05-18 下午4 11 59" src="https://github.com/Jean-SHA/asg-of-MFE5210/assets/128243716/e79b94e8-6d5b-4fee-93d2-545e67c7e703">



-- Part4：reference

1、光大证券-多因子系列报告之二十二：再论动量因子

2、Value and Momentum Everywhere

3、中国A股市场动量效应的特征和形成机理研究



