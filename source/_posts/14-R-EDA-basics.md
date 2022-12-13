---
title: "[数据分析] 使用R做EDA分析的基础知识"
date: 2022-04-09 02:01:32
category: 数据分析
description: "[第14篇]本篇主要介绍使用R对数据做探索性分析(Exploratory Data Analysis)时需要掌握的一些基础知识。"
tags: [R,工作学习]
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/data.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/14-R-EDA-basics.jpg
---

# 序言

因为最近想要给公司做一些预测性模型来标注保单的取消风险而提取了一些相关的数据，在使用机器学习模型之前按照惯例需要对数据进行一些`探索性分析(EDA, Exploratory Data Analysis)`，并可能以此结果来指导机器学习模型的建造。那么在这篇里就先介绍一些EDA分析的例行步骤，以及如何使用`R`来实现这些步骤。

# 正文

我在查找资料的时候发现了一个针对EDA教学且解释非常细致的教学网站，是[Data Carpentry][1]为生态学家使用R分析数据做的基础指南，虽然在标题中表现出相当的特殊性，但实际内容却是针对EDA分析的一般性知识。我会根据他的内容和结构大致介绍如何使用R来进行EDA分析。

## 读取数据

使用R做数据分析必须要介绍的一个包就是[Tidyverse][2]，这是一个集合了数据收集，转换，清洗，可视化等一系列满足数据科学需求的包的集合。`Tidyverse`中包括的`reader`包就是用来读取数据的工具，通常我们会使用`read_csv()`包来将`csv文件`读取为R中的数据框对象。

关于`read_csv()`的参数设置，如果直接以文件名读取文件而不设置任何参数的话，经常会导致如下图所示，第一列数据表头的读取错误，这时我们需要在函数中加入`fileEncoding = "UTF-8-BOM"`,因为`read_csv()`默认解码方式是使用`无BOM的UTF-8`，这样读取一些带有BOM这种文件头的文件就会被错误解码。

![第一列列名读取错误](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220426214059545.png)

另外两个我用得比较多的参数是`stringsAsFactors`和`na.strings`。`stringsAsFactors`设置为`TRUE`时R会将文件中读取的字段按`因子(factor)`处理，这样当数据中需要作为训练使用的字符串格式字段较多时不需要将他们逐一转换为因子格式。`na.strings`则被用于认定丢失值，也就是说数据中出现这个参数设置的值时这条数据会被认为`NA`。`read_csv()`的使用示例如下 ：

```R
df.raw <- read.csv("data_clean.csv", fileEncoding = "UTF-8-BOM", stringsAsFactors = TRUE,na.strings = c(""," "))
```

## 数据检视

数据拿到手的第一件事是查看数据的大致情况，R有一些简单的公式可以让分析师对数据有一些快速简单的了解。

```R
class(df.raw) # 返回对象的类型，例如data.frame
str(df.raw) # 返回对象及内部元素的结构概览
view(df.raw) # 使用Rstudio的Data viewer来检视数据，可以看到所有数据并有简单的查找，筛选，排序等功能。
head(df.raw) # 默认检视对象中的前n条数据，n默认为6。类似的还有tail()，用于检视最后n条数据
summary(df.raw) # 用于获取数据框中每列数据的简单统计情况
```

### 数据框数据

`数据框格式(data frame)`数据是数据分析中最常见的数据格式之一，它的特点是将数据以表格的形式储存，每一列都是一个长度相等的`向量(vector)`，而每一行则代表一条数据，由于列的本质是向量，因此每列中的数据类型都应该相同。数据框数据的引用方法：

```R
df.raw[2,6] #选出第2行第6列的数据，以数据框格式返回
df.raw[2, ] #选出第2行所有列的数据，以数据框格式返回
df.raw[, 6] #选出所有行第6列的数据，以数据框格式返回
df.raw[6] #省略逗号时效果同上，选出所有行第6列的数据，以数据框格式返回
df.raw[c(1, 2, 3),c(4, 5)] #选出第1，2，3行第5，6列的所有数据，以数据框格式返回
df.raw[1:3, 5:6] #效果同上，1:3表示1至3的整数序列
df.raw[[1]] # 选出所有行第1列数据，以向量格式返回
df.raw[[1, 1]] # 选出第1行第1列数据，以值的格式返回
df.raw[, -1] # 数字前加-号表示去除该坐标，选出其余所有数据，以数据框格式返回
df.raw["id"] #还可以以列名的格式选择到列，返回格式为数据框
df.raw$id #$符号加列名表示以向量格式返回该列数据
```

### 因子

