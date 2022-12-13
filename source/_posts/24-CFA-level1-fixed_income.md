---
title: "[金融分析] CFA一级《固定收益》学习笔记"
date: 2022-09-21 23:53:15
tags: [CFA一级,固定收益, 日常学习]
categories: 金融分析
description: "[第24篇] 本篇将包括CFA一级考试中固定收益(Fixed income)科目的学习笔记。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/CFA.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/24-CFA-level1-fixed_income.jpg
katex: true
---

# 概览

固定收益一共包括2个Session的6个Reading，主要包括的内容是各个Reading的内容如下表：

<table>
    <tr>
        <th>Sessions</th>
        <th>Readings</th>
        <th>Contents</th>
    </tr>
    <tr>
        <td rowspan="4">SS14</td>
        <td>R42</td>
        <td>Fixed-Income Securities: Defining Elements</td>
    </tr>
    <tr>
        <td>R43</td>
        <td>Fixed-Income Markets: Issuance, Trading, and Funding</td>
    </tr>
    <tr>
        <td>R44</td>
        <td>Introduction to Fixed-Income Valuation</td>
    </tr>
    <tr>
        <td>R45</td>
        <td>Introduction to Asset-Backed Securities</td>
    </tr>
    <tr>
        <td rowspan="2">SS15</td>
        <td>R46</td>
        <td>Understanding Fixed-Income Risk and Return</td>
    </tr>
    <tr>
        <td>R47</td>
        <td>Dundamentals of Credit Analysis</td>
    </tr>
</table>

# Session 14

## Reading 42 固收证券：定义

### 债券特征

债券的主要特征有`发行人(Issuer)`、`到期日(maturity)`、`面值(par value/principal value)`、`息票率(Coupon rate)`、`币种(Currency)`。

#### 发行人

- `超国家组织(Supranational organizations)`：由世界银行、欧洲投资银行、国际货币基金组织等国际组织发行。
- `国家(Sovereign governments)`：由主权国家的财政部发行。
- `地方政府(Non-sovereign governments)`:由地方政府发行。
- `准政府(Quasi-government entities)`：例如联邦全国抵押协会：房利美
- `公司(Companies)`
- `特殊目的企业(SPE/SPV)`

#### 到期日

到期日是指债券的本金被返还的日期。`Term to maturity(tenor)`是指从现在到到期日的时间。到期日小于一年的债券叫做`货币市场债券(Money market security)`，到期日大于一年的叫做`资本市场债券(Capital market securities)`，没有固定到期日的债券叫`永续债券(Perpetual bonds)`。

#### 面值

债券的面值通常是100或1000。

#### 息票率

`普通债券(Vanilla bond)`是指固定利率的债券，`零息债券(Zero-coupon bond)`是指不付利息的债券。

#### 币种

`双币债券(Dual-currency bond)`是指付息和偿还本金分别使用两种不同币种的债券。`可选币种债券(Currency option bond)`是债券持有人可以选择两种货币中的一种来获得支付。

### 债券市场

债券市场分为四种：当债券发行地与发行货币相同时，债券属于`national bond`。这时如果发行人属于发行地则债券为`domestic bond`；如果发行人不属于发行地，则债券为`foreign bond`。当发行地与发行货币不相符时，发行的债券叫`Eurobond`；如果债券即在本地发行又在其他国家发行，则属于`global bond`。

其中Eurobond又分两类，分别是实名登记的`Registered bonds`和见票即付的`Bearer bonds`。

### 债券合约(Bond indenture/Trust deed)

 对债权人来说债券合约中比较需要关注的概念有`发行主体(Legal information)`、`还款来源(The source of repayment)`、`抵押品(Collaterals)`、`信用增级(Credit enhancements)`、`条款(Convenants)`、`税(Taxation)`。

#### 还款来源

