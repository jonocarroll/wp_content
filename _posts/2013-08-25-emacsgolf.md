---
ID: 336
post_title: EmacsGolf
author: Jonathan Carroll
post_date: 2013-08-25 09:14:19
post_excerpt: ""
layout: post
permalink: >
  http://jcarroll.com.au/2013/08/25/emacsgolf/
published: true
tc-thumb-fld:
  - 'a:2:{s:9:"_thumb_id";s:3:"308";s:11:"_thumb_type";s:5:"thumb";}'
---
Who says I don't like sport?

<!--more-->

Competitive nerdiness? Oh yeah! On trying to learn as much as I can about using <a title="THE one true text editor" href="http://en.wikipedia.org/wiki/Emacs" target="_blank">Emacs</a> better (THE one true text-editor) I came across a wonderful site; <a title="Emacs Rocks!" href="http://emacsrocks.com" target="_blank">emacsrocks.com</a> which has video tutorials on some really handy features (Emacs is full of features to the point that people say 'Emacs is a great operating system, if only it had a decent text-editor!').

On that site the host mentioned something called <a title="VimGolf" href="http://vimgolf.com/" target="_blank">VimGolf</a> (<a title="That other editor" href="http://en.wikipedia.org/wiki/Vim" target="_blank">Vim</a> being that other -- probably useful -- text editor that defines the Trek/Wars level conflict between nerds) where people try to transform a text file from one given configuration to another using the smallest number of keystrokes (golf style; lowest count wins). On Emacs vs. Vim, there's an obligatory XKCD:

[caption id="" align="aligncenter" width="740"]<a href="http://xkcd.com/378/"><img src="http://imgs.xkcd.com/comics/real_programmers.png " alt="Of course, this has been implemented, and works." width="740" height="406" /></a> Of course, this has been implemented, and works.[/caption]

There's a mode in Vim that tracks keystrokes then submits that to the VimGolf site. There seems to be an Emacs implementation but I'm still working on getting that functional. For now, I'll just count by hand.

The challenge discussed on <a title="Emacs Rocks!" href="http://emacsrocks.com" target="_blank">emacsrocks.com</a> involves changing the following file:
<code>
one
two
three
four
five
six
seven
eight
nine
ten
1
2
3
4
5
6
7
8
9
10
</code>

into this one:
<code>
one    1
two    2
three  3
four   4
five   5
six    6
seven  7
eight  8
nine   9
ten    10
</code>

Seems easy? Go on - open the first bit up in Notepad and see how many keystrokes it takes you. Remember, no touching the mouse, and every time you hit the keyboard it counts as a keystroke, either for deleting something or entering something. As far as I can tell, multi-keys are counted as single keystrokes, so SHIFT+END is a single move.

Emacs (and Vim) have useful commands that you just don't find in things like Notepad. I don't think there's a way to, say, swap two lines in Notepad. That's the tip of the iceberg for usefulness in Emacs. Macros can be recorded, commands can be repeated, clever regions can be selected, and so on.

Anyway, back to the challenge. The VimGolf record for the above is 17 keystrokes (I don't use Vim, so these are irrelevant to me). <a title="Emacs Rocks!" href="http://emacsrocks.com" target="_blank">emacsrocks.com</a> showed a method that took 13 in Emacs:

<a title="Emacs Rocks! Episode 2" href="http://emacsrocks.com/e02.html" target="_blank">emacsrocks.com -- Episode 2</a>

which was then updated to 10 by some useful send-ins:

<a title="Emacs Rocks! Episode 3" href="http://emacsrocks.com/e03.html" target="_blank">emacsrocks.com -- Episode 3</a>
<code>
1. &lt;f3&gt;           # begin define-macro
2. M-9 C-x C-t    # (repeat x9) transpose-line
3. BACKSPACE      # delete newline
4. TAB            # insert TAB
5. M-&lt;            # move to start of buffer
6. &lt;f4&gt;           # end define-macro
7. M-9        # (repeat x9) macro
*** 10 keystrokes
</code>

I had a play around myself. My first attempt wasn't technically valid - it uses a custom command that doesn't exist in the vanilla install (iy-go-to-char as discovered via <a title="Emacs Rocks! Episode 4" href="http://emacsrocks.com/e04.html" target="_blank">emacsrocks.com -- Episode 4</a>). Still, I clock it at 16 keystrokes:
<code>
1. M-9 C-c n      # multiple-cursors next 9 lines
2. C-e            # move to end of line
3. C-q TAB        # insert TAB
4. C-g            # exit mc mode
5. -&gt;             # next line
6. C-f 0          # move to end of '10'
7. C-x r k        # kill rectangle
8. M-&lt;            # move to start of buffer
9. C-e            # move to end of line
10. C-x r y       # yank rectangle
*** 16 keystrokes
</code>

If I try starting from the middle of the file instead:
<code>
1. M-g M-g 11 RET # move to line 11 ('1')
2. C-f 0          # move to after '10'
3. C-x r k        # kill rectangle
4. M-&lt;            # move to start of buffer
5. C-e            # move to end of line
6. TAB            # insert TAB
7. C-x r y        # yank rectangle
*** 13 keystrokes
</code>

Not bad, but let's do better. Sticking to standard commands (though, some of these I discovered via <a title="Emacs Rocks!" href="http://emacsrocks.com">emacsrocks.com</a>) I can reduce this to: I had hoped the go-to was quick, but it's actually more keystrokes than just search-to, so let's ditch that idea:
<code>
1. C-s 1          # search for '1'
2. &lt;-             # move to start of line
3. M-&gt;            # move to end of buffer
4. C-x r k        # kill rectangle
5. M-&lt;            # move to start of buffer
6. C-e            # move to end of line
7. TAB            # insert TAB
8. C-x r y        # yank rectangle
*** 11 keystrokes
</code>

Re-thinking this a little and attacking from the end of the file rather than the start, I can get to:
<code>
1. M-&gt;            # move to end of buffer
2. C-r 1 C-r      # move to '1'
3. C-x r k        # kill rectangle
4. M-&lt;            # move to start of buffer
5. C-e            # move to end of line
6. TAB            # insert TAB
7. C-x r y        # yank rectangle
*** 11 keystrokes
</code>

Fewer operations, but the same number of keystrokes. It may be possible to bind the rectangle commands to a single keystroke, which would get this down to 9 and beat the emacsrocks.com version. Still, not too shabby. That's where I got to, but it may be possible to do better. I like the rectangle kill/yank and maybe there are some strokes to save on the movements.

As a last attempt I discovered a 2C-two-columns command  s that splits the buffer at a point, with the option to join it back together with  1 (in my case, after moving the numbers vertically back up). Apart from being too long (20), this also uses multiple-cursors, so invalid anyway:
<code>
1. C-s 1          # search '1'
2. &lt;-             # move to start of line
3. RET            # insert line-break
4. F2 s           # split on separator
5. C-SPACE        # mark
6. M-&lt;            # move to start of buffer
7. C-c C-a        # select cursor on all lines
8. C-e            # move to end of lines
9. TAB            # insert TAB
10. C-x o         # switch buffers
11. M-&lt;           # move to start of buffer
12. M-d           # delete word
13. 1             # insert '1'
14. F2 1          # merge buffers
15. DEL           # delete line breaks (multiple cursors still active)
*** 20 keystrokes
</code>

I like my best effort, and perhaps I'll play a few more rounds. I love these nerdy games, they're a great way to put some new knowledge to the test. I'm using the useful commands I've put into practice all the time now, which is making me much more efficient within Emacs.