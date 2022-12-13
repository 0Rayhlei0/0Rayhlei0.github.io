---
title: "[编程算法] 公司项目需要的自动化测试Selenium文档解读"
date: 2022-02-21 18:22:00
category: 编程算法
tag: [Python,Selenium,工作学习]
description: "[第4篇]本篇文章主要介绍了在公司项目中用Selenium做自动化测试的方法。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/algorithm.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/4-Selenium_documentation_learning.jpg
---

# 序言

基于刚进公司时接手的一个`自然语言处理`+`自动化测试`的项目，这篇文章我会主要覆盖Python的Selenium包的文档解读，由于在HKU时的毕业项目便涉及各种在线论坛的评论爬取，我对Selenium并不算陌生，但由于Selenium的内容功能是比较多的，本篇除了一些基础知识以外，我会重点关注与公司项目有关的部分。

# 正文

## 背景介绍

刚进公司的时候接手了一个前人的`自然语言处理`+`自动测试`项目。因为现在公司有一个由集团设定报价逻辑的报价系统，通常来说由代理或核保人员输入客户的相关资料便可以完成报价，但这个系统报价汽车险时要输入的资料非常繁琐，导致代理不愿意使用这个系统报价，影响报价率。考虑到这个系统中很多资料是没有意义的，因此前人建议代理直接填写车型排量司机年龄等必要资料，并用Python做了一个自动报价工具。

这个工具由两个大部分组成，第一个部分是自然语言处理，即使用`Cosine Similarity`算法将代理输入的车型信息与公司系统中的车型信息匹配，有机会我会再写一篇文章讲讲这部分。第二部分则是自动化测试，使用匹配到的车型信息利用Selenium自动填写资料并返回报价。前人对第一个部分的完成度是比较高的，因此我只是对代码`规范性`和`循环逻辑`稍作调整便可以获得较好的`文本匹配和稳定性`。但第二个部分他的测试显然是不够的（毕竟是未完成的项目），网站中有非常多的特殊情况例如某些资料未填写时其他资料将不会显示，司机年龄和驾龄都很小时会直接弹出错误信息不予报价，有时网站弹窗提示时需要先将该弹窗关闭才能继续操作等等。

**但由于代码本身涉及公司内部报价网站的架构，我`不会`在这里分享具体的代码或逻辑，因此本篇我会分享一些我在解决这些问题时通过[Selenium with Python][1]学习到的知识。**

## Selenium文档解读

在开始之前，我想先通过[这个问题][2]下大佬们的回答介绍一下`Selenium`和`Webdriver`是什么。`Selenium`是一个适用于各种浏览器和平台的网页应用的`自动测试套装`，各个主要的浏览器提供商都已将`Selenium`作为其浏览器内部部分进行支持，而我使用的则是`Selenium`为`Python`接入提供的一个包。而`Webdriver`则顾名思义是一个连接你的脚本和浏览器的一个程序，其通过在浏览器中注入`Javascript`的方式来控制浏览器行为，你可以想象你通过你的Python脚本告诉这个`“司机”(driver)`如何开这个`"车"(browser)`。

### 基本约定

在介绍具体的函数之前，首先介绍一下Selenium API的一个基本约定。Selenium API 有一些属性(Attribute)是可调用的(即方式methods)，有一些属性是不可调用的(即特性properties)，所有可调用的属性都以圆括号结尾。如下例：

```python
driver.current_url #这是一个property,是一个值。具体来说是"现在这个页面的URL"。
driver.close()#这是一个method，是一个动作。具体来说是"关闭当前窗口"。
```

### 打开网页

