---
title: "[编程算法]基于Selenium的自动网页报价机器人功能实现记录"
date: 2022-08-01 03:07:15
category: 编程算法
description: "[第21篇]本篇记录了使用Python Selenium包为公司开发自动网页报价机器人时的一些功能实现。"
tag: [Python, 工作学习, Selenium, RPA]
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/algorithm.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/21-Automated_Website_Logging_Robot.jpg
---

# 序言

早在我的第4篇博文《[公司项目需要的自动化测试 Selenium 文档解读][1]》中我就提到过现公司有一个集团设定报价逻辑的报价系统，其本质是一个内部的网站。核保人员只需要在网站上填入投保人的相关信息就可以从网站设定的逻辑中获得报价并将报价录入公司系统中。但这个过程中操作人员需要不停与网页互动，等待网站响应等，通常填写一个汽车险报价需要花费一个人10-15分钟时间，非常耗时，一个熟练的操作员一个小时也只能发出4-6张报价单，而我们每个月需要的报价量都是数以千计，这使得整个报价操作的人工成本非常高。有了这个自动操作的机器人后，每个报价将只需要50秒左右就能完成。

本篇博文是在之前的自动化报价机器人的基础上，为了更增加机器人运行稳定性等方面升级调整过程中对一些功能实现的代码记录。

# 正文

现在的操作是操作员直接将信息填写进Excel表格中，脚本机器人读取Excel信息然后依次将表格中的信息填写到网站的相应位置最后发出报价单并记录单号和报价。为了避免输入的信息有误，有选项的Excel使用表单选择信息，而如果网页接受信息后弹出错误或提醒，脚本也会记录下这个提示的内容。其他还有选择表单中最相近选项等功能都会在这篇中介绍。

## 检查输入文件

虽然我在收集数据的Excel表格中设置了如表单等内容验证的功能，但有些网站报价必须要有的信息我也必须在保证Excel中存在。因此在脚本开始报价之前必须先检视一遍Excel文件中是否有缺失的信息。我的实现方法就是使用`Pandas包`将Excel文件读取成文件框格式，然后将可以允许空值的列名除外，检视所有列中是否有空值，如果有则报错请用户将空值补全。代码的实现上值得说的主要是避免将`assert语句`重复多次而显得语句赘余，因此直接使用循环exec执行字符串的方式：

```python
# 遍历所有不在非必填清单中的列，如果不是没有任何空值则报错。
Non_compulsory_col = ["Body Type", "Customer Address", "Replace No", "Unit", "Building", "District"]
for names in [x for x in data_record.head() if x not in Non_compulsory_col]:
    exec("assert(not data_record['{column_name}'].isnull().values.any()),'There are missing values in {column_name} Column, please fill in.'".format(column_name = names))
```

## 获取错误信息

使用Selenium与网站交互时，可能有一些情况下某个客户不能按正常步骤获得报价，或者信息本身不符合报价条件，又或者信息填写错误等等都会导致及脚本无法按照预期获得最后结果。这种时候我们的脚本需要记录下这些错误的原因从而让用户可以相应调整信息输入或回复给报价人不能报价等。而可能导致错误信息的原因根据我的测试都有好几种，我希望脚本可以将所有可能的错误信息全部记录下来。

### 脚本结构

我将每一个报价过程中填写每一个页面的脚本各自封装成函数，需要的参数只有记录编号。这样将每一条信息输入过程模块化，就可以在报错时更快定位到报错的位置。而在每一个函数中都加上一个`try: except:`的结构，如果出现错误则收集所有错误信息并`return`，需要注意的是我的每一个模块本身是没有返回值的，也就是说如果不报错的话每一个函数的返回值都应该是`None`。那么最后在循环遍历所有记录的函数中依次调用每一个函数并且检视这些函数的返回值，如果返回值不为`None`则说明这个模块出现了错误，这时以`continue`语句结束该循环并且记录下返回的错误信息。

```python
# 运行每条记录并检视返回值，如果不为None则说明报错，在Remark中输入返回错误内容。
for x in range(len(data_record)):
    status = start_quoting(x)
    if status != None:
        data_record['Remarks'][x] = status
        print("Quote record %s failed."% str(x+1))
        print(status)
        continue
    ...
```

### 抓取错误信息

