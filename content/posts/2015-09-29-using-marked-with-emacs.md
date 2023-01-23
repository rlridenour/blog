---
comments: true
date: '2015-09-29T15:22:12Z'
tags:
- emacs
- markdown
title: Using Marked with Emacs
url: "/2015/09/29/using-marked-with-emacs/"

---
It's time to revisit a subject I covered in 2014, using Emacs to open a Markdown file in [Marked][marked], an excellent Markdown previewer for OS X.[^1] I have used two different methods of opening files in Marked from Emacs, both of which have respective advantages.

The first is a function expressly for opening files in [Marked][marked]. Add the following code to your emacs init file, and then press "Control-c m" to open the current file in Marked.

{{< highlight lisp >}}
(defun markdown-preview-file ()
  "run Marked on the current file and revert the buffer"
  (interactive)
  (shell-command
   (format "open -a /Applications/Marked\\ 2.app %s"
           (shell-quote-argument (buffer-file-name))))
  )

(global-set-key "\C-cm" 'markdown-preview-file)
{{< / highlight >}}

The second is a function for opening files in the default application for that type of file. This is part of Bozhidar Batsov's [Emacs Prelude][prelude] starter kit, which I highly recommend. Again, add the following to your init file:


{{< highlight lisp >}}
(defun open-with (arg)
  "Open visited file in default external program.
When in dired mode, open file under the cursor.

With a prefix ARG always prompt for command to use."
  (interactive "P")
  (let* ((current-file-name
          (if (eq major-mode 'dired-mode)
              (dired-get-file-for-visit)
            buffer-file-name))
         (open (pcase system-type
                 (`darwin "open")
                 ((or `gnu `gnu/linux `gnu/kfreebsd) "xdg-open")))
         (program (if (or arg (not open))
                      (read-shell-command "Open current file with: ")
                    open)))
					(start-process "prelude-open-with-process" nil program current-file-name)))

(global-set-key (kbd "C-c o") 'open-with)
{{< / highlight >}}

The second method is what I currently use. "Control-c o" opens the current file in the default application, which is set in the system. In order for it to work with Markdown files, you'll need to make [Marked][marked] the default application for Markdown files, which means that to open a file for editing from the Finder, you'll need to right-click and select "Open With." The advantage is that you can use the same command from Dired to open PDF's in your preferred PDF reader, Word docs in Word, etc.

[^1]: Its excellence lies partly in the fact that it's not simply a previewer, it also does many other things, like word count, reading analyses, and link validation.

[marked]: http://marked2app.com/

[prelude]: http://batsov.com/prelude/



