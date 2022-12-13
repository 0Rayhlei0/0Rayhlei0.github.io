---
title: "[MS Office]Access报价出单排版打印工具开发记录"
date: 2022-05-15 21:38:32
category: MS Office
description: "[第15篇]本篇主要介绍在使用Access报表功能帮助开发公司的报价单排版打印工具时使用的一些小技巧与代码。"
tag: [Access,VBA,工作学习]
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/office.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/15-A_quotation_printing_tool.jpg
---

# 序言

公司有个承保同事基于Excel开发过核保报价出单的打印工具，具体用处就是分发给保险代理使用的，填写保单信息如客户信息，承保险种，起止日期，雇员险雇佣地址，同一客户承保各险种所需的保额，费率等信息以及最后的保费计算和保单条款适用等。代理填写完成后按键自动根据填写内容导出格式化的报价单pdf文件。之前同事使用Excel制作这个工具时的思路是使用一张工作表收集所有信息，然后每页pdf使用一个工作表，用公式连接第一张信息表，最后做一个按键根据信息表中的信息打印需要打印的工作表。

这种方法实际上确实可行，但有两个缺点：一是公式太多会使思路简单的信息排版打印甚至打开文件都变得非常慢，二是填写的信息仅仅用于打印一次，若需要保存已经填写的信息需要将整个文件复制保存。另一方面，如果使用Access开发这个工具则可以完美避免这两个缺点，实际上Access可以说就是专门为了完成这些任务而设计出来的， 它的表单(form)用于填写信息，表(table)用于存储信息，报表(Report)用于展示和打印信息。因此我协助核保同事重新以Access设计了这个报价单打印工具，这篇文章主要记录一下实现一些小功能的方法。

# 正文

## 表单中计算日期

有一个小功能，因为一般险中大部分保单保期都是一年，因此想要在表单中设置选择起保日期后自动将保单失效日期填入一年后日期，例如2020年9月1日起保便自动填入2021年8月31日失效。这个功能看起来非常简单直观，可以使用VBA的`DateAdd()`函数计算1年后日期减1即可，但似乎Access的日期表单的计算功能有些小漏洞。

稍微介绍一下`DateAdd(interval, number, date)`函数，其三个参数中`interval`表示想要增加的日期单位，`number`表示想要增加的日期数量，`date`则是要增加的起始日期。其中`interval`参数的可用值及代表的意思如下：

| interval参数 | yyyy | q    | m    | y            | d    | w            | ww   | h    | n    | s    |
| ------------ | ---- | ---- | ---- | ------------ | ---- | ------------ | ---- | ---- | ---- | ---- |
| 意义         | 年   | 季度 | 月份 | 天数(以年计) | 天数 | 天数(工作天) | 周   | 小时 | 分钟 | 秒钟 |

但是在表单上实现这个简单功能的难点在于Access表单中日期栏位特殊的输入方式，日期可以通过日历表的控件直接选择输入，但如果直接在起保日期的`On Change`事件中直接写入`[End Date] = DateAdd("yyyy",1,[Start Date])-1`的话，会导致起保日期刚刚输入就被强制执行该公式，其结果就是起保日期的输入不准确，我猜想可能是因为`On_Change`事件本身是栏位发生任何变化都会触发，但日期的选择输入本身可能包括多个步骤，这导致事件会在日期没有完全输入时就被触发从而引发错误。但同时如果使用`After_Update`事件会导致日期输入后不能直接触发事件，而需要选择到其他控件才能触发，这两种方式都不适合我们需要的应用。

但知道了问题所在解决方案也就应运而生了，我对这个问题的解决方法是将计算分为两段执行，在起保日期被修改时将`Focus`设置到失效日期，而在起保日期失去`Focus`时再执行`[End Date] = DateAdd("yyyy",1,[Start Date])-1`。如此可以保证执行计算操作时起保日期已经被准确输入。实现代码示例如下：

```vb
Private Sub Start_Date_Change()
    [End Date].SetFocus
End Sub

Private Sub Start_Date_LostFocus()
    [End Date] = DateAdd("yyyy", 1, [Start Date]) - 1
End Sub
```

## 将报表打印至PDF

用户将报价单所需的所有信息通过表单输入数据表中后，我们可以通过表单上的按钮按需求打印已经排版好的报表至pdf，本章我先将这个按钮中的步骤分步讲解，最后再放出完整代码。

### 打开报表的打印预览模式

在要调整需要打印的内容之前必须先将需要打印的报表打开：

```vb
DoCmd.OpenReport "Full Quotation", acViewPreview, , "[Quotation ID (Access record only)] = Forms![Main-Quotation Info]![Quotation ID (Access record only)]"
```

`DoCmd.OpenReport`本身用于打开报表，其后的参数分别为`报表名称`，`打开方式`，`筛选名称`，`WHERE条件`，`打开窗口模式`和`OpenArgs`。各个参数的具体使用方法[见此][1]，我这里用到的参数只有`报表名称`，`打开方式`和`WHERE条件`。这里需要说明一点是`WHERE条件`的使用方法，这里的表达相当于在报表的`SELECT QUERY`中添加`WHERE`条件语句，此处加上的`[Quotation ID (Access record only)] = Forms![Main-Quotation Info]![Quotation ID (Access record only)]`代表报表中只展示`ID`与表单中当前选择的`ID`相同的记录，如果没有这条条件打印会展示所有记录。