导致程序没有按预期完成的可能原因有很多，有些是程序本身的bug，有些是填写信息无效，有些是系统判断不能报价等等。这时使用`try:except:`结构时报错本身的信息可以反映程序出错的原因，而网站上一些特定区域的提示则可以反映出网站未返回预期结果的原因，我们接下来要做的就是在自动测试的每一步中抓取这些信息并且保存。我使用的方法是用`list`将每一个可能出现错误信息的地方的信息都存起来，然后将有效的结果合成为一条字符串：

```python
# 以start quoting阶段为例。
try: ...
except Exception as e:
    # 首先标明在哪一个模块出现了错误。
    errormsg = ["Error in start quoting stage:"]
    # 然后将系统的错误信息附在list中。
    errormsg.append(str(e))
    try:
        # 如果error-list中有内容也附在后面。
        errormsg += [x.text for x in driver.find_elements_by_xpath("//ul[@id='error-list']/li[not(contains(@style,'display: none;'))]")]
    except: pass
    # 最后将errorText中的内容也附上。
    errormsg += [x.text for x in driver.find_elements_by_xpath("//li[@class='errorText']") if x.text != ""]
    # 将list中所有的信息用换行符隔开输出为一条字符串作为返回值。
    return "\n".join(x.strip() for x in errormsg if x.strip())+"\n"
```

这其中有两条值得详细讲一讲的代码：

1. XPATH的`"//ul[@id='error-list']/li[not(contains(@style,'display: none;'))]"`的用法中，需要注意的是`li[not(contains(@style,'display: none;'))]`表示前面那个`ul`元素下所有中`display`不为`none`的`li`元素：也即所有可见的`li`元素。
2. `"\n".join(list)`表示以`"\n"`分隔的方式将`list`中的每一项合并为一个字符串。而后面的`x.strip() for x in errormsg if x.strip()`则表示将`errormsg`这个`list`中每一项移除首尾空行后不为空的项组成的新`list`，也即移除`list`中的空项。

### 使用assert语句

有一些情况下程序没有按预期运行，但程序却无法立刻报错，例如按下某个按钮后网页没有按照预期进入下一个页面，但程序本身则是在运行下一个模块时才发现这个问题，或者有时候根本不能发现出现问题。这会降低错误抓取的信息的有效性，因此这时我们需要使用assert语句来在一些特定的地方判断代码是否已经按照预期达成了想要的效果。assert本身的使用就是设定一个判断，如果判断没有成立则让程序抛出一个`exception`，也就是强制进入我们的except的部分，对我们的脚本错误抓取来说非常有用。

```python
assert(driver.current_url.split("/")[-1]=="displayPortal.do"),"Login Failed, please check your credentials and try again."
```

上面这个assert语句会判断某个操作后，网页的url是否变为以`displayPortal.do`结尾，如果是则说明操作成功，否则进入报错流程。

## 匹配表单选项

我的程序是在前人开发的“直球版”脚本的基础上扩展，而前人在处理代理输入的车辆信息与报价网站车辆信息的匹配问题时使用的是`Cosine Similarity`的方法，将车辆的品牌、型号、描述等信息连起来之后与官网的描述拼接起来做`Cosine Similarity`比较，然后以相似度得分最高的结果为最终结果，其解决匹配错误的方法是将相似度得分以两车的排量差值扣减。这个方法有很多明显的缺点：

1. 将原本已经分段的信息合为一条，本质上是剔除了有用的信息（即分段点），这会导致匹配没有用上所有可用信息从而影响准确性。
2. 将代理填写的车辆信息与公司报价网站的通表对比，而通表是离线向相关同事拿的，这导致自动化程度不高且不容易实时同步最新车辆数据。
3. 将排量信息作为文本匹配相似度的修正值的信息使用效率非常低，事实上不同车型的排量信息应该是可以作为判断匹配是否成功的决定性依据的。

我想到的解决方法更加简便且匹配准确率更高，也非常简单，即直接提取网站上的表单列表，然后直接点对点逐条信息使用Python的字符串模糊匹配包`FuzzyWuzzy`进行匹配选择。

### FuzzyWuzzy

[FuzzyWuzzy][2]的使用`Levenshtein Distance(莱文斯坦距离)`算法计算两个字符串之间的相似度，此算法又称`Edit Distance(编辑距离)`算法，是指两个字符串之间，由一个转成另一个所需的最少编辑次数，编辑方法包括替换字符、插入字符、或删除字符。编辑距离越小，两个字符串的相似度就越大。

FuzzyWuzz有两个模块，分别是计算两条字符串相似度分数的`fuzz模块`和匹配列表中相似度的`process模块`。本节只介绍fuzz模块：

