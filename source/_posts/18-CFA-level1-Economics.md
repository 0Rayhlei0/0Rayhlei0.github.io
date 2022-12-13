---
title: "[金融分析] CFA一级《经济学》学习笔记"
date: 2022-06-18 14:50:45
tags: [CFA一级,经济学, 日常学习]
categories: 金融分析
description: "[第18篇] 本篇将包括CFA一级考试中经济学(Economics)科目的学习笔记。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/CFA.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/18-CFA-level1-Economics.jpg
katex: true
---

# 概览

经济学一共包括2个Session的7个Reading，主要包括的内容是各个Reading的内容如下表：

<table>
    <tr>
        <th>Sessions</th>
        <th>Readings</th>
        <th>Contents</th>
    </tr>
    <tr>
        <td rowspan="4">SS4</td>
        <td>R12</td>
        <td>Topics in Demand and Supply Analysis</td>
    </tr>
    <tr>
        <td>R13</td>
        <td>The Firm and Market Structures</td>
    </tr>
    <tr>
        <td>R14</td>
        <td>Aggregate Output, Prices, and Economic Growth</td>
    </tr>
    <tr>
        <td>R15</td>
        <td>Understand Business Cycles</td>
    </tr>
    <tr>
        <td rowspan="3">SS5</td>
        <td>R16</td>
        <td>Monetary and Fiscal Policy</td>
    </tr>
    <tr>
        <td>R17</td>
        <td>International Trade and Capital Flows</td>
    </tr>
    <tr>
        <td>R18</td>
        <td>Currency Exchange Rates</td>
    </tr>
</table>
# Session 4

## Reading 12 需求与供给分析

经济学中最重要概念之一就是供给与需求的关系，在本章中主要会介绍供给需求曲线的理论知识以及其中的弹性等概念。

### 供需曲线

#### 需求曲线(Demand curve)

分析市场`需求`时首先主要从买方的购买`意愿`与`能力`来分析，只有在同时具有意愿与能力时才能形成需求。会影响需求量的因素一般包括`商品价格`$P_{x}$、`收入水平`$I$以及`其他商品价格`$P_{y}$。

- 商品价格上升时，需求量下降，反之亦然。
- 收入上升时，需求量上升，反之亦然。
- 其他商品价格下降时，该商品需求量下降，则其他商品为该商品的`替代品`；若其他商品价格下降时，该商品需求上升，则其他商品为该商品的`互补品`。

通常经济学中会假设需求曲线的公式为这些因素对于需求量影响的`线性函数`。例如：
$$
Q_d^{x}=9-1.5P_{x}+0.02I+0.11P_{y}
$$
由于需求曲线绘制的是商品价格与商品需求量之间的关系曲线， 因此绘图时会假设$Q_x$与$P_x$为变量，其他因素如$I$与$P_{y}$则是常数。实践中绘制需求曲线时会将需求放在横坐标x轴，然后将价格放在纵坐标y轴。所以绘图时还要将上式表示为$P_x$关于$Q_x^d$的方程。例如假设$I=40$, $P_y=25$：
$$
P_x=8.37-0.667Q_d^x
$$
这就是需求曲线的表达式，截距为8.37，斜率为-0.667。

#### 供给曲线(Supply curve)

供给曲线与需求曲线类似，主要由生产商家的生产`意愿`与`能力`决定，而影响生产厂家的意愿与能力的因素通常是产品价格$P_x$与生产成本$cost$。

- 商品价格上升时，供给量上升，反之亦然。
- 生产成本通常包括人工成本和原材料成本，成本上升时，供给量下降，反之亦然。

供给曲线的表达式形式与需求曲线差不多，我就不额外举例了，依然要注意虽然供给曲线主要关注的是各个因素对供给量的影响，但写成表达式以及绘图时依然是表示为$P_x$关于$Q_x^s$的方程。

#### 需求与供给量的移动

需求与供给量的移动有两种情况，因为需求供给方程都是针对其自身价格的变化构建的函数，其他影响因素都被简化为固定的常量，因此当商品本身价格变动时引起的需求供给量的变化是`沿供给需求曲线变化(movement along line)`；而其他因素变化时实际上是导致供给需求曲线方程中的截距变化，也就是`曲线平移(curve shifting)`。至于平移方向需求与供给曲线一样，当因素会导致需求或供给量上升时，曲线右移；导致需求或供给量下降时，曲线左移。

#### 市场均衡(Market Equilibrium)

将需求曲线与供给曲线画在同一张图上，两个曲线的交点就是市场均衡点。也就是会导致需求量与供给量相同的商品价格。如下图：

![供给曲线与需求曲线的交点就是市场均衡点](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220620225227202.png)

亚当斯密的古典经济学理论认为市场是一只看不见的手，当商品价格高于均衡价格时， 市场需求低于市场供给，会导致商品难以销售，从而导致生产厂家降价销售。当商品价格低于均衡价格时，市场需求高于市场供给，商品供不应求，会有消费者愿意高价购买商品，导致生产厂家提高商品价格。

#### 消费者剩余与生产者剩余

消费者剩余(Consumer Surplus)是指消费者为购买一批商品所愿意支付的最高价值与其必须支付的价格之间的差值。同理生产者剩余(Producer Surplus)则是生产者生产一批商品可以获得的利润与其生产的最低机会成本的差值。其计算方法就是下图中的三角形面积：

![消费者剩余和生产者剩余](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220620231033401.png)

这两个指标分别体现的是消费者和生产者在生产活动中自己感觉到获取的额外利益，是一种衡量社会福利指标。

### 弹性(Elasticity)

CFA中只涉及对需求弹性的讨论，需求弹性是衡量`需求量`对某个影响因素变化而变化的敏感程度。

#### 价格弹性

##### 定义和计算

弹性的定义就是计算每当价格变化1%时，需求会变化的百分比，其中价格弹性的计算公式就是：
$$
e_{price}=\frac{\Delta Q_x^d\%}{\Delta P_x\%}=\frac{\Delta Q/Q}{\Delta P/P}=\frac{\Delta Q}{\Delta P}\times\frac{P}{Q}
$$
其中$\frac{\Delta Q}{\Delta P}$就是需求函数中的斜率(Q的系数)。这时计算出的`需求弹性`$e_{price}$就是需求曲线在$PQ$点的`点弹性`。相对于点弹性，还有存在`弧弹性`的概念，其就是指两个点之间的弹性，可以用这两个点中间的平均价格和需求量来计算。

##### 价格弹性的分类

价格弹性就是商品价格对商品需求量的影响敏感程度。价格弹性小于0时负相关，大于0则是正相关。弹性的性质分为三类：

- `富有弹性(Elastic)：`当$|e_{price}|>1$时，商品价格会加倍影响需求量。
- `缺乏弹性(Inelastic)：`当$|e_{price}|<1$时，商品价格会较少影响需求量。
- `单位弹性(Unit Elastic)：`当$|e_{price}|>1$时，商品价格与需求量变化影响相同。

