---
title: "[编程算法]自动报价机器人的GUI开发记录"
date: 2022-08-23 22:05:16
category: 编程算法
description: "[第22篇]本篇记录了22篇中的报价机器人的GUI设计以及一些功能的实现方法。"
tag: [Python, 工作学习, RPA, GUI]
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/algorithm.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/22-Automated_Website_Logging_Robot_GUI.jpg
sticky: 9
---

# 序言

这一篇文章与第4篇和第21篇其实是同一个项目，就是将公司的一些填写网页的机械重复劳动使用Python将其自动化，从而达到减少人工成本，增加公司报价效率的结果。这一篇之所以与前两篇分开是因为本篇主要记录的是这个报价工具的用户界面逻辑，虽然是同一个项目但在逻辑上与前两篇是分开的。这篇中主要会涵盖我使用Python内置的`tkinter包`给这个小程序做的GUI界面，并记录如何将各个功能实现或链接。

# 正文

## 界面设计

首先要明确软件本身就是为了加速用户处理报价的速度，而实际业务的输入都可以在Excel模板中调整规范，因此我们的软件界面本身可以尽可能的简介易用，我最终的第一版界面就如下图所示：

![软件界面](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/image-20220830204919666.png)

最上方两个`输入框(Entry)`用来收集登录网站要用的用户名和密码；一个开始`按钮(Button)`简洁易懂；往下第二层是选择报价的险种的`单选按钮(Radio Button)`，根据这个按钮的选项程序会切换不同报价的业务逻辑，第一版还只有私家车险的自动报价；再往下是一个巨大的`文本框(Text)`，程序在这里向用户展示必要的反馈信息；最后是展示报价进度的`进度条(Process Bar)`和`标签(Label)`。

简单来讲用户在输入必要信息后点击开始按钮，程序就会开始运行并反馈信息直到整个报价过程完成。

## 程序结构

整个程序一共包括三个`py文件`，分别负责私家车险报价功能实现，主程序界面，和一个图标文件。

- 报价功能文件中主要是程序从检查Excel文件到最后获取报价单号的全流程公式集，每个公式获取一个行号并以此操作Excel文件中相应行数的数据；以后如果增加不同险种的报价逻辑，只需要再增加相应的`py文件`即可。
- 在读取数据的主程序界面文件中包括一个主界面的类，其中定义了程序界面的控件和对应函数，同时以POP的方法定义了按键后程序的运行；
- 最后的图标文件是为了将图标的图片一并打包到最后的exe文件中而将`ico文件`转码为`py文件`，运行程序时再自动解码为`ico文件`的而存在的，本篇也会讲解如何转码解码。

## 程序主界面

首先是以OOP方法定义的主界面，实现上方界面的代码如下：