### 调整需要展示的页面

打开要打印的报表预览页面后才可以根据条件调整需要打印的页面：

```vb
If Reports![Full Quotation]!EC_FINAL.Value = "" Or Reports![Full Quotation]!EC_FINAL.Value = 0 Then
    Reports![Full Quotation]!PageBreakforEC.Visible = False
    Reports![Full Quotation]![EC Quotation].Visible = False
End If
If Reports![Full Quotation]!PL_FINAL.Value = "" Or Reports![Full Quotation]!PL_FINAL.Value = 0 Then
    Reports![Full Quotation]!PageBreakforPL.Visible = False
    Reports![Full Quotation]![PL Quotation].Visible = False
End If
If Reports![Full Quotation]!BI_FINAL.Value = "" Or Reports![Full Quotation]!BI_FINAL.Value = 0 Then
    Reports![Full Quotation]!PageBreakforBI.Visible = False
    Reports![Full Quotation]![BI Quotation].Visible = False
End If
If Reports![Full Quotation]!MAR_FINAL.Value = "" Or Reports![Full Quotation]!MAR_FINAL.Value = 0 Then
    Reports![Full Quotation]!PageBreakforMAR.Visible = False
    Reports![Full Quotation]![MAR Quotation].Visible = False
End If
```

在`Full Quotation`报表中，按ID连接并放入了不同险种信息的四个`子窗体(subform)`，当主窗体中关于各个险种的保费计算为0或空使，将相应的子窗体和分页符隐藏，从而可以达到不打印该页面的效果。需要强调的一点是隐藏操作必须在报表被打开的前提下，否则会报错。另外由于我们是在预览模式下操作隐藏对象，而不是在设计模式或布局模式打开，因此这里的隐藏操作是暂时性的，不会影响到报表本身的参数，也就是说这里的隐藏修改在关闭时不会被保存。

### 输出结果至PDF

当我们把需要打印的报表按需求在打印预览模式下调整好之后就可以直接使用命令将结果输出至PDF文件了。

```vb
fileName = Forms![Main-Quotation Info]![Quotation ID (Access record only)] & "_Quotation"
fldrPath = Application.CurrentProject.Path
filePath = fldrPath & "\" & fileName & ".pdf"

DoCmd.OutputTo objecttype:=acOutputReport, objectName:="Full Quotation", outputformat:=acFormatPDF, outputFile:=filePath
DoCmd.Close acReport, "Full Quotation", acSaveNo
MsgBox prompt:="PDF File exported to: " & vbNewLine & filePath, buttons:=vbInformation, Title:="Report Exported as PDF"
' open the output pdf
CreateObject("Shell.Application").Open (filePath)
```

这里首先将我们想要保存pdf文件的文件名和地址定义好并合成为完整文件地址，然后使用`DoCmd.OutputTo`命令将刚刚整理好的报表以PDF的格式保存至定义好的地址，然后关闭报表后打开导出的文件以供用户检视。

其中`DoCmd.OutputTo`命令中的可用参数分别是`对象类型`，`对象名`，`输出格式`，`输出文件路径`，`自动开始`，`模板文件`，`解码方式`和`输出质量`。各参数的具体使用方法可见[官方文档][2]。我们只需要将`对象类型`设定为`acOutputReport`，填好`对象名`，`输出格式`设为`acFormatPDF`并将`输出文件路径`设定为之前定义好的地址即可完成PDF文件的导出。后面的关闭报表，弹窗信息，打开导出文件操作都非常简单，我就不解释了。

### 完整代码

综上，这个工具导出报表至pdf的按钮完整代码如下：

