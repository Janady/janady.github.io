---

layout: post
title: 游乐园互联网升级
date: 2016-07-04 18:00:00 +0800
categories: management

---

本文阐释一下对游乐园项目互联网升级的思考。主要从已有问题/
信息整合的效果/项目安排等方面简单陈述。

## 核心理念

园区目前的信息化程度不高，以信息为核心重组交互方式可以挖掘价值和改善体验。

在高度不确定的软件行业，项目开发须与运营需高度结合。
以用户价值为核心进行持续迭代，最终实现目标。
为了避免变更引起繁重流程浪费精力，以及不明确的步骤产生目标不一致，
而采取的敏捷开发对团队成员能力有一定要求。

互联网平台的主要优势是重新定义了信息，围绕着信息生成、分享而构建
强大的生态。

## 关系脉络

项目的开展围绕着运营的需要，运营则以用户价值和园区价值的提升为基础。
下面通过思维导图理清其关系。

### 用户价值

园区以信息整合、设施更新、构建形象等方面来提升效率和趣味性。

![user value](/assets/user_value.png)

通过平台给用户带来的价值最直观的就是便捷，通过高效的信息渠道，
让园区与用户之间可以直接对话。在线上平台里，咨询、游玩攻略、
优惠信息等都更易拉近用户距离。而在用户与用户之间，通过活动、游戏、
图片、体验等的分享也能丰富体验和增加趣味性。

此外，园区设施的更新与线上系统的结合，更能直接的带来质变。
电子票据与门卡的结合可以降低枯燥排队时间。
园区娱乐项目的预约/显示排队时间等能让用户控制好时间以及降低焦虑。
消费购物等各个环节都可引入相应的智能硬件。

人脑能记住的其实只有形象，一切具体的事物都将被弱化，根据已有的认知
与灌输的概念，留下的是深刻的形象。
围绕已有的基础设施，植入一个伟大的形象便是品牌的胜利。

### 园区价值

![park value](/assets/park_value.png)

园区通过平台可以得到用户数据，可以提高管理效率。以此，可以在营销推广、最大化优势项目、加快问题响应、营造品牌认同等方向作优化。

## 平台模块

基于以上目标，可以在较高层次定义平台所需的支撑模块。
而项目的具体开展是依赖于运营的需要。
大部分模块需要会员管理模块为基础，初始的帐号系统便必不可少。
在会员管理模块中要做到信息收集分析，为其他模块提供数据。

![projects](/assets/projects.png)

初始的运营很难达到太高的用户粘性，不应追求其频繁使用，
而应结合园区内的设施提供实用价值。具体运营方案暂不清晰，
其他模块也无法进行详尽规划。
在敏捷开发的项目中，也不应在不确定性条件下做太多细致规划。

## 项目规划

根据当前的信息，在较高层面上作部分说明以及一些经验判断。
在各个具体子系统中均以一个熟练开发者的工作时长来说明（人/天），
从而大致得出项目规划。但实际情况需要不断根据运营计划而调整。

以下是依据在通用开发框架下所需的工作进行的预估。

---

#### 框架

构建系统环境，选用通用开发框架，进行单元测试部署。

**部署环境**

- 时间：7 人/天
- 并行：可以2-3人并行完成，其他工作依赖于框架选取

---

#### 用户管理

从用户价值及框架依赖来看，首先需要完成的是会员管理系统。
其中包含帐号系统，游戏、社区平台的扩展接口，购票、硬件等的绑定信息。

在用户系统中，初始的帐号系统是基础，其他部分可在相应模块开展时再扩展。

**帐号系统**

围绕着用户注册、登录、修改而进行。具体的注册流程需根据自身
用户特点而定，如采用何种密码措施，如何接入第三方帐号等。
以及后续的功能模块所需的帐号保护等。这是一个需要持续完善的模块。

- 时间：开发 7-30 人/天，设计 5-10 人/天， 产品 3-5 人/天
- 并行：大部分模块都会依赖于帐号系统。

**购票系统**

购票系统会涉及流程设计、支付安全等方面。生成的票据也可关联线下门禁
系统，可以实际产生效用，可能会成为线下运营的突破口。

- 时间：开发 30-60 人/天，设计 5-10 人/天， 产品 5-10 人/天
- 并行：此部分可以规划出更多小任务，加快并行开发及迭代速度。

