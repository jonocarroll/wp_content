---
ID: 85
post_title: Use an alias when using sudo
author: Jonathan Carroll
post_date: 2012-11-18 14:41:36
post_excerpt: ""
layout: post
permalink: >
  http://jcarroll.com.au/2012/11/18/use-an-alias-when-using-sudo/
published: true
---
Neat! Stolen from here: <a href="http://askubuntu.com/a/22043" title="Alias with sudo" target="_blank">http://askubuntu.com/a/22043</a>

To allow aliases when using sudo<!--more-->, add the following line to your ~/.bashrc:

[sourcecode language="bash"]
alias sudo='sudo '
[/sourcecode]

From the bash manual:

<blockquote>Aliases allow a string to be substituted for a word when it is used as the first word of a simple command. The shell maintains a list of aliases that may be set and unset with the alias and unalias builtin commands.

The first word of each simple command, if unquoted, is checked to see if it has an alias. If so, that word is replaced by the text of the alias. The characters ‘/’, ‘$’, ‘`’, ‘=’ and any of the shell metacharacters or quoting characters listed above may not appear in an alias name. The replacement text may contain any valid shell input, including shell metacharacters. The first word of the replacement text is tested for aliases, but a word that is identical to an alias being expanded is not expanded a second time. This means that one may alias ls to "ls -F", for instance, and Bash does not try to recursively expand the replacement text. If the last character of the alias value is a space or tab character, then the next command word following the alias is also checked for alias expansion.
</blockquote>

(Emphasis mine).

Bash only checks the first word of a command for an alias, any words after that are not checked. That means in a command like sudo ll, only the first word (sudo) is checked by bash for an alias, ll is ignored. We can tell bash to check the next word after the alias (i.e sudo) by adding a space to the end of the alias value.

via <a href="http://askubuntu.com/questions/22037/aliases-not-available-when-using-sudo">alias - Aliases not available when using sudo - Ask Ubuntu</a>.