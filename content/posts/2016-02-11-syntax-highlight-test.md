---
comments: true
date: '2016-02-11T05:35:56Z'
tags:
- jekyll
title: Syntax Highlighting Test
url: "/2016/02/11/syntax-highlight-test/"

---
Jekyll changed from Pygments to Rouge for syntax highlighting. Here is my LaTeX article format:

``` tex
\documentclass[11pt]{article}
% \usepackage{fontspec} %Uncomment if using XeTeX.
% \setmainfont[Mapping=tex-text]{Linux Libertine} %Uncomment if using XeTeX.
\usepackage{graphicx,epstopdf,amsmath,amssymb,bm,url}
\usepackage{microtype,todonotes}
% \usepackage[american]{babel}
\usepackage[letterpaper,centering]{geometry}
\usepackage[compact,small]{titlesec}
\usepackage[parfill]{parskip} % Line between paragraphs
\usepackage[authordate,url=false,isbn=false,backend=biber]{biblatex-chicago} %Change authordate to notes if desired.
\addbibresource{/Users/rlridenour/Dropbox/bibtex/randybib.bib}
\clubpenalty = 10000 % Reduce orphans and widows
\widowpenalty = 10000

% Choose one of the following (if not choosing the default, 
% viz., Computer Modern, font family):

% \usepackage{mathpazo}
% \usepackage{kpfonts}
% \usepackage{mathptmx}
\usepackage{newtxtext,newtxmath}
% \usepackage{libertine} \usepackage[libertine]{newtxmath}

\usepackage[T1]{fontenc} %Comment out if using LaTeX.
\usepackage{hyperref}

\title{Title}
\author{Randy Ridenour}
% \date{}  % Activate to display a given date or no date

\begin{document}
\maketitle



% \printbibliography


\end{document}
```