| Type of bond   | Source of repayment                  |
| -------------- | ------------------------------------ |
| 超国家组织     | 借新债还旧债<br />各个成员国所缴会费 |
| 国债           | 税收收入<br />发行货币               |
| 地方政府       | 税收收入<br />基建收入(路桥费等)     |
| 公司债         | 运营收入                             |
| 资产证券化产品 | 标的资产                             |

#### 信用增级

信用增级的方法分为内部和外部，其中内部方法包括`过度抵押(Overcollateralization)`、`保证金(Reserved fund)`、`瀑布结构(Waterfall structure)`。外部方法主要是担保，例如`保险担保(Surety bond)`、`银行担保(Bank guarantee)`、`信用证(Letter of credit)`。外部方法最大的问题在于`第三方风险(third-party/counterparty risk)`，即来自于担保人本身的风险，处理该风险的一个可能方法是`Cash collateral account`，即将债券所借的一部分资金存入CCA账户以抵消一部分违约风险。

#### 条款

条款分为`肯定性条款(Affirmative covenants)`和`否定性条款(Negative convenants)`。

肯定性条款更多管理性质：要求按时按量偿还本金利息；要求遵守相关法律法规；要求保持现有业务不变；要求保持资产不变并支付税款等。肯定性条款不会带来额外成本，也不会有重大限制。

否定性条款往往有成本，且有重大限制：限制发行过多债务； 不应发行级别比已有债券更高的债券；之前没有被抵押的资产不能被作为抵押品；限制给股东发行过多股利；限制处置过多固定资产；限制过多风险投资；限制兼并收购。

###  债券息票支付

息票的支付有多种方式: `Credit-linked coupon bond`是票息会随发券人的信用评级变化的债券(信用越高票息越低)；`Pay-in-kind bond`是发券人以支付更多债券的方式支付票息的债券；`Index-linked bond`是票息与某种指标(如通货膨胀率等)联系的债券。例如美国的`Treasury Inflation-Protected Securities(TIPS)`是美国抗通胀国债，半年付息，其息票率不变，本金会根据通胀率调整，因此票息会有所变化，但本金不会因为通货紧缩而变少。 

### 含权债券

`Callable bond`指债券发行人有权将债券赎回，通常当市场利率下降时，发行人会倾向于将债券赎回以避免支付高于市场利率的债券票息，对债券发行人有利。该债券有一个`递延期(deferment period)`，递延期间发行人不能将债券赎回。 `Make-whole call provision`的赎回价格不固定，其赎回价格为未来现金流的现值，当利率不断下降时其赎回价格没有上限。

`Putable bond`指债券持有人有权将债券回售，通常当市场利率上升时，债券持有人会倾向于将债券回售以获得资金投资赚取更高的市场利率，对债券持有人有利。

`Convertible bond`可以将债券转换为普通股股票，对债券持有人有利。可转债的`转换价值(Conversion value)`是可转换的股票市值，`转换价格(Conversion price)`是债券可以转换为股票的股价，当转换价值大于转换价格时属于`Above parity`，应该转换；反之为`Below parity`，不应该转换。公司愿意发行可转债的原因是1.降低利息费用(转换后不再需要支付利息) 2.降低杠杆率(转换后债务转为资本)。

`Warrant`可以给予债券持有人以某价格购买股票的权利。 

## Reading 43 固收交易市场

### 债券投资方

- `中央银行(Central banks)`：中央银行通过买卖债券的公开市场操作实行其货币政策。
- `机构投资者(Institutional investors)`：包括保险公司、对冲基金等使用债券来匹配其债务。
- `主权财富基金(Sovereign wealth funds)`：目标为长线投资的国有投资基金。
- `散户(Retail investors)`：散户投资固收产品通常是追求稳定的价格和收入。

### 一级市场

- `公开发行(Public offering)`：与股票发行相似，有`包销(Underwritten offering)`、`代销(Best efforts offering)`、`拍卖(Auction)`和`上架注册(Shelf registration)`。包销风险由投行承担，代销投行主要挣取佣金，拍卖用于发现价格，上架注册特点是一次注册多次发行。
- `定向增发(Private placement)`：向某个符合资质的投资者单独发行债券。

