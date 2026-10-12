# 吉林大学科研论文模板

吉林大学主题的中英文 LaTeX 科研论文模板，默认采用 A4 双栏排版，包含校徽、作者单位、摘要、公式、流程图、三线表、定理与证明、参考文献和附录示例。

本项目不是吉林大学本科、硕士或博士学位论文的官方模板。用于投稿时，请根据期刊或会议要求调整格式。正文、作者信息和实验数据均为占位示例，需要替换为真实内容。

## 快速开始

在项目根目录执行对应命令：

| 版本 | 主文件 | 编译器 | 编译命令 | 输出 |
| --- | --- | --- | --- | --- |
| 英文 | `main.tex` | pdfLaTeX | `latexmk -pdf main.tex` | `main.pdf` |
| 中文 | `main-cn.tex` | XeLaTeX | `latexmk -xelatex main-cn.tex` | `main-cn.pdf` |

首次使用时，选择一个主文件，填写题目、作者、学院和摘要，然后替换正文及参考文献。两个版本共用排版类、校徽和参考文献库，可以分别编译。

## 环境与编译

### 本地环境

建议安装完整的 TeX Live，包含 `latexmk`、pdfLaTeX、XeLaTeX、BibTeX，以及 `ctex`、`fontspec`、TikZ、`tcolorbox` 等宏包。精简安装需补齐缺失宏包和字体。中文源文件使用 UTF-8 编码。

请保留 `fonts/` 目录中项目自带的 `ByteSans-*.ttf` 和 `bytesans*.tfm` 文件。中文版使用 TeX Live 自带的 Fandol 中文字体，无需安装系统宋体。

```sh
# 英文版
latexmk -pdf main.tex

# 中文版
latexmk -xelatex main-cn.tex
```

`latexmk` 会自动执行参考文献处理和所需的多轮编译。每次修改后，重新运行对应命令即可。

没有 `latexmk` 时，依次执行：

```sh
# 英文版
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex

# 中文版
xelatex main-cn.tex
bibtex main-cn
xelatex main-cn.tex
xelatex main-cn.tex
```

清理中间文件并保留 PDF：

```sh
latexmk -c main.tex
latexmk -c main-cn.tex
```

### Overleaf

上传整个项目，保留 `fonts/` 和 `figures/` 目录。在项目设置中，根据上表选择主文件和编译器，然后重新编译。不要只切换主文件而忽略编译器设置。

英文版依赖 pdfTeX 字体映射，使用 pdfLaTeX；中文版入口包含兼容配置，使用 XeLaTeX。不要直接将英文版切换到 XeLaTeX，也不要用 pdfLaTeX 编译中文版。

## 文件说明

| 文件或目录 | 用途 |
| --- | --- |
| `main.tex` | 英文论文入口：论文信息、摘要和完整正文示例 |
| `main-cn.tex` | 中文论文入口：论文信息、摘要、关键词和完整正文示例 |
| `paper.cls` | 基础排版类，包含主题色 `jlublue` 的唯一颜色定义 |
| `preamble.tex` | 公共配置：A4 页面、校徽、首页校名、数学命令、定理和提示框 |
| `preamble-cn.tex` | 中文配置：加载公共配置，设置字体、缩进及中文标签 |
| `references.bib` | 两个版本共用的 BibTeX 文献库 |
| `figures/` | 插图目录，`jlu.pdf` 为现有的吉林大学校徽 |
| `fonts/ByteSans-Bold.ttf`、`fonts/ByteSans-Medium.ttf` | 标题等位置使用的英文字体 |
| `fonts/bytesans.tfm`、`fonts/bytesansmedium.tfm` | 英文版 pdfTeX 使用的字体度量文件 |
| `.gitignore` | 忽略编译中间文件和主文档 PDF，保留插图 PDF |

中文版通过 `preamble-cn.tex` 加载 `preamble.tex`，不需要再次手动引入公共配置。日常添加宏包或修改主题配置时，优先编辑相应的导言区文件。

## 填写论文信息

论文信息写在所选主文件的 `\begin{document}` 之前。中文示例：

```tex
\title{论文标题：\\可选副标题}
\author[1]{张三}
\author[1\corrauthor]{李四}
\affiliation[1]{吉林大学某某学院，吉林长春，130012}
\contribution[\mathsection]{通讯作者}
\checkdata[通讯邮箱]{\email{author@example.com}}
\checkdata[项目地址]{\url{https://example.com/project}}
\checkdata[关键词]{关键词一；关键词二；关键词三}

\abstract{这里填写论文摘要。}
```

英文版填写相应英文内容，将 `School of Your Discipline` 替换为学院英文名。英文入口使用 `\correspondence{\email{author@example.com}}` 设置通讯邮箱，也可以用 `\checkdata[Keywords]{...}` 添加关键词。

多个单位按编号关联：

```tex
\author[1,2]{作者姓名}
\affiliation[1]{吉林大学某某学院，吉林长春，130012}
\affiliation[2]{合作单位，城市，邮编}
```

