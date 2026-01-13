---
title: "Python数据可视化实战"
collection: portfolio
type: "Data Analysis"
permalink: /portfolio/python-data-visualization-practice
date: 2025-01-13
excerpt: "使用Matplotlib和Seaborn进行数据可视化实战，掌握探索性数据分析与模型评估可视化方法"
header:
  teaser: /images/portfolio/python-data-visualization-practice/age_distribution.png
tags:
  - 数据可视化
  - Python
  - Matplotlib
  - Seaborn
  - 探索性数据分析
  - 模型评估
tech_stack:
  - name: Python
  - name: Matplotlib
  - name: Seaborn
  - name: Pandas
  - name: Scikit-learn
---

## 项目背景
本项目旨在通过Python的Matplotlib和Seaborn库进行数据可视化实战，掌握常用统计图表绘制方法，为探索性数据分析（EDA）和模型评估选择合适的可视化图形，并练习编写可复用的绘图函数以提升代码效率。

## 核心实现
### 1.探索性数据分析（EDA）可视化<br><br>

**年龄分布直方图** <span style="font-size: 0.8em; color: #ffffff; background-color: #333333; padding: 2px 6px; border-radius: 4px;">使用 Seaborn 绘制年龄分布直方图，同时显示核密度估计曲线以观察分布趋势</span>

plt.figure(figsize=(8, 5))

sns.histplot(data=picu_data, x='age_month', kde=True)

plt.title("年龄分布直方图")

plt.show()

![年龄分布直方图](/images/portfolio/python-data-visualization-practice/年龄分布直方图.png)
---

**不同结局下实验室指标分布箱线图** <span style="font-size: 0.8em; color: #ffffff; background-color: #333333; padding: 2px 6px; border-radius: 4px;">创建 3x2 子图网格，绘制各实验室指标按患者结局分组的箱线图：</span>

colname = ['age_month', 'lab_5237_min', 'lab_5227_min', 'lab_5225_range', 'lab_5235_max', 'lab_5257_min']

fig, axs = plt.subplots(3, 2, constrained_layout=True, figsize=(10, 10))

for i in range(len(colname)):
    sns.boxplot(data=picu_data, x='HOSPITAL_EXPIRE_FLAG', y=colname[i], ax=axs[i//2, i%2])
    
plt.suptitle("不同结局下各实验室指标分布", fontsize=16)

plt.show()

![不同结局下各实验室指标分布](/images/portfolio/python-data-visualization-practice/不同结局下各实验室指标分布.png)
---

### 2.模型评估结果<br><br>

**混淆矩阵热力图** <span style="font-size: 0.8em; color: #ffffff; background-color: #333333; padding: 2px 6px; border-radius: 4px;">定义混淆矩阵绘制函数，用于评估分类模型性能：</span>

  def confusion_matrix_plot(y_true, y_pred_prob, threshold=0.5, title='混淆矩阵'): <br><br>
    y_pred = (y_pred_prob > threshold).astype(int)<br><br>
    cm = confusion_matrix(y_true, y_pred)<br><br>
    fig, ax = plt.subplots(figsize=(5, 4))<br><br>
    sns.heatmap(cm, annot=True, fmt='d', cmap='Blues', ax=ax)<br><br>
    ax.set_xlabel('预测标签')<br><br>
    ax.set_ylabel('真实标签')<br><br>
    ax.set_title(title)<br><br>
    ax.xaxis.set_ticklabels(['存活(0)', '死亡(1)'])<br><br>
    ax.yaxis.set_ticklabels(['存活(0)', '死亡(1)'])<br><br>
    plt.show()<br><br>

### **调用函数（基于逻辑回归模型结果）**

confusion_matrix_plot(y_true=y_test, y_pred_prob=y_pred_prob, threshold=0.5)

![混淆矩阵热力图](/images/portfolio/python-data-visualization-practice/混淆矩阵热力图.png)