`完全弹性(Perfectly elastic)`和`完全不弹性(Perfect inelastic)`则分别是指价格的变动对需求量影响无穷大(涨价一点就完全没人买)和价格变动对需求量无影响(不管价格如何变动，需求量都是固定的)。

##### 价格弹性与收入的关系

在同一条需求曲线上，单位弹性以上的点都是富有弹性的，以下的点都是缺乏弹性的。而厂商的收入是商品价格乘以商品销售量，当商品价格在单位弹性点之上时，每降一点价格都会增加更多销量从而使销售额增大；当商品价格在单位弹性点之下时，每升高一点价格只会导致少量的销量减少，同样是销售额增大。因此厂商的最大销售额就在商品价格处于单位弹性点时。

##### 需求弹性的影响因素

- `替代品数量(Availability of substitutes)：`当一个商品替代品数量越多时，这个商品的弹性越高。
- `相对收入的比例(Relative amount of income spent on the good)：`消费者购买商品的预算占收入比例越大，商品的弹性就越大。(对人们来说越贵的东西越容易被价格变动影响)
- `价格变化的时间(Time since the price change)：`时间越长替代品数量越多，因此时间越长弹性越大。

#### 交叉弹性(Cross Elasticity)

与价格弹性相似，交叉弹性就是衡量其他商品的价格对需求量影响的弹性的指标：
$$
e_{cross}=\frac{\Delta Q_x^d\%}{\Delta P_y\%}=\frac{\Delta Q_x/Q_x}{\Delta P_y/P_y}=\frac{\Delta Q_x}{\Delta P_y}\times\frac{P_y}{Q_x}
$$
这个公式与价格弹性几乎一样，不过其中的参数由$P_x$变成了其他商品的价格$P_y$。实际计算中就是\frac{\Delta Q_x}{\Delta P_y}为需求曲线函数中$P_y$前的系数。

##### 交叉弹性的分类

当交叉弹性为`负数`时，代表该其他商品价格负向影响本商品需求量，说明本商品与该其他商品互为`互补品`。反之当交叉弹性为`正数`时，说明本商品与该其他商品互为`替代品`。

#### 收入弹性

同样的，还有收入水平变化与商品需求量变化的弹性指标，`收入弹性`$e_I$：
$$
e_{I}=\frac{\Delta Q_x^d\%}{\Delta I\%}=\frac{\Delta Q_x/Q_x}{\Delta I/I}=\frac{\Delta Q_x}{\Delta I}\times\frac{I}{Q_x}
$$
与前面一样，需要注意的只有$\frac{\Delta Q_x}{\Delta I}$在实际计算中就是需求曲线函数中$I$前的系数。

##### 收入弹性的分类

当收入弹性为`正数`时，这件商品被称为`正常商品(normal goods)`。反之收入弹性为`负数`时，商品被称为`劣质品(inferior goods)`。对正常商品来说(即收入弹性为正数时)，`弹性在0-1之间`时，收入水平对商品需求量影响较小，商品为`必需品`。`弹性大于1时`，收入水平对商品需求量影响较大，商品为`奢侈品`。

#### 替代效应(Substitution effect)和收入效应(Income effect)

替代效应是指当商品价格上升时，消费者会寻找该商品的替代品，从而导致商品的需求量下降。而收入效应则是指当商品价格上升而收入不变时，收入的实际购买力下降，这时会由于收入弹性导致商品需求量的变化，人们对正常商品的需求量会下降，对劣质品的需求量会上升。

对于所有商品来说，替代效应都是正效应。而收入效应对正常商品是正效应，对劣质品是负效应。因此对于劣质品来说有两种情况，如果其收入效应大于替代效应时，总效应为负效应，即商品价格升高会导致商品需求量增加，该商品为`吉芬商品(Giffen goods)`。与吉芬商品相似的还有`韦博伦商品(Veblen goods)`，相似点体现在韦博伦商品的需求量也会随其价格的上升而上升(当价格更高越能带来优越感时)，但韦博伦商品的本质是奢侈品，而吉芬商品是劣质品。另外韦博伦商品目前没有理论支持。

### 利润、产量、收入以及成本

#### 会计利润vs经济利润vs正常利润

- `会计利润(Accounting profit)`的计算方法就是在总收入的基础上扣除`显性成本(explicit cost)`后的利润。
- `经济利润(economic profit)`则是在会计利润的基础上再扣除如`机会成本(opportunity cost)`和`企业家才能(entrepreneurial ability)`等`隐形成本(Implicit cost)`后的利润。
- `正常利润(normal cost)`则是当经济利润为0时的会计利润，计算时正常利润的值与隐形成本相等，也即投资至少需要用以覆盖成本的利润。也因此经济利润又被称为`非正常/超额利润(abnormal profit)`。

#### 产量(Product)

产量是衡量供应商供给能力的指标，我们主要需要介绍的是`总产量(Total Product)`、`平均产量(Average Product)`和`边际产量(Marginal Product)`三个概念：

- `总产量`是指一段时间内的所有产出，通常是一个关于`劳动力(Labour)`的函数。
- `平均产量`是指每单位劳动力的平均产量。
- `边际产量`是指在当前产量情况下，每增加一单位劳动力可以增加的产量。

`边际效益递减规律(The law of diminishing marginal returns)`是指通常在增加资产投入时，每单位投入的资产所能产生的边际效益会随着投入越来越多而变小，当边际效益为零时，总产出达到最大值。因此，当边际产量大于平均产量时，每单位投入都会使平均产量增加；相反如果边际产量小于平均产量，每单位投入都会使平均产量减少。当边际产量等于平均产量时，平均产量达到最大值。

#### 收入(Revenue)

收入和产量一样，也有`总收入(Total revenue)`、`平均收入(Average revenue)`和`边际收入(Marginal revenue)`三个概念：

- 总收入是指当一家公司以同样的价格售卖商品给所有客户时，总收入为价格乘以销售量，而销量本身与价格有关。
- 平均收入是指总收入除以总销售量，也就是产品价格。
- 边际收入是指每多卖出一个产品时，总收入的增加量。

当市场环境是`完全竞争市场(Perfect competition market)`时，所有厂商都没有定价权，只能被动接受价格，售卖同质化商品，数量多，且进入壁垒低。在这样的市场中，边际收入=商品价格=平均收入。

当市场环境是`非完全竞争市场时(Inperfect competition market)`时，即市场参与者不满足完全竞争市场的任意条件时，$边际收入=商品价格\times (1-\frac{1}{|价格弹性|})$。边际收入大于零时，总收入上升；边际收入小于零时，总收入下降；边际收入等于零时，总收入为最大值。

#### 成本

经济学中，认为短期内成本可以分为固定成本和可变成本，而长期时间中，成本中只有可变成本。需要掌握的结论有这些：

