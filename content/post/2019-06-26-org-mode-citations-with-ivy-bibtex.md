---
title: 'Org-Mode Citations with Ivy-Bibtex'
date: Wed, 26 Jun 2019 13:35:59 +0000
draft: false
tags: ['Emacs', 'Org Mode']
---

John Kitchin's [org-ref](https://github.com/jkitchin/org-ref) is a great way to handle citations in Emacs' org-mode. It uses [helm-bibtex](https://github.com/tmalsburg/helm-bibtex) to search for and select citatitions to insert, but does not support the corresponding ivy version. Org-ref does have an ivy search function, but it is not nearly as good as ivy-bibtex. Ivy-bibtex will insert citations into org documents, but its default format is not the same as it is in org-ref.

To fix that, I added the following to my init file:

``` tex
(defun bibtex-completion-format-citation-orgref (keys)
  "Formatter for org-ref citations."
  (let\* ((prenote  (if bibtex-completion-cite-prompt-for-optional-arguments (read-from-minibuffer "Prenote: ") ""))
         (postnote (if bibtex-completion-cite-prompt-for-optional-arguments (read-from-minibuffer "Postnote: ") "")))
(if (and (string= "" prenote) (string= "" postnote))
                (format "%s" (s-join "; " (--map (concat "autocite:" it) keys)))
    (format "\[\[%s\]\[%s::%s\]\]"  (s-join "; " (--map (concat "autocite:" it) keys)) prenote postnote))))
```

This prompts for both pre and post-note text when selecting the citation. Here are the org-mode citations that are produced:

*   Citation only: autocite:lewisCounterfactuals1973
*   Citation with post-text: \[\[autocite:lewisCounterfactuals1973\]\[::25\]\]
*   Citation with pre-text: \[\[autocite:lewisCounterfactuals1973\]\[As seen in::\]\]
*   Citation with both pre and post-text: \[\[autocite:lewisCounterfactuals1973\]\[As seen in::25\]\]

When exported, these produce the following LaTeX code:

```
\\autocite{lewisCounterfactuals1973}

\\autocite\[\]\[25\]{lewisCounterfactuals1973}

\\autocite\[As seen in\]\[\]{lewisCounterfactuals1973}

\\autocite\[As seen in\]\[25\]{lewisCounterfactuals1973}
```

I use Chicago parenthetical references – so these compile like this:

*   (Lewis 1973)
*   (Lewis 1973, 25)
*   (As seen in Lewis 1973)
*   (As seen in Lewis 1973, 25)

