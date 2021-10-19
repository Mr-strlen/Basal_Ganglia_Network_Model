# 2021 CPMCM  
2021年第十八届华为杯数学建模竞赛C题  
至于得了什么奖，已经不重要了（主要是结果还没出来啊）  
弄了四天，做了个粑粑，这里算是一个记录  
就不放代码了，把一些做出的结果图片放上来  
有关比赛期间的日常记录，哎，在这：https://www.zhihu.com/question/492261124/answer/2176448512  

## 整体分析
这道题给的限制条件很少，许多地方都需要背景知识和先验参数，所以有很大一部分时间就在搜集各种论文，指导小队下一步工作。  
主要的参考文献如下：  
1. Jiang X, Liu S, Lu B, et al. High-Frequency Stimulation for Parkinson’s Disease and Effects on Pathways in Basal Ganglia Network Model[J]. Journal of Medical and Biological Engineering, 2016, 36(5): 704-717.
2. Zhang X, Liu S, Zhan F, et al. The effects of medium spiny neuron morphologcial changes on basal ganglia network under external electric field: a computational modeling study[J]. Frontiers in computational neuroscience, 2017, 11: 91.
3. Rubin J E, Terman D. High frequency stimulation of the subthalamic nucleus eliminates pathological thalamic rhythmicity in a computational model[J]. Journal of computational neuroscience, 2004, 16(3): 211-235.
4. 深度脑刺激治疗帕金森病的动力学机制研究_张珂萍
5. 基于基底核模型的DBS作用机制研究_贾洪军
6. 帕金森状态的闭环DBS设计与分析_苏斐
7. 帕金森状态的建模与闭环控制_刘晨
  
以上文献都能在谷歌学术或者知网上找到  
  
* 其中1,2两篇文献均为刘深泉老师的研究，3是奠定了基底神经节分析的一篇。刘老师的工作和本次题目非常的接近，也是参考的重点，具体而言包括：  
  - 不同神经元的膜电位方程和公式
  - 突触连接的超参数选择
  - 神经网络的设计（相互连接方式，内部神经元数量，内部连接方式）
  - 仿真及仿真结果分析
  - DBS刺激参数选择
* 4-7篇文献主要是相关的毕业论文，也辅助构建了神经元的模型和超参数选择；在解答三四五问中，他们的实验结果为我们提供了参考意义

## 过程中的一些思考
1. 有关神经元模型构建时的参考链接
	- HH模型 https://zhuanlan.zhihu.com/p/102770891
	- 脉冲神经网络 神经元模型-HH模型（1） https://blog.csdn.net/qq_34970603/article/details/106356553
	- SNN系列｜神经元模型篇(1) Hodgkin Huxley https://blog.csdn.net/ly18846826264/article/details/103230383
	- Models of deep brain stimulation http://www.scholarpedia.org/article/Models_of_deep_brain_stimulation
	- Basal ganglia http://www.scholarpedia.org/article/Basal_ganglia
	- 簇发放brusting https://en.wikipedia.org/wiki/Bursting  
		代码 https://github.com/zackmcnulty/NBIO_301-Project
2. HH模型中，mhn参数初始化（时刻为0）从哪来  
答：认为初始状态是一个平稳状态，平稳状态在时间为正无穷时取到（问题一参考链接1,2）
3. 直流刺激评价结果  
答：画三个图
    - 单个神经元脉冲,"全或无" 大于某个阈值，出现周期响应
    - 分段直流刺激
    - 电流强度和频率的折线图
4. 交流刺激评价  
    - 符合直流，可以用来间隔调整
    - 频率不能改变发放频率
5. 簇发放模拟  
加入钙离子通道
6. 不同神经元的模型和超参数
7. 网络连接设计（包括每个区域内神经元数量，外部连接，内部连接）
### 问题二的解释思路
1. 介绍回路
2. 介绍网络结构
3. HH方程+介绍突触方程（复杂方程简化）
4. 介绍各种神经元
5. 进行仿真（给出超参数：神经元方城里面的参数，突触参数）
6. 时序图（统计每种神经元的放电频率mean±std）
7. 进行生理学解释
### 问题三的解释思路
1. 去除SNc后的网络图
2. 仿真时序图
3. 定量分析：峰数（如何定义），平均间隔时间/方差，独立性or相关性检验
4. 生理学解释

## 选题原因
以下是我在赛题开题之后，看到题目的第一感受和思考，非常不专业且带有主观色彩，看个乐子。  
### A题 相关矩阵组的低复杂度计算和存储建模 ×
一个纯数学推导的问题？  
淦，做这道题的，我一律奉为老神仙  

### B 空气质量预报二次建模
第一眼看上去和2020年的汽油辛烷值建模很像 
- 第一问，根据公式补充数据（数据预处理的一些手段，异常值） 
- 第二问，分类（无监督分类？）+特征解释 
- 第三问，预测（八仙过海了） 
- 第四问，优化（增加数据，协同） 

### C 帕金森病的脑深部电刺激治疗建模研究 √
吊，神经元放电模型，脑网络分析，就是我现在在做的东西  
有点想做这块，但是需要评估难度  
（事后发现和我做的东西吊毛关系没有）

### D 抗乳腺癌候选药物的优化建模 ×
需要有一定的药学背景，因为需要解释化合物分子表达式  
~~好吧，我知道做C题的朋友挺多的，去学习模式就可以了，但我就是对化学有抵触情绪，我老铁天天和我说化学天坑药学天坑，已经有PTSD了~~
- 第一问，特征筛选+解释
- 第二问，预测
- 第三问，分类预测模型
- 第四问，寻找取值范围
md这题的附录文件贼恐怖，我有PTSD  

### E 信号干扰下的超宽带（UWB）精确定位问题 ×
UWB无线定位问题，UWB在我实习的时候接触过  
可以看成一个机器学习的题目，但应该要涉及信号处理的部分（抗干扰，时频分析？）  

### F 航空公司机组优化排班问题
线性规划模型，简直就是19年航行轨迹题目的翻版，估计做的人也是最多的（毕竟啥专业的都能上手）  
- 第一问，建立线性规划模型给航班分配机组人员
- 第二问，引进执勤概念，除了需要满足子问题1的所有目标外，还需满足如下目标
- 第三问，编制排班计划，除了需要满足子问题1和2的所有目标外，还需满足如下目标