- 总成本=总固定成本+总可变成本，其中可变成本随生产量变化而变化，固定成本不随生产量变化。
- 平均总成本=平均固定成本+平均可变成本，其中平均固定成本只会随生产量增加而递减。
- 边际成本=总成本变化量/生产量变化量，边际成本的变化通常由可变成本变化导致。
- 边际成本、平均总成本、和平均可变成本随生产量变化的曲线都是先向下后向上的U型曲线。边际成本曲线通过平均总成本和平均可变成本的曲线最低点，也即当边际成本等于这两个成本时，它们达到最低值。

#### 一些零散的知识点

- 由于边际收入随生产量增加而减少，边际成本随生产量增加而增加，当边际收入等于边际成本时，利润达到最大化。
- 在完全竞争市场下，当商品售价等于平均总成本时，处于`盈亏平衡点(Breakeven point)`。售价大于该点时供应商会留在市场中，售价低于这点时供应商会因为固定成本而在短期内留在市场中。当商品售价等于平均可变成本时，处于`关门点(Shutdown point)`。售价高于这点供应商才会再短期内留在市场中，当低于这点时每卖出一份产品就会亏损一份钱，因此供应商应该立即停止生产。
- 在不完全竞争市场下，商家不是价格的接受者，因此可以通过对比不同生产量下总收入和总成本与总可变成本对比确定盈亏平衡点和关门点。
- `规模经济和规模不经济(Economies of Scale and Diseconomies of Scale)`通过`长期平均总成本曲线(Long-run average total cost curve)`确定，随着生产量增加LATC会先下降，后上升。LATC会随着生产量上升而下降的生产规模叫做规模经济，LATC随着生产量上升而上升的生产规模叫做规模不经济。

## Reading 13 公司和市场结构

### 市场结构特点

| Type                               | Number of Firms            | Degree of difference of products   | Difficulty to enter or leave | Pricing Power of Firm | The example in our life    |
| ---------------------------------- | -------------------------- | ---------------------------------- | ---------------------------- | --------------------- | -------------------------- |
| Perfect competition（完全竞争）    | Many                       | No difference                      | Very easy                    | None                  | Some agricultural products |
| Monopolistic competition（垄断竞争 | Many                       | Some difference                    | Relatively easy              | Some                  | Some retail products       |
| Oligopoly（寡头）                  | More than one but not many | Little or no difference            | Difficult                    | Some or Condiderable  | Steel, automobile, oil     |
| Pure monopoly（垄断）              | SIngle                     | Sole product, nearly no substitute | No way                       | Considerable          | Public sectors             |

`完全竞争市场：`对于完全竞争市场来说，短期内边际收入等于边际成本时利润最大，所有厂商都是价格接受者，供给曲线为水平，边际收入=市场价格=平均总收入，所有厂商的经济利润都为0。

`垄断竞争市场：`垄断竞争市场为了保证产品差异化会出现创新和产品升级，拥有一定的品牌认知度，并且会有广告出现。短期内体现出垄断市场特点，长期体现出完全竞争市场特点。边际收入等于边际成本时利润最大， 但短期内由于产品差异化，厂商可以根据需求曲线调整价格，从而获取经济利润，但长期内由于产品互相可以替代，厂商会将价格逐步调整为相同，经济利润逐渐变为0。

`寡头市场：`除了上表中的差异以外，寡头市场的特有特点是各个公司会考虑竞争对手的行为而进行决策`(Interdependence among competitors)`。描述寡头市场的四个经济模型在下面单独介绍。

`垄断市场：`能形成垄断市场说明其市场的进入壁垒较高，主要的垄断壁垒有两种:`法律壁垒(Legal barriers)`和`自然壁垒(Natural barriers)`。垄断公司的利润最大化点一定是按照其边际收入等于边际成本计算，其相比完全竞争市场供给更低，价格更高。通常政府会干预垄断公司要求其以平均成本或边际成本定价。

### 寡头市场模型

#### 拐折的需求曲线(Kinked Demand Curve Model)

![Kinked Demand Curve Model](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220719230332597.png)

在柺折的需求曲线中，首先要决定价格拐点，模型假设市场供需关系是有效的，也即当前的市场价格既是价格拐点，而寡头市场的特点是产品同质化，当有厂商试图在这个市场中提升价格时，其他厂商不会跟进提升价格，因此该厂商的产品需求量会急剧下降，也就是说在拐折点以上的弹性较大；而相反当有厂商降低价格时其他厂商会跟进降低价格，因此此时价格的降低不会造成那么大的需求量上升，也就是说在拐折点以下的弹性较小。

这个模型的缺点第一是拐点的计算没有理论依据，第二是由于在拐折点商品弹性变化， 该商品的边际收入会在拐点出现分段，导致有一段区间无法计算边际收入与边际成本相等的点(即利润最大点)。

#### 古诺模型(Cournot Model)

古诺模型主要描述只有两个公司的寡头市场，其假设两个企业的边际成本相同，且两企业相互知道对方的产品供给量，最后模型得到的结果是两公司会选择相同的市场供给量。

#### 纳什均衡(Nash Equilibrium Model)

当市场达到纳什均衡状态时，每个单独的公司改变其自身决策都不会使其获得更好的结果。纳什均衡的一个经典例子就是`囚徒困境`。其假设是每个决策者以自身利益最大化为目标进行决策，但个人利益最大化的结果并不一定是群体利益最大化。现实中纳什均衡点可能并不存在。

打破纳什均衡的方法是`合谋(Collusion)`，当市场参与者较少，产品趋同，成本结构类似时才可以达成合谋，即所有厂商达成一致以某个价格销售商品。

#### 主导厂商模型(Dominant Firm Model)

当市场中有一家公司占有明显更大的市场份额时，市场可以适用主导厂商模型。在这个模型中主导厂商类似于垄断市场，而其他小厂商则类似于完全竞争市场。主导厂商可以以其自身的边际收入等于边际成本的点定价，而其他小厂商只能作为价格的接受者。这里面有一个假设是主导厂商由于规模效应，其平均总成本可能低于小厂商，因此若其定价介于自己与小厂商的平均总成本之间时会导致小厂商退出市场从而获得更多市场份额。而长期来看由于主导厂商的定价权会导致市场短期内存在经济利润，因此长期会吸引新的厂商进入市场，从而使主导厂商的市场份额下降。

### 价格歧视(Price discrimination)

价格歧视是对不同的客户以不同的价格出售相同的产品或服务，其程度分为三级：

一级价格歧视：垄断企业能够向每个客户收取该客户愿意付出的最高价格，最理想情况但基本不可能实现。

二级价格歧视：垄断企业提供基于购买数量的价格选项以获得客户可以接受的最合理的商品价格。

三级价格其实：客户被以人口分类的方式区别对待提供不同的商品价格 。

### 集中度指标计算(Concentration Measures)

集中度指标用于衡量市场的垄断程度，其中`N-firm concentration ratio`是将市场上份额占比最多的前N家公司的市场份额相加，而`Herfindahl-Hirschman Index(HHI)`则是计算市场上所有公司份额的平方和。前者优点是易于计算，但缺点是对兼并收购不敏感，即当两家大公司合并时前者可能只会小幅度上升。