### 二级市场

- `交易所市场(Exchange market)`：交易双方必须服从交易所规定交易。
- `柜台市场(OTC dealer market)`：充当dealer的角色提供流动性，是债券二级市场的主要交易场所。`买卖价差(bid-ask spread)`越大，流动性越差。

### 回购协议(Repurchase Agreement)

一间机构将债券以某个价格卖给另一间机构并约定未来某个时间将该债券以特定价格购回。`回购价格(Repurchase Price)`通常大于售价并且包含买家收取的利息。`Repo rate`是回购协议中的利率，当回购时间更短、抵押债券信用更高、抵押品交割给借出方、其他融资渠道利率低`(借出方风险更小)`时Repo rate都会更低。`Repo margin/haircut`是指计算卖价时对抵押品打的折扣率，也即债券市场价值与回购售价的差值，Repo margin与Repo rate相同，当借出方风险更小时，repo margin也会更小。

### 结构化产品(Structured financial instruments)

- `资本保护债券(Capital protected instruments)`：购买零息债券，然后将省下的资本投资购买期权，若期权可以收益则在到期日可以获得高于期初本金的收益，若期权无收益也至少可以在到期日获得债券本金。
- `收益增强工具(Yield enhancement instruments)`：以更高风险的代价获取更高的期望收益。`信用联结票据(Credit-linked Notes)`就是一种收益增强工具，信用评级越低的债券票息越高。
- `参与性工具(Participation instruments)`：这种债券使投资者可以参与到某个资产的回报率。`浮动利率债券(Floating-rate bonds)`就是一种参与性工具， 其票息率与LIBOR挂钩，该工具不提供本金保护。
- `带杠杆的工具(Leveraged instruments)`：用于放大收益的工具，可以以小博大。

## Reading 44 固收估值

对于固收产品的估值的常规手段就是对未来现金流求现值，其难点主要包括估计现金流，决定合适的折现率。
$$
P=\sum^n_{t=1}\frac{C_t}{(1+r)^t}+\frac{B}{(1+r)^n}
$$

### 债券价格与YTM的关系

如下图所示，当YTM与债券票息相等时债券价格等于票面价值，关系为YTM越高债券价格越低的凸函数。

![不含权债券价格随收益率YTM的变化关系](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20221027204210133.png)

### 债券价格与时间的关系

如下图所示，在债券到期日当天，债券价格与票面价值相等，其关系为随时间接近票面价值的凹函数，变化速度越来越快。

![时间越接近到期日，价格越接近票面价值](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20221027215200986.png)

### 用即期利率(Spot rate)定价

`即期利率(Spot rate)`指能直接在市场上观察到的利率，与之相对的`远期利率(Forward rate)`指从未来的某个时间点开始的利率。使用即期利率估值是因为不同时间用于折现的利率不相等，但最后算出的债券价格应该与用YTM计算的价格相等。

### 平价，应计利息，全价

`应计利息(Accrued interest)`是指交易日至前一个付息日应该给到卖方的票息；`净价(Clean price)`是市场上的债券报价；净价加上应计利息就是`全价(Full price/ dirty price)`。 

### 矩阵估值法(Matrix pricing)

矩阵估值法主要被用于对一些交易量不高的债券估值，因为交易量不够因此这些债券通常报价不准确。具体方法是基于其他交易量比较活跃的可比较债券，使用`线性插补法(Linear interpolation)`计算结果。

### 等效年化利率

计息频率不同的债券之间的回报率不能被直接比较，因此若要比较则需先使用下方公式将各个债券计息频率转化为相同然后比较其回报率：
$$
Effective\ annual\ rate =(1+\frac{YTM}{m})^m-1\\
(1+\frac{APR_m}{m})^m=(1+\frac{APR_n}{n})^n
$$