**社区**

平台最终的活跃程度以及发展上限可能都会由社区的完善程度而决定。
社区的关键点在于运营，强调产品、开发、运营紧密配合，是个不断改进的
过程。

- 时间：开发 30- 人/天，设计 5- 人/天， 产品 5- 人/天
- 并行：取决于产品的规划需要，保证各方信息都在项目产品层面取得一致。

---

#### 资讯信息

资讯信息主要围绕用户需要那些有用的信息，平台希望用户关注到哪些信息而
展开。其中会包含优惠活动、客户服务、游玩攻略等方面。

**信息推送**

推广品牌形象，宣传生活方式，展示优惠信息等。

- 时间：开发 15-30 人/天，设计 5-10 人/天， 产品 5-10 人/天
- 并行：与其他模块相关性不大，内部也可拆分多个子任务。

**客户服务**

客户服务涉及内部客服与用户，其中包含的控制可能较多。整个流程暂不清晰，
预测偏差可能较大。

- 时间：开发 15-30 人/天，设计 5-10 人/天， 产品 5-10 人/天
- 并行：与其他模块相关性不大，内部也可拆分多个子任务。

**活动攻略**

如果只是由园区提供，内容会较少。若接入用户的分享及评价等排名，
会有较大工作量。在运营策略未清晰前，先以园区提供来计划。

- 时间：开发 5-10 人/天，设计 1-5 人/天， 产品 1-5 人/天
- 并行：与其他模块相关性不大。

---

#### 园区导览

园区导览会涵盖整个游玩过程中提供的信息服务。包含地图信息、
园区各项目的实时状况、智能推荐等。

**地图信息**

包含景区地图，休闲购物场所，游玩项目等。此处未包含进用户评价体系。

- 时间：开发 30-60 人/天， 设计 5-10 人/天， 产品 5-10 人/天
- 并行：条件成熟可以高度并行完成。

**实时状况，智能推荐**

展示各项目的实时状况，可能须结合相应的硬件产品收集数据。

- 时间：开发 30- 人/天， 设计 10- 人/天， 产品 10- 人/天
- 并行：条件成熟可以高度并行完成。

---

#### 智能硬件

绑定用户ID，上传用户数据，提供更好的策略分析与交互体验。

---

#### 范娱乐

围绕着园区的长期品牌规划而设计，旨在营造更加轻松趣味的环境，
让品牌深入人心。

**游戏中心**

搭建游戏中心，推出自己的主题游戏，引入热门游戏，提供第三方开发接口。
优化检索、评价、排序策略，实现平台的另一个突破口。

- 时间：开发 60- 人/天， 设计 15- 人/天， 产品 10- 人/天
- 并行：持续迭代

---

#### 电商平台

实现娱乐消费一体化，强化线下影响力。具体需跟据运营需求来定。


## 总结

根据运营需求，以信息化为中心，改善园区内外的交互体验方式。
为实现快速迭代，需要不断深入，这亦是一个渐进明细的过程。

在项目开发的角度，所需人员应按照并行开发的程度来决定。项目的细致及
规划程度也与相应的团队成员对项目的理解相关。所以提供的时间仅代表
粗略的经验预测，而大部分规划期间都会含有信息掌握的程度不够，
评估有乐观的倾向。

下面以实现初始的用户管理、购票系统、资讯信息的时间点展开时间上的预估。
由于敏捷开发要求的并非开发者在确定的模式中不断重复工作，
所以核心开发者的费用会在15k+/月。而测试先行的开发模式本身已经包含了
很多单元测试/集成测试的内容，初期完全没必要专业的测试人员。

**团队架构**

团队是一个逐步完善的过程。

- 组成：项目管理-1/产品经理-1/核心开发-3/UI设计-1
- 时间：3个月

**我对项目管理的理解**

- _认知一致_：不管如何拆分任务，如何协同处理。都应是从不同角度对高层
需求的一致描述。尽可能的做到系统是一个同构的体系。
- _创造力_：在认知一致的基础上提供更大的自由度，可以激发创造力。
- _效率_：规划拆分任务以及不确定/明细的任务都是效率损失的主要来源。
任务划分的过程便是根据不同人制定不同明细程度的任务。