`因子(factors)`是R中存储`分类数据(categorical data)`时所用的一种特色的数据格式，这些数据的特点是它们会从有限数量的可能值中取值。一个因子类的变量一旦被创建，它就只能从预设集中取值，这些预设集被称为`水平值(levels)`，而因子变量本身则被以与这些水平集中的`标签(labels)`一一对应的`整数`储存。因此虽然因子变量看起来像字符变量，但实际上在数据处理时他们是被当成`整型向量`处理。

#### 将其他类型变量转换为因子类型

虽然我们在读取数据时已经设置过了将字符串形式数据以因子形式储存，但即使不这样做我们也可以用`factor()`方程来手动将需要转换的字符型列转换为因子型。

```R
df.raw$id <- factor(df.raw$id)
```

#### 将因子变量水平值排序

通常R会按字母顺序排列水平值并编号，但有些时候由于水平值本身有顺序含义(例如大中小)，因此R也提供了手动将水平值排序的功能。

```R
df.raw$id <- factor(df.raw$id, levels = c("第一"，"第二", "第三"))
```

#### 因子型变量转换为其他类型

如果需要将因子类型转换为数字或字符类型需要注意一点，因为因子类型本身以数字形式储存，所以直接对因子类型数据使用`as.numeric()`会导致变量被直接转换为因子储存的整数索引值，正确方法应该如下：

```R
as.character(sex) #因子型转换为字符型时可以直接使用as.character
as.numeric(as.character(year_fct)) # 若要将因子标签转换为数字型，需要先转换为字符型
as.numeric(levels(year_fct))[year_fct] # 效率更高的方法是先将所有标签一一转换为数字，然后将这些数字对应至变量中
```

#### 因子水平值重命名

在R中，如果一个因子变量中存在缺失值，这些缺失值会被默认忽视，他们不会有自己的水平值。但事实情况中存在一些留有信息的缺失值，比如因为特定情况导致特定记录的值无法采集，这种情况下如果忽略这些缺失值实际上是丢失了有效信息，因此不同情况下我们也需要把缺失值放入水平值集中并可能需要重命名。

```R
sex <- surveys$sex
levels(sex)
#> [1] "F" "M" NA
sex <- addNA(sex)
head(sex)
#> [1] M    M    <NA> <NA> <NA> <NA>
#> Levels: F M <NA>
levels(sex)[3] <- "undetermined"
head(sex)
#> [1] M            M            undetermined undetermined undetermined
#> [6] undetermined
#> Levels: F M undetermined
```

总结下来就是使用`addNA()`可以将缺失值加入因子型变量中，然后使用`levels(sex)[3] <- "undetermined"`则可以将`undetermined`赋值给`sex`的第`3`个水平值。

## 数据清洗

在这一步中我们需要挑选，调整，创建一系列的变量，来达到获得理想的适合进行数据分析的数据集的结果。我们首先介绍一些`tidyverse`中`dplyr`包的功能，这个包中的函数可以实现上面提到的大部分数据操作。

### 挑选和筛选

要做数据清洗首先需要的第一个功能就是以特定需求挑选所需的数据，`dplyr`包中的`select()`和`filter()`就是分别用来挑选数据列和行的。具体用法如下：

```R
select(df.raw, id, sex, age) # 第一个参数为数据框，其他为需要挑选的列
select(df.raw, -id, -sex) # 在列前加-号表示不需要该列
filter(df.raw, sex == "M") # 筛选符合条件的记录
```

通常在我们处理数据集时要将数据集先后进行各种操作，如果将他们逐一赋值或嵌套会非常混乱且麻烦，因此`dplyr`也提供了方便的`pipe`功能，可以将前一步操作的结果直接输入下一步操作的第一个参数。例如我们想要从`df.raw`中先筛选出性别为`M`的记录，然后选出他们的`age`与`id`作为数据集：

```R
df.raw %>% #将df.raw输入到下一步
  filter(sex == "M") %>% # 筛选，第一个参数为df.raw
  select(age, id) # 挑选，第一个参数为filter(df.raw, sex == "M")
```

上方步骤中，`%>%`这个符号是代表`pipe`的操作符，在`Rstudio`中可以使用`Ctrl + Shift + M`来快速输入。

#### is.na()

`is.na()`公式是在用来判断对象是否为缺失值的公式，可以配合`filter()`公式使用来排除某列中为空的记录：

```R
df.raw %>%
  filter(!is.na(sex)) # 将sex列值缺失的记录筛选出去，!符号代表不需要
```

### 创建新列

通常如果我们需要在数据集中根据已有列创建新列，就需要使用`mutate()`函数。他的使用方法非常简单：

```R
mutate(df.raw, salary_in_k = salary/1000) # 创建一个名叫salary_in_k的列，内容为salary/1000
df.raw %>%
mutate(salary_in_k = salary/1000) # 以pipe的方式实现上句
```