举例来说，当使用`webdriver.Chrome()`将`Chrome driver`设定为`实例(instance)`并将该实例赋值给`driver`时，使用`driver.get(“xx网址URL”)`，浏览器便会被打开并导航至该指定网址，需要注意的是`Webdriver`会等到网页完全加载完毕之后才将控制权返回你的脚本，也就是说在这个阶段你通常不用担心你的程序会急着在没有加载出来的网页中操作或找寻你要的东西，但如果网页使用了大量的`AJAX(Asynchronous JavaScript And XML`, 用于直接在已加载的网页中读取网络服务器数据)，那么driver可能无法判断网页是否完全加载，如果要确保网页完全加载可能需要使用selenium的[waits](#等待加载(Waits))函数。

### 定位元素

当我们进入了想要测试的网页之后，首先要解决的问题就是如何让driver找到你想要互动的元素，Selenium提供的方式非常丰富，包括`id, name, Xpath, link text, partial link text, tag name, class name甚至css selector`。

#### 举例说明

举例来说，如果我们有一个如下的网页：

```html
<html>
 <body>
  <form id="loginForm">
   <input name="username" type="text" />
   <input name="password" type="password" />
   <input name="continue" type="submit" value="Login" />
   <input name="continue" type="button" value="Clear" />
  </form>
  <p class="content"> Are you sure you want to do this?</p>
  <a href="continue.html">Continue</a>
  <a href="cancel.html">Cancel</a>
</body>
</html>
```

那么你可以分别通过下面这些方式定位你想要的各个元素：

```python
login_form = driver.find_element_by_id('loginForm') # 通过id定位到表格
username = driver.find_element_by_name('username') # 获得第一个name是“username”的元素
username = driver.find_element_by_xpath("//form[input/@name='username']") # 第一个有子input元素名字是'username'的表格中的这个input元素
continue_link = driver.find_element_by_link_text('Continue') # 第一个描述是'Continue'的链接
continue_link = driver.find_element_by_partial_link_text('Conti') # 第一个描述包含'Conti'的链接
p_element = driver.find_element_by_tag_name('p') # 第一个tag是p的元素
content = driver.find_element_by_class_name('content') # 第一个class名是'content'的元素
content = find_element_by_css_selector('p.content') # 第一个css selector符合给定条件的元素
```

上面这些`find_element_by_*`的方式都只能用于找到页面中`第一个`出现的`符合条件`的元素，而如果把方式换成相应的`find_elements_by_*`那么它将以list的形式返回页面中符合条件的所有元素(但**注意{% label 没有 red %} `find_elements_by_id`**, 因为一个html文件中`id只能是唯一`的)。

另外除了以上这些`public methods`以外，`Selenium`还提供了两个`private methods`：

```python
from selenium.webdriver.common.by import By

driver.find_element(By.XPATH, '//button[text()="Some text"]')
driver.find_elements(By.XPATH, '//button')
## 除了By.XPATH外，像private methods也同样有By.ID, By.LINK_TEXT, By.PARTIAL_LINK_TEXT, By.NAME, By.TAG_NAME, By.CLASS_NAME, By.SELECTOR这些参数可以选择。
```

需要注意的是，这两种方式并没有本质区别，因为`find_element_by_*`就是以`find_element`定义的，[参考这里][3]：

```python
def find_element_by_xpath(self, xpath):
    return self.find_element(by=By.XPATH, value=xpath)
```

#### 更多关于XPath

XPath通常来说是用得最多的定位元素的方式。XPath本身是一个专门用来定位XML文件中`节点(nodes)`的语言，由于`HTML`也可以由`XML`实现(`XHTML`), 这也使得Selenium用户可以用这个强大的语言来定位网页元素。XPath之所以用得比较多是因为理论上它可以定位到网页中的任何一个元素，无论它有没有被用`id`或`name`定义过。

XPath在selenium中使用也可以有两种方式，`绝对引用`或`相对引用`：

- `绝对引用(不推荐)`：绝对引用的路径是从`root(html)`层开始往后推，虽然绝对引用可能可以更精确定位到想要引用的元素，但它的缺点却在于网页文件的一点点变动都会导致引用不正确。
- `相对引用`：相对引用是定位目标元素到它附近的(最好是母元素)有`id`或`name`属性的元素的相对路径，虽然有几率错过真正想找的元素(比如有两个`name`相同的元素)，但引用相对页面变动也更加稳定。

举例来说，在上面这个[网页][#举例说明]中,我们可以使用很多不同的XPath来定位同一个元素：

```python
login_form = driver.find_element_by_xpath("/html/body/form[1]") # 绝对引用定位form
login_form = driver.find_element_by_xpath("//form[1]") # 文件中第一个form
login_form = driver.find_element_by_xpath("//form[@id='loginForm']") # id是"loginForm"的form
username = driver.find_element_by_xpath("//form[input/@name='username']") # 第一个form里面有name为“username”的input子元素
username = driver.find_element_by_xpath("//form[@id='loginForm']/input[1]") # id是"loginForm"的form元素里的第一个input元素
username = driver.find_element_by_xpath("//input[@name='username']") # 第一个name是"username"的input元素
clear_button = driver.find_element_by_xpath("//input[@name='continue'][@type='button']") #第一个name是"continue"且type是"button"的input元素
```

[W3School][4]有更细致更全面的XPath有关的教程。

### 等待加载(Waits)

自动测试项目中非常影响实际测试效果的一个因素就是这个部分了。Waits顾名思义就是让程序等待，Python的time包中有一个`sleep()`函数就可以做到这点，让程序暂停执行一段设定的时间。那么Selenium中的`·`有什么不同呢？`time.sleep()`是没有任何其他条件地让程序暂停一段时间，但Selenium中的`waits`却是令程序在某个条件被达成之前等一段设定的时间。换言之`一旦条件达成便立即执行`。Selenium有两种waits。

#### 显式等待(Explicit waits)

使用显示等待会让程序在`给定条件`出现以前等待一段时间，超过这段时间或达成条件才进行下一步操作。默认设定下，程序会每隔`500毫秒`判断一次条件是否达成。以这段代码为例：

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Firefox()
driver.get("http://somedomain/url_that_delays_loading")
try:
    element = WebDriverWait(driver, 10).until(
        EC.presence_of_element_located((By.ID, "myDynamicElement"))
    )
finally:
    driver.quit()
```

`expected_condition`是`selenium`预设的一些判断条件的函数，代码中的`EC.presence_of_element_located()`接受`locator`参数，而`locator`则是一个`(by, path)`的`元组(Tuple)`，这也是这里有两层括号的原因。当这个元素可以被定位后该函数会返回一个`true`(Boolean), 如果无法被定位这个函数则会返回`not null`。([参考这里][5])

`expected_condition`提供的预设好的网页条件还有以下这些：

- title_is
- title_contains
- presence_of_element_located
- visibility_of_element_located
- visibility_of
- presence_of_all_elements_located
- text_to_be_present_in_element
- text_to_be_present_in_element_value
- frame_to_be_available_and_switch_to_it
- invisibility_of_element_located
- element_to_be_clickable
- staleness_of
- element_to_be_selected
- element_located_to_be_selected
- element_selection_state_to_be
- element_located_selection_state_to_be
- alert_is_present

如果这些预设好的条件无法满足你的需求，你还可以自己`定义等待条件`，参考[文档][6]中的方法。

##### 一些容易有疑问的条件

上面这些预设的等待条件中有几个`非常相似`的条件，我特别拎出来讲一讲他们的区别：

- presence_of_element_located：只要元素在文件物件模型(DOM)`出现`便会返回true。
- visibility_of_element_located：元素在DOM中`出现并且高度和宽度大于0 (visible)` 才会返回true。
- element_to_be_clickable：元素需要`出现，可见并且可以互动`才会返回true。

显然越下面的条件比上面越加严苛，如果你想让你的脚本按一个`button`，那么比起它的出现或者可见，你更应该关心它是不是已经`可以被按`了。其他的条件的具体解释也都可以参考[源代码][5]中的写法和注释。

#### 隐式等待(Implicit waits)

隐式等待比显式等待在写代码的层面上更加简单，针对性也没有那么强。它只是让driver不能立马在DOM中定位到某项元素时，多等一段设定好的时间。隐式等待时间的默认设置为0，在一次`Webdriver`的使用中它只需要被`设定一次`。使用方式如下：

```python
from selenium import webdriver

driver = webdriver.Firefox()
driver.implicitly_wait(10) # seconds
driver.get("http://somedomain/url_that_delays_loading")
myDynamicElement = driver.find_element_by_id("myDynamicElement")
```

### 操作元素

Selenium中可以用来操作元素的方式实在是太丰富了，我在这篇中只会提到我项目中会使用到的，也是最简单最基础的几个操作方法。

#### 点击元素

非常直观，在你找到的元素后面调用`.click()`方式，便可以让driver尝试点击这个元素。

#### 填写输入

当你定位到一个可以`input`的元素之后，可以使用`send_keys("whatevertext")`来将`引号`中的内容填入`Input元素`中。需要注意的一点是，`send_keys()`也可以发送其他如`回车(Keys.ENTER)`,`空格(Keys.SPACE)`等键盘上的功能键的指令 ,因此这个函数可以在任何元素上被调用。另外在文本框中文字不会将已有的文字清除，如果文本框中已经有文字，`send_keys()`只会在已有文字的后面附上新加的文字。因此通常使用此函数在文本框中输入文字时建议先使用`.clear()`将文字清除。

#### 选择表单

Selenium使用户可以获取下拉表单的选项数据，并且使用`setSelected`来选中特定`OPTION标签`的元素。可用的选中方式如下：

```python
from selenium.webdriver.support.ui import Select
select = Select(driver.find_element_by_name('name')) # 选中第一个name为"name"的元素
select.select_by_index(index) # 按序号(index)选中表单选项
select.select_by_visible_text("text") # 按可见文字选中
select.select_by_value(value) # 按选项值选中
```

其中`select_by_visible_text("text")`和`select_by_value(value)`的区别在于，想要选中给定的`<option value="foo">Bar</option>`这个选项，需要使用`select_by_visible_text("Bar")`或者`select_by_value("foo")`。

另外，Select类中还有一些非常有用的公式如：

- `all_selected_option`: 用于返回一个select标签下的所有已选项的list。
- `deselect_all()` : 清除所有已选项（仅对支持多选的元素有效）。
- `options`: 返回表单中所有可选项。

#### 获取文字

要从网页中爬取文字就一定要用到元素的`text`属性，该属性即可返回元素中的文字。

## Chrome开发者工具

虽然现在其实我对网页和网络的运作方式还处于一团迷雾的状态，但因为要爬取网页元素，也算是小小接触了`Chrome`中`按F12`就可以打开的`开发者工具`，要写关于网页的脚本这个界面是一定绕不开的。下面我会介绍两个我作为萌新`自己乱点摸索出来的`对爬虫或自动测试非常有用的两个功能。**因为是自己摸索，所以很有可能走了弯路都不自知。如果有更好的方法，或者完整的玩转F12的指南手册，还希望各位大佬在评论区不吝赐教。**

### 在网页文件中定位元素

刚刚接触开发者工具的时候完全不知道如何在花里胡哨的html文件中找到网页中的某个元素，只知道在body里面一个一个往下找，对应着页面上的高亮一点一点往里点，后来才知道原来用Chrome的`这个功能`就可以快速定位到元素在html文件中的位置，非常方便。这是全世界都知道所以才没有被任何教程提及吗？

![按下这个“定位”按钮再点想找的元素就可以定位到该元素在html中的位置](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics/post_img/image-20220224195103131.png)

### 得到元素的XPath

同样也是一个大概所有人都知道(所以没有在任何教程里见到提及)，但我是自己玩了老半天才偶然发现的功能。原来在开发者工具中右键点击元素，找到`复制→复制XPath`就可以直接得到这个元素相对路径的XPath，不确定Chrome的算法是怎样，但似乎这个复制XPath是在尽量选择`不会导致ambiguity`的方式引用。

![对元素点击右键，然后依次按复制→复制XPath](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics/post_img/image-20220224195027232.png)

# 最后

因为这个项目的机会，我对网页自动测试甚至是爬取网页的经验又增加了不少（当然我知道一般爬取网页的首选项肯定是`BeautifulSoup`，毕竟不经过浏览器互动的爬取会稳定不少，但现如今大部分的网页不用浏览器互动已经啥都爬不到了）。另外之后有时间我会再把项目前半部分关于`Cosine Similarity`文本相似度匹配的部分整理好再发一篇。

[第4篇]

[1]: https://selenium-python.readthedocs.io/index.html	"Selenium with Python"
[2]: https://stackoverflow.com/questions/54459701/what-is-selenium-and-what-is-webdriver	"What is selenium and what is webdriver"
[3]: https://stackoverflow.com/questions/51035651/difference-between-public-and-private-selector-methods	"Difference Between Public and Private Selector Methods"
[4]: https://www.w3schools.com/xml/xpath_intro.asp	"W3School XPath Tutorial"
[5]: https://www.selenium.dev/selenium/docs/api/py/_modules/selenium/webdriver/support/expected_conditions.html#visibility_of_element_located	"Source code for selenium.webdriver.support.expected_conditions"
[6]: https://selenium-python.readthedocs.io/waits.html	"Selenium with Python (Waits)"

