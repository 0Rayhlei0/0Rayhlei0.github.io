---
title: "[金融分析] CFA一级《公司金融》学习笔记"
date: 2022-06-02 23:51:42
tags: [CFA一级,公司金融, 日常学习]
categories: 金融分析
description: "[第16篇] 本篇将包括CFA一级考试中公司金融(Corporate Issuers)科目的学习笔记。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/CFA.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/16-CFA-level1-Corporate-Issuers.jpg
katex: true
---

# 概览

公司金融一共包括2个Session的5个Reading，各个Reading的内容如下表：

<table>
    <tr>
        <th>Sessions</th>
        <th>Readings</th>
        <th>Contents</th>
    </tr>
    <tr>
        <td rowspan="3">SS10</td>
        <td>R31</td>
        <td>Introduction to Corporate Governance and ESG</td>
    </tr>
    <tr>
        <td>R32</td>
        <td>Capital Budgeting</td>
    </tr>
    <tr>
        <td>R33</td>
        <td>Cost of Capital</td>
    </tr>
    <tr>
        <td rowspan="2">SS11</td>
        <td>R34</td>
        <td>Measures of Leverage</td>
    </tr>
    <tr>
        <td>R35</td>
        <td>Working Capital Management</td>
    </tr>
</table>

公司金融部分主要涉及的内容是以公司首席财务官的角度管理公司财务，主要的关注点就是最优化资金的来源与分配。

# Session 10

## Reading 31 公司治理

第一个Reading考点不多，主要是概念性内容。公司治理有两套主要理论，分别是`股东权益最大化(Shareholder theory)`和`公司利益相关者利益最大化(Stakeholder theory)`，前者是2015年前业界认为的公司治理最佳方法，即为公司股东争取最大利益，现在CFA通常认为后者为公司治理的主要目标，也即公司经营目标为包括股东在内的员工、管理者等各个相关方的利益最大化。

### 管理利益冲突

好的公司治理架构应该要降低`代理人冲突(principal-Agent Conflict)`，即避免公司管理人员为自己利益放弃股东利益，一个可行的方法是为管理者支付公司股票作为薪酬，以此绑定管理者与股东利益。

中小股东与控股股东利益冲突可以通过设计投票权的方式解决。

股东与债权人利益冲突体现在股东可能倾向于更高风险的项目，债券人希望风险更小。

### 董事会

董事会的重要要求是需要独立于层，好的董事会可以具有下面这些特点：

- `独立董事(Independent Director)`数量多于`执行董事(Executive Director)`。
- 董事会主席不能由公司首席执行官或前任首席执行官担任。
- 董事会成员与公司经营没有利益关系。
- 董事会成员经验少于十年。
- 董事会召开时不应有公司管理层在场。
- 好的董事会成员应该有专业技能。
- 分层分级董事会(Staggered boards)

董事会下设的专业委员会中审计委员会、薪酬委员会和提名委员会的成员必须全部 是独立董事。

### ESG Consideration

CFA近年强推ESG(环境、社会和管理)影响，建议投资人考虑在ESG方面执行较好的公司投资。主要的执行方法包括`负面清单(Negative screening)`、`正面清单(Positive screening)`和`行业最好(best-in-class)`。

## Reading 32 资本预算(Capital Budgeting)

本节内容主要考虑公司如何判断是否投资某个长期项目，其衡量方法有`NPV(净现值)`和`IRR(内部收益率)`等方法。

### 资本预算的流程

1. `Idea generation：`通过不同渠道获得一个不错的投资想法。
2. `Analyzing project proposals：`预测项目未来的现金流并评估项目的可盈利性。
3. `Create the firm-wide capital budget：`考虑项目的现金流时间，公司的资源以及公司整体的发展策略的匹配。
4. `Monitoring decisions and conducting a post-audit：`最后评估项目投资的结果。

### 项目分类

资本项目有以下四个分类：

`替代项目(Replacement projects)：`用来维持业务运营或减少成本的替换原有资产的投资项目。

