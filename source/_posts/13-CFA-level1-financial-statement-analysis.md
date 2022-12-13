---
title: "[金融分析] CFA一级《财务报表分析》学习笔记"
date: 2022-04-06 00:36:42
tags: [CFA一级,财务报表分析, 日常学习]
categories: 金融分析
description: "[第13篇] 本篇将包括CFA一级考试中财务报表分析(Financial Statement Analysis)科目的学习笔记。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/CFA.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/13-CFA-level1-financial-statement-analysis.jpg
katex: true
---

# 概览

财务报表分析一共包括4个Session的12个Reading，各个Reading的内容如下表：

<table>
    <tr>
        <th>Sessions</th>
        <th>Readings</th>
        <th>Contents</th>
    </tr>
    <tr>
        <td rowspan="2">SS6</td>
        <td>R19</td>
        <td>Introduction to Financial  Statement Analysis</td>
    </tr>
    <tr>
        <td>R20</td>
        <td>Financial Reporting Standards</td>
    </tr>
    <tr>
        <td rowspan="4">SS7</td>
        <td>R21</td>
        <td>Understanding the I/S</td>
    </tr>
    <tr>
        <td>R22</td>
        <td>Understanding the B/S</td>
    </tr>
    <tr>
        <td>R23</td>
        <td>Understanding the C/F</td>
    </tr>
    <tr>
        <td>R24</td>
        <td>Financial Analysis Techniques</td>
    </tr>
    <tr>
        <td rowspan="4">SS8</td>
        <td>R25</td>
        <td>Inventories</td>
    </tr>
    <tr>
        <td>R26</td>
        <td>Long-Lived Assets</td>
    </tr>
    <tr>
        <td>R27</td>
        <td>Income Taxes</td>
    </tr>
    <tr>
        <td>R28</td>
        <td>Long-Term Liabilities and Leases</td>
    </tr>
    <tr>
        <td rowspan="2">SS9</td>
        <td>R29</td>
        <td>Financial Reporting Quality</td>
    </tr>
    <tr>
        <td>R30</td>
        <td>Financial Statement Analysis: Applications</td>
    </tr>
</table>

其中该科目的重要考点主要集中在Session7和Session8,占考点总数的80-90%。从下面开始我会把每个Reading的知识点和重要考点一一整理记录下来。

# Session 6

本Session中主要涉及的是财务报表分析的一些概况型知识，其中R19主要介绍公司财务各财务各报表的大致作用以及特性，财务报表分析可能关注的信息类型等。R20主要介绍财务报告标准。

## Reading 19 介绍财务报表分析

### 财务报表分析的作用

公司编制财务报表用来向其投资者，债权人以及其他相关方展示其财务状况。而财务报表分析则是利用公司财务报表中的信息，以及其他相关信息做决策。

### 财务报表内容

一般公司的财务报表有五张，其中最重要的三张分别是：

`Balance sheet(B/S):` 该报表主要报告某个`时间点`公司的`财务状况(financial position)`。该报表有3个主要`elements`，分别为`Assets(资产)`,`Liabilities(负债)`和`Owner's equity(所有者权益)`。资产为公司所有的所有资源，负债为债权人所有的资金，所有者权益为股东所有的资金。该报表为`Accrual basis(权责发生制)`。会计恒等式：
$$
Asset = Liabilities + Owner' Equity
$$
`Income statement(I/S):`该报表主要报告公司在`一段时间内`的的财务表现。其中`主要elements`包括`Revenue(收入)`，`Expenses(支出)`和`Other income(其他收入)`。该报表为`Accrual basis(权责发生制)`。

`Cash flow statement(C/F):`该报表主要报告公司在`一段时间内`的现金收入与支付。各个`Cashflow(现金流)`被划分为`Operating cash flows`(主要指与公司正常经营相关的现金流), `Investing cash flows`(主要指买卖固定资产或参与其他公司投资相关的现金流)或者`Financing cash flows`(主要指与金融行为相关如发行或回收公司债务或权益证券也包括付给股东的分红等现金流)。该报表为`Cash basis(收付实现制)`。

而另外两张财务报表分别是：

`The statement of comprehensive income:`该报表主要报告`Other comprehensive income(OCI)`的变动，`OCI`指根据会计准则的4项不计入`I/S`中而直接计入`B/S`的`equity`中的收入。
$$
Comprehensive\ income = Net\ Income + Other\ comprehensive\ income
$$
`The statement of changes in equity:`该报表主要报告`一段时间内`equity的变动来源和数额。
$$
Equity = Capital + Retained\ Earnings + OCI
$$


### 主要报表间关系

公司的三张主要报表之间各有关联，每张表中有数字变动都会导致另外两张表中的数字相应变动，他们之间的关系两两来看。

#### B/S与I/S关系

`Income statement`的主要信息为`Revenue - Expense = Net Income`，而公司每年的`Net Income`除了付出的`Dividend`，剩下的部分要被计入`Balance sheet`中的`Equity`的`Retained Earnings(留存收益)`科目中。即 `Net income - Dividend = Retained Earnings`。

#### B/S与C/F关系

`Cash flow statement`中的主要信息为`Total CF = Operating CF + Investing CF + Financing CF`,而其中的Total CF则是当年现金流的净值，反映在`Balance sheet`中的`Asset`中的`Cash`科目中。即`年末Cash - 年初Cash = Total CF`。

#### I/S与C/F关系

Income statement 与 Cash flow statement的主要差别在于非现金交易，在`Income statement`的`Net income`中减去当年`非现金收入`并加上当年`非现金支出`便可以得到当年的`Total CF`。即 `Net income - Non-cash revenue + Non-cash Expense = Total Cash flow`。(疑问，receivable和payable属于noncash?)

### Elements(元素)与Accounts(科目)

财务报表中`Elements(元素)`为主要分类，分为资产，负债，所有者权益，收入，支出。而每一个Elements中都有不同的`Accounts(科目)`。例如`资产元素`中有现金，固定资产，无形资产等科目。`负债元素`中有应付账款，银行借款等科目。

#### Contra Accounts

`Contra accounts(备抵科目)`为资产科目，其特征为`负数`，该科目用来抵减资产金额。例如：应收账款的坏账，固定资产的减值等。

#### Measurement of financial elements

- `Historical cost(历史成本):` 用来计量`短期资产`(变现时间少于一年)，资产价值等于付出的成本。
- `Amortized cost(摊余成本):` 用来计量长期资产(变现时间大于一年)，资产价值以`摊销(amortization)`，`折旧(depreciation)`，`减值(impairment)`，`耗减(depletion)`后的历史成本记账。
- `Fair value(公允价值):`一般用来计算金融资产，需要有活跃报价。以两个`无信息差(knowledgeable)`，`自愿(willing)`，`非关联(arm's length)`的交易双方同意交易的价格计量。

### Other Relevant information(其他相关信息)

除了公司财务报表以外，金融分析师还需要从其他渠道获取补充信息，主要有六种，分别为`Financial statement notes(footnotes)`，`Management's commentary(MD&A)`，`Proxy statement`, `Interim reports`, `Interim reports`,  `Earnings announcement`和`External sources`。其中考得比较多的是`footnote, MD&A和Proxy`。

`Financial statement notes：`用来解释说明财务报表中的细节， 如会计方法，假设，估计，固定资产的折旧年限等等，如果需要了解财务报表中数字细节就要看这个财报附注。

`Management's commentary：`财务报表只能反映过去无法反映将来，`MD&A`是公司管理层对公司经营状况的解读，其中会包含公司经营目标，过去表现，重要事件，未来可能有的不确定性以及表外事项等。

`Proxy statements：`临时股东大会通告出现说明公司出现需要临时召集股东投票的重大事件，事项可能包括调整管理层薪资，董事会成员选举，重大股权激励等等。

`Interim report：`中期报告是未经审计的半年或季度财务报告，可以提供更高时效性的公司财务信息。

`Earning announcements：`业绩预告是比中期报告有更高时效性的公司表现报告，但也是未经审计可能调整。

