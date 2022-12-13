---
title: "[编程算法] 使用urllib和BeautifulSoup制作爬虫脚本收集公司公开信息的记录"
date: 2022-06-18 14:50:45
tags: [工作学习, Python, BeautifulSoup, 网页爬虫]
categories: 编程算法
description: "[第19篇] 本篇将介绍我最近为收集公司商业客户的公司成立时间等基本信息利用Python爬虫脚本在公开网站中收集数据的记录。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/algorithm.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/19-A-web-scraper-for-company-info.jpg
sticky: 3
---

# 序言

前段时间老板在看我司商业客户的数据统计结果时提出想要看一看我司现在商业客户的公司成立时间维度的分析，以此来推断新冠疫情是否对我司的一些统计指标造成了显著的影响。但我司数据采集时并没有向客户收集类似信息，而网上已经整理好的公司信息数据库一定是需要大笔花费才能买到的，好在我们只是需要像成立时间这样的基础信息，只要能找到可以查询到相应信息的公开网站，我们就可以使用Python写一个简单的爬虫脚本来系统性地收集这些数据。

这篇文章就介绍了我利用`urllib`和`BeautifulSoup`两个著名的爬虫库，从公开网站[香港数据库集][1]中扒出这些分析所需数据的小小的项目记录。

# 正文

## 准备阶段

当我们需要从网络上收集一些特定信息的时候我们要做的首先就是找到一个有这些信息公开网站，那么我开始这个项目的第一件事就是和我们负责商业客户的业务同事聊一聊他平时需要这些信息时通常去哪里看。同事给了我很多不同的选择，但其中有一些是香港政府的公司注册网站或其他收费的公司信息数据库平台，稍微浏览一下网站就知道这些网站通常都做了很严格的防爬虫措施。

最后通过一顿筛选我找到了这个号称是香港政府开放数据的数据库网站[香港數據庫集][1]，在这个网站中确实有许多政府相关的数据查询功能，其中就有[这个页面][2]可以根据公司名称查询公司信息。

## 研究网站

### 网站逻辑

要从网站上爬数据首先就是要把网站研究清楚，看使用什么方法最方便最快捷。首先搞清楚我们手上有的东西，事实上我们拥有的信息确实是非常的少，对于在我司购买商业保险的商业客户，我们除了他们的公司名和业务编号以外，并没有收集任何其他可以用于识别他们的信息。而这个网站可供用于引索的方法有四种：

- 通过公司名搜索，利用网站内建的搜索引擎链接公司名和公司独立信息页面。
- 通过公司注册编号，直接去往公司信息页面。
- 通过注册时间，每天都有一个单独的页面整理了所有这天成立的公司的清单，连接到公司信息页面。
- 通过注册地点，香港的每一个地区都有一个单独的页面整理注册在这个地区的公司清单，同样清单中包含每个公司信息页面的链接。

这其中后两种方法是非常绕的，对我们的目标也没有任何帮助(但不排除有其他需求时可以使用)。而前两种方法则分别有各自的利弊：

- 若通过公司名搜索有两个问题，一是可能无法搜到我想要的公司数据，而在爬虫运行的过程中我又很难判断哪些搜索成功，哪些没有；二就是这个搜索的方法会比较费时间，因为我需要将我的每一个公司名都单独搜索一遍，时间复杂度是O(n^2)。
- 通过注册编号搜索速度会快很多，因为公司的信息页索引编号其实就是公司注册编号，因此我们其实可以直接循环公司注册编号把整个数据库一锅端。但事实上现在这个编号数量已经到了三百多万，而我们要查的公司名总共也不过三万条。

最后很明显，只有`通过公司名搜索`这个方案可能可以较大程度上地满足我们的需求。

### 网站界面

确定可行的方法后，就开始实际研究如何获得想要的信息，正常以公司名查询公司信息的话，应该在公司名称搜索的页面中输入公司的详细名称，然后在返回的结果中默认第一条是网站数据库中与关键词最相似的结果。点击这个搜索结果的链接就可以进到公司的实际信息页面。

