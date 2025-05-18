# Implementing a dual-factor model for stock selection based on PCA algorithm
## Introduction
Constructing a dual-factor quantitative pricing model based on PCA-derived market and style factors, employing residual momentum and style trend strategies for stock selection.

## Main Libraries
numpy, pandas, sklearn, and matplotlib  

## File Usage Instructions
### Market factor
1. Principal Component Analysis (PCA) was applied to reduce the dimensionality of multi-asset return data and extract key market factors  
2. A correlation matrix was computed between the PCA components of different assets to analyze their interrelationships  
3. The results were saved in the file 'market_factor_1.csv'(PCA1)
### Style factor
1. Principal Component Analysis (PCA) was applied to reduce the dimensionality of multi-asset return data and extract key style factors  
2. A correlation matrix was computed between the PCA components of different assets to analyze their interrelationships  
3. The results were saved in the file 'style_factor_1.csv'(PCA2-3)  
### Dual-Factor Rolling Strategy
1. Factor-driven approach:  
   Extract market/style factors through PCA and regression as signal foundation  
2. Market factor & Style factor:   
   Generate factors monthly using make_market_factor_time and make_style_factor_time
3. Dual signals:  
   1. Residual momentum: Reflects mean-reversion effect of short-term pricing errors. For each industry indicator, fit linear regression with market/style factors: Generate long/short signals by ranking residual sums (top 10 vs bottom 10)   
   2. Style trend: Captures persistence of medium-long term style factors. Apply HP filter (λ=1600) to style factor to separate trend component. Ranking: Generate long/short signals by ranking trend signals  
4. Trading strategy implementation:  
   Strategy 1: Equal-weighted benchmark  
   Strategy 2: Residual momentum long-short portfolio   
   Strategy 3: Style trend long-short portfolio  
   Strategies 4-5: Dynamic weight adjustment  
      1. For top 22 assets by signal ranking: increase weight to 3x baseline  
      2. For bottom 22 assets: reduce weight to 1/3x baseline  
5. Visualization:  
Plot performance comparison charts of benchmark, residual momentum, and style trend strategies
### Dataset
Dataset name translation:  
Bonds (for PCA): 债券1forPCA  
Nanhua Commodity Index  Domestic Equities - Stock Composite Index: 南华商品指数  
Domestic Equities - Stock Composite Index: 国内权益-股票综合指数   
Equities - Stocks: 权益-股票     

## Formulas
### 1. Linear Regression Model  
y = β₀ + β₁·market_factor + β₂·style_factor  
### 2. Residual Momentum Signal  
Residual Signal = Σ(yₜ - ŷₜ) [t=108→119]  
### 3. Style Trend Signal  
Trend Signal = β₂·HP_trend[t=119]  
### 4. Dynamic Weight Portfolio Return
r_portfolio = (Σwᵢ·rᵢ)/quantity,  wᵢ∈{1/3,1,3}  

## Continuously updating, welcome to star and discuss  


#  基于PCA算法实现双因子模型选股  
## 简介
构建基于PCA的市场因子和风格因子的双因子量化定价模型，采取残差动量和风格趋势的选股策略

## 主要库
numpy, pandas, sklearn and matplotlib  

## 文件使用说明
### Market factor
1. 对多资产收益率数据进行主成分分析(PCA)降维，提取关键市场因子  
2. 计算不同资产PCA主成分间的相关系数矩阵，分析其关联性  
3. 结果保存在文件'market_factor_1.csv'中（第一主成分PCA1）
### Style factor
1. 对多资产收益率数据进行主成分分析(PCA)降维，提取关键风格因子  
2. 计算不同资产PCA主成分间的相关系数矩阵，分析其关联性    
3. 结果保存在文件'style_factor_1.csv'中（第一主成分PCA2-3）  
### Dual-factor rolling strategy
1. 因子驱动：  
   通过PCA和回归提取市场/风格因子，作为信号基础  
2. 市场因子 & 风格因子：  
   逐月调用make_market_factor_time和make_style_factor_time生成因子
3. 双重信号：
   残差动量：反映短期定价误差的均值回归效应。对每个行业指标，用市场因子和风格因子拟合线性回归：按残差和降序排名，生成做多/做空信号（前10名 vs 后10名）   
   风格趋势：捕捉中长期风格因子的持续性。对风格因子应用HP滤波（lamb=1600）分离趋势项（trend)排序：按趋势信号降序排名，生成做多/做空信号  
4. 交易策略实现：  
   策略1：等权重基准  
   策略2：残差动量多空组合   
   策略3：风格趋势多空组合  
   策略4-5：动态权重调整  
      1.对信号排名前22的资产，权重提升至3倍基准权重  
      2.对后22的资产，权重降至1/3倍  
5. 可视化：  
绘制基准、残差动量、风格趋势策略的收益对比图
### Dataset
翻译：  
债券1forPCA: Bonds (for PCA)  
南华商品指数: Nanhua Commodity Index  Domestic Equities - Stock Composite Index     
国内权益-股票综合指数: Domestic Equities - Stock Composite Index     
权益-股票: Equities - Stocks  

## 公式
### 1. 线性回归模型  
y = β₀ + β₁·market_factor + β₂·style_factor  
### 2. 残差动量信号  
残差信号 = Σ(yₜ - ŷₜ) [t=108→119]  
### 3. 风格趋势信号  
趋势信号 = β₂·HP_trend[t=119]  
### 4. 动态权重组合收益
r_portfolio = (Σwᵢ·rᵢ)/quantity,  wᵢ∈{1/3,1,3}  

## 持续更新中，欢迎收藏讨论