`扩张项目(Expansion projects)：`对已有产品或对新产品与服务的扩张性投资项目。

`强制投资(Mandatory investment)：`监管，安全或环境保护的强制性投资，最大特点是可能净现值小于0。

`其他项目(Other projects)：`又叫宠物项目，主要特点是项目现金流难以分析，可能主要是项目负责人喜欢而投资。

### 资本预算的五大原则

1. 项目预算的决策取决于项目的`增量现金流(incremental cash flow)`而不是会计利润。
2. 现金流中的`沉没成本(Sunk cost)`与`融资成本(Interest cost)`应该被忽略。
3. 现金流中的`外部性(Externalities)`与`机会成本(Opportunity Costs)`应该被考虑。其中外部性包括`negative externalities(cannibalization)`和`positive externalities`，即互斥项目中对旧产品的不利影响和互补项目中对旧产品的有利影响都应该被考虑，机会成本则是因为做该项目而导致少赚到的`另一个最好(Next Best)`的项目收益。
4. 项目现金流出现的时间非常重要，要考虑金钱的时间价值。
5. 所有分析用的现金流都是`税后现金流`。

### 资本预算的假设条件

`独立项目(Independent projects)`是互相之间没有关联的项目，考虑独立项目时只要其净现值大于0便可以投资。`互斥项目(Mutually exclusive projects)`是多个项目中只能选取其中一个投资时，应该将所有项目的可盈利性排列后选择最好的。

另外有一些项目的投资具有`顺序性(project sequencing)`，也就是说现在投资的某些项目可能为以后投资另一个项目创造机会。

最后若假设无限资本时只要有利可图的项目都可以投资，但现实情况是公司可以支配投资的资金有限，公司需要使用有限的资金获取尽可能多的投资收益。

### 项目估值的五大方法 

#### 净现值方法(Net present value)

项目所有相关现金流折现后的加总既是项目的净现值，NPV大于0即可投资。其优点为可以直观看见可盈利的数额；正净现值表示项目可以为公司股东盈利；折现率为现实值。缺点主要是忽略了项目的初始投资规模。

#### 内部回报率方法(Internal rate of return）

IRR是当我们认为投资项目净现值为0时项目的折现率，若IRR大于资金成本就可以投资。`当IRR结论与NPV结论冲突时，优先考虑NPV的结果。`IRR的主要优点为其反应了收益率，即考虑了收益与初始成本的关系。其缺点在于可能无法计算或算出多个结果(项目现金流的符号变动几次最多就可能有几个IRR的解)；IRR假设了现金流的再投资率就是IRR，这个假设不符合实际。

#### 回收期法(Payback period)

PBP是计算收回初始投资的时间，若PBP低于基准PBP就可以考虑投资。优点是简单且反映了项目的风险与流动性。缺点是忽略了时间成本，且忽略了回收期之后的现金流与项目的盈利能力。

#### 折现回收期法(Discount payback period)

DPBP是以折现后的现金流计算收回初始投资的时间，若DPBP低于基准DPBP就可以考虑投资。优点是反映了项目的风险与流动性，且考虑了时间成本。但其缺点依然是忽略了回收期后的现金流以及项目的盈利能力。

#### 盈利指数法(Profitability index)

盈利指数PI是未来现金流的折现现金流之和除初始投资成本，若PI>1则应该考虑投资。它的变形式就是净现值与初始投资数额的比值，大于0就应该考虑投资。其优点是相较于净现值方法考虑了初始投资的规模。其缺点是没有反映盈利的实际金额。

### NPV Profile

对比项目的净现值随资本融资成本变化而变化的影响，不同项目因为现金流的时间不同，他们的净现值对融资成本的变化速度有所不同，见下图：

![NPV Profile](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220609212809914.png)

这张图的特点有：

1. 两条线与X轴的交点为各自的IRR，与Y轴的交点为各自的无折现净值。
2. 两条线的交点处的回报率会导致两项目净现值相等，叫做`Crossover Rate`。
3. 两条线斜率不同的原因是其大额现金流出现时间不同，大额现金流出现越晚其净现值越容易被折现率影响。