两种集中度指标都有一个共同的缺点就是没有考虑市场的进入和退出壁垒。因为当市场壁垒较小时，既是是拥有大市场份额的公司也没有太多定价权。

## Reading 14 总产出，价格和经济增长

### 国内生产总值(Gross Domestic Product)

国内生产总值(GDP)是一个`国家/地区`在`一段特定时间内`生产的`最终商品或服务`的`市场总价值`。 当期的GDP**不包括**前期生产的商品的售卖或二次售卖、政府的`转移支付(transfer payments)`，生产中的商品、副产品、地下产业或`以物易物(Barter transaction)`。

与GDP类似的指标还有`国民生产总值(Gross National Product)`，GDP为属地概念，GNP为属人概念。

#### GDP的定义

`名义GDP(Nominal GDP)`简单来讲就是一个经济体生产的所有商品或服务在市场价格下的的总值，公式表达如下：
$$
\begin{align*}
Nominal\ GDP_t &= \sum_{i=1}^N P_{i,t}Q_{i,t}\\
&=\sum_{i=1}^N(price\ of\ good\ i\ in\ year\ t)\times(quantity\ of\ good\ i\ produced\ in\ year\ t)
\end{align*}
$$
`真实GDP(Real GDP)`是计算GDP时剔除物价水平变化的影响，使用基期物价水平，公式如下：
$$
\begin{align*}
Real\ GDP_t &= \sum_{i=1}^N P_{i,t-5}Q_{i,t}\\
&=\sum_{i=1}^N(price\ of\ good\ i\ in\ year\ t-5)\times(quantity\ of\ good\ i\ produced\ in\ year\ t)
\end{align*}
$$
需要说明的是公式中$P_{i,t-5}$是以5年前的物价水平作为基期物价水平，实际计算不一定是五年前。

`GDP平减指数(GDP Deflator)`是使用名义GDP和真实GDP的比值计算出的物价水平指数，用于反映通货膨胀水平，公式如下：
$$
GDP\ deflator=\frac{Nominal\ GDP}{Real\ GDP}\times 100
$$

#### GDP的计算

`The value-of-final-output method：`将生产的所有最终商品和服务的总价值加总的方法。

`The sum-of-value-added method：`将生产或分发商品及服务的各阶段的中间附加值累计计算总值的方法。

`Expenditure approach(支出法)`将国内所有支出相加获得总值：
$$
GDP = C+I+G+(X-M)
$$
其中$C$和$I$分别代表`私人部门`消费者在最终商品和服务的支出与国内私人总投资， $G$指`政府部门`的最终商品和服务的总支出，$X$和$M$则分别代表国际贸易的出口与进口，$(X-M)$则是国际贸易净出口额。

`Income approach(收入法)`将国内所有收入加总获得总值：
$$
GDP = Gross\ domestic\ income=Net\ domestic\ income+Consumption\ of\ fixed\ capital(CFC)+statistical\ discrepency
$$
其中$CFC$是用于衡量资产在生产过程中的正常损耗，统计误差则是用于将支出法与收入法所计结果统一的补充项。上式中`Gorss domestic income(GDI)`以下式计算：
$$
\begin{align*}
GDI &= Compensation\ of\ employees\\
&+ Gross\ operating\ surplus\\
&+ Gross\ mixed\ income\\
&+ Taxes\ less\ subsidies\ on\ production\\
&+ Tases\ less\ subsidies\ on\ products\ and\ imports
\end{align*}
$$
关于收入还有几个概念，`个人收入(Household primary income)`是衡量消费水平的重要指数，`可支配收入(Household disposable income)`是个人收入减去缴税部分后的收入水平，`家庭净储蓄(Household net saving)`是可支配收入减去家庭消费支出后的储蓄部分。

收入法还有一个变型式是将收入记为私人部门的$C$和$S$，即消费与储蓄加上政府部门的$T$即税收收入。将收入法计算的GDP与支出法计算的GDP联立可以得到下面的公式：
$$
S +T = I + G +NX
$$
其中$S$代表储蓄，$T$表示税收，$I$表示投资，$G$表示政府消费，$NX$表示净出口额。

### IS曲线(Investment与Saving的关系)

IS曲线反映的是国家商品市场的均衡，即投资与储蓄相等时总收入与利率的关系。 列式表达：
$$
Y= \frac{1}{1-b}(a + I + G +NX)
$$
其中$G+NX$假设为常数，a为正数，b为收入中的消费比例，范围在0-1之间，而投资$I$会随利率的增加而减少。因此可以得出结论利率$r$与总收入$Y$为负相关。进出口与财政政策则会引起IS曲线的平移，政府支出或出口增加会使曲线右移，总收入增加；反之政府税收或进口增加会导致曲线左移，总收入减少。

### LM曲线(Liquidity与Money的关系)

LM曲线反映的是货币市场均衡，即货币供给与货币需求的相等时，总收入与利率的关系。列式表达：
$$
\frac{MS_N}{P}=MD=L_1(Y)+L_2(r)
$$
其中$MS_N$是名义货币供给，$P$是物价水平。而$MD$货币需求有三类，`交易性需求(Transaction demand)`，`预防性需求(Precautionary demand)`和`投机性需求(Speculative demand)`。其中前两项被认为与总收入$Y$正相关，是一类需求$L_1(Y)$;第三项投机性需求是投资需要，受到利率$r$的影响较大，与$r$负相关，是二类需求$L_2(r)$。

$L_1(Y)$与$L_2(r)$总和不变，而当利率$r$下降使，投资性需求$L_2(r)$上升，此时一类需求$L_1(Y)$下降，而一类需求与总收入正相关，因此此情况下总收入也下降。利率$r$与总收入$Y$正相关。在给定的物价水平下，货币政策和物价水平使LM曲线平移。扩张的货币政策或物价下降增加$\frac{MS_N}{P}$，向右移动；反之向左移动。

#### 货币供给

通常认为货币供给由央行控制，因此货币供给曲线为不受利率影响数量的直线，如下图：

![货币需求供给曲线](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220725233559569.png)

 当货币供过于求时，利率较均衡点高，获取资金的成本高，市场倾向于购买证券，利率降低；反之利率升高。央行可以通过调整货币供给来影响短期的市场利率。

### 总需求和总供给曲线(AD&AS Curve)

对于CFA一级来说，我们需要掌握AD曲线的定义，反映的关系和移动，但AS曲线的推导比较复杂，只需要了解它的形状和移动。

#### AD曲线

 AD曲线主要是用于研究物价P和收入Y的关系，其纵坐标为P，横坐标为Y。使用IS-LM曲线模型可以知道当物价水平P上升时，实际货币供给量$MS_r$趋于减少，也就是说$L_1(Y)$与$L_2(r)$的总和减少，而$L_1(Y)$短期内不会变化，因此实际是$L_2(r)$减少，可以知道利率r上升，投资I减少，根据收入Y与投资I的关系可知Y会因此减少。由此可知物价水平P与总收入Y呈负相关关系。