### 固定利率债券收益衡量

债券在遇到假期或周末时会延迟付出现金流，因此在实际操作中债券的现金流付出时间会被理论上的有所推迟。

`Street convention yield`是忽略假期或周末影响的收益率；`True yield`是需要考虑假期或周末影响的收益率；同一个债券的前者因少计算现金流递延的时间价值影响，收益率会大于后者。

`Current yield`是将一年中所有收入的票息除以债券价格计算；`Simple yield`是将所有票息收入加上其直线摊销的收益或损失后除以债券价格。

`Yield to call(put)`的计算方法与计算YTM的方法一样，不过需要将至到期日的计息次数换为赎回(回售)日的计息次数，将赎回(回售)价格换为到期价值。`yield to worst`是`yield to call(put)`和`YTM`中最差的收益。`option-adjusted yield`指去除可赎回(卖回)债券的期权影响后的市场期望回报率，可赎回债券的OAY小于YTM，可卖回债券的OAY大于YTM。

### 浮动利率债券收益衡量

浮动利率债券的票息率为`LIBOR+Quoted margin`，折现率为`LIBOR+Discount margin`。若折现率高于票息率则债券为折价债券；若折现率低于票息率则债券为溢价债券。

### 货币市场的债券收益率

`Discount yield`是`美国短期国债(U.S. Treasury bills)`和`商业票据(Commercial paper)`的回报率计算方法；`Add-on yield`是LIBOR、银行大额存单利率以及BEY的计算方法。二者差别在于分母为FV或PV，其公式分别为：
$$
DR = (\frac{Year}{Days}\times(\frac{FV-PV}{FV}))\\
AOR = (\frac{Year}{Days}\times(\frac{FV-PV}{PV}))
$$

### Forward rate v.s. Spot rate

`远期利率(forward rate)`与`即期利率(Spot rate)`的关系是一定时间内的即期利率折现与当时的即期利率组合折现的效果相同，即：
$$
(1+S_T)^T=(1+S_1)(1+1y1y)...(1+(T-1)y1y)
$$
使用远期利率为债券估值时可以将每期的现金流按当个现金流的一年期远期利率折现，即：
$$
bond\ value=\frac{CF_1}{1+S_1}+\frac{CF_2}{(1+S_1)(1+1y1y)}+\frac{CF_n}{(1+S_1)(1+1y1y)...(1+(T-1)y1y)}
$$

### Yield spread

固定收益中的`Yield spread`就是某只固收债券的收益率与美国短期国债收益率的溢价部分，即`Risk premium`。CFA考试中较为重要的几个spread有下面几个：

`G-spread`： 公司债YTM减国债YTM，需要期限一致。

`Zero-volatility spread`：公司债Spot rate减国债Spot rate，需要期限一致。该spread中包含有流动性风险，信用风险，以及对于相对于含权债券来说期权的风险补偿。

`Option-adjusted spread(OAS)`：OAS对比Z-spread剔除了期权的风险补偿，也即Z-spread相比OAS多包含了期权的风险溢价。因此同样的含权债券，Callable的Z-spread大于OAS，Putable的Z-spread小于OAS。

## Reading 45 Asset-Backed Security

### 资产证券化(Securitization)

以买方为例，当市场上的买房人无法全款买房时，他们会向商业银行贷款，银行作为贷出方会消耗流动性，这时银行可以将与买房人的贷款合同出售给SPE/SPV机构，发行Asset-Backed Security，然后卖出给投资者重新获取流动性。资产证券化的过程中的主要参与方有作为`Originator`的商业银行和作为`Issuer`的SPE/SPV。其他参与资产证券化的参与者都属于第三方。

资产证券化的最大好处是增加流动性，且降低或移除了最终投资者与房贷风险提供者之间的隔离。投资者可以直接投资房贷风险。

### 住房贷款(Residential Mortgage)