### 项目NPV对公司股票价值的影响

理论上我们假设公司的股票价值会随公司新做投资的净现值变化，计算时将项目的净现值平摊至每一股，就是该项目对公司股票价值的影响。

## Reading 33 融资成本(Cost of Capital)

### 加权平均资本成本(Weighted Average Cost of Capital, WACC)

企业的平均融资成本就是WACC，其最大作用是可以被用来折现公司未来的现金流，也即是说这是`公司最低要求回报率`。其计算公式如下：
$$
WACC = W_{d}\times r_{d}\times(1-t)+W_{e}\times r_{e}+W_{ps}\times r_{ps}
$$
其中$W$代表资产占比，$r$代表该部分资产融资成本。$d$为债务资产，$e$为所有者权益资产，$ps$为优先股资产。

#### 计算权重$W$

权重的计算方法如下：
$$
W_{d} = \frac{D}{D+E}\ \ \ \ \ W_{e} = \frac{E}{D+E}
$$
即，权重既是该部分资产占总资产数额的占比，计算使用资产的`市场价值(Market Value)`。若公司披露其未来的`目标资本结构(Target Capital Structure)`，因为权重计算的是公司未来的现金流折现率，因此以目标结构计算，测算权重时可用的资本结构顺序为`目标>预测>目前>其他类似公司`。

#### 计算债务成本$r_{d}$

计算债务成本$r_{d}$主要有两种方法：

1. `持有至到期方法(Yield to maturity approach)：` 债券的现金流折现至其目前价值的折现率就是债券的YTM。
2. `债务评级法(Debt-rating approach)：`如果债券没有公允价值则使用债务评级法估算，以市场上同等级债券的债务成本为相同的参考。

#### 计算优先股成本$r_{ps}$

优先股就是永续年金，永续年金的价格为其股利除以其要求回报率，此要求回报率既是优先股成本，其计算方法为：
$$
r_{ps}=\frac{D_{ps}}{P}
$$
其中$D_{ps}$为优先股股利，$P$为优先股的`市场价格`(假设市场价格准确反映其要求回报率)。

####  计算股票成本$r_{e}$

股票融资成本的计算方法比较多，分别有`资本资产定价模型(CAPM)`，`股利折现模型(Dividend discount model)`和`债券回报率加风险溢价方法`。

##### CAPM模型

- `上市公司CAPM：`$r_{s}=r_{f}+\beta(r_{m}-r_{f})$ ，该公式中$r_{m}$为`市场组合收益(market rate of return)`，其减去无风险回报率$r_{f}$的结果为`市场组合风险溢价(market risk premium)`。$\beta$为股票收指数的影响程度，$\beta=2$代表指数增长1时股票增长2，该数值可以通过回归方程计算$\beta=\frac{Cov(i,m)}{\sigma^{2}_{m}}$。

- `非上市公司CAPM：`非上市公司的主要问题在于无法根据市场价格计算$\beta$，因此计算该值时使用Pure-play method估算非上市公司的$\beta$从而使用CAPM模型计算其回报率。该方法的基本原则是找到一家与目标公司相似的上市公司，假设他们的经营风险相同，分别移除上市公司的财务风险得到其$\beta_{Asset}$后加上目标公司的财务风险以估算非上市公司的$\beta$。

  这个方法中的一个重要值为`财务杠杆影响`$[1+(1-t)\frac{D}{E}]$，上市公司$\beta$除以该财务杠杆即为去杠杆，然后乘上目标公司财务杠杆以得到非上市公司的$\beta$。

- `新兴市场国家CAPM：`对于新兴市场国家由于其经济不稳定导致其可能市场风险更大，因此在计算这些国家的股东预期收益率时应该加上该国家的`国家风险溢价(Country risk premium)`。公式写作$r_{s}=r_{f}+\beta(r_{m}-r_{f}+CRP)$  ，而$CRP=SYS\times \frac{\sigma_{stock}}{\sigma_{bond}}$，其中SYS为国债利率利差，即稳定市场国家与新兴市场国家的国债利差。