![搜索公司名会返回一个有排序结果的页面，其中包含相应公司的信息页链接](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220619105617437.png)

在公司的信息页面中，则可以看到我们需要的成立日期等信息。我们之后要做的就是研究如何解析这一部分的html代码从而自动完成这两步操作并获取这些信息。

![进入公司信息页后便可以看到我们要的信息](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220619105916222.png)

## 编写脚本

经过上一步对网站的研究后，我们的思路就很清晰了，现在只需要按刚刚的步骤逐步将人手操作的部分写成脚本。

### 搜索公司名

首先要明确我们的输入，就是公司商业客户数据库中的客户名，直接把这些名字拿出来做成一个csv列表，然后遍历即可。那么第一步我们先完成获取每一个公司的信息页面的函数。因此我们想要构建一个输入是公司全称，输出是网站查询到的第一条公司信息的网页链接的函数。

另外，虽然我们人手查询时需要在输入框中输入查询字段并点击查询，但实质上通过地址栏我们可以看到这一步操作其实就是向网站服务器发送一条带有查询字段的搜索请求，因此我们的脚本实际并不需要做这些互动操作。

![查询公司名的本质就是向网站发送一条带有查询字段的搜索请求](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220619111505511.png)

通过研究网站的html结构，我写出来的代码如下：

```python
# 搜索页面的endpoint就是search?keywords=后加上搜索词的URL编码
endpoint = 'https://hkg.databasesets.com/zh-hant/gongsimingdan/search?keywords='
endpoint_main = 'https://hkg.databasesets.com'
def get_company_link(companyname):
    try:
        # 这个网站需要在请求中加入User-Agent的文件头，否则会拒绝请求。
        # 同时注意要将查询的公司名用quote()函数转换为URL格式
        index_page = urllib.request.Request(endpoint+quote(companyname), headers={'User-Agent': 'Mozilla/5.0'})
        # 如果网站不在10秒内返回请求则当做这条信息查询不到，直接函数返回0。
        html_index = urllib.request.urlopen(index_page, timeout=10).read()
    except:
        return 0
    bs_index = BeautifulSoup(html_index, "html.parser")
    # 在网站返回的html中找到所有class是'field-content'的元素
    comp_list = bs_index.find_all(class_='field-content')
    # 如果返回的清单是空，则代表搜索不到，函数返回0。
    if not comp_list:
        return 0
    else:
        # 如果清单不为空，则返回第一条记录的a元素中的链接。
        return endpoint_main+comp_list[0].a.get('href')
```

需要补充的一点是，搜索到的链接使用的是相对引用，因此我们直接拿到`href`信息后还要把它和网站的根URL连在一起才是可以直接访问的页面链接。

![这段html长这样](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220619113226433.png)

### 处理搜索名称

在实际测试脚本的时候我发现我们公司的数据中，客户公司名称有时候可能因为一些缩写导致不能搜索到正确结果，其中最主要的原因就是将`Company`缩写为`Co`，`Limited`缩写为`LTD`。如果直接使用这些名称搜索的话就搜索不到相应的公司。所以我想的办法就是去掉所有这些缩写的`CO`或者`LTD`字段，直接只搜索前面有意义的名字。

代码上实现如下，输入是公司名的字符串，输出是截掉特定字的结果：

```python
def trun_name(companyname):
    # 通过观察发现大部分的缩写都是下面这些
    trun_words = ['CO', 'LTD', 'CO.','LTD.']
    # 将输入字符串通过空格分开成清单，然后去除清单中满足条件的字符串，最后重新用空格组成字符串
    name_split = companyname.split()
    new_name_split = [x for x in name_split if x not in trun_words]
    new_name = ' '.join(new_name_split)
    return new_name
```

这里需要注意的是因为这些缩写在单词中也不少见，所以不能直接`replace()`，否则会把单词中的这些组合也都一并删除了。