而我们通常在创建新列的时候除了进行计算，也会做一些例如判断或将连续变量离散化分组的操作，下面介绍的两个函数就可以帮助完成这两个操作。

#### cut()

`cut()`函数可以被用来对连续变量进行离散化分组，实际用法如下：

```R
df.raw %>%
  mutate(Age = cut(Age, breaks = c(0,14,24,64,Inf), labels = c("Children","Youth","Adult","Senior"),include.lowest = TRUE))
```

该函数中，`breaks`参数既可以取不同取值点，也可以使用整数表示将区间平分为整数个。`include.lowest`设定为`TRUE`时分组区间的最左边区间会取双闭区间。其他参数或具体示例可以参考[该网站][3]。

#### ifelse()

`ifelse()`函数可以用来做各种判断取值，实际用法如下：

```R
df.raw %>%
  mutate(NOC = ifelse(is.na(NOC),0,NOC)) # 若NOC为NA，则使用0，否则使用本身的数值
```

### 数据分组计算

有些情况下我们需要对一些数据进行分组的计算和整理，比如统计某个特定分类的数量或者平均值，或者这个分类中各个更小的分类占这个分类数量的半分比等，就可以用`group_by()`这个函数实现，以我给公司分析的数据中使用的代码举例：

```R
# check the percentage of renewal for each product at each renewal point ---------------
# count the number of records for each group first
Renewal_CNT_table <- df.LAPSED %>%
  group_by(CNTTYPE, MAX_ZRENNO, Lapased_reason_desc) %>%
  summarise(count = n())
# the percentage of each number of renewed times for each product
Renewal_percent <- Renewal_CNT_table %>% 
  group_by(CNTTYPE) %>% 
  mutate(Total = sum(count)) %>%
  mutate(renewed_prcent = count/Total) %>%
  na.omit()
```

需要注意的一点是在上面代码的第二部分，我们`Total = sum(count)`的操作虽然是针对所有行，但`sum`本身却由于前面的`group_by(CNTTYPE)`只针对`CNTTYPE`中的每一个`factors`，以此算出了每个单独的`CNTTYPE`的和。

#### arrange()

`arrange()`函数可以用来将数据框以特定列的数值排列，用法如下：

```R
df.raw %>%
  arrange(sex, salary) %>% # arrange默认将列按从小到大，从A到Z的顺序排序
  arrange(desc(salary)) # 若要从大到小，从Z到A排序则需要加desc()函数
```

#### count()

对数据框对象使用`count()`函数并指定特定列名，效果等同于以该列分组后计数。实际使用如下：

```R
df.raw %>%
    count(sex, sort = TRUE)
```

## 数据可视化

探索性分析的最后一步就是将处理好的数据进行对比展示从而得出所需信息了，`tidyverse`中使用`ggplot2`来进行数据可视化。本节我会首先介绍下`ggplot2`的函数使用的基本格式，然后介绍一些常见的函数和参数，这里最后附上一个`ggplot2`的详细的[文档网站][4]。

### 函数格式

之所以专门要说一说函数的格式是因为`ggplot`的函数使用格式与其他常见包有较大的区别，当需要在一张图上增加不同功能或元素时不同部分之间使用`+`号连接。
> ggplot(data = <DATA>, mapping = aes(<MAPPINGS>)) +  <GEOM_FUNCTION>()

### ggplot()

`ggplot()`是`ggplot2`作图的最基础的模块，在这个函数内指定作图的数据源，同时在这个函数中我们也可以使用`aes()`函数设置图片可视化的不同维度。使用方法如下：

```R
ggplot(data = df.raw, # data参数中指定使用的数据集
       mapping = aes(x = sex, # x轴维度
                     y = salary, # y轴维度
                    fill = CNTTYPE)) #填充颜色
```

需要强调一下`aes()`的[使用方法][5]，该函数本身用来指定需要制作的图的各个参数，可以在`ggplot()`中设定，也可以在各层`GEOM_FUNCTION`中单独设置。其中`fill`这个参数如果使用特定颜色则表示使用改颜色填充图，若使用某个因子型变量则代表在图中使用不同颜色标明这个变量的不同值。

### 常用图类型及参数设置