由于AD曲线实际是IS曲线与LM曲线交点时市场状态的集合，因此AD曲线实际上就是货币市场与商品市场同时达到均衡状态时的物价P与总收入Y的关系。

影响AD曲线移动的因素就是会导致IS或LM曲线移动的因素，总的来说就是$C+I+G+(X-M)$中的各项因素和政府的货币政策与财政政策。举例来说：

- 消费者财富增加时会增加消费C，市场对未来的预期增强时会增加投资I，消费者对未来收入的预期增加时会增加消费C，资本效率上升时也会增加投资I。
- `扩张性的货币政策(Expansionary monetary policy)`是指政府增加货币供给，这会使银行有更多可贷资金，因此可能导致利率下降，从而刺激消费C和投资I。
- `扩张性的财政政策(Expansionary fiscal policy)`是指政府增加其支出预算，操作层面是指增加政府消费G或减少政府收入T，这会使市场总收入增加或市场可支配收入增加
- 汇率的变化会影响净出口额NX, 本国货币贬值或外国货币增值时，进口减少出口增加，导致NX增加。反之NX减少。
- 全球经济增长会导致其他国家的进口增加，也就是本国出口增加，导致NX增加。

#### AS曲线

AS曲线反映的是物价P与总产出Y的关系，纵坐标P，横坐标Y。 AS曲线需要从三个时间维度来看：

1. 超短期总供给曲线VSRAS曲线是完全弹性的，也就是物价水平不变的情况下产出依然会逐步增加，该情况主要出现于大萧条时，不常见。
2. 短期总供给曲线SRAS曲线是斜向上，即物价水平P与总产出Y正相关。
3. 长期总供给曲线LRAS曲线是垂直于总产出Y，也即物价水平不影响总产出Y。

##### LRAS曲线

长期总供给曲线LRAS曲线是稳定在`potential GDP`的水平，此时市场失业率为自然失业率水平。若市场产出小于`potential GDP`这意味着资源没有充分利用，也就是说市场失业率较高，市场处于`Recession`状态。反之若产出大于`potential GDP`这意味着经济过度利用的Inflation状态，失业率较低。

##### SRAS曲线

短期总供给曲线SRAS曲线是基于凯恩斯理论，认为工资具有粘性的基础上推导，也即短期内人工工资不会随物价水平变化而变化 。短期内物价水平上升，人员名义工资不变，表示真实工资下降，因此企业成本实际在下降，总产出Y上升。相反物价水平下降时，总产出Y下降，因此得出物价水平P与总产出Y负相关的结论。

##### AS曲线的移动

引起LRAS曲线移动的因素同样会导致SRAS曲线移动，但引起SRAS曲线移动的因素不一定会引起LRAS曲线移动。而会引起LRAS曲线移动的因素主要有五个，分别是劳动力供给、资源供给、劳动力受教育程度、实物资本、技术和生产力的增加都会使LRAS和SRAS曲线右移。而短期内会引起SRAS曲线移动的因素分别有名义工资减少、资源价格减少、未来预期物价上升、商业税收减少、补贴增加、汇率增加等都会使SRAS曲线右移。

### 宏观经济均衡状态(Macroeconomic equilibrium)

本节主要需要了解不同经济状态产生的原因与结果，以及使用模型分析的方法（新古典主义和凯恩斯的角度，即政府不干预或干预经济）。

#### 经济萧条(Recession)

总需求下降、导致产量和物价水平都下降。

在`政府不干预经济`的情况下，物价水平下降导致工人实际工资下降，生产成本从而下降从而促进总产出Y，短期总供给曲线SRAS右移使物价水平进一步降低而DGP恢复，市场均衡由1→2→3。

而在`政府干预经济`的情况下，政府会采用扩张的货币和财政政策，从而促进总需求曲线的右移，市场均衡由1→2→1。

![经济萧条状态的均衡](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220801232916678.png)

#### 经济过剩(Inflation)

总需求过剩，产量更高、物价水平也更高。

在`政府不干预经济`的情况下，物价水平上升导致生产成本上升，促使生产者减少产出Y，短期总供给曲线SRAS左移，GDP恢复到均衡水平但物价水平进一步上升，市场均衡由1→2→3。

在`政府干预经济`的情况下，政府采用紧缩的货币和财政政策，从而促进总需求曲线左移，市场均衡由1→2→1。

![经济过剩状态的均衡](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220801233432788.png)

#### 经济滞胀(Stagflation)

经济停滞(产出不足)，通货膨胀(物价上升)，主要原因是厂商生产成本的忽然上升，例如能源价格上升，导致厂商不愿意生产，短期供给曲线SRAS曲线左移，物价水平上升，产出下降。

在`政府不干预经济`的情况下，物价水平上升导致工人工资水平上升，总产出Y下降使失业率上升，长期而来工人只能接受更低工资，从而使生产成本重新降低，总产出Y回升，SRAS曲线右移，市场均衡由1→2→1，但需要时间较长。

在`政府干预经济`的情况下，政府会处于两难境地：如果政府采用紧缩政策，会使总需求曲线左移，物价水平回落，但总产出下降。如果政府采用扩张政策，会使总需求曲线右移，总产出恢复但物价水平会更增加。

![经济滞胀状态的均衡](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220801234315684.png)

#### 物价水平下降(Decrease in Input Prices)

物价水平下降会导致总需求曲线AS右移，总产出增加，物价水平下降，是较好的经济情况。

### 经济增长(Economic Growth)

影响经济增长的五大要素与引起LRAS曲线移动的因素相同，分别是：劳动力数量(Labor supply)、劳动力质量(Human capital)、实物资本(Physical capital stock)、科技(Technology)、和自然资源(Natural resources)。这些因素对生产力的影响可以由`道格拉斯生产函数(Cobb-Douglas Production function)`解释：
$$
Y = AK^\alpha L^{1-\alpha}
$$
其中Y指经济总产出，L指劳动力规模、K指资本量，A为`全要素生产率(Total factor productivity，由科技进步或劳动力受教育程度影响)`，$\alpha$为劳动力与资本的配比。

#### GDP增长率(Potential GDP growth rate)

$$
\Delta \% Y=\Delta \% A + \alpha \Delta \% K + (1-\alpha)\Delta \% L\\
\Delta \% y = \Delta \% A + \alpha \Delta \%k\\
\Delta \% Y = \Delta \% y + \Delta \% L
$$

其中各项含义与道格拉斯生产函数中各项含义相同，其中$\Delta \% y$为人均GDP变化率，$\Delta \%k$为人均资本变化率。 

## Reading 15 经济周期

`经济周期(Business Cycle)`是指经济活动中的波动情况，真实DGP和失业率是决定当前经济周期阶段的关键因素。经济周期的四个阶段分别是`低谷(trough)`、`扩张(expansion)`、`顶峰(peak)`、`紧缩(contraction)`。

![经济周期的四个状态](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220803225711694.png)

### 经济周期指标

判断经济周期有三个重要的指标，它们分别是：