### 获取公司信息

现在我们假设通过前两步的环节，我们已经可以通过公司名称获得他的信息页链接了。接下来我们就要从这个返回的信息页中解析并提取我们需要的信息并整理。从下面代码的结构可以看到我们需要的信息被存在一个个的`li标签`元素中，而我们需要的信息都在这个元素的子元素中，一个自然想到的方法是使用`BeautifulSoup`的`contents`属性来获得每个`li`元素的子元素内容，然后根据表头信息把其中的内容分类装进字典中保存。

![每一条信息都是个li元素，每个li都有一个表头一个冒号和对应的内容](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220619134323181.png)

代码如下：

```python
def get_comp_info(comp_link):
    # 与搜索公司链接的方法一样， 尝试请求公司信息页面，如果超过10秒钟则默认无法获取信息，返回空字典
    try:
        resp = urllib.request.Request(comp_link, headers={'User-Agent': 'Mozilla/5.0'})
        html = urllib.request.urlopen(resp, timeout=10).read()
    except:
        return {}
    bs = BeautifulSoup(html, "html.parser")

    # 用一个转置字典来规定每个标签名和其对应的保存名，以此达到case...when...的效果
    switcher_dict = {
        '注冊編號/Register Number':'RegisterNo',
        '中文名稱/Chinese Name':'ChineseName',
        '英文名稱/English Name':'EnglishName',
        '成立日期/Date of Establishment':'EstablishDate',
        '行業分類/Category':'Industry',
        '公司現狀/Active Status':'Status'
    }
    temp_info = {}
    x = bs.find_all('li')
    # 把页面中所有所有li元素遍历一次
    for item in x:
        temp=item.contents
        #判断每个li中的第一个子元素文字是否是转置字典中的字段，如果是则将第三个子元素的内容存入相应的字典值中
        try:
            temp_info[switcher_dict[temp[0].text]]= temp[2].text
        except: pass
	# 最后以字典的形式返回所有收集到的信息
    return(temp_info)
```

这段代码里值得说的一点可能就是转置字典的使用，其实就是为了让代码看起来干净一点，用这个方法代替了一溜if判断：

> temp_info[switcher_dict[temp[0].text]]= temp\[2\].text

这一句话的意思就是将转置字典`switcher_dict`中对应键的值写入`temp_info`字典中，但如果字典中没有相应的键则会报错，这时使用`try...except...`就可以跳过那些不需要的信息。

### 读取和写入数据

有了上面这些函数，我们就已经可以从输入任意公司名字到返回包含所需的该公司信息的字典了。接下来就只需要把我们的公司名称列表循环起来就可以了：

```python
# 读取公司名字列表
companyfile = pd.read_excel('Company_names.xlsx',converters={'ClientNo':str})
# 以追加模式打开/创建一个存储结果的csv文件
csv_file = open('Company_results.csv', 'a', encoding='utf-8',newline='')
fileheader = ['ClientNo','OurCompanyName', 'RegisterNo','ChineseName','EnglishName','EstablishDate','Industry','Status']
dict_writer = csv.DictWriter(csv_file, fileheader)
dict_writer.writeheader()

# 将公司名字列表中的所有行遍历一遍
for i in tqdm(range(len(companyfile)),desc="Number of Companies searched"):
    # 如果公司名字已经被搜索过就跳过这次循环
    if companyfile['Searched'][i] == 'Yes':
        pass
    else:
        # 如果没有被搜索过则把这条记录的公司名和客户号放入结果字典
        comp_info = {}
        comp_info['ClientNo'] = companyfile['ClientNo'][i]
        comp_info['OurCompanyName'] = companyfile['OurCompanyName'][i]
        # 先把要搜索的公司名用之前定义的trun_name函数裁剪一次
        Search_name = trun_name(companyfile['OurCompanyName'][i])
        # 然后把裁剪后的名字输入get_company_link函数获取公司信息页链接
        Comp_link = get_company_link(Search_name)
        # 如果拿不到网页链接，则只把公司名和客户号推进结果字典
        if Comp_link == 0:
            dict_writer.writerow(comp_info)
        # 否则使用get_comp_info函数获取该公司的信息并和公司名客户号合并成一个字典
        else:
            comp_info.update(get_comp_info(Comp_link))
            dict_writer.writerow(comp_info)
        # 每完成一条记录，就把当条记录标记为已搜索    
        companyfile['Searched'][i] = 'Yes'
        # 每一百次循环就把搜索标记存储一次
        if i%100 == 0:
            companyfile.to_excel('Company_names.xlsx', engine='xlsxwriter',index=False)
        sleep(1.1)   
csv_file.close()
```