```vb
Private Sub PrintToPDF_Click()
    ' Open the report of current quotation
    DoCmd.OpenReport "Full Quotation", acViewPreview, , "[Quotation ID (Access record only)] = Forms![Main-Quotation Info]![Quotation ID (Access record only)]"
    ' Hide the quotation pages with no premiums
    If Reports![Full Quotation]!EC_FINAL.Value = "" Or Reports![Full Quotation]!EC_FINAL.Value = 0 Then
    Reports![Full Quotation]!PageBreakforEC.Visible = False
    Reports![Full Quotation]![EC Quotation].Visible = False
    End If
    If Reports![Full Quotation]!PL_FINAL.Value = "" Or Reports![Full Quotation]!PL_FINAL.Value = 0 Then
    Reports![Full Quotation]!PageBreakforPL.Visible = False
    Reports![Full Quotation]![PL Quotation].Visible = False
    End If
    If Reports![Full Quotation]!BI_FINAL.Value = "" Or Reports![Full Quotation]!BI_FINAL.Value = 0 Then
    Reports![Full Quotation]!PageBreakforBI.Visible = False
    Reports![Full Quotation]![BI Quotation].Visible = False
    End If
    If Reports![Full Quotation]!MAR_FINAL.Value = "" Or Reports![Full Quotation]!MAR_FINAL.Value = 0 Then
    Reports![Full Quotation]!PageBreakforMAR.Visible = False
    Reports![Full Quotation]![MAR Quotation].Visible = False
    End If
    
    ' Output the report to pdf file
    Dim fileName As String, fldrPath As String, filePath As String
    Dim answer As Integer
    Const FILE_OPENED = 2501
    
    fileName = Forms![Main-Quotation Info]![Quotation ID (Access record only)] & "_Quotation"
    fldrPath = Application.CurrentProject.Path
    filePath = fldrPath & "\" & fileName & ".pdf"
    
    On Error Resume Next
    DoCmd.OutputTo objecttype:=acOutputReport, objectName:="Full Quotation", outputformat:=acFormatPDF, outputFile:=filePath
    DoCmd.Close acReport, "Full Quotation", acSaveNo
    MsgBox prompt:="PDF File exported to: " & vbNewLine & filePath, buttons:=vbInformation, Title:="Report Exported as PDF"
    ' open the output pdf
    CreateObject("Shell.Application").Open (filePath)
    
    Select Case Err.Number
        Case 0
        ' no error
        Case FILE_OPENED
        MsgBox ("The file is already opened, please close it before replace.")
        
        Case Else
        'unanticipated error - inform user
        MsgBox Err.Description, vbExclamation, "Error"
    End Select
    
End Sub
```

额外想讲解的一点是`Select Case`语句在这个代码中用于捕捉错误信息的应用，`Select Case`语句的详解见[官方文档][3]，其用法与`If...Then...Else`语句中`ElseIf`的用法相似，但不同的是`ElseIf`可以在每个判断中加入不同的判定条件，只需要返回结果是`True`或`False`即可，而`Select Case`语句则需要先在`Case`后给定要判断的变量，然后在不同的`Case`下判断`该变量`是否满足每个条件。

在这里这个语句的应用则是先捕捉错误代码，然后根据捕捉到的不同错误代码的值弹出不同的信息。

## 将子窗体数据更新至表

在工具的主窗体上嵌有一个关于各个险种条款的子窗体，子窗体通过`ID`与主表数据连接，其中内容都是不同条款的`复选框(Checkboxes)`，选中则代表包括该条款否则不打印。

通常情况下子窗体数据的修改会被同步至其对应的表中，但这里有个特殊情况，就是条款为了方便选择设置过默认选项，而有一些保单确实不需要默认选项以外的条款选择，这就导致有一些情况下用户可能根本就不修改这个子窗体中的内容就打印报表。这就导致子窗体中的数据没有被更新至对应的表中，自然也不会被报表打印出来。

要解决这个问题，一个很自然的想法是使用VBA代码修改表单中的内容后强行保存，这样Access为了保存修改后的内容就会必须在表中存储相应数据，这时再将刚刚修改的内容改回默认值保存，表中就有了这个记录。将这个行为触发定义在输入某个前置控件内容后，便可以实现用户无感更新子窗体数据。

```vb
Private Sub EC_Quotation_No__WOD_QR__AfterUpdate()
    ' 先SetFocus至子窗体，这样后面的保存记录指令才可以正确对子窗体数据执行
    Forms![Main-Quotation Info]!EC_Clauses.SetFocus
    '修改子窗体中数据保存再改回默认值保存，以强制创建更新数据至表
    Forms![Main-Quotation Info]!EC_Clauses.Form![Extra-ordinary Weather Condition Clause_EC] = False
    DoCmd.RunCommand acCmdSaveRecord
    Forms![Main-Quotation Info]!EC_Clauses.Form![Extra-ordinary Weather Condition Clause_EC] = True
    DoCmd.RunCommand acCmdSaveRecord
    Me![EC Quotation No (WOD/QR)].SetFocus
End Sub
```

## 更新组合框数据

有一个Access应用开发中常常会用到的功能，就是以表单当前选择的数据信息来筛选组合框中的内容范围，通常在组合框中`Row Source`栏中的填入筛选出想要显示的数据的`SQL Query`即可实现，但除此之外还必须对组合框控件进行`Requery`操作才会使下拉选框中的内容被相应更新。

但Access VBA在这方面似乎有个小BUG，那就是如果你把`Requery`放在`On_click`事件上，虽然可以达到点出想要的下拉框的效果，但似乎是由于并行事件太多有很大机率会导致Access直接崩溃重启。经过一些测试我发现如果将`Requery`绑定在`On got focus`事件上则可以达到相同的效果但不会导致程序崩溃。

# 最后

本篇文章通过开发报价单打印工具进一步加强了我对Access数据库应用开发的经验，在此记录了一些可能适用范围较广可以在其他项目上借鉴的小技巧。

[第15篇]

[1]: https://docs.microsoft.com/en-us/office/vba/api/access.docmd.openreport	"DoCmd.OpenReport method (Access)"
[2]: https://docs.microsoft.com/en-us/office/vba/api/access.docmd.outputto	"DoCmd.OutputTo method (Access)"
[3]: https://docs.microsoft.com/en-us/office/vba/language/concepts/getting-started/using-select-case-statements	"Using Select Case statements"

