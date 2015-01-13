---
layout:     post
title:      Emacs Org-mode Links and Exported Html
date:       2015-01-13
categories: emacs
---

If you have an archive of files in org-mode and you want to link between them,
say from today’s entry to the entry of 9 March 2013, you have several options,
as laid out here:

[http://orgmode.org/manual/Search-options.html](http://orgmode.org/manual/Search-options.html)

## The Simplest Case, for .org

The simplest is to provide the text of the header in the link, like so:
so:

    [[file:2013.org::Saturday 9 March 2013][9 March 2013]]

which with the addition of the final square bracket collapses in the text into
“9 March 2013”, and when you’re on the link and type “C-c C-o”, it will open the
“2013.org” file at the header “Saturday 9 March 2013”.  If you find you’ve made
an error in the link target or title, typing “C-c C-l” will let you edit them.

[http://orgmode.org/manual/Handling-links.html](http://orgmode.org/manual/Handling-links.html)

And this works perfectly, until you export it to html, and then, of course, it
doesn’t.

## The Extra Step, for .html

To get a link also to work in html, you need to set a custom_id on the header,
which you do like this:

	*** Saturday 9 March 2013
    	:PROPERTIES:
	      :CUSTOM_ID: 20130309
	    :END:

This will also attach an id attribute to the header element in the exported
html, so in both .org and .html it is recognized as #20130309, and if you then
change the link to

    [[file:2013.org::#20130309][9 March 2013]]

it will work as before in the *.org file, and also in the exported *.html file.
