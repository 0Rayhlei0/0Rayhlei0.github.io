---
title: "[编程算法]论文解读《Attention is all you need》"
date: 2023-7-2 12:37:12
tags: [日常学习, Deep Learninng, 论文解读]
categories: 编程算法
description: "[第29篇] 本篇解读NLP领域著名论文,提出Transformer结构的《Attention is all you need》以及其他自然语言模型的相关知识。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/algorithm.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/29-Paperstudy_attention_is_all_you_need.png
katex: true
sticky: 1
---

# 前言

随着最近ChatGPT的爆火，`自然语言处理(Natural Language Processing, NLP)`再一次成为人工智能领域最热门的课题之一，而ChatGPT所使用的`“基于Transformer结构的大语言模型(Large Language Model, LLM)”`也在一夜之间成为了几乎所有开发者争相研究的内容。

本篇将以理解发明Transformer结构的开山之作《Attention is all you need》为引，介绍自然语言处理模型的发展历史和相关知识。

# 正文

## NLP模型发展历史

人类对自然语言模型的研究从上世纪50年代开始，当时人们对机器处理自然语言的主流研究方向是认为机器应该像人类理解语义那样，通过输入处理各种单词语法规则，将人类语言转换为机器可使用的语言来完成自然语言任务([Noam Chomsky, 1957][1])。直到70年代初Fred Jelinek

[第29篇]

[1]: https://doubleoperative.files.wordpress.com/2009/12/chomsky-syntactic-structures-2ed.pdf	"Syntactic Structures By Noam Chomsky, 1957"