每个作者和单位分别写一条命令。无需通讯作者说明或项目链接时，删除相应的 `\contribution`、`\correspondence`、`\checkdata` 行，并移除作者编号中的 `\corrauthor`。摘要使用 `\abstract{...}` 命令填写。

## 正文与插图

使用 `\section`、`\subsection` 等组织正文。两个入口均提供可直接替换的公式、定理、表格和流程图示例。

图片放入 `figures/`，使用如下方式插入；`\caption` 后放置 `\label`：

```tex
\begin{figure}[t]
  \centering
  \includegraphics[width=\linewidth]{your-figure.pdf}
  \caption{图片说明。}
  \label{fig:example}
\end{figure}

如\cref{fig:example}所示，……
```

双栏正文中的普通 `figure` 和 `table` 只占一栏。跨栏内容使用 `figure*` 或 `table*`，图片宽度可设为 `\textwidth`；跨栏浮动体通常出现在页顶。

`\cref{...}` 和 `\Cref{...}` 可引用已编号的公式、图表等对象。中文版已将示例使用的公式、图表、章节和定理引用名称设置为中文。

提示框写法：

```tex
\begin{highlightbox}[核心思想]
填写关键结论或方法说明。
\end{highlightbox}
```

## 参考文献

在 `references.bib` 中添加文献条目，并通过引用键使用：

```tex
\citep{lamport1994latex}
\citet{lamport1994latex}
\citep{lamport1994latex,knuth1984texbook}
```

模板使用 `natbib` 的数字引用模式，文献样式为 `plainnat`，默认只列出正文引用的条目。新增文献后重新运行对应的 `latexmk` 命令；手动编译时运行 BibTeX 后还需编译两次。

中文版将文献列表标题设为“参考文献”，文献条目的格式仍由 `plainnat` 决定。当前样式不是 GB/T 7714；如需其他格式，应按照投稿要求选择兼容的文献样式。

## 排版与主题配置

### 单栏与附录

正文默认双栏。需要单栏时，在所选主文件中将

```tex
\documentclass[twocolumn]{paper}
```

改为

```tex
\documentclass{paper}
```

附录默认另起一页并切换为单栏。如需双栏附录，删除主文件中的 `\onecolumn`，保留 `\clearpage` 和 `\appendix`。

### 校徽、校名与颜色

首页右上角默认显示 `figures/jlu.pdf`。在主文件中替换或隐藏校徽：

```tex
\paperlogo{figures/your-logo.pdf} % 替换校徽
% \paperlogo{}                  % 隐藏校徽
```

英文首页校名为 `JILIN UNIVERSITY`，中文首页为“吉林大学 JILIN UNIVERSITY”。分别在 `preamble.tex` 和 `preamble-cn.tex` 的 `firststyle` 页眉配置中调整。

主题色统一使用 `jlublue`，在 `paper.cls` 中定义为 `1D5CAB`。如需调整颜色，修改这一处定义即可，无需在导言区重复定义颜色。

页面边距和页眉高度通过 `preamble.tex` 中的 `\geometry{...}` 调整。修改这一配置会同时影响中英文版本。

### 中文字体

中文字体配置位于 `preamble-cn.tex`，默认使用 Fandol；中文正文首行缩进为两个汉字宽度。若要使用其他中文字体，应在加载 `ctex` 后通过 `\setCJKmainfont`、`\setCJKsansfont` 等设置，并确保本地或 Overleaf 环境中具有对应字体文件。

`main-cn.tex` 开头的兼容代码用于处理类文件中的 pdfTeX 专用命令。中文版本通过 `fontspec` 加载英文字体，不需要为中文支持修改 `paper.cls`。

## 常见问题

| 现象 | 处理方式 |
| --- | --- |
| 中文入口提示需要 XeLaTeX | 使用 `latexmk -xelatex main-cn.tex`，或修改编辑器的编译器设置 |
| 找不到 ByteSans 字体或度量文件 | 检查配套 `.ttf`、`.tfm` 文件是否保留在 `fonts/` 目录 |
| 找不到 Fandol 字体或 `ctex.sty` | 补齐 TeX Live 中文字体和宏包组件 |
| 引用显示为问号或参考文献未更新 | 检查引用键与 `\label`，并执行包含 BibTeX 的完整编译流程 |
| 更换编译器后出现旧缓存相关错误 | 先用 `latexmk -c` 清理对应主文件，再用正确的编译器重新编译 |
| 图表没有出现在源码所在位置 | 图表是浮动体；检查尺寸及放置选项，跨栏图表优先使用 `[t]` |

## 来源说明

排版类基于原 `ustc_conference.cls` 整理，来源注释保留于 `paper.cls`。吉林大学主题适配将原主题色名称统一为 `jlublue`，其余学校配置在导言区实现；字体路径已调整为 `fonts/`，中文支持不额外修改类文件。

原始源文件中未附独立许可说明，本目录未为原有类文件与字体另行声明许可证。公开分发时请核实原始资源及校徽的使用许可。
