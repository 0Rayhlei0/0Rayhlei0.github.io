---
title: "[MS Office]使用 MS Access 开发文档管理查询工具"
date: 2022-03-27 21:38:17
tags: [Access, VBA, 工作学习]
sticky: 4
categories: MS Office
description: "[第11篇] 本篇介绍了我使用MS Access为公司文档管理和查询开发的小工具，使用者可以使用这个工具非常方便地查询所需文档。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/office.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/11-MSAccess-documentation-tool.jpg
---

# 序言

初次来到这家公司就发现公司的`文档记录`不太完备，很多`数据概念`和`数据库定义`要么模棱两可要么需要询问老员工，这乍看起来是个不影响干活的小事但实际上这不仅可能造成工作效率低下的结果，甚至可能导致`严重的问题`(类似于报告口径不一，数据结果错误导致决策错误或公司声誉受损等等)，因此这其实是一个`风险暴露`。我也因此决定至少给我们自己团队做一个`文档数据库`来设立一个可以参考标准口径，避免一些不必要的风险，同时加强同事日常工作和交接的效率与质量。

我虽然不是第一次接触VBA但其实这是我第一次接触`Access数据库`的应用开发，整个工具开发花了我接近七八天的时间，学到的东西也不少。在这篇文章中我会首先介绍一下工具本身的功能，然后是我学习到的Access应用开发的一些基本知识，以及介绍我在实现一些功能时用到的一些VBA代码。

# 正文

