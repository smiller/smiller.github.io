---
layout:     post
title:      Beginning Emacs Lisp
date:       2015-01-12
categories: emacs lisp
---

## The Problem

A while back I converted an archive of non-code-related files to org-mode.  The
files had citations in a markdown-like format, so:

	> ADA  <br/>
	COUNTESS OF LOVELACE  <br/>
	1815-1852  <br/>
	Pioneer of Computing  <br/>
	lived here

which, processed through Calibre, produced a nice readable pdf with blockquotes
and linebreaks.

For a while after that, I wrote in org-mode and viewed the files within emacs,
so I just indented quotations, like so:

		Quandunque i colli fanno più nera ombra, 
		Sotto il bel verde la giovane donna 
		Gli fa sparir, come pietra sott’ erba.

and then one day I used org-mode’s export-to-html functionality (C-c C-e h o)
and I lost all the blockquoting and line-breaks.  org-mode needs prose citations
surrounded by

	#+begin_quote
	#+end_quote

to be rendered with \<blockquotes> in export-to-html, and if you want it to
respect line breaks as well, you need to use

	#+begin_verse
	#+end_verse

So.  Going forward I needed to insert begin/end blocks for new citations, and I
had a bunch of older citations I would need to reformat.  Here’s what I build
with emacs lisp to solve the problem.

## The Solution

### The Simplest Case

