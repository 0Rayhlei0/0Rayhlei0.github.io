---
title: "[MS Office] 升级Excel报告一键自动化更新数据"
date: 2023-08-06 21:44:12
tags: [Excel, VBA, 工作学习]
categories: "MS Office"
description: "[第31篇]记录此前工作中将部门每月保费预测的报告配合使用公式和VBA实现一键更新。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/office.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/31-excel-tool-develop-2.jpg
---

# 序言

今年初时原部门的老板希望我能帮她把部门每月测算当月预计收入保费的报告自动化，该报告主要用于在每月中时根据当时的保费入账情况、当月待自动/手动续保费、新单保费入账规律、取消保单、应付\应收保费等测算当月底预计的保费收入。此前这个报告每个月都分别由业务部门的两个同事通过手动查Tableau数据并以财务截止日期天数手动估算当月可入账保费额，自动化后需要至少一天时间的估算只需一键即可更新，也因此这个报表不仅不再需要专人更新，任何人都可以随时计算预测结果。

# 正文

这个项目其实本身没有太多值得讲的东西，主要的工作量都在于工具的设计上，让需要手动操作的部分尽量少，最后做到填写两个日期和数据库的账号密码，然后一键就可以更新所有的数据和图表。里面以后可能有机会用到的内容我就分Excel公式和VBA代码两部分来说，整个工具本身我就不放出来了。

## Excel公式

### 计算上一个星期日的日期

因为我们的一些小保单的保费入账时间是每周By batch的，这样可以将每周的保费一次性录入系统，也因此我们的工具需要计算财务月度截止日期前一个星期日的日期，以计算该月一共有多少个星期日的方法来计算该月一共入账多少个Batch。要做到这点我们可以用下面这个公式：

```vb
=TEXT(INT((CUTOFF-1)/7)*7+1,"DD-MMM-YYYY")
```

上面这个公式包含了一个`Text(数字,日期格式)`公式用以将前面算出的数字结果转换为相应的日期格式，而里面这个`INT((CUTOFF-1)/7)*7+1`就很有意思了。这个公式的原理就是excel中的日期本质上其实是数字，数字0转换为日期就是1900-1-0即1990年1月0日，也就是说真正的日期是从1开始的，而Excel把0日期这天当成是星期六，往后每加7天就是一个星期六，即7代表的“1900年1月7日”和14代表的“1900年1月14日”等等。那么倒算回来某个给定日期其实都是7\*n+m天，而每个7\*n都代表一个星期六，这样来说只需要将给定的日期除以7的商并向下取整后成回7，其实就算到了上一个星期六，再加1就是上一个星期天了。公式中将截止日先减1再除以7则是为了让星期天当天时不计算上一个星期天（假设今天是星期天，减一后就成了星期六，也就是一个可以被7整除的日期，这样不会被约去小数自然也就不会计算到上一个星期日。）

### 计算两个日期间有多少个星期日

同上一个部分，既然每个星期日有一个batch那我自然也需要计算两个截止日之间一共有多少个星期日，以此来计算当月一共会录入多少个batch。使用下面这个公式：

```vb
=SUM(N(TEXT(ROW(INDIRECT(DATEVALUE(B2)+1&":"&DATEVALUE(B4))),"ddd")="Sun"))
```

从里到外拆解上面的公式就是：

1. 使用`DATEVALUE()`将两个日期转换为数字格式。
2. 使用`INDIRECT()`将两个日期数字变成一个范围。
3. 使用`ROW()`取上面这个范围的行数，也即将两个日期间的所有数转换成一个数组。
4. 用`TEXT(ROW(*),"ddd") = "Sun"`来将上面的数组转换成"ddd"也即星期几的三位格式，如果是周日则返回True否则返回False。
5. 用`N()`把上面的数组转换为1或0的数组，然后使用`SUM()`就可以算出数组中一共有多少满足条件的元素。

## VBA代码

这个工具里的VBA部分只是根据填好的日期组好一句SQL查询字符串，然后通过代码和IBM iAccess建立和公司数据库的联系，使用VBA的`ADO(ActiveX Data Objects)`接口接收储存数据库数据后把结果写在excel的对应位置中，从而达到一键从数据库更新数据刷新表格的目的。关于ADO的详细介绍可以看[这篇知乎介绍][1]和[ADO的documentation][2]。