`External sources：`分析师还需要从公司外部获取相关信息，可能来源包括研究报告，整体经济状况，行业状况，相关新闻等。

### Audit(审计)

#### 审计原因

公司财务报告需要审计的原因是`Principal-agent relationship`，也即`委托代理冲突`。其根本原因在于现代公司治理体系下公司所有者与公司管理者分治导致公司管理者可能为自己利益欺瞒公司所有者(即股东)。因此除董事会监督外，还需要由外部审计对公司管理者出具的公司财务报告进行审计。

#### 审计概念

1. 审计本身提供对公司财务报表的`独立`审核，审计师不能与公司内部关联。
2. 审计师对公司财务报告的正确性提供`合理`保证(非100%)，保证公司财报没有`重大`误差。
3. 审计师除了对财报进行审计外还对公司内控程序进行审计，以此判定财报数字的可信度。

#### 审计Opinion

审计师完成财报审计后提供审计意见，共有4种`意见(Opinions)`:

`Unqualified opinion：`无保留意见，表示公司财务报表没有重大误差。

`Qualified opinion：`保留意见，表示公司财务报表中有个别性质不严重的偏差。

`Adverse opinion：`否定意见，表示公司财务报表中存在重大或大量误差。

`Disclaimer of opinion：`无法表示意见，表示因审计师活动受限以致无法出具审计意见。

### Accounting Equation(会计恒等式)

$$
\begin{cases}
Asset = Liability + Equity\\
Equity = Capital + Retained Earnings + OCI\\
Retained Earnings_{End} = Retained\ Earning_{Begin}+Net\ Income - Dividend\\
Net\ Income = Revenue - Expense
\end{cases}\hspace{5cm}
$$

$$\Darr\hspace{12cm}$$
$$
\begin{align*}
Asset&=Liability\\
&+Contributed Capital\\
&+Retained\ Earnings_{Begin}\\
&+Revenue\\
&-Expenses\\
&-Dividend declared\\
&+OCI
\end{align*}\hspace{10cm}
$$

### Accrual Accounting(权责发生制)

当每笔交易都是现款现货交易时，权责发生制与收付实现制记账结果一致，因此当收发货时间与收付款时间不一致时就会产生差异，不同情况下权责发生制的记账方式如下：

#### Cash received in advance

交易未完成，现金已收到：已收到现金，因此在`资产`中记入一笔`现金`，同时在`负债`中计入`Unearned revenue(预收账款)`。

#### Cash paid in advance

交易未完成，现金已支付：已支付现金，因此在`资产`中扣除一笔`现金`，同时在`资产`中扣去`Prepaid expense(预付账款)`。

#### Cash received in arrears

交易已完成，现金未收到：已完成交易因此`收入`增加一笔`Accrued revenue(应计收入)`，反映在`Equity`中。同时在资产中计入`Account Receivable(应收账款)`。

#### Cash paid in arrears

交易已完成，现金未支付：已完成交易，因此在`支出`扣除一笔`Accrued expense(应计费用)`，反映在`Equity`中。同时在负债中计入`Account Payable(应付账款)`。

## Reading 20 财务报表标准

### 合格报表的六个特点(Characteristics)

#### 2个基本特征

两个基本特征是每个合格报表都需要满足的：

`Relevance(相关性)：`公司在财务报表上披露的信息必须与投资者的投资决策相关。相关的信息会帮助财务报表的使用者评估公司过去，现在以及将来可能发生的事件，有影响投资决策的可能性。

`Faithful representation(信息正式性)：`信息需要`完整(Complete)`,`中性(Neutral)`并且`没有错误(free from error)`。符合这三个要件我们就可以说报表是faithfully presented。

#### 4个增强特征

4个增强特征不一定需要满足，但可以增强2个基本特征：

`Comparability(可比性)：`财务报表展示方法和口径在不同公司和不同时间两个维度上都是一致的。

`Verifiability(可验证性)：`不同的观察者用相同的方法读财报可以得出相似的结论。

`Timeliness(及时性)：`报表信息需要被及时披露，上市公司法定至少每年披露一次。

`Understandability(可理解性)：`只需要有基本的商业和财务知识就可以读懂，不能太过晦涩。

### 会计准则的十个要求(General features)

会计准则对报表编制的十个基本要求如下：

`Going concern basis(持续经营)：` 财务报表的编制需要在假设公司会持续长期经营的前提下。

`Accrual basis of accounting(权责发生制)：`除现金流表外，所有财务报表均以权责发生制的基础编制。

`Fair presentation(真实表达)：`财务报表披露的信息不能有重大错误，需要真实表达。

`Consistency(一致性)：`不同时间使用的会计方法需要一致。

`Materiality(重大性)：`财务报表在对可能影响投资者决策的信息上要没有错误或遗漏。

`Comparative information(可比性)：`当期财务报表中至少应当提供所有列报项目上一个可比会计期间的比较数据。

`Aggregation(汇总)：`财务报表中类似的项目要被汇总，不同项目要被分开。

`No offsetting(不可抵消)：`不同项目中相反的科目数额不可以直接抵消。

`Reporting frequency(及时性)：`财务报表需要至少每年报告。

`Classified balance sheet(资产负债分类)：`报表中需要根据资产和负债的流动性的不同将其分类为`短期(current)`和`长期(non-current)`。

`Minimum information(最少信息)： `财务报表及其附注中有其规定的最少需要披露的信息。

### IFRS(国际会计准则)与US GAAP(美国会计准则)的主要区别

US GAAP倾向于使用历史成本估计价值，而IFRS倾向于使用公允价值估计价值。另外，IFRS为`Principles-based approach`,即以宽泛的框架为准则，对每家公司会计的具体要求较少。而US GAAP为`Rules-based approach`，对准则的指定较为精细而具体。

# Session 7

本节中主要分别介绍公司主要的三大财务报表，以及分析的具体方法。其中R21-R23分别介绍利润表，资产负债表和现金流表，R24主要介绍财务分析技术。

## Reading 21 理解利润表

### 利润表的两种列式方法

通常利润表有两种记账列式方式，一般会计准则规定的是`By function格式(按会计科目列式，也称Multi-step format)`，也有按发生的费用的性质列式的`By Nature格式(按费用性质列式，也称Single-step format)`，通常上市公司发布的利润表都会按会计科目列式，但各项费用的性质一般会列在附注中。需要注意一点的是利润表中第一项的Revenue实际上是Net Revenue，也就是去掉预计商品`退货(Returns)`和`违约(Allowances)`的实际成交的收入。

![image-20220415193138021](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220415193138021.png)

#### 变更会计方法

当需要变更会计方法时，若变更的是会计政策(Accounting Principle),可能需要`追溯调整(retrospective)`。若变更的是`会计估计(Accounting estimate)`，`不需要追溯调整(Prospective)`。若发生错误，必须追溯更改。

#### 少数股东权益(Non Controlling Interest/Minority Interest)

被公司持股超过51%的公司被称为`绝对控股(Majority shareholder)`，被绝对控股的公司属于控股公司的子公司，其财务报表需要与母公司合并，其中不属于母公司股份的利润在利润表中被列为`少数股东权益`扣除。

### 第三种列式方式

如上图中所示，除了上节提到的两种记账方式，还有另一种格式会在By function格式的基础上，在EBT后加上增加两个利于投资者计算公司正常经营能力的`非经常性项目(Nonrecurring Items)`和`中止经营项目(Discontinued operations)`。

#### 非经常性项目

`非经常性项目`通常在`税前`计算，用来计算售卖资产或部分业务所得利润等不常发生的项目，去掉这部分利润后可以反映公司真实的经营情况`(Normalization adjustment)`。

#### 中止经营项目

`中止经营项目`通常在`税后`计算，用来计算中止业务时的`淡出期(phase out period)`中，要被中止的这块业务产生的利润，去掉这部分利润可以反映公司未来的经营情况`(Pro-forma adjustment)`。

### 收入与成本确认(Revenue & Expense recognition)

#### 收入确认