房贷债券分为`RMBS(住房贷款债券)`和`CMBS(商业地产债券)`两种，其中RMBS又分为MPS和CMO两种。美国房贷的特点是固定利率(fixed-rate)、等额等息(level payment)、完全摊销(fully amortized)。几个重要的概念如下：

- `Loan-to-value ratio(LTV)`是贷款金额与房价的比值，LTV越高贷款人风险越高。
- `Foreclosure`是追索权，若贷款是`Recourse loan`则有追索权，出售房产金额不够偿还未还贷款的部分可以向借方追索；`Nonrecourse loan`则没有追索权。
- `Strategic default`：当房价低于未还贷款部分时可能产生战略性违约的情况。
- `Interest-only mortgage`：某几年中不需要偿还本金的房贷。
- `Conforming mortgage`：符合一定承销标准的贷款，即优质贷款；其次还有风险更高的`Non-conforming mortgage`。

### Mortgage passthrough securities(抵押转手证券)

MPS即转手证券，所有贷款被放入一个池中并以份额的形式卖给所有投资者，没有风险分层。MPS属于债券产品，因此也有票息，被称为`Pass-through rate`。关于MPS需要计算的概念有：

- `Weighted average maturity(WAM)`：贷款池中每个贷款未还贷金额与整个贷款池的比为这个贷款的份额权重，将每份贷款的剩余还贷期数加权平均既是该池的WAM。
- `Weighted average coupon(WAC)`：与WAM相似，将贷款池中贷款的Mortgage rate加权平均就是贷款池的WAC。

#### Prepayment risk(提前偿还风险)

提前偿还风险主要包括`收缩风险(COntraction risk)`和`扩张风险(Extension risk)`，前者通常由于市场利率下降，贷款人可以从市场上获取更便宜的资金用于偿还房贷，因此会出现更多提前偿还，导致收缩风险。反之市场利率上升导致扩张风险。

#### Prepament rate(提前还款率)

`conditional prepayment rate(CPR)`是贷款池中的未还贷款被提前还款的年化率(年化提前还款率)。`Public Securities Association(PSA)`prepayment benchmark在100%的情况下首月CPR为0.2%，且以每个月上升0.2%的速度升至30个月时的6%，且维持CPR为6%至360个月。不同百分比的PSA在100%的情况下乘以变化的倍数，CPR越高提前还款率就越高。

另外每月的提前还款率为`single monthly mortality rate(SMM)`：
$$
SMM=\frac{本月提前还款}{月初本金余额-本月应还本金}\\
(1-CPR)=(1-SMM)^{12}
$$

### Collateralized mortgage obligations(担保式抵押契约)

CMO是将贷款池中的风险分层卖给不同投资者，有两种主要的契约形式：

#### Sequential Pay tranches

顾名思义，该类契约按顺序还款，假设将贷款池分为ABC三种风险池，还款现金流进入后的流程如下：

1. 先满足ABC的利息部分
2. 多余现金流先还A的本金，然后剩下的还B的现金流，以此类推
3. 若还款甚至无法满足ABC利息，利息部分先满足A再满足B并以此类推

C部分贷款还款速度最慢，拥有最大拓张风险，A部分拥有最大收缩风险。

#### Planned amortization class(PAC) CMO

PACCMO中分为PAC和Support两部分，其中PAC部分就是Sequential Pay的结构，而Support部分则是在偿还所有利息后先偿还该部分本金，或在现金流不足时不偿还该部分。因此Support部分同时拥有最大的扩张风险和收缩风险，而有Support支撑的PAC部分则有相对稳定的现金流，average life相对稳定。

### CMBS(商业地产贷款债券)

住房楼、写字楼、仓库、商场、酒店、医院等都属于商业地产范畴，商业地产都是有限责任主体，因此都是无追索权贷款(Non-recourse loans)，反映商业地产贷款风险的两个主要指标：
$$
Debt-to-service\ coverage\ ratio=\frac{net\ operating\ income}{debt\ service}\\
Loan-to-value\ ratio=\frac{current\ mortgage\ amount}{current\ appraised\ value}
$$
前者为租金与月供的比值，比值越高风险越低。后者为贷款与房价的比值，比值越高风险越高。