本文会直接介绍`工具的功能`及`开发中学习到的知识`，以及一些功能的`代码实现方法`。关于Access中各对象基本定义及功能的介绍可以去我的另一篇文章[分割 MS Access 数据库为前端和后端](http://raylei.space/2022/02/25/6-MSAccess_database_split/)看看。

## 工具结构

目前这个文档工具有3个主要的文档数据库：

1. `Key Measurements SQL：`记录了日常业务中可能涉及的主要术语与指标的定义及其SQL样例。
2. `Database Documentation：`记录了团队经常使用的数据库表及相应各个字段的详细信息。
3. `Marco Polo Dashboards：`记录了公司Tableau平台上的Dashboards的网址, 详细信息及使用方法。

其中前两个文档只需要实现名字的查询即可，而第三个`Tableau Dashboard`我则希望可以实现信息关键词的查询，因为团队中有些同事的数据查询需求其实已经在`Tableau`上有查询模板，我希望增加这个功能可以使用户通过他们需求的关键字可以查询到能帮助他们的`Dashboard`。

另外我为工具设置了`两个主要入口`，一个供`数据维护者`使用，使用`分割窗体(Split form)`，用户可以在界面中进行数据的`增删改查`，包括对工具本身的版本记录进行修改。

![维护端界面演示](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/1.gif)

另一个则是供`其他同事`使用，界面更为简洁，用户从下拉菜单中选择要查询的数据，并且可以通过不同的方式筛选出要`查询`的数据，但没有增删改已有数据的权限。

![用户端界面演示](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/2.gif)

## Access表单工具开发基础知识

Access的基本概念和定义我已经在第6篇博文中介绍过，在本节中我会注重介绍一些开发表单工具可能需要知道的基础知识，有了这些基本知识，稍加摸索尝试就可以很快上道了。

### 四种视图

要做Access的`表单(Form)工具`开发首先要搞清楚的是四种不同的`视图(View)`各自的作用及用法。在表单下通过`开始(Home)选项卡`中`视图(View)组`中的视图切换视图，四种不同的视图的用法和用处各有不同：

- `窗体视图(Form View)：`该视图下表单即为用户正常使用的状态，没有开发者选项，开发者可以在该视图下测试表单是否如预期运行。
- `数据表视图(Datasheet View)：`该视图下表单主要显示该表单的数据信息，呈现方式与表(Table)中相同，开发者可以用该视图检视表单的数据信息。
- `布局视图(Layout View)：`该视图下表单可以呈现窗体视图外观的同时不触发控件事件，在该视图下开发者依然可以通过属性栏配置表单。通常使用这个视图调整一些与表单外观有关的功能会得到比较直观的反馈。
- `设计视图(Design View)：`该视图下的表单会呈现出更多更详细的信息，例如表单的高度宽度尺，格线，页眉和页脚，该视图下可以调整的参数会多于布局视图但修改可能不会太直观。

### 属性表

Access中对表单的各方面配置都可以在`属性表(Property Sheet)`中完成，在`布局或设计视图`下右键单击表单，选择`属性(Property)`便会弹出当前控件的可调整属性，其中拥有自己属性的对象除了各种`控件(Control)`以外，还有`表单(Form)`，`页眉(Header)`，`页脚(Footer)`和`主体(Detail)`。

属性表中会显示当前选择的对象的类型（`控件类型或窗体(Form)或节(Section)`）及名称，而每个对象的配置参数又分为4个`选项卡`：
`格式(Format)：`在该选项卡中可以调整对象的外观参数以及一些控件的显示。

`数据(Data)：`该选项卡内容涉及数据显示相关设置，如数据源，默认值，数据验证或其他数据相关的配置。

`事件(Event)：`该选项卡主要涉及各种触发事件，开发者可以在不同的事件中加入宏或VBA代码来实现各种功能。

`其他(Other)：`基本上其他类找不到的参数设置就在这里找。

### 宏和VBA代码

Access中有`宏(Macro)`和`VBA代码(Code)`的`生成器(Builder)`，在控件的事件选项卡中点击`...`按键就可以进入生成器选择窗口，而宏和代码都可以一定程度上完成对某个事件的编程，他们的区别在于功能性和复杂度上。`宏`使用已经定义好的动作模块来设定事件动作，`简单快捷但自由度受限`，而`VBA代码`则需要开发者更高的代码能力，但能够实现更加`复杂的事件任务`。

![宏界面](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/macro.jpg)

![vba界面](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/vba_code.jpg)

在我们的工具中一些功能的实现结合了宏和VBA代码两种方式的使用。

## 部分功能的代码实现

我们的工具中每一个`按钮控件(Button Control)`都会涉及一个或多个代码块，但有些功能确实很简单我就不详细说了，这里我挑几个我觉得需要注意或者花了我一些功夫才写好的功能，那就由简及难一一介绍一下吧。

### 控制分割窗体的宽度

当我们设置表单的格式为`分割窗体(Split form)`时，我们无论在视图中如何调节它的宽度它在被打开时都会自动占满屏幕，这会减弱我们做出来的工具在不同设备上呈现的一致性，让我非常不爽。查了一下之后发现原来分割窗口的宽度可以用`MoveSize方式`调整。根据微软的官方文档，`MoveSize`的使用方法如下，其中数值的单位为`twip`：

> *expression*.**MoveSize** (*Right*, *Down*, *Width*, *Height*)

那么我们只需要在表单的`加载(On Load)`事件中加上这个表达就可以实现打开表单时自动调整宽度。

```vb
Private Sub Form_Load()
	DoCmd.MoveSize , , 7 * 1600
End Sub
```

### 设置打开Zoombox按钮

我的文档工具中因为涉及较长文本的输入，而且会有比较多的主动换行，因此直接在窗口文本框输入可能不太方便编辑，一般情况下用户可以在文本框中按`Shift+F2`的快捷键组合来打开当前文本框的`Zoombox`，用户可以在这个更大的窗口中编辑文字，查询时内容展示也更加清晰明了。

![Zoombox按钮演示](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/3.gif)

但显然快捷键组合对于普通用户来说有些过于繁琐了，因此我加了一个按钮，可以使用户在选择文本框后点击该按钮来打开这个文本框的`Zoombox`，只是在代码实现上稍微一些小小的注意事项，因为按钮本身是不具备`启动Zoombox`这个属性的，因此我们要将`focus`设定在点击按钮前的一个控件上，我的代码如下：

```vb
Private Sub Text_zoom_Click()
    Const NOT_ZOOMABLE = 2046

    On Error Resume Next
    Screen.PreviousControl.SetFocus
    RunCommand acCmdZoomBox
    
    Select Case Err.Number
        Case 0
        ' no error
        Case NOT_ZOOMABLE
        MsgBox ("Please select a TextBox before zoom in!")
        
        Case Else
        'unanticipated error - inform user
        MsgBox Err.Description, vbExclamation, "Error"
    End Select
End Sub
```

简单来说就是点击按钮后对点击前的控件执行`acCmdZoomBox`即`打开Zoombox`的命令，而如果在按按钮前点击的控件不具备这个功能，程序会返回`错误代码2046`，如果捕捉到这个错误代码就弹出`“请先选择一个要放大的文本框”`提示。

### 查找筛选符合条件的数据

为了方便用户`查改数据`，我需要给表单加入`搜索`的功能，比较方便的方法就是使用表单中的`筛选功能`，通过`关键字搭配通配符`在不同的`字段`筛选便可以找出符合条件的数据。

![关键字筛选演示](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/4.gif)

而对于工具的数据维护界面我使用的是`分割表单`，因此只要将需要的数据筛选出来，用户就可以在分割窗口中选择自己想要编辑的记录来操作。代码块如下：

```vb
Private Sub find_record_Click()
    Dim category_search_term As String
    Dim dashboard_search_term As String
    Dim category_null As String
    Dim dashboard_null As String
    
    ' for each null input, filter for every entry by sending * or IS NULL
    On Error Resume Next
    If IsNull(category_search) Then
        category_search_term = ""
        category_null = " OR [MP Category] IS NULL"
    Else
        category_search_term = category_search.Value
        category_null = ""
    End If
    
    If IsNull(dashboard_search) Then
        dashboard_search_term = ""
        dashboard_null = " OR [MP Dashboard] IS NULL"
    Else
        dashboard_search_term = dashboard_search.Value
        dashboard_null = ""
    End If
    
    Me.Filter = "([MP Category] LIKE '*" & category_search_term & "*' " & category_null & ") AND " _
    & "([MP Dashboard] LIKE '*" & dashboard_search_term & "*' " & dashboard_null & ")"
    Me.FilterOn = True
    
    Select Case Err.Number
        Case 0
        ' no error
        Case Else
        'unanticipated error - inform user
        MsgBox Err.Description, vbExclamation, "Error"
    End Select
End Sub
```

需要注意的一点是，因为`筛选`需要使用表单上的`文本框`输入内容，因此在直接使用`TextBox.Value`获取内容时可能会出现`空值报错`，而同时如果仅仅只将筛选值以`""`形式传给筛选条件的话，筛选会以`"Field LIKE '**'"`的条件筛选，这时筛选出的内容会`不包括内容为空的记录`，这在用户端可能无所谓，毕竟如果指针列的字段都为空很可能说明这条记录本身就没有完成，所以筛选出来也没有意义。但在维护端如果筛选不出字段为空的记录的话就会导致未完成的记录再也不能被筛选出来。

因此我在筛选器的语句中除了加入要筛选的内容外，还多了一重判断`“若输入为空，则在筛选条件中加入语句OR Field IS NULL”`以此筛选出该字段为空的记录。筛选器设置好后再用`Me.FilterOn = True`的语句将该设置应用在表单上筛选才会生效。这样就完成了记录筛选查找功能。

### 通过关键字限制组合框内容

在维护端要筛选出符合特定条件的记录可以直接筛选后在分割窗口中选择想要操作的数据，但在客户端我不希望使用分割窗体这么`"复杂"`的功能，我希望给用户更加简单易懂的操作界面。因此出现了我在这个工具开发中想出来的最有意思的一段代码和功能。那就是通过关键字搜索来限制`组合框(ComboBox)`中的显示内容，并且通过组合框的中值的选择来定位记录。

![组合框选择记录演示](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/5.gif)

最开始实现这个功能我是希望可以将在上一节的筛选后的`记录集(RecordSet)`填入组合框的`行来源(Row Source)`，结果找了半天也没有发现`Access VBA`有这个操作方法。因此我想到的办法是在`查找记录`控件的筛选记录功能之上再加入一个获取筛选出的记录的索引并`新建一个表`，然后直接将`行来源`的引用关联到这个新建的表中不就可以实现实时控制组合框内容了吗？测试了一下真的挺好用。代码如下：

```vb
Private Sub search_dashboard_Click()
    Dim category_search_term As String
    Dim dashboard_search_term As String
    
    ' for each null input, filter for every entry by sending *
    On Error Resume Next
    If IsNull(category_search) Then
        category_search_term = ""
    Else
        category_search_term = category_search.Value
    End If
    
    If IsNull(dashboard_search) Then
        dashboard_search_term = ""
    Else
        dashboard_search_term = dashboard_search.Value
    End If
    
    ' Disconnect the combobox with the list table before deleting it.
    If Not Combo_Dashboard_Lookup.RowSource = "" Then
        Combo_Dashboard_Lookup.RowSource = ""
    End If
    
    ' Delete the combobox list table if it exists
    If TableExists("combo_dashboard") Then
        DoCmd.DeleteObject acTable, "combo_dashboard"
    End If
    
    'make a table that store the index for this search and fill in the combobox row source with the result
    strSQL = "SELECT ID,[MP Category], [MP Dashboard] INTO combo_dashboard FROM Marco_Polo_Dashboards " & _
    "WHERE [MP Category] LIKE '*" & category_search_term & "*' " & _
    "AND [MP Dashboard] LIKE '*" & dashboard_search_term & "*' " & _
    "ORDER BY [MP Category], [MP Dashboard];"
    CurrentDb.Execute strSQL
    Combo_Dashboard_Lookup.RowSource = "SELECT ID,[MP Category], [MP Dashboard] FROM combo_dashboard ORDER BY [MP Category], [MP Dashboard]; "
    
    ' filter the records based on search terms too
    Me.Filter = "[MP Category] LIKE '*" & category_search_term & "*' AND " _
    & "[MP Dashboard] LIKE '*" & dashboard_search_term & "*'"
    Me.FilterOn = True
    
    Select Case Err.Number
        Case 0
        ' no error
        Case Else
        'unanticipated error - inform user
        MsgBox Err.Description, vbExclamation, "Error"
    End Select
End Sub
```

这段代码中需要注意的点有几个：

1. 与维护端相比，用户端中我`去掉了筛选出空值记录`的功能，因为如果内容为空那么大概率这条记录还没有完成，不需要被用户查到。
2. 关于`组合框`的`行来源`，我在表的`加载(On Load)`事件中加入了向`组合框行来源`中添加原表中所有引索的SQL语句，然后在`关闭(On close)`事件中加入了`清除行来源`并删除临时表的代码。这样可以保证为了查找引索而创建的临时表只在表单被打开的时候存在。
3. 临时表中的`引索`和`记录集`中的记录被以同样的方式`排序`和`筛选`，以此保证筛选出来的记录与组合框中的待选记录在顺序和内容上都相同。
4. 最后要实现组合框中的数据控制显示的记录有两种方式，一种比较简单的是通过`控件向导`添加`组合框`，其中有选择是否使用`组合框`控制记录显示。而第二种则是直接写`宏或代码`，因为其实控件向导实现这个功能的方法也就是在`“更新后(On Update)”`事件中添加一个`以当前组合框选择的记录ID`来查找记录的宏。

### 多关键字查询筛选记录

完成了基本的查询功能之后，我还希望在`Tableau Dashboard`的文档工具中再加上一个`多关键字查询`的功能，我的设想是使用多个`AND条件`在`Description字段`中筛选用空格隔开的`每一个关键词`，这样如果用户想要找到一张可以看到`“CCBA YoY GWP”`的`Dashboard`，他只需要输入后就可以找到`Description`中同时出现了这几个关键词的记录，从而帮助用户快速定位他们需要的`Dashboard`。

![关键词搜索演示](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/6.gif)

而代码的实现逻辑也非常简单，即使利用上节中使用的限制组合框筛选数据的原理，只不过对于提取新建引索表的SQL语句需要根据输入框中的关键词循环一下，其中第一个词前用`WHERE DESCRIPTION LIKE '*FIRSTWORD*'`的格式而后面其他词则用`AND`替代`WHERE`。具体代码如下：

```vb
Private Sub search_keywords_Click()
    Dim keywords_search_term As String
    Dim arrKeywords
    Dim varKeyword
    Dim strSQL As String
    Dim strFilter As String
    
    ' for each null input, filter for every entry by sending *
    On Error Resume Next
    ' if the key words are empty, select all records.
    If IsNull(keywords_search) Then
        strSQL = "SELECT ID,[MP Category], [MP Dashboard] INTO combo_dashboard FROM Marco_Polo_Dashboards " & _
            "ORDER BY [MP Category], [MP Dashboard];"
        strFilter = "Description LIKE '**'"
    Else
    ' looping the keywords input add "AND" criterias for each keyword.
        strSQL = "SELECT ID,[MP Category], [MP Dashboard] INTO combo_dashboard FROM Marco_Polo_Dashboards "
        arrKeywords = Split(keywords_search.Value, " ")
        Dim loopOne As Boolean
        loopOne = True
        For Each varKeyword In arrKeywords
            ' In the first loop, use WHERE and afterwards use AND to complete the SQL sentence.
            If Not varKeyword = "" And loopOne Then
                strSQL = strSQL & " WHERE Description LIKE '*" & varKeyword & "*'"
                strFilter = "Description LIKE '*" & varKeyword & "*'"
                loopOne = False
            ElseIf Not varKeyword = "" And Not loopOne Then
                strSQL = strSQL & " AND Description LIKE '*" & varKeyword & "*'"
                strFilter = strFilter & " AND Description LIKE '*" & varKeyword & "*'"
            End If
        Next
        ' sort the records in ascending order
        strSQL = strSQL & " ORDER BY [MP Category], [MP Dashboard];"
    End If
    
    ' Disconnect the combobox with the list table before deleting it.
    If Not Combo_Dashboard_Lookup.RowSource = "" Then
        Combo_Dashboard_Lookup.RowSource = ""
    End If

    ' Delete the combobox list table if it exists
    If TableExists("combo_dashboard") Then
        DoCmd.DeleteObject acTable, "combo_dashboard"
    End If
    CurrentDb.Execute strSQL
    Combo_Dashboard_Lookup.RowSource = "SELECT ID,[MP Category], [MP Dashboard] FROM combo_dashboard ORDER BY [MP Category], [MP Dashboard]; "
    
    ' filter the records based on search terms too
    Me.Filter = strFilter
    Me.FilterOn = True

    Select Case Err.Number
        Case 0
        ' no error
        Case Else
        'unanticipated error - inform user
        MsgBox Err.Description, vbExclamation, "Error"
    End Select
End Sub
```

到这里基本上这个小工具中值得讲的东西就都讲完了。

## 工具下载

我把一个只有测试内容的`副本`放在这里，有兴趣的可以打开看看每个部分功能具体是怎么实现的：

下载链接：[点击这里](/attachment/BancaDB_Documentation.accdb)

因为是第一次接触`Access`的VBA编程，我其实也发现了一些不好的编程习惯导致的不方便的情况，比如看网上大家的代码，有一个`约定俗成的规矩`是大家会在不同控件名称前加上这个控件的`类型简称`，比如`表A`命名为`tblA`,但我刚开始编的时候并没有意识到这个对读改代码有多重要，现在再改又比较麻烦了，各位先担待着，下次不会这样了。

# 最后

个人觉得通过这样一个小小的项目在一定程度上掌握了`数据库小应用的开发`是非常好的，以后面对某些难题又多了一个可能的解决方案，例如需要向客户定期收集资料时，可以做一个`Access前端`然后将表放在`SharePoint List`上，这样客户在前端收集到的资料就可以第一时间传送到云上的数据库中，这会比邮件沟通更大程度地增加`效率`和`用户体验`。

[第11篇]

[1]: https://docs.microsoft.com/en-us/office/vba/api/access.docmd.movesize	"DoCmd.MoveSize method (Access)"