具体用法以下面的代码为例：

```vbscript
'Establishing Connection
    Set iSeriesDataCN = New ADODB.Connection
    iSeriesDataCN.Open "Provider=IBMDA400;Data Source=xxxxx;", UserName, Password
   
'Forge the target SQL query
    SQL = "SELECT xxx" & _
	"FROM xxx"

'Run SQL
    Set rsWorkRecord = New ADODB.Recordset
    rsWorkRecord.CursorLocation = adUseClient
    rsWorkRecord.Open SQL, iSeriesDataCN

'Paste Value and close connection
' Put in the headers
    For x = 1 To rsWorkRecord.Fields.Count
          ResultWs.Cells(2, 1).Offset(0, x - 1).Value = rsWorkRecord.Fields(x - 1).Name
    Next x
'dump the dataset to sheet
    ResultWs.Cells(3, 1).CopyFromRecordset rsWorkRecord
    rsWorkRecord.Close
```

将上面的步骤逐一讲解一下：

1. **建立连接：**首先创建一个Connection对象，然后用Connection的Open方法传入参数连接到目标数据库。创建对象的方法除了上面以外还可以用`Dim iSeriesDataCN As New ADODB.Connection`。 Open方法输入的参数包括`connection.Open ConnectionString, UserID, Password, OpenOptions`，对象中的多数方法具有属性，当操作数缺省时属性可以提供参数。使用 Connection.Open，可以省略显式 ConnectionString 操作数并通过将 ConnectionString 的属性设置为“DSN=pubs;uid=sa;pwd=;database=pubs”隐式地提供信息。与此相反，连接字符串中的关键字操作数 uid 和 pwd 可为 Connection 对象设置 UserID 和 Password 参数。
2. **创建SQL查询：**这里其实就是将SQL查询语句通过字符串的形式传输给之前建立的连接。因为是字符串所以用`"引号"`括起来并且换行后用后加`& _`字符的方式，其中`&`符号用于拼接字符串，`_`符号表示代码将在下行继续，注意空格。如果需要创建的SQL查询中有变量，只需要将变量名和其他字符串用`&`符号连接即可。
3. **创建记录集Recordset：**通过`recordset.Open Source, ActiveConnection, CursorType, LockType, Options`的方式向之间创建的连接发送SQL查询并将结果储存在这个记录集对象中。记录集对象的`CursorLocation`属性指示游标服务的位置，游标的作用简单来说就是返回数据库中表的结果集的机制，后续对记录集的操作都通过游标库实现。游标位置有三种可能值：(1)adUseNone：不使用游标服务（这个常量已经过时，并且仅出于向后兼容性的考虑）；(2)adUseServer——服务器游标，默认值。使用数据提供者的或驱动程序提供的游标。这些游标有时非常灵活，对于其他用户对数据源所作的更改具有额外的敏感性。但是，Microsoft Client Cursor Provider（如已断开关联的记录集）的某些功能无法由服务器端游标模拟，通过该设置将无法使用这些功能。(3)adUseClient——客户端游标。使用由本地游标库提供的客户端游标。本地游标服务通常允许使用的许多功能可能是驱动程序提供的游标无法使用的，因此使用该设置对于那些将要启用的功能是有好处的。为了向后兼容，还支持同义adUseClientBatch。**当要实现远程数据服务时，在与服务端通信的客户端上使用Recordset 或 Connection对象时， CursorLocation属性只能设置为adUseClient。**
4. **粘贴返回的数据至工作表：**这部分就不详细讲了，可能的操作还很多。

# 最后

这个工具非常简单，除了上面的两个关于日期的公式以外，主要还是关于从excel直接连接外部数据库并通过VBA编程实现一键更新数据功能的实现。

[1]: https://zhuanlan.zhihu.com/p/387155361	"Ado中Recordset记录集最全的属性 方法 事件说明(含脑图)-适合Access及Excel VBA"
[2]: http://www.office-cn.net/t/ado/index.html?htm_dasdkadooverview.htm	"微软ADO程序员参考"

[第31篇]