#### 赎回保护(Call protection)

债券购买者通常不希望发债人提前偿还债券，因此CMBS一般会设置赎回保护，用以减少提前偿还对债券持有人造成的风险。主要的手段有下面四种：

Prepayment lockout：合约规定禁止还款的时间段。

Defeasance：使用国债组合复制被提前还款的缺失现金流而对冲风险。

Prepayment penalty points：对提前还款收取额外的违约金。

Yield maintenance charges(make-whole charge)：提前还款需要将未来的现金流以一定值折现还款。

### Non-mortgage asset-backed securities

非房产债券的主要代表有`汽车贷款债券(Auto loan ABS)`和`信用卡应收账款债券(Credit Card Receivable ABS)`。需要注意的点有：

- 汽车贷款的提前偿还主要是汽车的二手出售和损毁的情况下，车主会将获得的现金流用于偿还车贷。
- 信用卡应收账款池中的现金流主要包括信用卡利息费用、信用卡费用和本金的提前偿还等。
- 信用卡应收账款债券的Lockout periods是指ABS持有人在锁定期内不能受到提前还款的本金和利息。

### Collateralized Debt Obligations

CDO是将垃圾债券收集成池后分层卖出给投资者的产品。分层后`最高的评级(Senior tranche)`至少要达到A级,中间BBB级但不低于B级的分层叫做`Mezzanie tranche`，最低的分层叫`Subordinate/equity tranche`，通常由投行自留。CDO与ABS的区别在于CDO需要资金经理主动管理。

CDO在卖出给投资者时是浮动利率债券，但池中的垃圾债券可能有些付出固定利率，因此CDO的基金经理通常需要使用利率Swap将固定利率交换为浮动利率，从而解决利率错配的风险问题。

## Reading 46 固收风险和收益

固收产品的主要收益来源有三个，`本金和票息收入`、`票息收入的再投资`、`债券到期前卖出的资本盈亏`。总收益是票息及其再投资收益和售价的未来总价值。使用总收益可以计算年化持有期间收益率：
$$
Annualized\ holding\ period\ return=(\frac{total\ return}{bond\ price})^\frac{1}{n}-1
$$

### 利率风险

广义的利率风险主要是`票息的再投资风险`和`市场价格变化风险`两种，而对债券来说狭义的利率风险主要是后者，即利率变化对债券价格的影响。利率变化对这两者的影响是可以一定程度地相互抵消的，在短期时利率变化的价格风险影响会大于再投资风险(利率上升导致损失)，在长期时则是相反再投资风险占据主导(利率上升导致收益)。

#### Duration Gap

要计算Duration Gap首先要知道`麦考利久期(Macaulay Duration)`，麦考利久期就是以折现现金流作为权重的现金流平均回流时间。而Duration Gap = Macaulay Duration - Investment horizon。

当Duration Gap大于0时(即麦考利久期大于投资期限时)，投资是属于短期，利率的价格风险大于再投资风险；Duration Gap等于0时，利率变化的两种风险刚好抵消；Duration Gap小于0时，投资属于长期，再投资风险大于价格风险。

#### Modified duration 

`修正久期(Modified duration)`计算债券价格对利率变化的敏感程度：
$$
Modified\ duration=\frac{Macaulay\ duration}{1+periodic\ market\ yield}
$$
由于修正久期只考虑债券价格与利率变化的线性变化关系，因此在利率变化较小的时候比较准确。

#### Effective duration

当利率减少或增加固定的值时导致的债券价格增加和减少的区别就是Effective duration，有效久期是衡量含权债券最有效的久期：
$$
Effective\ duration=\frac{V_--V_+}{2\times V_0\times \Delta curve}
$$