读取和写入数据这一步我用了分开的方式，不直接在原本的公司名单文件中写入公司信息，而是只读取名字然后每次读取搜索后标记一下。这样就不至于如果中途程序中断不知道从哪里再开始。标记的信息每100次循环才存储一次，这样如果中断，需要重复的次数也不会超过一百次，得到的结果只需要对客户号去重就可以的到完整的结果。

到这里我们只需要运行这个脚本就已经可以开始慢慢收集数据了，我最后跑完整个三万三千条数据一共花了60个小时，平均每条记录需要运行5-10秒，而结果中大概有一万两千条是实际有数据的，足够我们数据分析的用途使用了。

> Number of Companies searched: 58:  88%|████████████████████████████████▌    | 29366/33412 [55:30:09<5:20:53,  4.76s/it]

## 其他可能改进

虽然我们已经完成了手上数据的收集工作，但作为一个爬虫脚本，他还有一些可以改进的地方，就包括使用Proxy发送请求，以防止网站屏蔽IP，从而达到加速脚本的作用；其次还可以利用Windows scheduler的定时任务，固定时间定时获取新的公司信息情况。

### 使用Proxy发送请求

想要不被目标网站屏蔽IP的一个简单而有效的方法就是使用Proxy，这样对目标网站来说我们的发送的请求就是从不同来源发来，也就不会被发现我们在爬取数据。这个方法也可以使我们可以多开并行爬取，把爬虫速度提升很多。使用方法也很简单，可以利用`PythonBroker`实时获取有效的Proxy地址并添加在请求的头文件参数中即可。

参考资料：

- [PythonBroker][3]
- [如何使用Proxy with Python Requests? ][4]
- [python爬虫——urllib使用代理][5]

### 增加实时更新的功能

之后因为我们可能需要按时更新我们的公司数据清单，但因为公司的成立日期不会有变化，因此为了减少我们每次的工作量，可以使用Python首先对比每次清单名称中新增的公司名，然后只查询这些新增的公司的信息，然后推入已有的数据库中。

至于定时脚本的方法，可以使用Windows系统自带的`Windows scheduler`完成定时运行脚本的步骤。

参考资料：

- [How to Schedule Python Script using Windows Scheduler][6]

# 最后

在本篇中我介绍了我利用Python脚本收集一些公司没有的数据的项目的全过程，最后部分还有一些我在研究项目过程中有看到，且我认为可能对以后的类似项目有帮助的内容或方法，也记录在这里备用。

[第19篇] 

[1]: https://hkg.databasesets.com/	"香港數據庫集 / Hong Kong Datasets"
[2]: https://hkg.databasesets.com/zh-hant/gongsimingdan/search	"香港數據庫集：香港最新成立/注册及已更名的公司名单"

[3]: https://github.com/constverum/ProxyBroker	"ProxyBroker"
[4]: https://www.scrapingbee.com/blog/python-requests-proxy/	"How to Use a Proxy with Python Requests?"
[5]: https://blog.csdn.net/kdl_csdn/article/details/103989024	"python爬虫——urllib使用代理"
[6]: https://datatofish.com/python-script-windows-scheduler/	"How to Schedule Python Script using Windows Scheduler"