- `Ratio of inventory to sales`：当扩张快要到达顶峰时，销售速度开始放缓，存货开始累积，导致存货销售比高于其平常水平，此时厂商作为应对会减少生产，导致顶峰后的紧缩。相反当紧缩快要到达低谷时，厂商发现其销售开始加速，存货开始更快消耗，存货销售比低于正常水平，厂商为满足上涨的需求会增加生产，存货销售比从而向正常水平靠近。这个指标需要在扩张或衰退的后期才能反映出结果，因此该类指标被称为`lagging indicator`。
- `Utilization of labor levels`：在扩张初期，厂商不确定是否经济已经复苏，因此失业率不会有较大变化，但工人可能出现加班情况，直到在复苏后期厂商确定经济复苏时才会开始扩招人员，社会失业率降低。同理在紧缩的前期，经济开始衰退时，由于解雇裁员有成本，厂商不会马上削减人数，而是会减少劳动力劳动时间，最后在经济衰退确认后才开始削减人力开支，社会失业率增加。
- `Utilization of physical capital levels`：与劳动力类似，可以反映出经济在扩张或收缩的前后阶段。

其他用于判断经济周期的指标还有购房趋势、房价与收入比、本国GDP相对其他经济体GDP变化情况等。

### 经济周期理论

对于经济周期变化的原因有不同的理论解释，其中最主流的就是凯恩斯主义理论、货币主义理论、和古典主义理论。本部分主要需要了解不同学派对于“`什么引起了经济周期？`”和“`是否主张政府干预经济？`”的答案差异。

#### 凯恩斯学派(Keynesian school)

凯恩斯学派主张认为政府应该采取赤字财政，`主张政府应该干预经济`。凯恩斯学派认为`总需求的变化`引起经济周期。后期发展的新凯恩斯主义与原本的凯恩斯主义只有一点差别，凯恩斯主义认为员工工资具有粘性，不会忽然巨变，而新凯恩斯主义认为所有商品价格都具有粘性。

#### 货币主义学派(Monetarist school)

货币主义学派的主要思想可以归结为`货币数量论`，该理论认为市场中的货币供给乘以货币流转次数与物价水平乘以商品总产量相同。同时短期内经济体的货币流转次数与商品产量不会有大幅改变，因此若央行增加货币供给就会使物价水平上升，导致通货膨胀。`主张政府不乱发货币，不干预经济`。

#### 古典主义学派(Neoclassical school)

古典主义最基本的理论就是亚当斯密提出的`看不见的手(Invisible hands)`，即市场可以自己调节，回复到均衡状态，因此古典主义学派都`主张政府不应该干预经济`。其中`新古典主义`认为`技术进步`引起经济周期；奥地利学派认为`政府的参与`引起经济周期；`新兴古典主义(New classic school: Real Business Cycle Theory)`结合新古典主义和奥地利学派，认为`外部冲击(external shock)`引起了经济周期，经济体的主要的外部冲击便是科技进步和政府干预。

### 失业率(Unemployment)

`就业人群(Employed)`是有工作的人口数量，`劳动力(Labor force)`则是指有工作和正在找工作的人口数量，劳动力数量要剔除不适龄人群、学生、无工作意愿人群等，`工龄人口(Working age population)`则指年龄在可工作年龄内的人口数量。

两个重要的指标计算：
$$
Labor\ force\ participation\ rate(劳动力参与率)=\frac{labor\ force}{Working\ age\ population}\times 100 \% \\
Unemployment\ Rate(失业率)=\frac{number\ of\ unemployed}{Labor\ force}\times 100 \%
$$
`摩擦性失业(Frictional unemployment)`指因为摩擦裸辞等原因辞职，在两份工作之间会有失业期。

`结构性失业(Structural unemployment)`指劳动力技能与岗位不匹配，例如因为科技进步导致一些职业技能不再被需要等等。

`周期性失业(Cyclical unemployment)`指因为经济周期导致的失业率的波动。

最后三个与失业率相关的名词解释：`Underemployed`指一个人有工作，但其有从事明显比目前更高产出的工作的资质。`Discouraged worker`指不愿意找工作的人群，这群人可能会在经济回暖时重新进入劳动力市场，从而拉高失业率。`Voluntarily unemployed`指自愿失业的人群，例如家庭主妇等，这个人群不计入劳动力人口。

### 通货膨胀(Inflation)

通货膨胀指所有物价水平持续上涨，其衡量方法是`当期物价水平相对基期物价水平的上涨百分比`。通常低水平的通货膨胀有刺激经济的作用，但`恶性通货膨胀(Hyperinflation)`则是指物价水平增长极快的情况。`通货紧缩(Deflation)`指物价水平持续下降。`反通货膨胀(Disinflation)`指通货膨胀率在持续下降，此时通货膨胀率还是正值，只是通胀速度放缓。

#### 通货膨胀指标

- `The consumer price index(CPI)`：CPI指数以特定商品或服务的当前价格与其基期价格的比值作为指标衡量物价水平。因为不同国家的商品篮子不同，导致不同国家的CPI指数不具备可比性。
- `GDP Deflator`：名义GDP与真实GDP的比值。
- `Producer price index(PPI)`/`Wholesale price index(WPI)`：计算方法与CPI指数类似，但其主要使用燃料、金属、农产品等生产者层面的商品作为物价指标物，其对物价水平提高的反映早与CPI指数。
- `Headline inflation`：在计算CPI指数时使用所有产品的价值作为指标，相当于GDP Deflator。
- `Core inflation`：不包含食物和能源等价格容易受到市场供求关系影响的消费者物价指数(CPI)，更真实反映通胀水平。

#### 消费者物价指数(CPI Index)

CPI指数使用当期物价比基期物价，方法是每个商品的价格与产量的乘积和，其中La氏指标使用各商品基期的产量计算，Pa氏指标使用各商品当期的产量计算：
$$
Laspeyres\ Index=\frac{\sum P_t\times Q_0}{\sum P_0\times Q_0}\\
Paasche\ Index=\frac{\sum P_t\times Q_t}{\sum P_0\times Q_t}
$$
La氏指标与Pa氏指标有三个主要缺点，CFA协会分别给出了解决方法：

- 没有考虑新产品：随时间推移将新出现的产品加入商品篮中。
- 没有考虑产品质量变化：使用`hedonic pricing(享乐定价法)`。
- 没有考虑商品间的替代效应：使用`Fisher Index`，即La氏指标与Pa氏指标的几何平均$I_F=\sqrt{I_P \times I_L}$。

#### 通货膨胀的原因

主要有`成本变化引起(Cost-push inflation)`和`需求变化引起(Demand-push inflation)`两种:

前者由于员工工资升高或生产原材料价格上升导致生产成本升高，经济滞胀，央行采用宽松的货币政策进一步拉高物价水平。

后者由于政府宽松的货币或财政政策以及出口增加导致，引起市场总需求增加，短期内导致实际GDP大于正常水平，工资要求更高工资引起生产成本升高，工厂减少产出，总生产曲线左移进一步拉高物价。

### 经济指标(Economic Indicators)

