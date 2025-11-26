近些年来关于不确定性量化的相关研究
====

一、不确定性的表征
----

二、不确定性量化方法
----
### 2.1贝叶斯与采样方法<br>
### 2.1.1开山之作 Dropout as a Bayesian Approximation: Representing Model Uncertainty in Deep Learning<br>
 &nbsp;&nbsp;&nbsp; [Dropout as a Bayesian Approximation: Representing Model Uncertainty in Deep Learning](https://arxiv.org/abs/1506.02142)<br>
&nbsp;&nbsp;&nbsp;这篇文章建立了MC Dropout方法与传统贝叶斯神经网络的关系，他在理论上面证明了MC Dropout方法随机高斯过程等效，进而证明了其与贝叶斯神经网络相同，将MC Dropout方法与不确定性量化建立了联系。

### 2.1.2关于Dropout方法的拓展<br>
 &nbsp;&nbsp;&nbsp; 1、[Rate-In: Information-Driven Adaptive Dropout Rates for Improved Inference-Time Uncertainty Estimation](https://arxiv.org/abs/2412.07169)<br>
&nbsp;&nbsp;&nbsp;这篇文章提出了一种名为 Rate-In 的新方法，在推理阶段根据每层特征图的信息损失动态调整 dropout 率，从而提升神经网络的不确定性估计能力，尤其适用于医学图像等高风险场景。<br>
<br>

 &nbsp;&nbsp;&nbsp; 2、[Enabling Uncertainty Estimation in Iterative Neural Networks](https://arxiv.org/pdf/2403.16732)<br>
&nbsp;&nbsp;&nbsp;这篇文章提出了一种无需修改网络结构、也无需多次训练模型的新方法，用来估计迭代神经网络的预测不确定性。核心思想是：模型在推理时的收敛速度越快，预测越可靠；收敛越慢，不确定性越高。通过计算多次迭代输出的方差来衡量不确定性，该方法在道路检测和气动力预测等任务上表现优于深度集成和MC Dropout，且计算成本更低。<br>
<br>

 &nbsp;&nbsp;&nbsp; 3、[Make Me a BNN: A Simple Strategy for Estimating Bayesian Uncertainty from Pre-trained Models](https://arxiv.org/abs/2312.15297)<br>
&nbsp;&nbsp;&nbsp;这篇文章提出了一种名为 ABNN（Adaptable Bayesian Neural Network） 的高效方法，可在不重新训练整个网络的前提下，将预训练的确定性 DNN 转化为具备不确定性估计能力的贝叶斯网络。其核心策略是仅在归一化层引入高斯扰动并进行轻量级微调，即可实现媲美深度集成的预测性能和不确定性估计效果，且计算成本与训练时间远低于传统 BNN 和集成方法。<br>
<br>

 &nbsp;&nbsp;&nbsp; 4、[Training-Free Uncertainty Estimation for Dense Regression: Sensitivity as a Surrogate](https://arxiv.org/abs/1910.04858v3)<br>
&nbsp;&nbsp;&nbsp;这篇论文提出了一种无需重新训练或修改模型结构的训练无关（training-free）不确定性估计方法，用于密集回归任务（如超分辨率、深度估计）。其核心思想是：在推理阶段对输入或中间特征施加轻微扰动（如旋转、噪声、dropout），通过观察输出方差来估计不确定性。论文从理论上证明了模型对扰动的敏感度与预测不确定性之间存在正相关关系，并提出了三种简单有效的方法：infer-transformation、infer-noise 和 infer-dropout。实验表明，这些方法在多个任务上与甚至优于需要训练的主流方法（如MC Dropout、深度集成）相当，且计算开销极低，适用于黑盒或灰盒模型。<br>
<br>

 &nbsp;&nbsp;&nbsp; 5、[Dropout Sampling for Robust Object Detection in Open-Set Conditions](https://arxiv.org/abs/1710.06677)<br>
&nbsp;&nbsp;&nbsp;这篇论文首次将 Dropout Sampling（Dropout 变分推断） 引入目标检测任务，用于在开放集（open-set）条件下提升检测鲁棒性。作者通过在推理阶段保持 Dropout 开启，进行多次前向采样，估计每个检测结果的标签不确定性（label uncertainty），并利用熵阈值过滤掉对未知类别的高不确定性检测，从而减少误检。实验表明，该方法在合成数据集和真实机器人数据集上均显著提升了召回率（+12.3%）和精度（+15.1%），有效降低了开放集错误率，适用于机器人视觉等实际应用场景。<br>
<br>

 &nbsp;&nbsp;&nbsp; 6、[Efficient Bayesian Uncertainty Estimation for nnU-Net](https://link.springer.com/chapter/10.1007/978-3-031-16452-1_51)<br>
&nbsp;&nbsp;&nbsp;这篇论文引入了一种新的方法来估计医学图像分割中nnU-Net的不确定性。我们提出了一种高效的后验权重空间采样方案，用于贝叶斯不确定性估计。与蒙特卡洛Dropout和均值场贝叶斯神经网络等先前的基线方法不同，我们提出的方法不需要变分架构，并保持原始nnU-Net架构的完整性，从而保留了其优异的性能和易用性。此外，我们通过边缘化多模态后验模型提升了分割性能。我们将在公开的ACDC和M &M心脏MRI数据集上应用我们的方法，并展示了在一系列基线方法上改进的不确定性估计。所提出的方法进一步增强了nnU-Net在医学图像分割方面的准确性和质量控制能力。<br>
<br>

 &nbsp;&nbsp;&nbsp; 7、[Test-time Data Augmentation for Estimation of Heteroscedastic Aleatoric Uncertainty in Deep Neural Networks](https://openreview.net/forum?id=rJZz-knjz)<br>
&nbsp;&nbsp;&nbsp;这篇论文提出了一种无需修改模型或重新训练的测试时数据增强（test-time data augmentation, TTA）方法，用于估计深度神经网络在医学图像分析中的异方差偶然不确定性（heteroscedastic aleatoric uncertainty）。其核心思想是：在测试阶段对输入图像进行几何和颜色变换（如旋转、翻转、亮度调整等），通过观察模型在这些扰动下的输出变化，来估计输入相关的预测不确定性。该方法在糖尿病视网膜病变（DR）检测任务上进行了验证，结果表明其不确定性估计与预测错误高度相关，可用于主动筛选高风险样本供医生复核，从而提升临床决策的可靠性。相比传统贝叶斯方法（如MC Dropout、MCBN），TTA 更简单、通用，且不受训练方式限制，是一种实用、可解释的不确定性估计工具。<br>
<br>

 &nbsp;&nbsp;&nbsp; 8、[SoftDropConnect (SDC) -- Effective and Efficient Quantification of the Network Uncertainty in Deep MR Image Analysis](https://arxiv.org/abs/2201.08418)<br>
&nbsp;&nbsp;&nbsp;这篇论文提出了一种新的贝叶斯推理方法——SoftDropConnect（SDC），用于量化深度神经网络在医学图像分析中的不确定性。不同于传统的 Dropout 或 DropConnect 方法，SDC 在训练和测试阶段通过连续均匀分布对网络连接权重进行软调制，而非直接丢弃连接，从而保留信息流的完整性，减少信息损失。<br>
<br>

三、不确定性的评价以及校准
----

四、不确定性的应用领域
----
