---
title: 'Truth Tables in LaTeX'
date: Sat, 10 Feb 2018 19:35:49 +0000
draft: false
tags: ['LaTeX', 'Logic', 'Teaching', 'Uncategorized']
---

Typesetting truth tables has never been easy. LaTeX is the gold standard for displaying logic and mathematics, but tables are awkward to edit at best. Tables are much simpler in Microsoft Word, but displaying formulas is a horrible experience.[1](#fn-1012-1) Here is my current workflow. 

The text that I'm using this semester is [_Introduction to Formal Logic with Philosophical Applications_](https://global.oup.com/ushe/product/introduction-to-formal-logic-with-philosophical-applications-9780199386482?cc=us&lang=en&) by Russell Marcus. Instead of arrows and the ampersand, it uses the horseshoe, triple bar, and dot. So, I add the following lines to my LaTeX preamble to simplify entering the symbols.[2](#fn-1012-2)

{{< highlight tex >}}\newcommand{\lneg}{\mathord{\sim}} 
\renewcommand{\land}{\bullet} 
\newcommand{\lif}{\supset} 
\newcommand{\liff}{\equiv} 
{{< / highlight >}}

Then, I enter the truth table in either Excel or Numbers. For example, this would be a simple one line table determining the truth value of a formula for a given valuation: 

![Numbers truth table](http://rlridenour.files.wordpress.com/2018/02/numbers-truth-table1.png "numbers-truth-table.png") Copy the cells that you want included in the truth table. Go to [Tables Generator](http://www.tablesgenerator.com), and select "LaTeX Tables" from the top menu bar. Below the top menu bar is a drop-down menu bar. Click on "File" then "Paste table data..." and paste the table data. Table Generator will generate a nicely formatted LaTeX table: \[code lang=latex\] \begin{table}\[\] \centering \caption{My caption} \label{my-label} \begin{tabular}{llllllll} P & Q & R & P & \lif & (\lneg Q & \land & R) \\ 1 & 1 & 1 & 1 & 0 & 0 & 0 & 1 \end{tabular} \end{table} \[/code\] I delete the first four lines and the last line, leaving just the table data and the lines declaring the tabular environment: \[code lang=latex\] \begin{tabular}{cccccccc} P & Q & R & P & \lif & (\lneg Q & \land & R) \\ 1 & 1 & 1 & 1 & 0 & 0 & 0 & 1 \end{tabular} \[/code\] At this point, typesetting will fail because the symbols need to be in math mode. So, I've found two options. The first is to put all the commands for the symbols in math mode: \[code lang=latex\] \begin{tabular}{cccccccc} P & Q & R & P & \(\lif\) & (\(\lneg\) Q & \(\land\) & R) \\ 1 & 1 & 1 & 1 & 0 & 0 & 0 & 1 \end{tabular} \[/code\] The second option is to change "tabular" to "array" and put the entire table into math mode: \[code lang=latex\] \\[ \begin{array}{cccccccc} P & Q & R & P & \lif & (\lneg Q & \land & R) \\ 1 & 1 & 1 & 1 & 0 & 0 & 0 & 1 \end{array} \\] \[/code\] Arrays are centered on the page. If you would prefer them printed at the left margin, add "fleqn" to the document class options: `\documentclass[fleqn]{article}` Since the array is in math mode, the letters will be italicized. I use the newtxmath font package, and it has a "frenchmath" option that sets the math font to non-italic. Other math fonts may have a similar option. Finally, whichever option is used, we need to add two lines. Adding a vertical line character to the table or array formatting options will place a vertical line between the valuation section and the rest of the truth table. Adding the booktabs package to the preamble will allow us to separate the sentence from the rest of the truth table. This gives us the final version, \[code lang=latex\] \\[ \begin{array}{ccc|ccccc} P & Q & R & P & \lif & (\lneg Q & \land & R) \\ \midrule 1 & 1 & 1 & 1 & 0 & 0 & 0 & 1 \end{array} \\] \[/code\] which produces this: ![Truth Table](http://rlridenour.files.wordpress.com/2018/02/truth-table.png "truth-table.png")

* * *

1.  Apple's Pages now allows users to [add formulas](https://support.apple.com/en-us/HT207569) with LaTeX. It's looking like a good solution for those who like more traditional word processors. [↩](#fnref-1012-1)
2.  The AMS LaTeX packages already include a command called "\lor" for entering the vee or wedge. [↩](#fnref-1012-2)