利润表的编制基于权责发生制，因此仅在交易完成后才会确认收入。作为卖方要确认收入需要满足以下几点：

- 买卖双方需要存在买卖合同。
- 合同中要明确规定买卖双方各自的`责任与义务(performance obligations)`，用以确认合同是否已经履行。
- 合同要明确交易价格。
- 合同中规定的交易价格可以被按照责任义务履行的进度分配。
- 当双方都已满足合同规定的各自义务时可以确认收入。

  对于最后一点双方是否满足合同规定的义务的判断，会计准则规定当客户实际获得资产的控制权时交易完成。需满足以下任意一点：

- 当卖方有权要求卖方付款时。
- 买方已经获得法律上的所有权认可。
- 买方已经实质上拥有资产。
- 与商品相关的风险与收益已经从卖方转移给买方。(使用较多)
- 买方已经接受资产。

#### 成本确认

 根据Matching principle(配比原则)，与收入直接相关的成本要在同一时间段内确认。当合同期限大于一年，需要按时间分配收入时，可以按成本在不同时间的分配计算业务进度，并以进度百分比计算相应收入。

#### 毛净收入（Gross and net reporting of revenue）

 对于代理行业而言，其直接从客户手中收取的费用被称为`毛收入(Gross revenue)`, 毛收入与其成本之间的差值为其`净收入(Net revenue)`。US GAAP准则规定公司仅在同时满足以下四点时可以以毛收入记收入(基本不可能满足):

- 公司必须是合同的主要义务方(primary obligor)。
- 公司可以独立选择其供应商。
- 公司承担存货和信用风险。
- 公司具有实际定价权。

### Earnings per share(每股净利润)

每股净利润简称EPS，一般需要了解了两个概念分别为`Basic EPS(基本每股收益)`和`Diluted EPS(稀释每股收益)`。

#### Basic EPS

`基本每股收益`为公司净利润减去优先股红利后，以该会计核算时间中的加权平均普通股数量平分的利润。以下式表示：
$$
Basic\ EPS = \frac{NI-div_{preferred\ stock}}{weighted\ average\ number\ of\ common\ shares\ outstanding}
$$
由于会计核算时间段内普通股数量可能发生变化，因此需要计算该段时间内的加权平均普通股数量。普通股数量变化的四种情况及各自的计算方法如下表：

| 事件                     | 数量变化 | 计算方法     | 举例                       |
| ------------------------ | -------- | ------------ | -------------------------- |
| 股票增发(new issue)      | 增加     | 按时间加权   | 存在时间占比x增发数量      |
| 股票回购(repurchase)     | 减少     | 按时间加权   | 存在时间占比x回购数量      |
| 股票激励(stock dividend) | 增加     | 直接追溯调整 | 事件发生前所有股数按比增加 |
| 股票分割(stock split)    | 增加     | 直接追溯调整 | 事件发生前所有股数翻倍     |

#### Diluted EPS

 `稀释后每股收益`为公司所有`可转债(Convertible debt)`，`可转换优先股(Convertible preferred stock)`，和`股票期权(Stock option/warrant)`全部转换为公司普通股后的每股收益。以下式表示：
$$
Diluted EPS = \frac{adjusted\ income\ available\ for\ common\ shares}{weighted\ avg.\ comon\ \&\ potential\ common\ shares\ out}\\
=\frac{[NI-div_{preferred}]+[div_{convrtible\ prederred}]+[interest_{convertible\ debt}](1-t)}{WACSO+[shares_{conversion\ of\ conv.\ pfd.\ shares}]+[shares_{conversion\ of\ conv.\ debt}]+[shares_{insuable\ from\ stock\ opt.}]}
$$
上方公式实际就是在基本每股收益的计算式中分别在分子与分母中加上三种可转证券转换为普通股后的影响：

- `可转债(Convertible debt):`由于可转债在转换之前为债权，因此公司要付出利息，因此可转债转换为普通股后要将本需要付出的利息`扣税后`加回分子，并将转换的普通股数量加入分母。
- `可转换优先股(Convertible preferred stock)：`由于优先股有固定的分红，因此可转换优先股转换为普通股后要将本需扣除的优先股分红加回分子，并将转换的普通股数量加入分母。
- `股票期权(Stock option/warrant)：`假设公司发行的看涨期权(Call option)被行权，公司将期权持有者用于以合约价格购买股票的收入假设以市场全年均价买回后，仍然不足的部分以增发股数加入分母。

#### Anti-dilution

由于可转债和可转换优先股对基本每股收益的影响不一定是负面的，可能由于其转换导致每股净利润增加，这种情况叫做`反稀释(anti-dilution)`。在这种情况下基本每股收益才是稀释后每股收益，即稀释后每股收益为`转换后每股收益`与`基本每股收益`中`较小`者。

### Common-size I/S

出于对公司各项收入成本利润占比结构情况的直观表现，我们有时会使用各项目占Revenue的百分比的格式展示利润表。

### Comprehensive Income(综合收益)

综合收益包括留存收益和其他综合收益，其中其他综合收益是四项由会计准则规定不计入利润表而直接反映在资产负债表的所有者权益项中。这四项被国际会计准则和美国会计准则认定为其他综合收益的项目分别是：

- Foreign currency translation gain/losses(外币报表折算产生的外汇损益)
- Adjustments for minimum pension liability(精算假设变动导致最小养老金负债的调整)
- Unrealized G/L on available-for-sale securities(可供出售金融资产价格波动导致的浮盈浮亏 )
- Unrealized G/L from cash flow hedging derivatives(对冲用金融衍生品价格波动导致的浮盈浮亏)

最后在美国会计准则之外，`国际会计准则`还规定了`第五项`不计入利润表的其他综合收益：

-  使用重估模型计算长期资产价值时，其公允价值与历史成本的差异。若有`收益(Gain)`则计入资产负债表中的其他综合收益科目，若有`损失(Loss)`则计入利润表。

## Reading 22 理解资产负债表

在`Reading22`中的资产负债表部分较为简单，关于资产负债表的主要的较难的内容会在`Session8`中详细覆盖。

### 资产负债表的格式和组成部分