In a new file, about to add a quotation, I want a shortcut to add either
\#+begin\_quote / #+end\_quote or #+begin\_verse / #+end\_verse and put the
cursor on the empty line between.  This sounds like what
[yasnippets](http://capitaomorte.github.io/yasnippet/) is designed for, but I
wasn’t sure how that would work when I got to converting existing quotations, so
I broke out my ~/.emacs.d/mods-org.el file and added two new shortcuts:

	(global-set-key (kbd "M-s M-q")
			(lambda()
			  (interactive)
			  (insert "#+begin_quote")
			  (newline)
			  (newline)
			  (insert "#+end_quote")
			  (newline)
			  (previous-line)
			  (previous-line)))

	(global-set-key (kbd "M-s M-v")
			(lambda()
			  (interactive)
			  (insert "#+begin_verse")
			  (newline)
			  (newline)
			  (insert "#+end_verse")
			  (newline)
			  (previous-line)
			  (previous-line)))

This meets my simplest case requirement and is fairly self-explanatory.  Going
forward, I can type

	M-s M-q ;; q for quote

to get

	#+begin_quote
	_
	#+end_quote

and

	M-s M-v ;; v for verse

to get

	#+begin_verse
	_
	#+end_verse

[commit](https://github.com/smiller/.new.emacs.d/commit/6fc7348bd16543dab3f55f9b785ee5f1bb19036d)

### Narrowing the Scope

The fact that I put them in ~/.emacs.d/mods-org.el instead of
~/.emacs.d/key-bindings.el foreshadows the next step: they aren’t global key
bindings, I’m only going to use them in org-mode, and in a ruby class they’d
just be noise.  So, since I’ve already got a hook for entering text-mode (which
I’m also using for org-mode), let’s change them from global key bindings to key
bindings which are added to org-mode specifically.

I’ve got an ~/.emacs.d/mode-hooks.el file which already has a custom
text-mode-hook, so I can add two lines to that:

	(defun my-text-mode-hook ()
	  …
	  (define-key org-mode-map (kbd "M-s M-q") 'begin-end-quote)
	  (define-key org-mode-map (kbd "M-s M-v") 'begin-end-verse)
	)

	(add-hook 'text-mode-hook 'my-text-mode-hook)

And change the functions, in the ~/.emacs.d/mods-org.el file, from anonymous
functions in the global-set-key blocks to the named functions we have just
referenced:

	(defun begin-end-quote ()
	  (interactive)
	  (insert "#+begin_quote")
	  (newline)
	  (newline)
	  (insert "#+end_quote")
	  (newline)
	  (previous-line)
	  (previous-line))

	(defun begin-end-verse ()
	  (interactive)
	  (insert "#+begin_verse")
	  (newline)
	  (newline)
	  (insert "#+end_verse")
	  (newline)
	  (previous-line)
	  (previous-line))

Now if we’re in org-mode, the key-bindings do what we expect, but if we’re in
ruby-mode and type them, or type (C-h k) to get the definition of a key binding
and then type (M-s M-v), we get

	M-s M-v is undefined

[commit](https://github.com/smiller/.new.emacs.d/commit/f7d9aa3b667a23061a9191b84ca852fecdba48e0)

### Reformat Existing

That handles the going forward case, but doesn’t handle the case where I’m in an
older file and want to reformat an existing quotation.  To handle both, I’d like
to check when I use the shortcut to see if I’ve got a selected a region or not.
If I haven’t, it’s the going forward case, and I should do what I was doing
before, but if I have, then presumably I want to put the #+before and #+after
blocks around the selected region.

We can tell this because emacs lisp gives us a function
[use-region-p](http://www.gnu.org/software/emacs/manual/html_node/elisp/The-Region.html)
which returns true if there is a region selected.  The most basic if block in
emacs lisp looks like this:

	(if (condition)
    	(do-true-thing)
	  (do-false-thing))

so in our case we have:

	(if (use-region-p)
		(begin-end-quote-for-region)
	  (begin-end-quote-for-new))

and begin-end-quote-for-new is the old begin-end-quote method, and
begin-end-quote-for-region looks like this:

	(defun begin-end-quote-for-region ()
	  (interactive)
	  (insert "#+end_quote")
	  (newline)
	  (goto-char (region-beginning))
	  (insert "#+begin_quote")
	  (newline))

An extra bit of inwardness here is that the cursor starts at the end of
the selected region, so we can just insert "#+end\_quote" and it will show up
after the end, and (region-beginning) and (region-end) hold the beginning and
end of the selected region, so (goto-char (region-beginning)) gets us back to
the beginning so we can insert "#+begin\_quote" before it.

[commit](https://github.com/smiller/.new.emacs.d/commit/1c18565c48237d44f60e9ed68a832a8056085ace)

This gets us to the point where if we’d selected the first quotation and hit M-s
M-v, we’d end up with

    #+begin_verse
    > ADA  <br/>
	COUNTESS OF LOVELACE  <br/>
	1815-1852  <br/>
	Pioneer of Computing  <br/>
	lived here
	#+end_verse

which is a definite improvement, but it still has the old formatting codes.  Can
we get rid of those?

### Remove Old Formatting

First off, we only want to do this in the reformat existing case.  That’s fine,
those two methods (begin-end-quote-for-region and begin-end-verse-for-region)
are already separate, so in each of those methods include a
(remove-old-formatting) method.

What we want to do in pseudo-code is take the selected region and apply

	s/^> //
	s/  <br/>$//

to it.  (We only need the second transformation for verse, not
quotes, and if these got any more complicated we might want two separate
methods, but we can leave them in one for now.)

[setq](https://www.gnu.org/software/emacs/manual/html_node/eintr/Using-setq.html#Using-setq) defines a variable.

[filter-buffer-substring](http://www.gnu.org/software/emacs/manual/html_node/elisp/Buffer-Contents.html)
grabs the text from arg1 to arg2 (and we’re using (region-beginning) and
(region-end) which return the start and end of the selected region), and with
the optional third argument of t deletes the text after copying it.

After that, we’ve got the contents of the selected region in a variable, “in”,
and we can run
[replace-regexp-in-string](http://www.gnu.org/software/emacs/manual/html_node/elisp/Search-and-Replace.html)
on it, taking as arguments search-value, replace-value, and string-to-search in,
and using setq to define to variable we’re storing the result in.

Once we’ve made all the changes we need, we use
[insert](http://www.gnu.org/software/emacs/manual/html_node/elisp/Insertion.html)
the finally modified string back into the buffer.

	(defun remove-old-formatting ()
	  (setq in (filter-buffer-substring (region-beginning) (region-end) t))
	  (setq out (replace-regexp-in-string "^> " "" in))
	  (setq out2 (replace-regexp-in-string "  <br/>$" "" out))
	  (insert out2)
	)

[commit](https://github.com/smiller/.new.emacs.d/commit/853147cf787d7bb52faa7b6409f7e72b117944c9)

And at the end of that, we get:

    #+begin_verse
    ADA
	COUNTESS OF LOVELACE
	1815-1852
	Pioneer of Computing
	lived here
	#+end_verse

Which is very nearly there, but not indented.  How about as a last step we
indent it, so if we’re viewing it in org-mode it still looks like a blockquote?

### Indenting

Let’s put this in our remove-old-formatting method, because again it’s something
that we’ll only want in the reformat existing case.  Given that it’s no longer
just removing old formatting, let’s change the method name to
fix-old-formatting, and to keep things at the same level of
abstraction, let’s put the old remove-old-formatting lines in a new method called
remove-old–formatting-code and add a method indent-if-not-indented.  So we have:

	(defun fix-old-formatting ()
	  (remove-old-formatting-code)
	  (indent-if-not-indented)
	)

	(defun remove-old-formatting-code ()
	  (setq in (filter-buffer-substring (region-beginning) (region-end) t))
	  (setq out (replace-regexp-in-string "^> " "" in))
	  (setq out2 (replace-regexp-in-string "  <br/>$" "" out))
	  (insert out2)
	)

Remember that we have some existing citations in the form

	> ADA  <br/>

and some already indented as

		Quandunque i colli fanno più nera ombra, 

Further, some of the already indented ones have multiple layers of indentation,
and setting a single indentation would break that.  So while [indent-region](https://www.gnu.org/software/emacs/manual/html_node/elisp/Region-Indent.html)
itself is simple enough, once again using (region-beginning) and
(region-end) to give us the selected region, and the third argument for the
number of columns to indent:

	(indent-region (region-beginning) (region-end) 4)

we need to make it conditional on it not already being indented, so we end up
with:

	(defun indent-if-not-indented ()
	  (setq firstFour (filter-buffer-substring (region-beginning) (+ (region-beginning) 4)))
	  (if (not (string= firstFour "    "))
		  (indent-region (region-beginning) (region-end) 4)
		)
	)

using filter-buffer-substring again to grab the first four characters of the
region (without the optional third argument so we don’t delete it), and if they
aren’t spaces, do the indent.  If they are, it’s one of the newer existing
quotations and we should leave it as it is, as one of them for instance was
pseudo-code

		count = 500 
		day.each do
		  wrote_words?(count) ? 
		count += 100 : 
		count -= 100
		  count = 100 if count < 100
		  count = 1500 if count > 1500
		end

and not doing that check would have clobbered all the internal indenting.

[commit](https://github.com/smiller/.new.emacs.d/commit/a8eb0e60c4ef3fd948f4813cffb05f7077fbe33e)

With that, we finally get the desired end result for the older existing quotations:

	#+begin_verse
		ADA
		COUNTESS OF LOVELACE
		1815-1852
		Pioneer of Computing
		lived here
	#+end_verse

without clobbering existing indentation for the more recent existing quotations:

	#+begin_verse
		count = 500 
		day.each do
		  wrote_words?(count) ? 
		count += 100 : 
		count -= 100
		  count = 100 if count < 100
		  count = 1500 if count > 1500
		end
	#+end_verse

## End and Afterthoughts

The current state of my ~/.emacs.d/ is
[here](https://github.com/smiller/.new.emacs.d).  It is very much a work in
progress.  Also, having just looked at Sacha Chua’s more
[literate emacs config](http://pages.sachachua.com/.emacs.d/Sacha.html) using
[org-babel](http://orgmode.org/worg/org-contrib/babel/), I’m quite tempted to
try that out, instead of composing the two or three additional
explanatory/introductory blog posts that occurred to me would be helpful as I
was writing this up.