##### 股利折现模型

股利折现模型又称`Gordon dividend growth model`。其基本原理是假设公司股利每年以g的增速永续增长，而公司的现时价值就等于所有未来股利的现值。
$$
V_{0}=\frac{D_{0}\times (1+g)}{r-g}=\frac{D_{1}}{r-g}
$$
其中$D_{0}$为股票现值，$D_{n}$为第n次股利，r为股东要求回报率, g为股利增长率(ROE乘股利留存率)。

使用股利折现模型就可以推出股东要求回报率，也即是股票成本的公式：
$$
r_{e}=\frac{D_{1}}{V_{0}}+g
$$

##### 债券回报率加风险溢价方法

顾名思义，该模型认为股票成本为债券要求回报率加风险溢价：
$$
r_{e}=YTM+RP
$$
其中YTM为公司长期债券的要求回报率，RP为股票和债券回报率间的历史差值。

#### 最优资本预算

- WACC是公司整体的资本成本，只有当项目风险与公司已有的项目风险相同时，项目现值才可以使用公司WACC计算折现。
- 对于项目投资来说，投资的收益(IRR)会随着投资数目的增加而减少，边际融资成本(MCC)会随着投资数目的增加而增加。因此当两条线相较时(IRR=MCC)资本规模是`最优资本预算(Optimal Capital Budget)`。
- 融资成本突破点(Break point)的计算方法是用导致融资成本(债券或股票)变化的融资数额除以公司该类资本的占比。

### 股票发行成本

股票发行的发行成本通常是股票发行过程中支付给相关投资银行、会计师事务所、律师事务所等相关中介机构的费用，而我们在计算股东要求回报率时应该考虑该成本。

#### 定量计算(CFA不推荐)

该方法认为股票发行成本应作为股票发行价格的抵减。而股东要求回报率就在股利折现模型的基础上在股票现值上抵减掉该发行成本。
$$
 r_{e}=\frac{D_{1}}{V_{0}-F}+g\ \ \ \ \ \ or\ \ \ \ \ \ r_{e}=\frac{D_{1}}{V_{0}\times (1-f)}+g
$$
但由于该方法导致一次性的发行成本影响公司未来的所有现金流的折现率，不符合实际情况因此不受CFA推荐。

#### 定性计算(CFA推荐)

该方法认为股票发行成本作为一次性的期初现金流出。

# Session 11

## Reading 34 杠杆衡量(Measures of leverage)

 `杠杆(leverage)`的本质既是使用`固定支出(fixed cost)`。`经营性杠杆(Operating leverage)`由固定运营成本导致，衡量方法是`DOL(Degree of Operating Leverage)`。`财务性 杠杆(Financial leverage)`由债务融资及其支出导致，衡量方法是`DFL(Degree of Financial Leverage)`。总杠杆由`Degree of Total Leverage(DTL)`衡量。

`商业风险(Business risk)`是由经营杠杆导致，使用销售变化导致EBIT变化来衡量，由`销售风险(Sales risk)`和`操作风险(Operating risk)`组成。销售风险是指货物和服务的价格和数量相关的不确定性；操作风险是指

`财务风险(Financial risk)`是由财务杠杆导致，使用EBIT的变化导致EPS的变化来衡量。

### 经营性杠杆(DOL)

经营性杠杆的定义就是销售变化导致的EBIT变化，计算方法使用计算式：
$$
定义式：DOL=\frac{percentage\ change\ in\ EBIT}{percentage\ chnage\ in\ unit\ sold}=\frac{\frac{\Delta EBIT}{EBIT}}{\frac{\Delta Q}{Q}}\\
计算式： DOL=\frac{Q(P-VC)}{Q(P-VC)-FC}=\frac{S-TVC}{S-TVC-FC}
$$
其中$Q$是`销售量`，$P$是销售价格，$VC$是变动成本，$FC$是固定成本，$S$是总销售额，$TVC$是总变动成本。显然，当固定成本$FC=0$时，$DOL=1$是最小值。

