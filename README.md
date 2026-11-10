# 吉林大学英文科研论文模板

本分支为英文版（`main`）。[中文版请切换到 `cn` 分支](https://github.com/shaijing/jlu-paper-template/tree/cn)，使用其中的 `main-cn.tex`。

本模板采用 A4 双栏排版，包含校徽、作者单位、摘要、公式、流程图、三线表、定理与证明、参考文献和附录示例。它不是吉林大学本科、硕士或博士学位论文的官方模板。用于投稿时，请根据期刊或会议要求调整格式；正文、作者信息和实验数据均为占位示例。

## 快速开始

安装 TeX Live（包括 `latexmk`、pdfLaTeX 和 BibTeX），在项目根目录运行：

```sh
latexmk -pdf main.tex
```

生成的文件为 `main.pdf`。没有 `latexmk` 时，依次运行 `pdflatex main.tex`、`bibtex main`，然后再运行两次 `pdflatex main.tex`。清理中间文件可运行 `latexmk -c main.tex`。

在 Overleaf 中上传整个项目，保留 `fonts/` 和 `figures/` 目录，并设置主文件为 `main.tex`、编译器为 pdfLaTeX。配套的 ByteSans 字体使用 pdfTeX 字体映射。

## 文件说明

| 文件或目录 | 用途 |
| --- | --- |
| `main.tex` | 论文信息、摘要和完整正文示例 |
| `paper.cls` | 基础排版类和主题色 `jlublue` |
| `preamble.tex` | A4 页面、校徽、首页校名、数学命令、定理和提示框 |
| `references.bib` | BibTeX 文献库 |
| `figures/jlu.pdf` | 吉林大学校徽 |
| `fonts/` | ByteSans 字体和 pdfTeX 字体度量文件 |

## 使用与修改

在 `main.tex` 的 `\begin{document}` 之前填写题目、作者、学院、通讯方式和摘要。通过 `\author[1]{...}` 与 `\affiliation[1]{...}` 关联作者和单位。无需通讯作者说明或项目链接时，删除相应的 `\contribution`、`\correspondence`、`\checkdata` 行，并移除作者编号中的 `\corrauthor`。

将图片放入 `figures/`，用 `\includegraphics` 插入。普通 `figure` 和 `table` 占一栏；跨栏内容使用 `figure*` 或 `table*`。正文示例包含公式、引用、定理、提示框、表格和附录，可直接替换。使用 `\citep{...}` 或 `\citet{...}` 引用 `references.bib` 中的条目。文献样式为 `plainnat`，投稿时按要求调整。

默认使用双栏。单栏排版可将 `main.tex` 中的 `\documentclass[twocolumn]{paper}` 改为 `\documentclass{paper}`。附录默认另起一页并切换单栏；如需双栏附录，删除 `\onecolumn`。

首页右上角默认显示 `figures/jlu.pdf`。可在 `main.tex` 中用 `\paperlogo{figures/your-logo.pdf}` 替换，或用 `\paperlogo{}` 隐藏。主题色 `jlublue` 在 `paper.cls` 中定义，页边距和首页页眉在 `preamble.tex` 中调整。

## 公式与证明的配色框

`preamble.tex` 预定义了五个可换行的 `tcolorbox` 环境：

| 环境 | 配色 | 用途 |
| --- | --- | --- |
| `mainresultbox` | 校蓝 | 主要定理或核心结果 |
| `keypropositionbox` | 绿色 | 关键命题或公式 |
| `keylemmabox` | 青色 | 引理 |
| `definitionbox` | 紫色 | 定义 |
| `keyproofbox` | 橙色 | 对应的证明 |

把 `theorem`、`proposition`、`lemma`、`definition`、`equation` 或 `proof` 放在配色框内，原环境的编号和 `\label` 引用仍然有效。例如：

```tex
\begin{keylemmabox}
  \begin{lemma}\label{lem:example}
  State the claim here.
  \end{lemma}
\end{keylemmabox}

\begin{definitionbox}
  \begin{definition}\label{def:example}
  Define the central term here.
  \end{definition}
\end{definitionbox}
```

定理、命题和证明分别以相同方式放入 `mainresultbox`、`keypropositionbox` 和 `keyproofbox`。原有的 `highlightbox` 继续用于带标题的文字提示。

## 来源与许可

排版类基于原 `ustc_conference.cls` 整理，来源注释保留于 `paper.cls`。原始源文件中未附独立许可说明，本目录未为原有类文件与字体另行声明许可证。公开分发时请核实原始资源及校徽的使用许可。