```python
import base64
import tkinter
import threading
from tkinter import *
from tkinter import ttk
import os
import logging

class Qnect_Quoter(object):
    def __init__(self):
        # the main window
        self.root = tkinter.Tk()
        # Title of the tool
        self.root.title("Qnect Quoter")
        # add ico from the icon.py file and delete the file after
        picture = open("picture.ico", "wb+")
        picture.write(base64.b64decode(img))
        picture.close()
        self.root.iconbitmap("picture.ico")
        os.remove("picture.ico")
        # mainwindow size
        self.root.geometry("725x605")
        self.root.resizable(False, False)

        # Main Page frame
        self.input_frame = ttk.Frame(self.root)
        self.selection_frame = ttk.LabelFrame(self.root, text="Quoting Cover")
        self.textbox_frame = ttk.Frame(self.root)
        self.pb_frame = ttk.Frame(self.root)

        # Create input cells for Qnect acount and passwords
        self.account_label = ttk.Label(self.input_frame, text="Qnect Account: ")
        self.account_input = ttk.Entry(self.input_frame, width=20)
        self.password_label = ttk.Label(self.input_frame, text="Password: ")
        self.password_input = ttk.Entry(self.input_frame, width=20)
        # The button to start quoting
        self.start_button = tkinter.Button(self.input_frame, command=self.start_quote, text="Start Quoting")

        # Create radio buttons for selection of quoting coverages
        self.alignment_var = StringVar()
        self.alignments = ["Private Car"]

        # Display textbox and scrollbar for information
        self.info_text = tkinter.Text(self.textbox_frame, width=85, height=28)
        self.scrollbar = ttk.Scrollbar(self.textbox_frame, orient="vertical", command=self.info_text.yview)

        # add a process bar to the window
        self.pb = ttk.Progressbar(self.pb_frame, orient="horizontal", mode="determinate", length=700)
        self.pb_label = ttk.Label(self.pb_frame)


    def gui_arrang(self):
        self.input_frame.grid(padx=10, sticky=EW)
        self.selection_frame.grid(padx=10, sticky=EW)
        self.textbox_frame.grid(padx=10, sticky=EW)
        self.pb_frame.grid(padx=10, pady=10, sticky=EW)
        self.account_label.grid(row=0, column=0, padx=5, pady=10, sticky=W)
        self.account_input.grid(row=0, column=1, padx=5, sticky=W)
        self.password_label.grid(row=0, column=2, padx=5, sticky=W)
        self.password_input.grid(row=0, column=3, padx=5, sticky=W)
        self.start_button.grid(row=0, column=4, padx=30, sticky=E)
        radio_column = 0
        for alignment in self.alignments:
            radio = ttk.Radiobutton(self.selection_frame, text=alignment, value=alignment, variable=self.alignment_var)
            radio.grid(column=radio_column, row=0, ipadx=10, ipady=10)
            radio_column += 1
        self.info_text.grid(row=1, column=0)
        self.scrollbar.grid(row=1, column=1, sticky=NS)
        self.info_text["yscrollcommand"] = self.scrollbar.set
        self.pb.grid(row=0, sticky=EW)
        self.pb_label.grid(row=1)


    def start_quote(self):
        global completed, listening
        login_thread = threading.Thread(target=LoginValidate)
        login_thread.start()
        completed = False
        # make sure there is only one Waiting_for_login() loop going on, otherwise will create several loops each click.
        if not listening:
            Waiting_for_login()
            listening = True
            
            
def main():
    global main_window
    main_window = Qnect_Quoter()
    main_window.gui_arrang()
    logging.basicConfig(filename="Run.log", format='%(asctime)s %(message)s', filemode='w')
    logger = logging.getLogger()
    logger.setLevel(logging.ERROR)
    tkinter.mainloop()
    pass


if __name__ == '__main__':
    main()
```

上面代码中值得注意的主要有几点，`Tkinter`各控件的详细使用方法与示例参考[这个网站][1]：

1. 导入`tkinter包`时的`tk`使用的是1991年引入的经典控件，而使用`tkinter`中的`ttk module`创建的控件则是2007年新的控件风格。另外`from tkinter import *`语句的意义是为了导入`tkinter包`中表示方位的字符"E""EW""N"等，这些字符可以在`grid方法`中表示控件偏向某个方向，或向哪个方向延申。
2. `__init__`中定义各个控件的初始化信息，以及主程序窗口的设置参数，从上至下初始化输入框，选择框，信息框，以及进度条框四个`框架(Frame)`。
3. `gui_arrang(self)`函数中使用`grid函数`将不同控件与框架在主窗口中分别排列，这个方法比`pack方法`自由度更高，比`place方法`需要的成本更低，排版更漂亮。
4. `self.start_button`按钮绑定的程序是`start_quote(self)`，而该程序会在运行后开始一个新的线程并在主程序的循环外同步运行`LoginValidate`，这个函数会验证并通过报价模块的函数获取其从Excel文件中提取的`pandas数据框对象`与打开的`webdriver对象`。与此同时程序会开始一个等待`LoginValidate`函数完成的监听过程`Waiting_for_login`，该监听过程会在判断前一个线程的目标完成后开启新线程运行相应的报价程序。
5. 在`main()函数`中，实例化一个主界面，并使其进入`mainloop()`，同时在loop之前加入一个记录报错信息的`logger`。这个logger会记录运行中的错误信息与时间并写入log文件中以便debug。

## 链接功能模块

接上节内容，`main.py文件`中除了主界面的元素等内容外，还有几个函数，用来调用协调主界面元素与实际报价的功能模块。我就按顺序首先讲讲`start_quote(self)`中新线程运行的`LoginValidate()`：

```python
def LoginValidate():
    # initiate the process bar
    main_window.pb["value"] = 0
    main_window.pb_label["text"] = ""
    global completed
    # get the inputs from the UI
    username = str(main_window.account_input.get())
    password = str(main_window.password_input.get())
    covername = str(main_window.alignment_var.get())
    if any([not username, not password, not covername]):
        update_info_text("Please input QNECT username, password and select a cover you wish to quote.\n")
        return 0

    global data_record, driver
    # validating the input file
    update_info_text("Loading File...\n")
    load_file = PrivateCarQuoting.load_data(Filename)
    if load_file[0] != 0:
        update_info_text(load_file[0])
        return 0
    else:
        update_info_text("File loaded!\n")
        data_record = load_file[1]

    # Login to Qnect
    update_info_text("Connecting to Qnect...\n")
    login_qnect = PrivateCarQuoting.Login(username, password)
    if login_qnect[0] != 0:
        update_info_text(login_qnect[0])
        try:
            driver = login_qnect[1]
            driver.quit()
        except: pass
        return 0
    else:
        update_info_text("Log in Success!\n")
        driver = login_qnect[1]
        completed = True
        
        
def update_info_text(text):
    main_window.info_text.insert(END, text)
    main_window.info_text.see(END)
```