#### Dollar duration

当利率变化1%时，具体的债券价格变化：
$$
Dollar\ duration=Modified\ duration\times Price
$$

###  影响久期的特殊因素

- 债券期限越长，久期越大
- 票息越低，久期越大
- 市场利率越低，久期越大
- 含权债券的久期更短

### 组合久期

计算债券投资组合的久期主要有两种方法：

1. 将组合现金流直接加权平均计算麦考利久期，缺点是实践中难以确定现金流，因此难以在实践中应用。
2. 将组合中不同的债券按`市值(而不是价格)`作为权重计算他们的久期的加权平均数。

### 凸性(Convexity)

久期(Duration)是债券价格对利率的一阶导，而凸性则是价格对利率的二阶导，也就是久期随利率变化的敏感度。凸性部分需要掌握的公式有两个，其一是凸性的计算公式：
$$
effective\ convexity=\frac{V_-+V_--2V_0}{(\Delta curve)^2V_0}
$$
其二则是凸性调整后的久期：
$$
\frac{\Delta P}{P}=[-MD\times (\Delta y)]+[0.5\times Conv\times (\Delta y)^2]
$$

#### 含权债券的凸性

对于Callable bond来说，利率下降会导致债券价格接近但不会超过call price。对于Putable bond来说，利率上升会使债券价格不断接近但不会低于Put price的价格底。

## Reading 47 信用分析基础

信用风险是指当债券发行人无法足额或及时支付利息或本金的风险，一般分为`违约风险(Default risk)`和`损失严重性(Loss severity)`两个维度，两个维度相乘可以得到`预期损失(Expected Loss)`，其中$1-损失严重性=Recovery\ rate$。另外债券的`Spread risk`也会随着发行人的信用降级而增加。

### 求偿顺序(Seniority ranking)

 `有抵押品债券(Secured bond)`优先度高于`无抵押品债券(Unsecured bond)`，同等级的债权人都同等对待，不管这些债券的其他性质如何(Pari Passu)。

### 评级

评级机构会对`债券发行人评级(Issuer credit rating)`、`产品评级(Issue rating)`。同一发行人发行的产品可能有不同的评级，这种现象叫做`Notching`，越差的发行人出现notching现象的可能性越高(发行人发行的`Senior unsecured debt`的评级通常与公司评级相同)。

`交叉违约条款(Corss default provision)`下，当债券发行人的某个产品发生违约事件时，该发行人发行的其他产品债权人可以发起求偿。`结构性从属(Structural suborination)`条款规定子公司在付齐应付的的债券利息和本金前不可以向母公司输送利润。

有四个理由投资者不能只依靠信用评级来衡量风险：

1. 信用评级是动态变化的。
2. 评级机构不是永远不会犯错的。
3. 有一些突然事件导致的风险(Idiosyncratic or event risk)是很难被信用评级捕捉的。
4. 评级通常滞后于市场。

#### 4C法评级

评级机构通常根据`能力(Capacity)`、`抵押品(Collateral)`、`条款(Covenants)`和`意愿(Character)`四个方面对债券进行评级。

- 能力：使用`Porter's five force model`进行行业分析，行业基本面(周期或非周期、行业成长前景、公布的行业数据等)，公司基本面(竞争位置、经营历史、管理层策略和执行、财务比率等)，发行人流动性分析(现金、营运资金、经营性现金流、银行授信额度、近期是否有大量资本支出等)。
- 抵押品：`专利权(Patents)`是高质量的无形资产；`声誉(Goodwill)`不是高质量无形资产；折旧费用较高标志着资产利用率较低；股票市值低于公司账面价值说明公司资产质量较低；人力资源较难估计。
- 条款：主要关于肯定性条款和否定性条款的规定和应用。
- 意愿：公司战略的可靠性；业绩记录；会计政策和税务政策；欺骗和欺诈记录；对债权人的历史记录。

[第24篇]