经济指标根据其反映经济状况的时间的不同，分为三类：

- `Leading EI`：先行指标的拐点在经济转变之前，用于预测经济走势。
- `Coincident EI`：同步型指标拐点与整体经济情况基本同步，用于验证预测指标。
- `Lagging EI`：滞后型指标拐点滞后于经济变化，例如失业率等。

重要的先行指标有`S&P 500指数`、货币供给、长期债券与短期借款间的利差、消费者指标、平均周生产时间、平均周失业保险索赔、生产商新订单数量、小厂商交货时间、新建房地产数量等。

# Session 5 

## Reading 16 货币与财政政策

政府`财政政策(Fiscal policy)`指政府通过调整其财政支出与税收来干预经济活动的方法。而`货币政策(Monetary policy)`则是指中央银行通过改变私人部门获得资金的成本(利率)来影响市场中的货币供给，并以此干预经济的方法。本章主要覆盖政府干预经济所采取的货币政策与财政政策的具体工具，以及其缺点。

### 货币政策

#### 货币乘数

中央银行每发行一元钱货币，其可能通过贷款流入市场的部分就是除去准备金的部分，而贷款流入市场后可能继续通过储蓄回到商业银行，商业银行又可以继续将这部分存款除去准备金部分后继续贷款，以此构成以$1-准备金率$的比率递减的等比数列，该数列和既是银行通过贷款在市场上创造的货币数量：
$$
Money\ created = \frac{new\ deposit}{reserve\ requirement}
$$
此处$reserve requirement$是央行规定的商业银行最低准备金率，$\frac{1}{reserve\ requirement}$便是货币乘数，其假设所有贷款都没有被消费，而是回到银行，是商业银行创造货币的理论最大放大效果。

#### 货币数量论(Quantity Theory of Money)

货币数量论的基本式就是货币供给数量乘货币流转速度等于物价水平乘真实产出：
$$
money\ supply\times velocity=price\times real\ output
$$
其中该理论假设流转速度V与真实产出Y为常数，即货币供给在长期直接影响物价水平，而不会影响总产出与失业率(该结论即被称为`货币中性Money neutrality`)。

#### 费雪效应(Fisher Effect)

费雪效应描述名义利率为真实利率与期望通货膨胀率的和：
$$
R_{Nom}=R_{Real}+E[I]
$$
费雪效应的背后原理是真实利率比较稳定，因此名义利率的变化主要由预期通货膨胀率引起。

#### 中央银行货币工具

- `政策利率(Policy rate)`：指央行盯住的市场利率，不同国家央行所看的市场利率不同， 但基本都是短期利率，其基本思想是通过短期利率影响长期利率。当利率降低时，市场获取资金的成本降低，市场倾向借贷，释放流动性，是扩张性的货币政策；反之则是紧缩性的货币政策。
- `法定存款准备金率(Reserve requirements)`：指央行规定的商业银行最低的存款准备金，准备金率越低，则商业银行可以贷出的金额就越多，释放流动性，是扩张性的货币政策；反之是紧缩性的货币政策。
- `公开市场操作(Open market operations)`：指央行在公开市场上买卖债券，央行购买证券则是将钱放出市场，释放流动性，是扩张性的货币政策；反之则是紧缩性的货币政策。这是美联储最常使用的货币政策工具。

#### 中性利率(Neutral interest rate)

一个经济体的中性利率是指既不会引起经济上涨也不会引起经济下降的货币供给增长速度。即：
$$
Neutral\ rate = \Delta \% GDP + target\ inflation=r_{real}+target\ inflation
$$
同时`政策利率(Policy rate)`是指真实GDP与真实通货膨胀率的和，因此对比政策利率与中性利率的本质就是对比`真实通货膨胀率(real inflation)`与`目标通货膨胀率(target inflation)`的大小，政府的目标是保证政策利率向中性利率看齐。

#### 货币政策的限制

货币政策影响的是短期利率，但`长期利率可能不会随着短期利率的变化而变化`：

- `bond market vigilantes`：当市场认为货币紧缩政策将会降低未来通货膨胀率的时候，他们会预期未来通货膨胀率更低，这会导致长期债券的价格上升，债券价格上升意味着长期利率的上升。反之亦然。
- `Liquidity trap`：由于市场经济处于萧条状态，银行或个人对市场信心不高，因此即使央行采取扩张的货币政策，增加了市场流动性，可能也并不能达到增加银行贷款或者刺激消费的目的。

## 财政政策

`凯恩斯学派(Keynesian economists)`认为财政政策对经济总需求的增长有非常强的影响，而`货币主义流派(Monetarists)`认为财政政策对经济的刺激是暂时性的而不会对长期的经济产生影响。财政政策的目标主要有三点：

- 影响经济活动水平和总需求
- 人口财富和收入的再分配
- 资源再分配

#### 财政政策工具

##### Spending Tools(支付工具)

- `转移支付(Transfer payments)`例如养老金低保等，向一部分人征税并为另一部分人支付，这部分支付不计入GDP。
- `经常性支出(Current spending)`例如公务员工资等政府的日常开支。
- `资本性支出(Capital spending)`例如公路学校等政府在基础设施建设上的支出。

支付增加增加总需求，是扩张性的财政政策，反之则是紧缩性的财政政策。

##### Revenue Tools(收入工具)

- 直接税(Direct taxes)：例如个人所得税和企业所得税等和收入有关的征税。
- 间接税(Indirect taxes)：例如销售税和增值税等价量税，**间接税对经济的影响更快**。

税收增加会减少社会可支配收入，是紧缩性的财政政策，反之则是扩张性的财政政策。

#### 财政乘数

与货币乘数的概念相似，财政乘数既是计算每单位财政净支出的增加会促进多少单位的经济总产出：
$$
Fiscal\ multiplier=\frac{1}{1-b(1-t)}\\
where\ b=Marginal\ propensity\ of\ consumption=\frac{C}{Y(1-t)}
$$

#### 财政政策的限制

- `Lag(滞后性)`：Recognition lag、Action lag、Impact lag等滞后性导致财政政策对经济的影响比较慢。
- `Crowding-out effect(挤出效应)`：政府部门的支出提高导致私人部门消费减少。
- `Ricardian Equivalence`：该效应认为扩张的财政政策例如减少税收不会导致总需求增加，而反而会使私人部门增加储蓄。

#### 债务比率(Debt Ratio)

债务比率的计算方法是国家总债务与国家GDP的比值。

### 货币政策与财政政策的混合使用

货币政策影响利率，从而影响私人部门和政府部门的支出，最后影响经济总产出。财政政策通过影响政府部门支出影响经济总产出。当货币政策与财政政策为同向时(同时扩张或同时紧缩)，其影响也是同向，但当两个政策方向相反时：

- 货币政策宽松，财政政策紧缩：由于两个政策会反向影响公共支出，因此此时对总产出的影响**不确定**。
- 货币政策紧缩，财政政策宽松：货币紧缩导致利率上升，从而使得私人部门的投资和消费下降，引起总产出下降。财政宽松导致政府部门消费上升，引起总产出上升，此时财政政策的影响大于货币政策，最后总产出上升。