上面这个函数主要需要完成的是验证数据并通过主界面实例将结果动态反馈至主界面，并在成功收集数据，打开webdriver对象后返回这两个对象以供后面的程序使用。特别需要注意的是其中的`complete`变量，这是一个`布尔变量`，只有在所有验证成功完成后这个变量才会被标记为`真`。在这个变量被标记为真后另一个线程中正在监听`complete`结果的函数`Waiting_for_login()`才会开始执行：

```python
listening = False
def Waiting_for_login():
    global completed, listening
    if completed:
        listening = False
        update_info_text("Start Quoting...\n\n")
        quoting_thread = threading.Thread(target=PrivateCarQuote)
        quoting_thread.start()
    else:
        main_window.root.after(100, Waiting_for_login)
```

这里需要注意的一点主要是`listening`这个变量在这里的意义是为了控制同时发起的线程，因为在`start_quote(self)`按钮的函数中会直接调用`Waiting_for_login()`函数，而每一个被运行的`Waiting_for_login()`函数又会在得到`complete`变量之前，每100毫秒循环运行自己，这会导致如果程序一直不能`complete`时，如果用户一直点击按钮，就会创建多个线程运行同一个函数，而在`complete`被完成时，所有的多个函数被同时执行。因此这里以一个`listening`变量控制，只有在`listening`为`假`时，按按钮才会运行新的`Waiting_for_login()`函数。

到这里，我这个第一版的报价工具用户界面就已经基本完成了，上方这个`Waiting_for_login()`函数在以后增加不同的险种报价功能后还应该改成输入一个单选按钮的结果，在线程中运行对应报价流程的函数，但目前还没有这个功能的需求，单选按钮就当是占位符了。

## ico文件转码

运行下面这段代码将`ico文件`编码为`py文件`：

```python
import base64

open_icon = open("QBE_Vertical_White_RGB.ico","rb")
b64str = base64.b64encode(open_icon.read())
open_icon.close()
write_data = "img = %s" % b64str
f = open("icon.py", "w+")
f.write(write_data)
f.close()
```

然后在主程序中加入下面这些代码从而将上面生成的`icon.py`文件中的内容重新解码为`ico文件`：

```python
# add ico from the icon.py file and delete the file after
picture = open("picture.ico", "wb+")
picture.write(base64.b64decode(img))
picture.close()
self.root.iconbitmap("picture.ico")
os.remove("picture.ico")
```

## Webdriver manager SSL验证

在最后将文件打包为exe文件后还遇到一个关于`Webdriver manager`的奇怪BUG，为了避免每次运行`webdriver`时都要去下载最新的`chrome driver`， 我使用了`webdriver manager包`，它会自动检测当前缓存中的`webdriver`版本并对比当前最新版本，如果本机不是最新版本则会自动去官网下载并打开，只需要一句代码：

```python
from webdriver_manager.chrome import ChromeDriverManager

driver = webdriver.Chrome(ChromeDriverManager().install())
```

这句话在`Pycharm`中运行非常顺畅，但当我把文件打包成exe文件后再运行就会在这句报错，说SSL未验证，我最后也没有找到原因，只能根据`webdriver manager`官方文档的指导通过修改os环境参数`WDM_SSL_VERIFY`来跳过SSL验证。

> ```python
> os.environ['WDM_SSL_VERIFY'] = '0'
> ```

# 最后

以上就是整个自动报价机器人的操作界面的记录，到这里我就算是独立完成了一个可以大幅减少公司重复劳动工作的RPA程序，到我写完这篇文章的时候这个报价工具已经同时完成了向两个不同渠道的400余个报价案件的测试，在4小时内完成了普通一个人人手需要十几个工作日才能完成的报价量，之后这个软件的升级或改进如果有意义的话我会再开一篇。

[第22篇]

[1]: https://www.pythontutorial.net/tkinter/	"Python Tutorial Tkinter"
[2]: https://www.cnblogs.com/yyds/p/6901864.html	"Python之日志处理(Logging模块)"

