---
title: LaTex入门
date: 2021-05-15 16:53:15
tags: LaTex
categories: Learn
cover: https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/20211114222546.png
---
大学生写论文排版真的是太过折磨人，还是LaTex用起来方便一点，不需要学的非常精，只要学点基础的语法，能改模板就好了。
<!-- more -->
### 我的LaTex学习笔记

```latex
\documentclass{article}
\usepackage{ctex}%中文支持宏包
\usepackage{graphicx}%图像宏包
\graphicspath{{img/}}
\title{ LaTex }
\author{\kaishu 辛巳流火\heiti 辛巳流火}
\date{\heiti {\bfseries 辛巳流火}}

\begin{document}
    \maketitle

    \section {文本}
        abc \LaTeX 啦啦啦
    \section {公式}
        \subsection{行内公式}$f(x)=a_{b_{c_{d_{e_{f_{g_{h_{i_{j_{k_{l_{m_{n_{o_{p_{q_{r_{s_{t_{u_{v_{w_{x_{y_{z}}}}}}}}}}}}}}}}}}}}}}}}}^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{2^{}}}}}}}}}}}}}}}}}}}}}}}}}}}}}}-1$

        \subsection{行间公式}$$f(x)=f(x)^{f(x)^{f(x)}}$$

        \subsection{带编号行间公式}
        \begin{equation}
            f(x)=x^2-1
        \end{equation}
    \section {引号}
        左单：`左双：``右单：'右双：''
    \section {连字符}
        -  --  ---
    \section {图像}
       
        \begin{figure}[htbp]%h:此处t:页顶b:页底p:独立一页
            \centering
            \includegraphics[width=10cm]{001.jpg}
            \caption{一张壁纸} \label{lll}
        \end{figure}
        插入一张图像如图\ref{lll}
    \section {表格}
        \begin{tabular}{|l||c|c|c|p{1.5cm}|}
            \hline
            姓名&语文&数学&英语&备注\\
            \hline \hline
            hgy&100&100&100&优秀\\
            \hline

        \end{tabular}
    \section {粗体}
        第一种\textbf{加粗}方式

        第二种{\bfseries 加粗}方式
    \section {公式}
\end{document}
```