### 财务性杠杆(DFL)

财务性杠杆定义是EBIT变化导致EPS的变化，计算方法使用计算式：
$$
定义式：DFL=\frac{percentage\ change\ in\ EPS}{percentage\ change\ in\ EBIT}=\frac{\frac{\Delta EPS}{EPS}}{\frac{\Delta EBIT}{EBIT}}\\计算式： DFL=\frac{EBIT}{EBIT-Interest}
$$
当财务费用为0时$DFL=1$为最小值。

### 总杠杆(DTL)

总杠杆有经营性杠杆和财务性杠杆组合，用于衡量销售变化导致的每股净利润变化。
$$
DTL=DOL\times DFL\\
DTL=\frac{Q(P-VC)}{Q(P-VC)-FC-Interest}=\frac{S-TVC}{S-TVC-FC-Interest}
$$
其中$Q$是`销售量`，$P$是销售价格，$VC$是变动成本，$FC$是固定成本，$S$是总销售额，$TVC$是总变动成本。同样的当两个杠杆都为1时$DTL=1$是最小值。

### 盈亏平衡销量(Breakeven Analysis)

$$
Q_{BE}=\frac{FC+Interest}{P-VC}
$$

其中$P$是销售价格，$VC$是变动成本，$FC$是固定成本, 即`除去变动成本后的售价(边际贡献, Marginal Contribution)`达到该销量后刚好可以覆盖所有固定成本时，该销量既是盈亏平衡销量。

`经营性盈亏平衡(Operating breakeven)`是指不计算财务利息时的盈亏平衡点，即固定成本除边际贡献。

## Reading 35 营运资金管理(Working Capital Management)

### 流动性衡量

公司财务官在管理公司营运资金时的一个重要作用就是监督公司的财务流动性，其中流动性主要分为两种：

- `Primary sources of liquidity(主要流动性)：` 主要流动性的使用是健康的财务行为，主要包括销售产品或服务，收集应收款项，短期投资获利等等。
- `Secondary sources of liquidity(次要流动性)：`当公司需要动用次要流动性时，可能说明公司财务状况已经不太健康。主要的三种行为分别是变卖长期或短期资产，债务重组，申请破产保护。

另外有两个可能会导致公司流动性问题的原因分别是`收钱慢(Drags on liquidity)`和`付钱快(Pulls on liquidity)`。收钱慢主要的表现有`应收账款无法收回(Uncollectable A/R)`和`老旧存货(Obsolete Inventory)`。流动性的其他知识在`财务报表分析`中已经学习过。

### 应付账款管理(Payable management)

当供应商希望鼓励公司尽快支付应付账款时可能会有为公司提供早鸟优惠，为在早期付款的公司提供一些优惠。这时我们需要计算这些早鸟优惠的`等效年利率(Effective annualized return)`来为是否接受该优惠决策。该EAR的计算方法就等价于计算在什么折现率下最晚付款期限前付款的现值等于早鸟折扣付款。

### 现金管理(Cash management)

现金管理是指公司在短期内现金盈余或缺少时进行的短期投资或融资行为。投资的部分会在数量方法课中覆盖，在公司金融中主要涉及的是短期融资行为。主要的短期融资方法包括：

- `银行授信(Lines of credit)：`银行的授信的可信赖程度从低到高分别有`不承诺的授信(Uncommitted line of credit)`、`承诺的授信(Committed line of credit)`和`循环授信(revolving line of credit)`。
- `抵押贷款`(Pledge assets as collateral for bank borrowings)
- `银行承兑汇票(Banker's acceptances)：`主要用于出口商品的公司，得到买家银行指定日期的无条件支付现金的承诺。
- `银行保理(Factoring)：`将公司应收账款折价卖给银行以获得短期流动性。

还有一些非银行的短期融资方法：

- 其他民间贷款：通常对小公司或信用较低的公司来说融资成本较高。
- 商业票据(Commercial paper)：公司直接发售债券。


[第16篇] 