## Reading 17 国际贸易

###  相关概念

- `进口(Imports)与出口(Exports)`：指公司、个人、及政府向外国购买或销售产品及服务。
- `自给自足的经济(Autarky or closed economy)`：指不与其他国家进行交易的国家。
- `自由贸易(Free trade)`：指国家对进出口没有任何限制或收费。
- `贸易保护(Trade protection)`：指国家对进出口有禁令、限制或收费。
- 世界价格(World price)：指商品或服务在没有限制的世界市场上的交易价格。
- `本土价格(Domestic price)`：指商品或服务在本地的价格，可能由于本土贸易限制与世界价格不同。
- `净出口(Net export)`：国家的出口价值减去其进口价值，大于零时为`贸易顺差(Trade surplus)`，反之为`贸易逆差(Trade deficit)`。
- `外商直接投资(Foreign direct investment)`：指在外国所有的生产资源，如土地、工厂、自然资源等。
- `跨国公司(Multinational corporation)`：指在一个或多个外国进行外商直接投资的公司。

### 比较优势与相对优势

当一个国家在生产产品时拥有以比其他国家更低成本生产的能力时，这个国家就拥有`绝对优势(absolute advantage)`；如果一个国家生产产品相较于生产其他产品的机会成本低于其他国家时，这个国家就拥有`相对优势(comparative advantage)`。

由于国家之间存在比较优势，因此一些国家生产某些产品时机会成本低于其他国家，因此国家间的贸易才会产生，交易双方才会获得双赢。

#### 李嘉图模型(Ricardian Model)

在李嘉图模型中，劳动力是衡量生产力的唯一变量，`劳动力生产效率(labor productivity)`的区别反映了科技水平的差距，也就是比较优势存在的关键。

#### 赫克歇尔-俄林模型(Heckscher-Ohlin Model)

该模型认为除了`劳动力`是衡量生产力的变量外，还有`资本`。也就是说劳动力生产率和资源本身是产生比较优势的原因。

### 贸易限制(Trade restrictions)

主要的贸易限制有5种：

- `关税(Tariffs)`：政府向进口商品征收的税款。
- `配额(Quotas)`：商品在一定时间内的进口限额。
- `出口补贴(Export subsidies)`：政府对公司出口商品的补贴。
- `最小国内供给(Minimum domestic content)`：对某些产品由本国厂商供给的最小要求百分比。
- `自愿出口限制(Voluntary export restraint)`：出口国家在第一定时间内可以出口到本国的数量限额。

### 资本限制(Capital restrictions)

一些国家会对本国资产的流入流出施加限制，其目的主要为以下几点：

- 减少本国资产价格的波动性
- 维持较为固定的汇率
- 保证本国利率维持在较低水平
- 保护某些重要战略产业

### 国际收支平衡表(Balance of Payment)

 国际收支平衡表是记录国家间交易的国际贸易的收支平衡表，主要需要了解的是表中主要包含的三个账户：

1. `经常账户(Current Account)`：主要包含日常商品和服务的买卖、投资收益(利息或股利)、单边转移。
2. `资本账户(Capital Account)`：主要包含个人资产转移、自然资源或无形资产的买卖。
3. `金融账户(Financial Account)`：主要涉及资金借贷等。

需要特别注意的是在一些特殊的情况：例如专利使用费和专利买卖的区别，其中专利使用费一般计入经常账户，而专利买卖则计入资本账户；买卖取票债券时计入金融账户，而股票或债券的投资收益则应该计入经常账户。

最后，影响国际收支平衡的主要因素从GDP收支法结果推导为下方公式：
$$
X-M=private\ savings+government\ savings-investment
$$

### 国际组织

- `国际货币基金组织(International Monetary Fund)`：功能上主要维持全球金融秩序。职责上会维持汇率稳定、促进国际贸易发展、成员国需要时借出外汇。
- `世界银行(World Bank)`：功能上主要是为了扶贫。职责上帮助发展中国家加强政府法律体系，加强发展中国家的金融体系，反贪腐等。
- `世界贸易组织(World trade organization)`：功能上主要负责国际贸易秩序。
- free trade areas (区域内无贸易限制) -> Customs union(成员国对外采取统一贸易限制) -> Common market(区域内劳动力与资本流动无限制) -> Economic union(成员国成立共同组织与经济政策) -> Monetary union(成员国使用统一货币)

## Reading 18 汇率

### 基本概念

- `base currency`指汇率中被标价的货币，`price currency`指标价用的货币。
- `名义汇率(Nominal exchange rate)`中剔除各个国家的物价水平(除以该国家的物价水平指数)即可得到`真实汇率(Real exchange rate)`。
- `基期汇率(Spot rate)`指立即交易时的汇率，`远期汇率(Forward rate)`指远期合约中约定的汇率。
- `卖方(Sell side)`指提供外币的银行机构，`买方(Buy side)`指购买外币的跨国公司等机构。
- `交叉汇率(Cross rate)`是指两个货币通过某个第三方货币计算的汇率。

### 远期汇率

若远期汇率减去基期汇率大于零，这说明`远期升水(Premium)`；反之若小于零说明`远期贴水(Discount)`。需要注意的是计算题中一个point表示0.01%，以百分比形式计算时，底数为基期汇率。

### 利率平价理论(Interest Rate Parity)

利率评价理论是联系利率与汇率关系的公式：
$$
\frac{F}{S}=\frac{1+r_X}{1+r_Y}
$$
其中$F$与$S$分别为远期汇率和基期汇率，$r_X$与$r_Y$分别是X和Y两国的名义无风险利率。

 该公式的理论逻辑是使用本币投资获取的利息应该与基期汇率换至外国货币后投资获取的利息再用远期汇率换回本币的收益相同，否则会产生套利机会。

### 本币贬值改善国际贸易

#### 弹性法(Elasticity Approach)

将本币贬值相当于购买本国商品的价格降低，从而促进本国商品总需求上升，同时外币标价的商品价格相当于上升，导致对外国商品的需求量下降，以此达成促进净出口量，改善贸易赤字的目的。但需要注意的是这种方法要成功的前提是商品`弹性较大`，即商品需求量随价格变化而变化的幅度较大。

#### J-Curve

由于本币贬值时，影响发生会有一定的滞后性。例如有一些订单已经签订，需要按原有订单生产，此时货币贬值会导致贸易额减少一段时间，随后由于需求量的变化大于汇率的影响，再将净出口额提升，形成J型曲线。

#### 吸收法(Absorption Approch)

吸收法使用GDP支出法推导，净出口额$NX=Y-(C+I+G)$，其中$(C+I+G)$即被称为总吸收。此时如果要通过贬值货币改善贸易赤字，就需要判断货币贬值是否能促进总产出Y，当经济体非充分就业时，本币贬值会刺激总产出Y上升，而当经济体已经充分就业时，本币贬值不会刺激总产出变化，因此无效。

[第18篇]  