- `资产(Assets)`反映公司资金去向，资产的主要定义是会为公司提供`未来经济利益的流入(probable future economic benefits)`。包括`Current and Non-current assets（短期和长期资产）`。
- `负债(Liabilities)`为公司债权人所有资金，负债的主要定义是会导致公司`未来经济利益的流出(an outflow of economic benefits in the future)`。包括`Current and Non-current liabilities（短期和长期负债）`。
- 所有者权益(Stockholders' equity)是属于公司股东的资金，权益的主要定义是公司资产减去负债后的`剩余权益(residual interest)`。

资产负债表主要对投资者提供的信息是公司的`流动性(liquidity)`，`偿债能力(solvency)`与`对股东利润分配的能力(ability to make distribution to shareholders)`。资产负债表在`IFRS`和`US GAAP`准则下都是`分类表(Classified balance sheet)`，即将资产负债分为短期与长期，用以衡量公司流动性。`IFRS`准则下资产负债表为`Liquidity-based presentation`，即将各科目按流动性从高到低排列。

#### 资产

<table>
    <!--标题-->
    <tr>
        <th>大类</th>
        <th>常见科目</th>
        <th>解释</th>
    </tr>
    <!--Current assets-->
    <tr>
        <td rowspan="6">Current Assets</td>
        <td>Cash and equivalents</td>
        <td>现金和现金等价物，通常无风险变现时间在30天以内的固收证券可以作为现金等价物。</td>
    </tr>
    <tr>
        <td>Accounts receivable</td>
        <td>应收账款，该科目需要扣除坏账准备(bad debt allowance)，以帐龄计算。</td>
    </tr>
    <tr>
        <td>Inventory</td>
        <td>存货，对制造业公司来说该部分是最重要科目，分Raw materials, work-in-progress和finish good三个部分核算，具体会在Session8中详解。</td>
    </tr>
    <tr>
        <td>Prepaid expenses</td>
        <td>预付账款，已经付了钱但还没有收到货，预计未来某天会收到该数额的货物。</td>
    </tr>
    <tr>
        <td>Short-term investments</td>
        <td>短期投资，变现时间少于一年的金融资产</td>
    </tr>
    <tr>
        <td>Other current assets</td>
        <td>其他变现时间少于一年的资产</td>
    </tr>
    <!--Non current assets-->
    <tr>
        <td rowspan="5">Non Current Assets</td>
        <td>Property, Plant and Equipment(PP&E)</td>
        <td>固定资产，主要涉及内容是折旧计算，例如直线法，加速法使用cost model或revaluation model等方式折旧等。具体会在Session8中详解。</td>
    </tr>
        <tr>
        <td>Intanible assets</td>
        <td>无形资产，例如专利等，计算方法与固定资产非常相似，但计算内容是摊销(amortization)，没有残值。</td>
    </tr>
    <tr>
        <td>Long-term investments</td>
        <td>长期投资，变现时间大于一年的金融资产</td>
    </tr>
    <tr>
        <td>Deferred tax assets</td>
        <td>递延所得税资产，由于税收以现金收付制计算，而资产负债表以权责发生制计算，因此税收与资产负债表存在差异，此科目用以记录该部分差值。</td>
    </tr>
    <tr>
        <td>Pension assets</td>
        <td>养老金资产，按美国DB plan计算，员工每工作一年就按其退休前公司的1%给付其养老金，该科目是 按精算假设计算未来可能给付员工的养老准备金数额。</td>
    </tr>
</table>

#### 负债

<table>
    <!--标题-->
    <tr>
        <th>大类</th>
        <th>常见科目</th>
        <th>解释</th>
    </tr>
    <!--Current liabilities-->
    <tr>
        <td rowspan="6">Current Liabilities</td>
        <td>Bank overdraft</td>
        <td>透支，向银行的短期借款</td>
    </tr>
    <tr>
        <td>Accounts payable</td>
        <td>应付账款，已收到货物但还未付款</td>
    </tr>
    <tr>
        <td>Accrued expenses</td>
        <td>预提费用，与应付账款类似科目，是还未付款的，但预提费用不是与产品本身成本相关，而是管理费用。</td>
    </tr>
    <tr>
        <td>Unearned revenue</td>
        <td>预收账款，已收到货款还未交货，因此欠交易方货物</td>
    </tr>
    <tr>
        <td>The current portion of long-term debt</td>
        <td>当期偿还的长期债务，指长期债务中在当一年内需要偿还的金额</td>
    </tr>
    <tr>
        <td>Current taxes payable</td>
        <td>应交税金， 当年需要缴付的税金 </td>
    </tr>
    <!--Non current liabilities-->
    <tr>
        <td rowspan="5">Non Current Liabilities</td>
        <td>Notes payable</td>
        <td>应付债券(1-10年)</td>
    </tr>
    <tr>
        <td>Bonds payable</td>
        <td>应付债券(10年以上)</td>
    </tr>
    <tr>
        <td>Capital/Financial lease obligations</td>
        <td>应付融资租赁款</td>
    </tr>
    <tr>
        <td>Pension liabilities</td>
        <td>养老金负债，与养老金资产类似，需要缴付的部分就是养老金负债。</td>
    </tr>
    <tr>
        <td>Deferred tax liabilities</td>
        <td>递延所得税负债，与递延所得税资产类似，税收与资产负债表差异部分记账。</td>
    </tr>
</table>

#### 所有者权益

<table>
    <!--标题-->
    <tr>
        <th>常见科目</th>
        <th>解释</th>
    </tr>
    <tr>
        <td>Capital</td>
        <td>股本面值，发售的股票的面值部分。</td>
    </tr>
    <tr>
        <td>Additional paid-in-capital</td>
        <td>股本溢价，发售的股票的溢价部分，与股本面值的和为实收股本。</td>
    </tr>
    <tr>
        <td>Treasury stock</td>
        <td>库存股，公司已经回购但还未注销的部分，一般为负数，用于抵减股本。</td>
    </tr>
    <tr>
        <td>Retained earnings</td>
        <td>留存收益，每年的净利润扣除股利后为当年留存收益的变化值。</td>
    </tr>
    <tr>
        <td>Accumulated other comprehensive income</td>
        <td>其他综合收益，该部分为不计入利润表的4+1项特殊收入Comprehensive Income(综合收益)。</td>
    </tr>
    <tr>
        <td>Minority interest</td>
        <td>子公司资产负债表中按控股比例不属于控股公司的部分。</td>
    </tr>
</table>

### Common size B/S

与`Common size I/S`相似，为以比例形式展示资产负债表，将资产负债表中每个数字除以总资产。

### 金融资产(Financial instruments)

 <table>
    <!--标题-->
    <tr>
        <th colspan="2">USGAAP</th>
        <th colspan="2">IFRS</th>
    </tr>
    <tr>
        <td>Held-to-maturity</td>
        <td>持有至到期</td>
        <td>Amortized cost(AC)</td>
        <td>以摊余成本进行计量的金融资产</td>
    </tr>
    <tr>
        <td>Trading security</td>
        <td>交易性金融资产</td>
        <td>Fair value through profit or loss (FVTPL)</td>
        <td>以公允价值计量且变动计入当期损益的金融资产</td>
    </tr>
    <tr>
        <td>Available-for-sale</td>
        <td>可供出售金融资产</td>
        <td>Fair value through other comprehensive income (FVTOCI)</td>
        <td>以公允价值计量且变动计入其他综合收益的金融资产</td>
    </tr>
</table>

####  Held-to-maturity

持有至到期的金融资产通常为债券，债券的摊销核算方法如下：

1. 首先把债券每年的现金流和本金按无风险利率折价为现值。
2. 然后每年`年末的资产价值`为为当年`年初的现值`+`该现值的无风险利息收益`-`票面利息`。
3. 当年的`摊销费用`为`年末价值`-`年初价值`。

其中`年末及年初的资产价值`计入`资产负债表`，`无风险利息收益`计入`利润表`，`票面利息`计入`现金流表`。

#### Trading security

交易性资产为公司以短线交易为目的而持有的金融资产，该类资产的`浮盈浮亏(Unrealized G/L)`计入`利润表`。

#### Available-for-sale

交易性金融资产在IFRS准则下，即可以是债券投资，也可以是股票投资。但在US GAAP准则下可供出售的金融资产只可能是债券。该资产以公允价值计量且变动计入`资产负债表的其他综合收益`。

## Reading 23 理解现金流量表

现金流量表通常用于反映公司在会计年度中支付和受到的现金，且其现金在不同活动中的组成结构等，所有非现金活动均不体现在现金流量表中。现金流主要分为3类，`经营活动现金流CFO`, `投资活动现金流CFI`和`融资活动现金流CFF`。现金流量表可以帮助判断公司的`流动性`，`偿债能力`和`财务灵活度(financial flexibility)`。

### 现金流量表科目分类 US GAAP vs IFRS

<table>
    <!--标题-->
    <tr>
        <th colspan="2", align = "center">US GAAP</th>
    </tr>
    <tr>
        <th colspan="2", align = "center">Cash flows from Operating Activities经营活动现金流</th>
    </tr>
    <tr>
        <th align = "center">Inflows</th>
        <th align = "center">Outflows</th>
    </tr>
    <tr>
        <td>从客户处获得的现金</td>
        <td>付给员工和供应商的现金</td>
    </tr>
    <tr>
        <td>卖出交易性金融资产获得的金额</td>
        <td>买入交易性金融资产付出的金额</td>
    </tr>
    <tr>
        <td></td>
        <td>经营活动费用支出</td>
    </tr>
    <tr>
        <td><font color="red">收到的利息</font></td>
        <td><font color="red">支出的利息</font></td>
    </tr>
    <tr>
        <td><font color="red">收到的股利</font></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td>支出的税金</td>
    </tr>
    <tr>
        <th colspan="2", align = "center">Cash flows from Investing Activities投资活动现金流</th>
    </tr>
    <tr>
        <th align = "center">Inflows</th>
        <th align = "center">Outflows</th>
    </tr>
    <tr>
        <td>卖出长期资产收入金额</td>
        <td>获取长期资产付出金额</td>
    </tr>
    <tr>
        <td>卖出股票债券资产收入金额</td>
        <td>买入股票债券资产付出金额</td>
    </tr>
    <tr>
        <td>收回借给别人的借款金额</td>
        <td>借款给别人的金额</td>
    </tr>
    <tr>
        <th colspan="2", align = "center">Cash flows from Financing Activities融资活动现金流</th>
    </tr>
    <tr>
        <th align = "center">Inflows</th>
        <th align = "center">Outflows</th>
    </tr>
    <tr>
        <td>发行债券获取的金额</td>
        <td>偿还债券付出的金额</td>
    </tr>
    <tr>
        <td>发行股票获取的金额</td>
        <td>回购股票付出的金额</td>
    </tr>
    <tr>
        <td></td>
        <td><font color="red">付出的股利</font></td>
    </tr>
</table>
在US GAAP准则下，利息的收入和支出都属于CFO，而收到的股利属于CFO但支出的股利属于CFF。而在IFRS准则下，利息和股利的收入都可以计入CFI或CFO，利息和股利的支出都可以计入CFF或CFO。另外US GAAP准则下的税金计入CFO中，但IFRS准则下不同活动产生额税金计入不同的现金流量科目中。

### 现金流计算

#### 经营活动现金流CFO计算

现金流的计算方法有两种，`直接法`将各个活 动的收入与支出金额相加最后得出总现金流。 `间接法`将利润表中的净收入做相关调整后计算出总现金流。直接法不如间接法准确，但可以看到各个经营活动现金流的构成，因此会计准则鼓励公司使用直接法制现金流量表。

现金流计算时，负债的增加意味着现金增加，资产的增加意味着现金的流出。 

##### 间接法

<table>
    <tr>
    	<th colspan="2", align = "center">间接法计算CFO</th>
    </tr>    
    <tr>
        <td>净利润</td>
        <td></td>
    </tr>
    <tr>
        <td>+ 非现金费用或损失</td>
        <td rowspan="3">利润表项目</td>
    </tr>
    <tr>
        <td>- 非现金收入或获利</td>
    </tr>
    <tr>
        <td>+ 营业外获利或损失</td>
    </tr>
    <tr>
        <td>- 不包含现金的短期资产增加量(存货，应收账款)</td>
        <td rowspan="2">资产负债表项目(营运资本Working capital)</td>
    </tr>
    <tr>
        <td>+ 不含付息债务的短期负债增加量(应付账款)</td></td>
    </tr>
    <tr>
        <td>=CFO</td>
        <td></td>
    </tr>
</table>

需要注意几点：在考试中通常只对非现金费用进行调整，因为实务中非现金收入最终都会转为现金收入，但非现金费用例如折旧永远都属于非现金费用；一级考试中通常营业外获利或损失为0；CFA一级考试中通常直接用净利润+非现金费用-营运资本计算CFO，营运资本=不含现金的流动资产-不含付息债务的流动负债。

##### 直接法

<table>
    <tr>
    	<th colspan="2", align = "center">直接法计算CFO</th>
    </tr>    
    <tr>
        <td>从客户处收入的现金</td>
        <td>初始应收款项+净收入-结算应收款项=净收入-应收款项增量</td>
    </tr>
    <tr>
        <td>- 支付给供应商的现金</td>
        <td>支付现金=期末存货-期初存货+货物营业成本-应付账款增量</td>
    </tr>
    <tr>
        <td>- 支付给员工的现金</td>
        <td>支付给员工的现金=工资费用-应付工资增量</td>
    </tr>
    <tr>
        <td>- 支付给债权人的利息</td>
        <td>支付给债权人的利息=利息费用-应付利息增量</td>
    </tr>
    <tr>
        <td>- 支付的税金</td>
        <td>支付的税金=税金费用-应付税金增量</td>
    </tr>
    <tr>
        <td>=CFO</td>
        <td></td>
    </tr>
</table>

主要注意的点有：CFA一级的重点考试内容是从客户出收入的现金和支付给供应商的现金，其中支付给供应商的现金中，货物营业成本通常默认不包括折旧费用 ，若题目表示该数额包含折旧费用，则需要加回。

#### 投资活动现金流CFI计算

投资活动的主要两个类别是`买卖长期资产`,`买卖金融资产`和`借款`，考试中主要考察的是长期资产买卖。考试中两个公式可能需要同时使用。

#####  购买固定资产的现金支出

$$
期末账面价值=期初账面价值+购买支出-处置资产账面价值-减值
$$

##### 卖出固定资产的现金收入

$$
获利或损失=收到金额-处置资产账面价值
$$

#### 融资活动现金流CFI计算

融资活动的现金流主要考察的是股利的现金流计算，需要掌握的公式只有一个：
$$
支付的股利=宣告支付的股利-应付股利
$$

###  Common Size C/F

现金流量表的Common size有两种计算方法：

1. 将现金流的各个科目除以总收入；
2. 将现金流入和流出科目分别除以现金总流入和总流出。

### 自由现金流(Free Cash Flow)

该部分内容在CFA一级中涉及较少，但是CFA二级重点考察的内容。一级中考察的主要是根据公司财务报表计算公司自由现金流的方法。自由现金流的定义为，满足公司的所有生产经营活动后盈余的现金流，其又分为`公司自由现金流(Free cash flow to the firm FCFF)`和`股权自由现金流(Free cash flow to equity FCFE)`。

#### 股权自由现金流

$$
股权自由现金流=公司自由现金流-利息\times(1-税率)+净借款
$$

#### 公司自由现金流

共有三种方式计算公司自由现金流：
$$
公司自由现金流=息税前利润(EBIT)\times(1-税率)+非现金支出-固定资本投入-营运资本投入\tag{1}
$$

$$
公司自由现金流=净利润(NI)+利息\times(1-税率)+非现金支出-固定资本投入-营运资本投入\tag{2}\\
$$

$$
公司自由现金流=经营活动现金流(CFO)+利息\times(1-税率)-固定资本投入\tag{3}\\
$$

## Reading 24 财务分析技术

###  财务比率分析(Ratio analysis)

#### Profitability ratio

用于衡量公司从收入中产生利润的能力，主要基于利润表计算。

`Return on assets(总资产收益率, ROA)：`(净利润+税后利息)/平均总资产(Average total assets)。 反映公司为公司所有者的盈利能力。

`Return on Equity(净资产收益率, ROE)：`净利润/平均总权益(Average total equity)。反映公司为股东盈利的能力。

 `Operating return on assets：`EBIT/平均总资产。与ROA的区别在于ROA为税后此指标为税前。

`Return on total capital(ROTC)：`EBIT/平均总资本(Average total capital)。资本比资产少计不付息的负债部分。

`Return on common equity：`(净利润-优先股股利)/平均普通股权(Average common equity)。反映公司为普通股股东盈利能力。

#### Activity ratio

用于衡量公司使用资产产生收入的效率，主要有六个`周转率(turnover)`指标。

 `Total asset turnover(总资产周转率)：`净收入/平均总资产 。计算每一份资产可以产生的收入，反映资产使用效率。

`Fixed asset turnover(固定资产周转率)：`净收入/平均净固定资产(Average net fixed assets)。反映固定资产使用效率。

`Working capital turnover(营运资本周转率)：`净收入/平均营运资本。营运资本是不包含现金的流动资产减去不包含付息债务的流动负债，是日常经营占用的资金。

`Inventory turnover(存货周转率) ：` COGS(货物成本)/ 平均存货(average inventory)。用365除周转率为存货周转周期。对比存货周转率时要在相同行业/商业模式的公司间比较。

`Receivable turnover(应收账款周转率)：`净收入(Net revenue)/平均应收账款(average A/R)。用365除周转率为平均收回账款周期。收款周期是否过长应该对比公司行业的平均账期。

`Payables turnover(应付账款周转率)：`购买(Purchase)/平均应付账款(average A/P)。用365除周转率为平均付款周期。付款周期应该对比应付账款在付款时的现值与提前付款的优惠。

最后，`经营周期(Operating Cycle)=平均收款周期+存货周转周期`，`现金循环周期(Cash converison cycle)=平均收款周期+存货周转周期-平均付款周期`。

#### Liquidity ratio

衡量公司偿付短期债务的能力，反映公司财务流动性水平，主要有4个指标。

`Current ratio(流动比率)：`Current assets(流动资产)/Current liability(流动负债)。流动比率越高流动性越强，但流动资产中可能拥有滞销存货，因此可以使用其他比率更好衡量流动性。

`Quick ratio(速动比率)：`(现金+交易性证券+应收账款)/流动负债≈(流动资产-存货)/流动负债。

`Cash ratio(现金比率)：`(现金+交易性证券)/流动负债

`Defensive interval(防御区间)：`(现金+交易性证券+应收账款)/平均日开支。用来衡量公司流动资产能够覆盖日常开支的天数，通常需要大于45天。

#### Solvency ratio

衡量公司偿付长期债务的能力。

`Financial leverage(财务杠杆比率)：`资产(Assets)/权益(Equity)。财务杠杆越大表示负债越多，风险越大，收益率越高。

`Interest coverage(利息保障倍数)：`EBIT(息税前利润)/利息。该比率大于1时代表公司盈利，反之代表亏损。

`Fixed charge coverage(固定支出保障倍数)：`(EBIT+租金)/(利息+租金)。该比率大于1时代表公司盈利足够支付固定支出。

#### Valuation ratio

公司投资估值的指标，反应公司股票是被高估还是被低估。主要指标为`市盈率(P/E)`，`市现率(P/CF)`，`市销率(P/S)`，`市净率(P/BV)`四个指标。估值指标需要与`市场基准(Benchmark)`比较才能知道高低，基准通常为可比公司或板块平均基准。关于估值指标的具体计算和应用会在股票科中详解。

### 杜邦分析(Dupont system of analysis)

使用杜邦分析法可以将净资产收益率(Return on equity)拆分分析，从而得出结论是公司的哪部分表现变化导致了净资产收益率的变化。

#### 三因子分析(three-part approach)

$$
ROE(净资产收益率)=\frac{NI}{Sales}(净利率)\times\frac{Sales}{Assets}(总资产周转率)\times\frac{Assets}{Equity}(财务杠杆)
$$

三因子分析中，净利润表示公司盈利能力，总资产周转率反映公司管理效率，财务杠杆反映公司财务风险。

#### 五因子分析(five-part approach)

$$
ROE(净资产收益率)=\frac{NI}{EBT}(税负比率)\times\frac{EBT}{EBIT}(利息负担比率)\times\frac{EBIT}{Sales}(经营利润)\times\frac{Sales}{Assets}(总资产周转率)\times\frac{Assets}{Equity}(财务杠杆)
$$

五因子分析将净利润进一步拆解出税负比率和利息负担比率，由此看出税负和利息对公司净资产收益率的影响。

## 净盈余假设(Clean surplus relationship)

假设股东权益的增加只与留存收益的增加有关，一个公司的`长期净增长率`为`净资产收益率`乘`留存率`。表示为下式：
$$
g(sustainable\ growth\ rate)=ROE\times RR=ROE \times(1-\frac{div\ declared}{Operating\ income\ after\ taxes})
$$

# Session 8

## Reading 25 存货

资产负债表中计算存货的主要公式为：
$$
COGS(已售货物成本) = 初始存货+采购-年终存货
$$

### 资本化成本vs费用化成本

公司在生产过程中发生的成本可以被计入产品成本或生产费用，计入产品成本的成本被计入资产负债表中，该成本被`资本化(capitalized)`，计入生产费用的成本被计入利润表中，该成本被`费用化(expensed)`。成本资本化或费用化的标准以其成本发生时间在产品达到可销售状态前后为分界线。

`资本化成本：`原料采购成本，转化成本(工厂人工与费用等)，俗称料工费。成本资本化可以将成本发生时间递延，产品销售时才确认成本。

`费用化成本：`产品仓储成本，管理成本，销售成本，`生产过程中发生的非正常浪费`。

### 存货计价方法

在IFRS准则下，存货的计价方法有`个别计价法(Specific identification)`，`先进先出法(FIFO)`，`加权平均法(Weighted average cost)`等三种方法，在US GAAP准则下除了这三种计价方法外还有一种`后进先出法(LIFO)`。

| 个别计价法                                                   | 先进先出法                                                   | 加权平均法                                           | 后进先出法                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ---------------------------------------------------- | ------------------------------------------------------------ |
| 每件商品以其实际的成本计算，其成本与存货价值计算最为准确，但操作成本较高。该方法通常用于销量少单价高的商品，例如珠宝奢侈品等。 | 大部分公司使用的计价方法，卖出的存货总以库存中最老的存货成本计算。通常导致成本被低估，但存货价值较为准确。 | 存货价值以库存存货的平均价值计算，该方法使用也较少。 | 只有US GAAP 准则中可以使用，卖出的存货总以库存中最新的存货成本计算。通常可以使货物成本被准确反映，但存货价值被低估。 |

`先进先出法`和`后进先出法`由于前者导致`成本被低估`，通常相较后者会导致更高的息税前利润与更高的赋税，从而导致更低的经营性现金流，以及更低的存货周转率等。当我们改变计价方法时，其他方法`改为后进先出法不需要追溯调整`，但其他改变都需要追溯调整。

### 存货的核算体系(Periodic vs Perpetual)

存货的核算体系有`定期盘存制(Periodic)`和`永续盘存制(Perpetual)`的区别之分。定期盘存制通常在每个会计月末进行库存和成本的核算，而永续盘存制则是一直以最新的价值来核算库存和成本。`先进先出法和个别计价法`在两个核算体系下算出的库存和成本价值`结果相同`，`后进先出法和加权平均法则不一样`。

### 后进先出法转为先进先出法

为了对比使用FIFO和LIFO的两家公司的财务报表数据，金融分析师通常需要将LIFO的核算结果调整为FIFO。其转换的最关键的概念则是`LIFO Reserve`，当美国公司基于US GAAP准则以LIFO方法核算成本与库存时，他们需要同时披露`LIFO Reserve`的数值，该数值为`FIFO口径下的存货与LIFO口径下存货价值的差异`。
$$
存货_{FIFO}=存货_{LIFO}+LIFO\ Reserve\\
COGS_{FIFO}=COGS_{LIFO}-\Delta LIFO\ Reserve（LIFO\ Reserve为时点数，在利润表需要记为变动值）\\
NI_{FIFO}=NI_{LIFO}+\Delta LIFO\ Reserve\times (1-Tax)
$$

### 后进先出法的清算(LIFO Liquidation)

使用后进先出法计算COGS时可能由于公司生产效率下降使库存中的更便宜的旧存货慢慢被消耗导致在物价上涨阶段反而出现产品成本下降的现象，这个现象被称为`LIFO Liquidation`。如果一家公司出现该现象，首先说明当前COGS没有反映真实成本，其次LIFO Reserve会出现下降(因为库存量会有下降)。

### 存货的减值(Inventory Impairment)

 存货的价值为历史成本估算，但可能出现特殊情况导致存货账面价值不能反映其真实价值，这时需要对其进行减值计算。

| US GAAP                                                      | IFRS                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `账面价值`与`市场价值`中取其低者。<br />市场价值既是存货的`重置成本(replacement cost)`，且重置成本最低为`可实现净值-normal profit margin`，最高为可实现净值。 | `账面价值`与`可实现净值`中取其低者。<br />`可实现净值(Net realizable value) = 售价-销售成本` |
| 当存货账面价值高于市场价值时，存货应当在资产负债表中被减值为市场价值，减值以Loss计入利润表，减值后`不可以`转回。 | 当存货账面价值高于其可实现净值时，存货应当在资产负债表中被减值为可实现净值，减值以Loss计入利润表，IFRS准则中可以被最多重新转回至账面价值，转回以Gain计入利润表。 |

## Reading 26 长期资产

### 长期资产的资本化vs费用化

长期资产与存货类似，需要对其成本进行资本化与费用化的分类，资本化的长期资产成本会记入`有形或无形资本(Tangible/Intangible Assets)`逐年减值或摊销。与存货相似，被资本化的费用计入资产负债表，费用化的费用计入利润表。另外存货的资本化与费用化不影响现金流量表，但长期资产的资本化费用被计入投资性现金流，费用化的费用被计入运营性现金流。

#### 资本化和费用化对报表的影响

长期资产资本化或费用化对报表的影响主要体现在费用化会使账面`总资产`和`股东权益`更`高`，而其费用被作为减值或摊销成本摊至每年，因此会使每年的`净利润更加平稳`，并且会使`投资性现金流减少`（因为费用被计入CFI）。需要注意的是存货的资本化和费用化会影响公司的缴税数额，但`长期资产`的资本化和费用化`不会影响赋税`，因为存货部分税务报表与财务报表相同，因此只有存货的费用化影响的净利润会造成缴税数额的变化。

#### 资本化和费用化的认定

长期资产的资本化与费用化的分界线为`“资产达到可使用状态”`，即资产达到可使用状态前的成本资本化，反之则费用化。

`资本化成本：`购买价格，税收，保险，运输费，安装测试费，`资产改良支出(该支出在可使用之后发生但成本资本化)`等。

`费用化成本：`设备减值，修理维护费用，员工训练成本等。

#### 资本化的利息计算

正常情况下借款的利息成本都应该费用化计入利润表，但以构建固定资产为目的借款所产生的的利息应该被资本化计入资产负债表。

### 无形资产(Intangible Assets)

没有物理形态的长期资产，如技术、专利、品牌、口碑等都可被归类为无形资产。会计准则中无形资产分为三类：

`可辨认的无形资产(Indentifiable IA)：`可以被直接买卖的如`专利(Patents)`、`商标(Trademarks)`、`版权(Copyright)`等有有限或无限使用期限的无形资产，计入资产负债表。

`不可辨认的无形资产(Unidentifiable IA)：`不可以被直接购买的无形资产，比如`商誉(Goodwill)`，通常是购买资产时对方品牌的溢价部分，计入资产负债表。

`自主研发的无形资产(Internally generated)：`研发费用中`研究(Research)`费用被费用化，`开发(Development)`费用在IFRS准则中满足特定条件后可以费用化，在US GAAP准则中除`内部使用的软件的开发`以外开发费用也要被费用化。

有使用期限的无形资产按年限摊销，没有使用期限的无形资产要每年进行`减值测试(Annual impairment test)`。

### 折旧摊销方法

所谓折旧摊销就是将长期资产的成本在其使用期间进行系统性的成本分摊，分析师需要注意报表上的折旧费用可能与实际的设备折旧损耗不同。折旧摊销主要有三种计算方法：

`直线法(Straight line)：`$每年花费=(原值-残值)/使用寿命$

`双倍余额递减法(Double declining balance)：`$每年花费=（2/使用寿命）\times 当年初的资产净值$

`生产单位折旧法(Units-of-production)：`$每年花费=[(原值-残值)\times 期限内产值]/设备总产值$

双倍余额递减法又称加速折旧法，相较与直线法其特点是前期折旧速度块，后期折旧速度慢，因此`前期`加速法会导致`更高的减值成本和更低的净利润`从而影响其他指标，后期相反。但两种方法均`不影响赋税数额`。

 由于资产的折旧与摊销中的`使用年限`和`资产残值`都基于主观估计，因此常被公司用于调整财务报表。

### 资产的减值(Impairment)

#### IFRS准则下的减值

当资产的`账面价值(Carrying value)`大于资产的`可回收价值(Recoverable amount)`时，对资产进行减值同时在利润表中计入减值损失。资产的可回收价值取`处置价值(即公允价值-处置成本)`和`使用价值(即未来可产生现金流的现值)`中的孰高值。

#### US GAAP准则下的减值

美国准则下的资产减值分为两步，第一步为`定性判断`，若资产的`账面价值`大于该资产未来产生的`不折现`现金流，则不需要减值。若定性为需要减值，则第二步计算`减值金额为资产账面价值减去资产的市场公允价值或未来现金流的现值`。

#### 资产减值对财务报表的影响

资产减值对现金流没有影响，但会导致资产负债表中资产减少，同时利润表计入了减值损失，从而影响其他财务数字。主要注意的是，减值虽然会`减少当年的净利润`，但会`增加未来年度的净利润`，因为资产减值会使未来的折旧数额减少。

#### 减值的转回

与存货类似，US GAAP准则下大部分减值`不允许`转回，`用于销售的资产(Held for sale)`除外。IFRS准则下大部分减值`允许`转回，`商誉(Goodwill)`除外。

### 长期资产的重估(Revaluation)

在计算长期资产的`净值(Net Book Value)`时，US GAAP通常使用`历史成本模型(Historical cost model)`,即原值减去减值和折旧后得到净值，但IFRS准则下除了使用成本模型，还可以使用重估模型计算资产净值。如果公司使用重估模型对资产估值时，发生的损失计入利润表，发生的利润计入资产负债表的其他综合收益(OCI)，但需要特别注意当发生价值转回时，`先抵原账户`，即之前若之前重估导致利润表发生损失，转回时先将这部分计回利润表，其他多出部分才计入其他综合收益；同理若之前重估导致其他综合收益计入收益，损失掉时先扣除OCI中这部分，剩下才计入利润表。

另外需要注意，重估模型下资产依然要进行折旧摊销，每年的折旧费用根据其重估后的价值计算。

### 资产的核销(De-recognition)

长期资产会在被`售卖(sold)`、`丢弃(abandoned)`和`交换(exchnaged)`三种情况下会被从资产负债表中消除。

### 投资性房地产(Investment Property)

 当公司所有的房产以自用为目的时计入固定资产，但若`以出租为目的`时计入`投资性房地产`，若以售卖为目的可以计入存货。在US GAAP准则下，投资性房地产与普通固定资产没有区别，因此这个概念只适用于IFRS准则。

投资性房地产的估值方法也有成本模型和公允价值模型(fair value model)两种方法， 公允价值模型与重估模型虽然都根据公允价值为资产估值，但不同于重估模型的收益计入其他综合收益，公允价值模型中的收益和损失都计入利润表。

## Reading 27 递延所得税

`递延所得税(Deffered Income tax)`是由于基于会计准则编制的财务报表与基于税法编制的税务报表的规定或计算不同导致的缴税款与实际公司财务记账金额不同时产生的科目，本年度相较财务报表数额实际`多/少`缴的税款需要计入递延所得税`资产/负债`。

### 财务报表术语vs税务报表术语

|           | 财务报表                       | 税务报表                     |
| --------- | ------------------------------ | ---------------------------- |
| 利润      | Accounting Profit(会计利润)    | Taxable income(应纳税所得额) |
| 所得税    | Income tax expense(所得税费用) | Taxes payable(应交税金)      |
| 资产/负债 | Carrying value(账面价值)       | Tax base(税基)               |

 关于财务报表与税务报表的科目区别，除了以上的对应科目以外，还有一些各自专属的科目：

`递延所得税负债和递延所得税资产(Deferred tax liabilities&Deferred tax assets)：`在会计报表的资产负债表中计入的本年度财务与税务报表的差距，本年度多缴的税计入递延所得税资产，少缴的税计入递延所得税负债。

`递延所得税减值(Valuation allowance)：`会计报表备抵科目，递延所得税资产可能不能被兑现时计入该资产的减值。

`以前年度亏损(Tax loss carry forward)：`该科目为税务报表科目，若公司以往年度出现过亏损，该亏损可以被带往将来年度抵减税款，一般可抵减年限有限制。

### 暂时性差异vs永久性差异

递延所得税由财务报表和税务报表的差异造成，但`只有暂时性差异可以产生递延所得税`。永久性差异例如公司遭受的罚款导致比会计报表中多交的税金或公司购买国债利息收入的免税金额等，不会导致递延所得税。因为永久性差异不会导致公司未来资金的流入或流出。

### 计算递延所得税

递延所得税的计算方法一般有`利润表法`和`资产负债表法`，通常使用利润表法可以快速定性递延所得税是资产还是负债，而当要计算具体金额时，使用资产负债表法会更方便。

`利润表法：`会计报表和税务报表每年的税前收益差异乘上当年税率相加至所需年度，若实际多交税则记递延所得税资产，反之记递延所得税负债。

`资产负债表法：`若需要计算的科目为`资产科目`，则使用`(财务价值-税务价值)*税率`；若需要计算的科目为`负债科目`，则使用`(税务价值-财务价值)*税率`。最后结果若为`正数`，则为`递延所得税负债`；若结果为`负数`，则为`递延所得税资产`。

### 导致递延所得税的常见科目

 `固定资产(Fixed assets)：`由于财务报表与税务报表的减值口径不同，导致固定资产的账面价值差异造成递延所得税。通常财务报表为展示更多利润，会延长折旧年限等，造成实际交税更少，形成递延所得税负债。

`无形资产(Intangible assets)：`财务报表的研发费用倾向于被费用化，但税务报表允许无形资产研发资本化。因此财务报表利润较税务报表少，因此实际交税较多，形成递延所得税资产。

`应收账款(Account receivable)：`财务报表中的坏账准备金不允许被记入税务报表，因此财务报表中的利润较税务报表少，因此实际交税多，形成递延所得税资产。

`预收账款(Unearned revenue)：`收款时直接计入税务报表，但财务报表要等到交易完成后才能确认，因此税务报表中利润更大，导致实际缴税金额大，形成递延所得税资产。

`保修费用(Warranty liability)：` 对保修的准备金，与坏账准备金类似，税务报表中等到保修费用实际支出时才被确认，因此财务报表中利润较低，实际缴税金额高，形成递延所得税资产。

### 税率改变的影响

若税率发生改变，而税务与财务差异不变：
$$
新递延所得税=旧递延所得税 \times \frac{新税率}{旧税率}
$$
若税率和税务与财务表差异同时发生：
$$
财务口径所得税费用=当年新增的税法口径应交税金+当年新增的递延所得税负债-当年新增的递延所得税资产
$$

### 有效税率(Effective Tax Rate)

实际操作中，公司的有效税率由公司当年实际缴税额除以公司税前利润。有五个可能原因导致有效税率与`税法规定税率(Statutory Tax Rate)`不同：

1. 公司在不同地区所得税税率不同。
2. 永久性差异导致有效税率与法定税率不同。
3. 年内税率改变。
4. 海外子公司获得的利润在当年缴付给当地的税款可能高于母公司所在地的法定税率。
5. 特定地区免税期或其他特定优惠政策等。

### 递延所得税分析

当递延所得税资产有较高概率不能被实现时，计`递延所得税减值(Valuation allowance)`。若递延所得税负债在未来有较高概率不能被实现，分析师可以将该部分当作`股东权益`；若可能被实现则当作`实际负债`；若未来实现的概率不确定，则`忽略`该科目。

## Reading 28 长期负债

本章主要关注应付票据或应付债券等以融资为目的的长期负债以及融资租赁中应付租赁款的核算方法。其中`持有至到期债券(Held-to-maturity)`的核算方法在Reading 22中已经覆盖过。

### 债券记账

当公司发行债券时应以债券未来现金流的现值在`资产负债表`中计入`应付债券(Bond Payable)`并获得`等额现金`，每年在`利润表`中计入`以现值计算的利息费用`，在`现金流量表`中计入支付的`票面利息(coupon)`。

`市场利率>票面利率：`票面利率低因此债券比票面更便宜，每年实际支付的票面利息低于自然利息，因此经营性现金流被高估，投资性现金流被低估。

`市场利率=票面利率：`每年年末价值都等于账面价值。

`市场利率<票面利率：`票面利率高因此债券比票面更值钱，每年实际支付的票面利息高于自然利息，因此经营性现金流被低估，投资性现金流被高估。

#### 零息债券

计算`零息债券(Zero coupon bond)`时与上方方法一样，只是不付票面利息，可以以市场利率>票面利率的债券计算。

#### 发行成本

在US GAAP准则下，`发行成本资本化(Deferred charge)`并在债券存续期间摊销。在IFRS准则下，发行成本直接从融资中扣除。

#### 公允价值估值

上方提到的记账方法使用的市场利率为债券发行时的市场利率，但公司可以选择使用公允价值来对应付债券估值，这时市场利率的波动和发行公司的信用风险波动都会导致债券市场价格的变动。

#### 债券中止确认(Derecognition of Debt)

债券发行公司可能会在债券到期前提前赎回债券。可能原因有：1. 市场利息大幅下跌。2. 公司经营过程中产生盈余现金。3. 公司通过发售股票获得额外资金。

#### 债券条款(Debt Covenant)

债券的常见条款有两类，肯定条款(affirmative covenant)和否定条款(negative covenants)。其中肯定条款包括公司要按时支付本金利息，维持财务指标，维护抵押物等。否定条款包括公司不能使用借款支付股利或回购股票，不能发行更多债券，不能进行公司并购。

### 融资租赁和经营租赁

经营租赁和融资租赁的主要区别在于经营租赁为支付租金换取使用权，融资租赁则是分期付款，付完时获得资产。在IFRS准则下只有融资租赁没有经营租赁，而在`US GAAP准则下`只要满足一下任意一个条件即为融资租赁：

1. 租赁期结束时资产的所有权转至承租人。
2. 租赁期结束时承租人可以以较低的价格购买资产。
3. 承租期占资产可使用年限的75%以上。
4. 所付租金的现值占资产公允价值的90%或以上。
5. 定制化资产，租赁资产只能由承租人使用。

### 融资租赁的记账方法

租赁时首先资产计入固定资产，同时负债中计入应付租赁款，这数额以未来租金的现值计算。利润表中计算摊销折旧费用以及负债的利息费用，现金流量表中计入每年实际支付的租金。

### 养老金

美国上市公司给员工的养老金分为`Defined conrtibution plan(DC plan)`和`Defined benefit plan(DB plan)`两种，其中DC plan的养老金风险由员工承担，DB plan的养老金风险由公司承担。另外养老金中资产与负债可以互相抵消，以净值计算。

# Session 9

## Reading 29 财务报表质量

财务报表质量在CFA二级和三级中是非常重要的部分，但一级中只要知道大致概念即可。

### 财务报表质量档次

公司财务报表质量由高到底分别为：

1. 真实，可供投资参考，可持续，盈利充足(支付股东资金成本后仍有盈余)。
2. 真实，可供投资参考，不可持续，较低盈利质量。
3. 符合会计准则，但会计方法选择有偏差。
4. 符合会计准则，但有意利用方法操纵利润。
5. 不符合会计准则。
6. 财务报表造假。

### 常见的财务造假方法

| 做高利润                 | 做低利润             |
| ------------------------ | -------------------- |
| 资本化当期成本           | 费用当期成本         |
| 调高固定资产使用寿命     | 调低固定资产使用寿命 |
| 调高固定资产残值         | 调低固定资产残值     |
| 调整折旧方法(使用直线法) | 加速折旧             |
| 推迟确认减值             | 提前确认减值         |
| 少记坏账准备金           | 多记坏账准备金       |
| 降低递延所得税减值       | 提高递延所得税减值   |

### 舞弊三角(Fraud triangle)

通常判断公司财务造假可能的三个条件，如果公司具有三点其财务造假的可能性较高：

1. **造假动机(Motivation)**
2. **造假机会(Opportunity)**
3. **造假的自我辩护(Rationalization)**

## Reading 30 财务报表分析应用

分析师可以使用财务报表分析：

1. 判断公司的商业模式和盈利模式
2. 对公司进行盈利预测
3. 对比不同口径的财务报表

[第13篇] 