- `geom_point()：`根据数据绘制点图，`size`, `color`, `shape`三个参数分别可以控制点的`大小`，`颜色`和`形状`。可以增加`geom_rug()`,`geom_density_2d()`或`stat_ellipse()`等功能增强显示，具体参见[此页面][6]。
- `geom_smooth()：`对点图绘制回归线，`method`参数可以选择默认的`loess`或`lm`，后者可以通过`formula = y ~ poly(x, 3)`参数指定回归的次数，`se`参数设定为`TRUE`时显示回归线的置信区间，`fullrange`设定为`TRUE`时回归线会跨过整个图，`level`参数是置信水平，默认为`0.95`。
- `geom_line()：`根据数据点绘制线图，可以使用`linetype`调整线的形状，在`group`参数中可以对不同的分组绘图。
- `geom_abline()：`在图中添加线，`intercept`和`slope`参数分别设定线的截距和斜率。除了`abline()`以外还有`vline()`, `hline()`, `geom_segment（）`。具体使用参见[此页面][7]。
- `geom_boxplot()：`绘制箱型图，`outlier.colour`, `outlier.shape`, `outlier.size`三个参数分别设置异常值的颜色，形状和大小。另外有一个`notch`参数设置为`TRUE`时将绘制展示中位数置信区间的箱型图，用以对比两组数据中位数的差异。可以配合`geom_dotplot()`或`geom_jitter()`在箱型图中绘制点分布，具体使用参见[此页面][8]。
- `geom_bar()：`柱状图，`stat`参数若为`identity`则y轴以y值计算，若为`bin`则y轴以记录数计算，`position`参数可以为`dodge,stake`或`fill`来对比，堆叠或百分比显示柱状图。另外可以使用`coord_flip()`翻转坐标轴或使用`coord_polar("y", start=0)`来制作饼图。其他更多设置参考[此页面][9]
- `geom_histogram()：`直方图，用于展示数据的分布情况。也可以像柱状图一样使用`position`参数调整不同组数据的展示方式，`alpha`参数用于调整图像透明度。更多使用方法参考[此页面][10]。
- `geom_density()：`概率分布图，与直方图效果类似，但是使用曲线围出的面积为1的概率分布图来描述不同值出现的概率，可以配合直方图展示。

### 其他常用函数

#### 多面对比(Faceting)

`facet_wrap(facets = vars(sex))`或`facet_grid(rows = vars(sex), cols = vars(age))`可以分别以两种方式制作多图对比。效果如下：

![facet_wrap()](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220426115942939.png)

![facet_grid()](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220426115930523.png)

要将多图对比时也可以使用`图1 + 图2 + plot_layout()`的表达方式将多图展示，该用法需要先安装`patchwork`的包，具体参数及用法参见[该网站][11]。

#### 设置图标签

`geom_text()：`该函数可以在图中标出各点的文字信息，用法如`geom_text(label=rownames(mtcars))`。

`labs():`可以使用该函数修改图片的各个文字标签，主要参数有`title`修改图标题，`x`修改x轴标注，`y`修改y轴标注，`fill`修改legend标注等。

#### 图片主题

`theme_gray()：`灰色背景与白色格线。

`theme_bw()：`白色背景与灰色格线。

`theme_linedraw()：`在theme_bw()的基础上图界有黑线包裹。

`theme_light()：`浅灰色线与轴，更凸显数据本身。

`theme_minimal()：`几乎没有背景标记。

`theme_classic()：`R的经典图片格式，有图片边框无格线。

`theme_void()：`无任何标记。

`theme_dark()：`暗灰色背景，适用于颜色丰富的图片。

[1]: https://datacarpentry.org/R-ecology-lesson/index.html	"Data Analysis and Visualization in R for Ecologists"
[2]: https://www.tidyverse.org/	"Tidyverse"
[3]: https://r-coder.com/cut-r/	"Cut function in R"
[4]: http://www.sthda.com/english/wiki/ggplot2-essentials	"ggplot2 - Essentials"
[5]: https://ggplot2.tidyverse.org/reference/aes.html	"Construct aesthetic mappings"
[6]: http://www.sthda.com/english/wiki/ggplot2-scatter-plots-quick-start-guide-r-software-and-data-visualization	"ggplot2 scatter plots : Quick start guide - R software and data visualization"
[7]: http://www.sthda.com/english/wiki/ggplot2-add-straight-lines-to-a-plot-horizontal-vertical-and-regression-lines	"ggplot2 add straight lines to a plot : horizontal, vertical and regression lines"
[8]: http://www.sthda.com/english/wiki/ggplot2-box-plot-quick-start-guide-r-software-and-data-visualization	"ggplot2 box plot : Quick start guide - R software and data visualization"
[9]: http://www.sthda.com/english/wiki/ggplot2-barplots-quick-start-guide-r-software-and-data-visualization	"ggplot2 barplots : Quick start guide - R software and data visualization"
[10]: http://www.sthda.com/english/wiki/ggplot2-histogram-plot-quick-start-guide-r-software-and-data-visualization	"ggplot2 histogram plot : Quick start guide - R software and data visualization"
[11]: https://www.rdocumentation.org/packages/patchwork/versions/1.1.1/topics/plot_layout	"plot_layout: Define the grid to compose plots in"

