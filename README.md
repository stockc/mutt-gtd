mutt-gtd
========

Little mutt hack to toggle gtd tags via the custom email header field X-Label 

Motivation and idea:
--------------------

After reading http://www.nikilster.com/thoughts/how-to-win-at-email/#sthash.PvTgsQ0I.dpbs (via @felixge) I started using http://blitiri.com.ar/p/other/mutt-labels/ but disliked the amount of required keystrokes to actually do the tagging of single emails.

Wouldn't it be easier to simple toggle a fixed set of tags? Currently I only use "urgent", "todo", "review" and "waiting" for my email gtd.

Here is the result.

Put the script x-label-toggler in your ~/bin directory and modify ~/.muttrc in the follwing way. (Note: If you place it into another directory than ~/bin than modify the folling configuration accordingly)

Map the keystrokes to the toggling script:
------------------------------------------

```
macro index <esc>w "<enter-command>set editor=\"~/bin/x-label-toggler waiting\"\n\
<edit><next-undeleted>\
<enter-command>set editor=vim\n" "Toggle label"
macro index <esc>t "<enter-command>set editor=\"~/bin/x-label-toggler todo\"\n\
<edit><next-undeleted>\
<enter-command>set editor=vim\n" "Toggle label"
macro index <esc>u "<enter-command>set editor=\"~/bin/x-label-toggler urgent\"\n\
<edit><next-undeleted>\
<enter-command>set editor=vim\n" "Toggle label"
macro index <esc>r "<enter-command>set editor=\"~/bin/x-label-toggler review\"\n\
<edit><next-undeleted>\
<enter-command>set editor=vim\n" "Toggle label"
macro index \Cw "<limit>~y waiting\n" "Limit view to label waiting"
macro index \Ct "<limit>~y todo\n" "Limit view to todo"
macro index \Cu "<limit>~y urgent\n" "Limit view to urgent"
macro index \Cr "<limit>~y review\n" "Limit view to review"
```

Enable coloring in mutt:
------------------------

```
color index green default '~y waiting | ~(~y waiting)'
color index yellow default '~y review | ~(~y review)'
color index brightred default '~y todo | ~(~y todo)'
color index brightred default '~y urgent | ~(~y urgent)'
```

Enable display of X-Label
-------------------------

```
set index_format="%4C %Z %{%b %d} %-15.15L %?M?(#%03M)&(%4l)? %?y?(%.20Y) ?%s"
```

Trying it out:
--------------

In mutt you can now hit <esc>w to mark an email with tag "waiting" and unmark it by hitting <ecs>w again. To limit your view to emails with tag "waiting" just hit <ctrl>w.

Happy tagging in mutt
Christoph
