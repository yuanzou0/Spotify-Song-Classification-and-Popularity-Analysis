# Spotify Song Classification and Popularity Analysis

## 项目概述 (Project Overview)
本项目旨在探索和分析 Spotify 平台上歌曲的各项音频特征（如能量、响度、时长、调性等）与其受欢迎程度（Popularity）、流派（Genre）以及其他属性之间的关系。通过统计测试、回归分析和主成分分析（PCA）等机器学习方法，本项目深入挖掘了影响歌曲流行度的潜在因素。

**作者**: Yuanzou Gao

## 数据预处理 (Data Preprocessing)
在进行核心分析之前，对数据进行了以下清理和预处理：
- 将歌曲时长（duration）的单位从毫秒（ms）转换为秒（s）。
- 检查并处理缺失值（使用 `dropna` 确保数据完整性）。
- 对数值型变量（如 `popularity`, `duration`, `loudness`, `tempo`）进行标准化处理，以消除量纲差异带来的影响。

## 核心分析与发现 (Key Analyses & Findings)

本项目主要回答了以下10个问题以及一个附加问题：

1. **特征分布的偏态性 (Feature Distribution)**
   - **发现**: 通过直方图和 Kolmogorov-Smirnov 检验发现，所有分析的特征（如能量、响度、原声度等）均不服从正态分布。
2. **歌曲时长与流行度的关系 (Duration vs. Popularity)**
   - **发现**: 歌曲时长与流行度之间几乎没有线性关系（皮尔逊相关系数为 -0.055）。
3. **显式内容（Explicit）与流行度的关系**
   - **发现**: 使用 Mann-Whitney U 检验表明，带有显式内容标签的歌曲在统计学上比非显式歌曲更受欢迎。
4. **大调与小调（Major vs. Minor）对流行度的影响**
   - **发现**: 大调歌曲和小调歌曲在流行度上没有显著差异。
5. **能量与响度的相关性 (Energy vs. Loudness)**
   - **发现**: 两者之间存在强正相关（皮尔逊相关系数 0.775），即响度越大的歌曲通常能量也越高。
6. **流行度的最佳单一预测指标**
   - **发现**: 在所有特征中，器乐度（Instrumentalness）是流行度的最佳预测指标，呈负相关（系数 -0.4457）。但其解释力依然很弱（$R^2 = 0.0210$）。
7. **多变量回归预测流行度**
   - **发现**: 结合所有特征构建的回归模型在测试集上的 $R^2$ 仅为 0.0517，说明音频特征只能解释一小部分流行度的变异，预测流行度是一个复杂的任务。
8. **主成分分析 (PCA)**
   - **发现**: 根据 Kaiser 准则，保留了3个主要成分，这3个成分能够概括数据集中的大部分信息。
9. **使用效价（Valence）预测调性模式（Mode）**
   - **发现**: 逻辑回归模型显示，随着效价（Valence，即音乐的积极程度）的增加，歌曲为大调的概率也随之增加。
10. **预测“古典”流派 (Predicting Classical Genre)**
    - **发现**: 比较了使用“时长”和“主成分”预测古典音乐的逻辑回归模型。虽然两个模型表现都不尽如人意，但基于 PCA 的模型在识别古典音乐方面相对更好。

**附加发现 (Extra Credit)**:
- **调性与流派的关系**: 不同的音乐流派对特定的调性有明显的偏好。例如，Disney 音乐偏好 Key 0，而 Grindcore 强烈偏好 Key 2。

## 仓库文件说明 (Repository Structure)
- `Capstone.ipynb`: 包含主要数据清理、可视化和机器学习模型构建的 Jupyter Notebook。
- `classification.ipynb`: 包含分类模型相关分析的 Jupyter Notebook。
- `Report.pdf`: 详细的项目分析报告，包含所有问题的图表、统计输出和详细解释。
- `musicData.csv` / `spotify52kData.csv`: 项目使用的数据集文件。

## 使用的工具与库 (Tools & Libraries)
- Python
- Pandas, NumPy (数据处理)
- Matplotlib, Seaborn (数据可视化)
- SciPy (统计检验)
- Scikit-learn (机器学习与 PCA)