该模块下主要介绍四个函数（方法），分别为：`简单匹配（Ratio）`、`非完全匹配（Partial Ratio）`、`忽略顺序匹配（Token Sort Ratio）`和`去重子集匹配（Token Set Ratio）`。

- `简单匹配`直接以编辑距离计算相似度，与本章开头提到的剔除分段信息的原理相同，这种方法匹配出的结果准确度一般不如其他方法。
- `非完全匹配`将两条输入字符串中的短者对比另一条字符串中所有同长度的子串计算编辑距离，这种方法较简单匹配好，但若几个词间顺序变换会对结果产生较大影响。
- `忽略顺序匹配`以空格为分隔符将字符串分为多个子串并将所有字母转换为小写移除标点符号，最后将所有子串以首字母排序后组合在一起计算编辑距离。
- `去重子集匹配`使用set操作来直接取出字符串中的子串，因此重复或多余的子串会被忽略。

使用者可以根据自己的用例来选择适合的方法计算字符串相似度，他们的使用方法如下：

```python
from fuzzywuzzy import fuzz

#简单匹配
Ratio = fuzz.ratio("Hello world!", "Hello world!")
#非完全匹配
Ratio = fuzz.partial_ratio("Hello world!", "Hello world!")
#忽略顺序匹配
Ratio = fuzz.token_sort_ratio("Hello world!", "Hello world!")
#去重子集匹配
Ratio = fuzz.token_set_ratio("Hello world!", "Hello world!")
```

在我们的例子中，`去重子集匹配`应该是提供最精准的匹配结果的方法。

### 匹配车辆信息

车辆信息分为品牌、型号、描述等字符串信息和排量、吨位等数字信息，在匹配字符串信息时我们就使用上节提到的`fuzz`方法：

```python
from selenium.webdriver.support.ui import Select
import numpy as np

def match_option(value, element):
    # 使用Select函数将网站相应表单中的选项提取成list，
    option_lst = Select(element).options
    # 依次计算其相似度
    match_score = np.array([fuzz.token_set_ratio(x.text,value) for x in option_lst])
    # 最后返回相似度最高的选项字符
    return option_lst[np.argmax(match_score)].text

#使用Select函数的select_by_visible_text方法即可选择匹配的选项
matched_option = match_option(value, element)
Select(element).select_by_visible_text(matched_option)
```

上面这个函数中只需要传入一个需要匹配的字符串(代理提供的信息)与一个selenium网页元素(相应的网页表单)便可以返回表单中与代理提供的信息最匹配的选项，最后使用Select函数的`select_by_visible_text()`方法选择到匹配的选项。

而匹配数字信息的方法就更加简单直观了，直接在表单中找到离给定数字最近的选项：

```python
def find_nearest(array, value):
    # 使用numpy方法返回列表中与给定值的绝对差值最小的值
    array = np.asarray(array)
    idx = (np.abs(array - value)).argmin()
    return array[idx]

def match_cc(car_cc, element):
    lst = []
    for opt in Select(element).options:
        cc = opt.get_attribute('value')
        if cc != "":
            lst.append(int(cc))
#     lst = [int(x.get_attribute('value')) for x in Select(element).options if x.get_attribute('value') != ""]
    return find_nearest(lst, car_cc)
```

上面的代码没有什么好讲的，唯一的一点就是`match_cc()`函数中被我注释掉的那条代码和现在用的这个`append`的代码哪个更加合适一点，因此都放在这里。

```python
matched_option = match_cc(car_cc, element)
assert(abs(matched_option-int(data_record['Cylinder Capacity'][record_no]))<100),"No similar car available!"
```

最后在选择排量后，将选择的排量与给定的排量信息对比，如果差值大于100则说明匹配一定有误。

# 最后

在这篇文章中我记录了对之前的自动脚本的一些改进方法，同时为了方便没有任何专业知识的同事操作这个自动报价机器人，我还使用`tkinter包`另外设计了一个GUI界面，这其中也有许多值得一说的小技巧和实现记录，我会在下一篇文章中详细介绍。

[第21篇]  

[1]: http://raylei.space/2022/02/21/4-Selenium_documentation_learning/	"公司项目需要的自动化测试 Selenium 文档解读"
[2]: https://www.analyticsvidhya.com/blog/2021/07/fuzzy-string-matching-a-hands-on-guide/	"Fuzzy String Matching – A Hands-on Guide"

