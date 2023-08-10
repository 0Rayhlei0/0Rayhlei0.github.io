---
title: "[MS Office] 升级Excel报告一键自动化更新数据"
date: 2023-08-06 21:44:12
tags: [Excel, VBA, 工作学习]
categories: "MS Office"
sticky: 2
description: "[第31篇]记录此前工作中将部门每月保费预测的报告配合使用公式和VBA实现一键更新。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/office.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/30-Japanese_Chapter_16.jpg
---

1. <font size=4>{% label 特别声明%}</font>

   {% label 本文中的出现的数据均经过随机扭曲处理，仅工具排版，逻辑与公式可供参考。 %}

   ---

   # 序言

   今年初时原部门的老板希望我能帮她把部门每月测算当月预计收入保费的报告自动化，该报告主要用于在每月中时根据当时的保费入账情况、当月待自动/手动续保费、新单保费入账规律、取消保单、应付\应收保费等测算当月底预计的保费收入。此前这个报告每个月都分别由业务部门的两个同事通过手动查Tableau数据并以财务截止日期天数手动估算当月可入账保费额，自动化后需要至少一天时间的估算只需一键即可更新，也因此这个报表不仅不再需要专人更新，任何人都可以随时计算预测结果。

   # 正文

   技术层面来说

[第31篇]
