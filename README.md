# 我要炒美股
对2020-2024年美股数据的分析<br>

<strong> 数据集来源 </strong>
<a href="https://www.kaggle.com/datasets/dhavalpatel555/us-stock-market-2020-to-2024/" title="kaggle数据">Kaggle</a>
kaggle：<br>


<strong> 数据预处理 </strong><br>

<strong> 数据相关性分析 </strong><br>

<strong> 几种机器学习模型的拟合尝试 </strong><br>

<strong> 分别使用arima模型和多元线性回归模型对未来股价进行预测 </strong><br>

<strong> 结合机器学习模型对多元线性回归进行改进，R2提升近20% </strong><br>


# 数据预处理
1. 数据预览
2. 数据格式统一
3. 数据缺失值的填补

# 数据相关性分析
1. 绘制直方图观察数据分布情况
2. 绘制时序数据图并添加布林线和移动平均线来确定波动性
3. 绘制相关性热力图
4. 对相关性大的数据进行格兰杰因果检验
5. 对数据进行因子分析
6. 特征工程

# 机器学习模型拟合
## xgboost
XGBoost（eXtreme Gradient Boosting）是一个高效的、灵活的、可移植的机器学习库，专门针对提升树（boosted trees）算法进行了优化。它在Gradient Boosting框架的基础上进行了改进，旨在提高模型的性能和速度。XGBoost在众多机器学习竞赛中展现了其强大的性能，包括Kaggle竞赛中的多个冠军解决方案。<br>
![image](https://github.com/baibairui/stock_pridict/assets/123094711/bfda4f2a-0e35-4694-9038-35d4a697c851)

**核心特性**

XGBoost拥有一系列引人注目的特性，主要包括：

- **高效实现**：支持多种语言（包括Python、R、Java等），并且能够在单机、Hadoop、Spark、Flink等多种分布式环境中运行。
- **灵活性**：支持回归、分类、排名等多种机器学习任务。
- **可扩展性**：通过近似算法（如分位数倾斜）有效处理大规模数据集。
- **剪枝**：提供深度优先和宽度优先的剪枝策略，从而避免过拟合。
- **正则化**：内置L1和L2正则化项，有助于减少模型的复杂性和提高模型的泛化能力。
- **缺失值处理**：自动处理缺失值。

**使用场景**

XGBoost可以应用于广泛的机器学习任务中，包括但不限于：

- **分类问题**：二分类、多分类问题
- **回归问题**：预测连续值
- **排序问题**：如搜索排序
- **时间序列预测**

## lstm
长短期记忆网络（Long Short-Term Memory, LSTM）是一种特殊类型的循环神经网络（RNN），能够学习长期依赖关系。LSTM由Hochreiter & Schmidhuber（1997）引入，旨在解决传统RNN在处理长序列数据时遇到的梯度消失和梯度爆炸问题。LSTM在多个领域，包括自然语言处理、语音识别和时序数据分析等，都有广泛应用。
![image](https://github.com/baibairui/stock_pridict/assets/123094711/40d8e14b-8769-42b7-a1e3-4ec91784b673)

**核心特性**

LSTM的关键在于其内部结构，尤其是“门”（gate）机制，包括：

- **遗忘门**：决定哪些信息需要被遗忘或丢弃。
- **输入门**：决定哪些新信息被存储在细胞状态中。
- **输出门**：决定下一个隐藏状态和当前细胞状态的关系，这影响了网络下一步的输出。

这些门的结构使LSTM能够有效地添加或移除信息，解决了长期依赖的问题。

**使用场景**

LSTM适用于各种涉及序列数据的任务，例如：

- **自然语言处理**（NLP）：包括文本生成、机器翻译、情感分析等。
- **语音识别**：将语音转换为文本。
- **时间序列预测**：如股票价格预测、天气预测等。

## knn
K最近邻（K-Nearest Neighbors, KNN）是一种基本且广泛使用的监督学习算法，用于分类和回归。其工作原理极其简单：对于一个待预测的数据点，算法会在训练集中找到与之最近的K个邻居，然后根据这些邻居的信息来预测该数据点的标签。

**核心思想**

KNN算法的核心思想可以概括为“物以类聚，人以群分”。其判断依据基于邻居的多数投票（对于分类问题）或平均（对于回归问题）。<br>
![image](https://github.com/baibairui/stock_pridict/assets/123094711/0ac9eeb8-a32d-4c94-871a-ec8ee39fe283)

**关键特性**

- **非参数学习**：KNN是一种非参数学习算法，不假设数据的分布，可以捕捉到数据的复杂关系。
- **简单但有效**：尽管算法结构简单，但在很多情况下仍然非常有效。
- **惰性学习**：KNN属于惰性学习算法，因为它实际上不从训练数据中学习一个判别函数，而是把数据库直接用于预测分类。

**应用场景**

KNN算法可以应用于多种场景，包括但不限于：

- **分类任务**：如文本分类、客户分群等。
- **回归任务**：如房价预测、股票价格等。
- **推荐系统**：根据用户的“邻居”（相似的用户）的喜好来推荐商品。

**算法步骤**

1. **确定K值**：选择一个适当的K值。
2. **计算距离**：计算未知数据点与所有已知数据点的距离。
3. **找到最近的K个邻居**：选择距离最近的K个点。
4. **投票或平均**：对于分类问题，根据最近邻居的多数类别来分类；对于回归问题，取最近邻居的输出变量的平均值作为预测值。

## cnn
卷积神经网络（Convolutional Neural Networks, CNN）是一种在计算机视觉任务中广泛使用的深度学习架构。CNN通过模拟人类视觉系统的机制，能够有效地识别图像中的模式和特征，如边缘、颜色和纹理等。CNN的强大能力使其在图像分类、对象检测、面部识别和许多其他领域都有广泛应用。<br>

![image](https://github.com/baibairui/stock_pridict/assets/123094711/edcb5d01-84de-4a40-ab32-e602b29885c2)

**核心组件**

CNN主要由以下几种类型的层构成：

- **卷积层（Convolutional Layer）**：通过卷积操作提取输入图像的特征。
- **激活层（Activation Layer）**：通常使用ReLU激活函数增加网络的非线性。
- **池化层（Pooling Layer）**：降低特征图的空间尺寸，减少计算量并提取重要特征。
- **全连接层（Fully Connected Layer）**：将学到的“高级”特征表示映射到样本的类别。

**工作原理**

1. **特征提取**：通过卷积层和池化层自动学习输入图像的特征表示。
2. **分类**：使用一个或多个全连接层对提取的特征进行分类。

**应用场景**

CNN在多个领域都有出色的表现，包括但不限于：

- **图像分类**：识别图像中的对象。
- **对象检测**：在图像中识别对象的位置和类别。
- **图像分割**：将图像分割成多个区域，用于进一步分析。
- **面部识别**：识别或验证个人的身份。

## Rnn
循环神经网络（Recurrent Neural Networks, RNN）是一类用于处理序列数据的深度学习模型。RNN能够处理不同长度的输入序列，并在内部维持一个状态（隐藏状态），该状态能够捕捉到目前为止观察到的序列的信息。RNN特别适合于时间序列数据、自然语言文本、语音等序列化信息的任务。<br>
![image](https://github.com/baibairui/stock_pridict/assets/123094711/7139af85-4605-43b4-b0c6-ad1b224f49a7)

**核心概念**

- **隐藏状态**：RNN的核心，它保存了过去时间点的信息。
- **时间步长**：序列中的每个元素被模型逐一处理的过程。
- **参数共享**：在处理序列的每个时间步时，RNN使用相同的权重，这有助于模型泛化。

**工作原理**

在每个时间步，RNN接收两个输入：当前时间步的输入数据和上一个时间步的隐藏状态。模型将这两个输入结合起来更新其隐藏状态，并可能生成一个输出。更新隐藏状态的过程会在序列的每个时间步重复进行，使得模型能够“记住”和综合过去的信息。

**应用场景**

RNN在许多涉及序列数据的任务中表现出色，包括：

- **自然语言处理**（NLP）：如文本分类、机器翻译、情感分析等。
- **时间序列预测**：如股票价格预测、天气预测等。
- **语音识别**：将语音信号转换为文本。

**RNN的变体**

尽管标准RNN在处理序列数据方面具有潜力，但它们经常遇到梯度消失或爆炸的问题，这限制了它们学习长距离依赖的能力。因此，开发了几种RNN的变体，如：

- **长短期记忆网络**（LSTM）：通过引入三种门控机制来解决梯度消失问题。
- **门控循环单元**（GRU）：比LSTM简单，但同样有效地解决了长距离依赖问题。

## 拟合效果比较

# 对未来数据进行预测
## 自回归积分滑动平均模型（ARIMA）介绍

自回归积分滑动平均模型（Autoregressive Integrated Moving Average, ARIMA）是时间序列分析中广泛使用的一种模型。它结合了自回归（AR）、差分（I）和滑动平均（MA）三个部分，旨在模拟时间序列数据中的一系列不同组件，如趋势、季节性等。<br>
ARIMA模型提供了另一种时间序列预测的方法。指数平滑模型（exponential smoothing）和ARIMA模型是应用最为广泛的两种时间序列预测方法，基于对这两种预测方法的拓展,很多其他的预测方法得以诞生。与指数平滑模型针对于数据中的趋势（trend）和季节性（seasonality）不同，ARIMA模型旨在描绘数据的自回归性（autocorrelations）。<br>
![image](https://github.com/baibairui/stock_pridict/assets/123094711/3c18fb45-d8b5-4c6a-add5-6949e681f6fb)


### ARIMA模型的三个组成部分

- **自回归（AR）**：`p` 部分表示模型中使用的时序数据的滞后数（lags），即过去值的数量。它捕捉了序列中的自回归特性。
- **差分（I）**：`d` 部分代表使序列平稳所需的差分次数，即连续计算前后数据点之间差异的次数。差分帮助去除数据中的趋势和季节性成分。
- **滑动平均（MA）**：`q` 部分是模型中使用的滑动平均项数，它捕捉了误差项的滑动平均特性。

### 模型表示

ARIMA模型通常表示为 ARIMA(p, d, q)，其中：
- `p` 是自回归项的阶数。
- `d` 是差分的阶数。
- `q` 是滑动平均项的阶数。

  其中的差分阶数通常需要通过ADF检验来确定，选择能使时间序列平稳的差分次数<br>
  ![image](https://github.com/baibairui/stock_pridict/assets/123094711/c1c43a66-0c3d-4aa4-add5-e9bdda928eb1)
![image](https://github.com/baibairui/stock_pridict/assets/123094711/0b17557b-4890-4201-92a8-a9dc60d0f23b)


### 工作原理

ARIMA模型通过结合自回归特性、差分以去除数据中的非平稳趋势和季节性成分、以及滑动平均来捕捉时间序列的未来点。模型首先对序列进行必要的差分，使其平稳，然后利用自回归和滑动平均模型来预测未来值。

### 应用场景

ARIMA模型在金融、经济、销售等领域的时间序列数据分析中有广泛应用，特别适用于：

- 销售预测
- 股票价格分析
- 经济指标预测
- 能源消耗预测


## 多元线性回归

### 多元线性回归介绍

多元线性回归（Multiple Linear Regression, MLR）是统计学中的一种线性回归模型，它用来估计两个或多个自变量（解释变量）与一个因变量（响应变量）之间的关系。与简单线性回归不同的是，多元线性回归分析允许你探索多个自变量对因变量的影响。<br>

![image](https://github.com/baibairui/stock_pridict/assets/123094711/8f088e3a-8141-4736-bb85-b1bc99102904)

### 模型定义

多元线性回归模型可以表示为：

![image](https://github.com/baibairui/stock_pridict/assets/123094711/3dfd1374-c090-47f9-af94-9d4a03d80432)


其中：

- \( Y \) 是因变量（目标变量）。
- \( X_1, X_2, \ldots, X_n \) 是自变量（特征变量）。
- \( \beta_0 \) 是截距项，也称为常数项。
- \( \beta_1, \beta_2, \ldots, \beta_n \) 是每个自变量的系数，表示自变量对因变量的影响强度。
- \( \epsilon \) 是误差项，表示模型无法解释的随机变异。

### 应用场景

多元线性回归广泛应用于经济学、社会科学、生物统计和工程等领域，用于：

- 预测分析：例如，预测房价、销售额、股票价格等。
- 风险评估：例如，在金融领域评估信贷风险。
- 优化策略：通过理解不同因素对结果的影响，帮助企业或个人做出更好的决策。

### 假设

多元线性回归分析基于以下几个假设：
- 线性关系：自变量和因变量之间存在线性关系。
- 无多重共线性：模型中的自变量之间应相互独立。
- 同方差性：对于所有的观测值，残差的方差应相同。
- 正态分布的残差：残差（误差项）应呈正态分布。

# 对预测模型进行改进
1. 将Rnn和XGboost作为基层，多元线性回归模型作为元层，使用stack堆叠模型对基本的多元线性回归模型进行改进
2. 将改进前后的效果进行对比
   
