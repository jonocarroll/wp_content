---
ID: 1046
post_title: 'Data Munging with R Preview &#8211; Storing Values (Assigning)'
author: Jonathan Carroll
post_date: 2017-06-23 21:11:20
post_excerpt: ""
layout: post
permalink: https://jcarroll.com.au/?p=1046
published: false
---
<style>
.admonitionblock>table{border-collapse:separate;border:0;background:none;width:100%}
.admonitionblock>table td.icon{text-align:center;width:80px}
.admonitionblock>table td.icon img{max-width:none}
.admonitionblock>table td.icon .title{font-weight:bold;font-family:"Open Sans","DejaVu Sans",sans-serif;text-transform:uppercase}
.admonitionblock>table td.content{padding-left:1.125em;padding-right:1.25em;border-left:1px solid #ddddd8;color:rgba(0,0,0,.6)}
.admonitionblock>table td.content>:last-child>:last-child{margin-bottom:0}
.exampleblock>.content{border-style:solid;border-width:1px;border-color:#e6e6e6;margin-bottom:1.25em;padding:1.25em;background:#fff;-webkit-border-radius:4px;border-radius:4px}
.exampleblock>.content>:first-child{margin-top:0}
.exampleblock>.content>:last-child{margin-bottom:0}
.sidebarblock{border-style:solid;border-width:1px;border-color:#e0e0dc;margin-bottom:1.25em;padding:1.25em;background:#f8f8f7;-webkit-border-radius:4px;border-radius:4px}
.sidebarblock>:first-child{margin-top:0}
.sidebarblock>:last-child{margin-bottom:0}
.sidebarblock>.content>.title{color:#7a2518;margin-top:0;text-align:center}
.exampleblock>.content>:last-child>:last-child,.exampleblock>.content .olist>ol>li:last-child>:last-child,.exampleblock>.content .ulist>ul>li:last-child>:last-child,.exampleblock>.content .qlist>ol>li:last-child>:last-child,.sidebarblock>.content>:last-child>:last-child,.sidebarblock>.content .olist>ol>li:last-child>:last-child,.sidebarblock>.content .ulist>ul>li:last-child>:last-child,.sidebarblock>.content .qlist>ol>li:last-child>:last-child{margin-bottom:0}
.literalblock pre,.listingblock pre:not(.highlight),.listingblock pre[class="highlight"],.listingblock pre[class^="highlight "],.listingblock pre.CodeRay,.listingblock pre.prettyprint{background:#f7f7f8}
.sidebarblock .literalblock pre,.sidebarblock .listingblock pre:not(.highlight),.sidebarblock .listingblock pre[class="highlight"],.sidebarblock .listingblock pre[class^="highlight "],.sidebarblock .listingblock pre.CodeRay,.sidebarblock .listingblock pre.prettyprint{background:#f2f1f1}
.literalblock pre,.literalblock pre[class],.listingblock pre,.listingblock pre[class]{-webkit-border-radius:4px;border-radius:4px;word-wrap:break-word;padding:1em;font-size:.8125em}
.literalblock pre.nowrap,.literalblock pre[class].nowrap,.listingblock pre.nowrap,.listingblock pre[class].nowrap{overflow-x:auto;white-space:pre;word-wrap:normal}
.literalblock.output pre{color:#f7f7f8;background-color:rgba(0,0,0,.9)}
.listingblock pre.highlightjs{padding:0}
.listingblock pre.highlightjs>code{padding:1em;-webkit-border-radius:4px;border-radius:4px}
.listingblock pre.prettyprint{border-width:0}
.listingblock>.content{position:relative}
.listingblock code[data-lang]:before{display:none;content:attr(data-lang);position:absolute;font-size:.75em;top:.425rem;right:.5rem;line-height:1;text-transform:uppercase;color:#999}
.listingblock:hover code[data-lang]:before{display:block}
.listingblock.terminal pre .command:before{content:attr(data-prompt);padding-right:.5em;color:#999}
.listingblock.terminal pre .command:not([data-prompt]):before{content:"$"}
table.pyhltable{border-collapse:separate;border:0;margin-bottom:0;background:none}
table.pyhltable td{vertical-align:top;padding-top:0;padding-bottom:0;line-height:1.45}
table.pyhltable td.code{padding-left:.75em;padding-right:0}
pre.pygments .lineno,table.pyhltable td:not(.code){color:#999;padding-left:0;padding-right:.5em;border-right:1px solid #ddddd8}
pre.pygments .lineno{display:inline-block;margin-right:.25em}
table.pyhltable .linenodiv{background:none!important;padding-right:0!important}
.quoteblock{margin:0 1em 1.25em 1.5em;display:table}
.quoteblock>.title{margin-left:-1.5em;margin-bottom:.75em}
.quoteblock blockquote,.quoteblock blockquote p{color:rgba(0,0,0,.85);font-size:1.15rem;line-height:1.75;word-spacing:.1em;letter-spacing:0;font-style:italic;text-align:justify}
.quoteblock blockquote{margin:0;padding:0;border:0}
.quoteblock blockquote:before{content:"\201c";float:left;font-size:2.75em;font-weight:bold;line-height:.6em;margin-left:-.6em;color:#7a2518;text-shadow:0 1px 2px rgba(0,0,0,.1)}
.quoteblock blockquote>.paragraph:last-child p{margin-bottom:0}
.quoteblock .attribution{margin-top:.5em;margin-right:.5ex;text-align:right}
.quoteblock .quoteblock{margin-left:0;margin-right:0;padding:.5em 0;border-left:3px solid rgba(0,0,0,.6)}
.quoteblock .quoteblock blockquote{padding:0 0 0 .75em}
.quoteblock .quoteblock blockquote:before{display:none}
.verseblock{margin:0 1em 1.25em 1em}
.verseblock pre{font-family:"Open Sans","DejaVu Sans",sans;font-size:1.15rem;color:rgba(0,0,0,.85);font-weight:300;text-rendering:optimizeLegibility}
.verseblock pre strong{font-weight:400}
.verseblock .attribution{margin-top:1.25rem;margin-left:.5ex}
.quoteblock .attribution,.verseblock .attribution{font-size:.9375em;line-height:1.45;font-style:italic}
.quoteblock .attribution br,.verseblock .attribution br{display:none}
.quoteblock .attribution cite,.verseblock .attribution cite{display:block;letter-spacing:-.025em;color:rgba(0,0,0,.6)}
.quoteblock.abstract{margin:0 0 1.25em 0;display:block}
.quoteblock.abstract blockquote,.quoteblock.abstract blockquote p{text-align:left;word-spacing:0}
.quoteblock.abstract blockquote:before,.quoteblock.abstract blockquote p:first-of-type:before{display:none}
.admonitionblock td.icon [class^="fa icon-"]{font-size:2.5em;text-shadow:1px 1px 2px rgba(0,0,0,.5);cursor:default}
.admonitionblock td.icon .icon-note:before{content:"\f19c";color:#19407c}
.admonitionblock td.icon .icon-tip:before{content:"\f0eb";text-shadow:1px 1px 2px rgba(155,155,0,.8);color:#111}
.admonitionblock td.icon .icon-warning:before{content:"\f11c";color:#00b200}
.admonitionblock td.icon .icon-caution:before{content:"\f134";color:#bf3400}
.admonitionblock td.icon .icon-important:before{content:"\f071";color:#bf0000}
</style>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.6.3/css/font-awesome.min.css">
<style>
.listingblock .pygments .hll { background-color: #ffffcc }
.listingblock .pygments, .listingblock .pygments code { background: #f8f8f8; }
.listingblock .pygments .tok-c { color: #408080; font-style: italic } /* Comment */
.listingblock .pygments .tok-err { border: 1px solid #FF0000 } /* Error */
.listingblock .pygments .tok-k { color: #008000; font-weight: bold } /* Keyword */
.listingblock .pygments .tok-o { color: #666666 } /* Operator */
.listingblock .pygments .tok-ch { color: #408080; font-style: italic } /* Comment.Hashbang */
.listingblock .pygments .tok-cm { color: #408080; font-style: italic } /* Comment.Multiline */
.listingblock .pygments .tok-cp { color: #BC7A00 } /* Comment.Preproc */
.listingblock .pygments .tok-cpf { color: #408080; font-style: italic } /* Comment.PreprocFile */
.listingblock .pygments .tok-c1 { color: #408080; font-style: italic } /* Comment.Single */
.listingblock .pygments .tok-cs { color: #408080; font-style: italic } /* Comment.Special */
.listingblock .pygments .tok-gd { color: #A00000 } /* Generic.Deleted */
.listingblock .pygments .tok-ge { font-style: italic } /* Generic.Emph */
.listingblock .pygments .tok-gr { color: #FF0000 } /* Generic.Error */
.listingblock .pygments .tok-gh { color: #000080; font-weight: bold } /* Generic.Heading */
.listingblock .pygments .tok-gi { color: #00A000 } /* Generic.Inserted */
.listingblock .pygments .tok-go { color: #888888 } /* Generic.Output */
.listingblock .pygments .tok-gp { color: #000080; font-weight: bold } /* Generic.Prompt */
.listingblock .pygments .tok-gs { font-weight: bold } /* Generic.Strong */
.listingblock .pygments .tok-gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.listingblock .pygments .tok-gt { color: #0044DD } /* Generic.Traceback */
.listingblock .pygments .tok-kc { color: #008000; font-weight: bold } /* Keyword.Constant */
.listingblock .pygments .tok-kd { color: #008000; font-weight: bold } /* Keyword.Declaration */
.listingblock .pygments .tok-kn { color: #008000; font-weight: bold } /* Keyword.Namespace */
.listingblock .pygments .tok-kp { color: #008000 } /* Keyword.Pseudo */
.listingblock .pygments .tok-kr { color: #008000; font-weight: bold } /* Keyword.Reserved */
.listingblock .pygments .tok-kt { color: #B00040 } /* Keyword.Type */
.listingblock .pygments .tok-m { color: #666666 } /* Literal.Number */
.listingblock .pygments .tok-s { color: #BA2121 } /* Literal.String */
.listingblock .pygments .tok-na { color: #7D9029 } /* Name.Attribute */
.listingblock .pygments .tok-nb { color: #008000 } /* Name.Builtin */
.listingblock .pygments .tok-nc { color: #0000FF; font-weight: bold } /* Name.Class */
.listingblock .pygments .tok-no { color: #880000 } /* Name.Constant */
.listingblock .pygments .tok-nd { color: #AA22FF } /* Name.Decorator */
.listingblock .pygments .tok-ni { color: #999999; font-weight: bold } /* Name.Entity */
.listingblock .pygments .tok-ne { color: #D2413A; font-weight: bold } /* Name.Exception */
.listingblock .pygments .tok-nf { color: #0000FF } /* Name.Function */
.listingblock .pygments .tok-nl { color: #A0A000 } /* Name.Label */
.listingblock .pygments .tok-nn { color: #0000FF; font-weight: bold } /* Name.Namespace */
.listingblock .pygments .tok-nt { color: #008000; font-weight: bold } /* Name.Tag */
.listingblock .pygments .tok-nv { color: #19177C } /* Name.Variable */
.listingblock .pygments .tok-ow { color: #AA22FF; font-weight: bold } /* Operator.Word */
.listingblock .pygments .tok-w { color: #bbbbbb } /* Text.Whitespace */
.listingblock .pygments .tok-mb { color: #666666 } /* Literal.Number.Bin */
.listingblock .pygments .tok-mf { color: #666666 } /* Literal.Number.Float */
.listingblock .pygments .tok-mh { color: #666666 } /* Literal.Number.Hex */
.listingblock .pygments .tok-mi { color: #666666 } /* Literal.Number.Integer */
.listingblock .pygments .tok-mo { color: #666666 } /* Literal.Number.Oct */
.listingblock .pygments .tok-sa { color: #BA2121 } /* Literal.String.Affix */
.listingblock .pygments .tok-sb { color: #BA2121 } /* Literal.String.Backtick */
.listingblock .pygments .tok-sc { color: #BA2121 } /* Literal.String.Char */
.listingblock .pygments .tok-dl { color: #BA2121 } /* Literal.String.Delimiter */
.listingblock .pygments .tok-sd { color: #BA2121; font-style: italic } /* Literal.String.Doc */
.listingblock .pygments .tok-s2 { color: #BA2121 } /* Literal.String.Double */
.listingblock .pygments .tok-se { color: #BB6622; font-weight: bold } /* Literal.String.Escape */
.listingblock .pygments .tok-sh { color: #BA2121 } /* Literal.String.Heredoc */
.listingblock .pygments .tok-si { color: #BB6688; font-weight: bold } /* Literal.String.Interpol */
.listingblock .pygments .tok-sx { color: #008000 } /* Literal.String.Other */
.listingblock .pygments .tok-sr { color: #BB6688 } /* Literal.String.Regex */
.listingblock .pygments .tok-s1 { color: #BA2121 } /* Literal.String.Single */
.listingblock .pygments .tok-ss { color: #19177C } /* Literal.String.Symbol */
.listingblock .pygments .tok-bp { color: #008000 } /* Name.Builtin.Pseudo */
.listingblock .pygments .tok-fm { color: #0000FF } /* Name.Function.Magic */
.listingblock .pygments .tok-vc { color: #19177C } /* Name.Variable.Class */
.listingblock .pygments .tok-vg { color: #19177C } /* Name.Variable.Global */
.listingblock .pygments .tok-vi { color: #19177C } /* Name.Variable.Instance */
.listingblock .pygments .tok-vm { color: #19177C } /* Name.Variable.Magic */
.listingblock .pygments .tok-il { color: #666666 } /* Literal.Number.Integer.Long */
</style>
<div class="paragraph">
<p>Since about October last year, I&#8217;ve been writing an introduction to R book. It&#8217;s
been quite the experience. I&#8217;ve finally started making time to document some of
the interesting things I&#8217;ve learned (about R, about writing, about about how to
bring those two together) along the way.</p>
</div>
<div class="paragraph">
<p>The book is aimed at proper beginners; people with absolutely no formal coding
experience. This tends to mean people coming from Excel who need to do more than
a spreadsheet can/should.</p>
</div>
<div class="imageblock" style="text-align: center">
<div class="content">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAmcAAAFiCAIAAAA89ehoAAAAA3NCSVQICAjb4U/gAAAAGXRFWHRTb2Z0d2FyZQBnbm9tZS1zY3JlZW5zaG907wO/PgAAIABJREFUeJzs3XV4FFfXAPAzsr6bjWyyG3chQtDgrsXdoUCBUipQ6sJHixRavBTX4l6kBYprcLcEiLsn67uzM/P9MbBvugnJBkIC7f09ffqQu3funNEzcmcGY1kWEARBEASxA17bASAIgiDIWwNlTQRBEASxF8qaCIIgCGIvlDURBEEQxF4oayIIgiCIvVDWRBAEQRB7oayJIAiCIPZCWRNBEARB7IWyJoIgCILYC2VNBEEQBLEXypoIgiAIYi+UNREEQRDEXihrIgiCIIi9UNZEEARBEHuhrIkgCIIg9kJZE0EQBEHshbImgiAIgtgLZU0EQRAEsRfKmgiCIAhiL5Q1EQRBEMReKGsiCIIgiL1Q1kQQBEEQe6GsiSAIgiD2Ims7gEqYTaZ7d25euxSbnZmRk5efm52Tm5cNgClVSjc3N4VC4ePrV79RTFR0A75AUNvBIgiCIP9yGMuytR1DOXKys04cPXzh7Jn4h/e0Wq1UKjboDTRNA2AMsAA4BgA40DQNDIvjuIAviGncvGXbtm26dlEo3Go7fARBEOTf6Y3LmiXFxetX/rZz62bKbGZYViAUMjTt6emZlp5KsDQAAOAMBgA4zbI4TmA4QdM0sCyJEQIBacItw0eOHTP6fQdHx9qdEARBEOTf5w3KmkaDYe/2zetXLjMY9CKRWCQSFhaVGE0mnkDg7OySnZPFAwYDFgADABbDaZYBIFjAAMP4fIFIJJBJxVm5BXIHRxcH2aDBQ7sPGCQUi2t7shAEQZB/jzcla6anJs/+/ouU1NSCnFyGpnEMI3kEy4LRZMZIkuTzzWYLjmE4sAAsxgIGQBK4WCTGSVyn0xkMBgZjaBYwVkzypaQI9/FS+Hq6fTl9npvKo7YnDkEQBPmXeCP60N6+ff2Hbyffv3fPYDDgBG7Ua0U8vCQvV52fx5iMJMOwlBlnGQsNLManKFbA59NGo0Wv1eVn63IzJZipXpBXv+4d/b09gbKQGEkzOENijxMefjdl9O27d14xvO49+7iqPK3/nTx1ulqmulKpqWm/zFtw7/597s+LF2O5AC5fuVozAQCATq9fvmJltx69g0LDVZ4+YRFRQ4aNOPTnXzUWgJXN5NfK3EAQBKn9PrQ7t2zfvmklZTRhLPYkLs7f28fTzXXD6lUZqSlPE54mJ6c+SUpKz87KyisoMoBMIgGL2czSbZs1jaoT7O7qqHJzcZRLBQKehcc/fvxTEYlpiosYIWYxSlkTpcvJm/HFFyMmf9GvW6fantAq271377wFC729vaIiI2slgNTUtEFDhiUkJlpLCgoKT546ffLU6ffGjpn706xaiQpBEKQW1XLW/OvkhR1rN8sI3qPUZEJIEjh8/unHDny+s1TIOjsopBHN6kXxhIL8kpIfZs5Jy9dqNBoHkahD86ZTJ0006Ur4OM0yZgxnGZP+cdzDAE+Xnj2GHjt76erd24nxTzwdJNkFOX6hqjnfzHZz9WrZuM7LBbll0wYzRZ07d37SR59U7+RX7MiRozU5Ohssy457fyKXMkeNHDFi2FAXF5eExMQlS3+7eDF23foNDRvUHzigfy1GiCAIUvNq8wptQlr2Z999x+AmM2USiIQms8lBIklOTGjXvg2t12OUUYIzDjxg9WqVXDzt84/6dGoZ4uHywYhBLaLrkJSBx5gxmsIYhgAMGDbU13/F/HmN6kfEPbxDGbVCvkBtMIFQojHqZXxs29b9afn6l4vTyclJ6eYmd3CwKWcYZsPG3zt27uobEOTtF9imXcdly1dQFMX9evLUae4SYn5+wa9Ll9Wt38jTx79PvwGpqWnWFtLTMz797PPwyGgPb79GMc2+nzZdrVZbh71z9x4AfDJlqqvK81FcnHUoHMeq2qCd8ZR29tz5W7duA8DI4cMWzPu5fv16Pj7e7dq22b1jW8MGDVQqVWZmlv0jTU1NGzh4qLdf4M2bt8otrHR+IgiCvAlq7VyzxGDuMXi0Ji1JFBHwKDuZAQInoF3bNu907gwWijLqpDySpYwEAA00WEyuMsn4YX0j/dwbRtXDGIY1agkLRfJIBiNYDGdZHGPBoi5WObnNnT19yv9NMwFrwUktRcsdRTJc/Dgjbn+6bpRMIBcQ1TUJH0/+dNfuPQDg6+ND8ngPHz36YcasK1evbdq4HgCEz9+6sHDx4jVr1wsEArPZfDH20uBhw2PPn8UwrKioqGefvunpGR4eHu3btbtw8eKqNWsTEhO3b92scHFp2bLFhQsXASAsLNRdpZJKpIUFhVyDW7Zu375jJ4/HoyjKzgbticdm6k6ePPVsMj/+sHQ5j8fbu3uHRCLh/qx4pAI+n6s2b8HCM2fPAYCZosotrHR+IgiCvAlq51zTaGE2XE3pM2aip48vizMimdDCJ9QlmvzkDB83d8pgphjQGUwsy6NNmIAQ4xZSxJeAiWrRsIGYh8skIhwDkiekMSHF8BkLn8SkQr7YYjETuMXNzUmj0WbnlxgowEmeVq+7+/CeWOqgKdCuv5JB0dXTZ/jU6TPcLv7Lzz+7fvXS5Yvnpn33LQAcOfr34X9eWT1y9O/LseeTEx4PGTwIAJ4+TeDO4U6dPmOx0CqVat/uHVs2bVg4fx4AnDh56lFcXHR03bWrVnKDT5r4/q4d27y9vawNnj13Pvb82eSEx4MGDuAavH37TsUN2hOPDe7arEQi8ffzs/nJmjIrHak1GR8/cWLdmlUXz52JCK9TbqH98xNBEKQW1U7WPJdUnKPFXdz91GaWxsCJJzTqdDTLpqenG41GUio2mcxiiQzDCJYlKAvDMCwARuAkDjgA0LSFwcHAMhYccIEAwzEeDjjO0LiFonS0Wd+3d1+aIkSkGDOaGL3ex9M7MCCUKlEXqY03M7TVMgkHDh4CALFY9PFHk7iS9yeME4tFAGCzl58wflxgQABJkuPHvceVpKSmAkD/fn3v3b5x7/YNNze3nNxcV1cX7teMjMyKR/3+hHHBwUF8Pn/C+HEv0eCL4rGh1+sBwNnZqeJg7Bzp2NGje/XsERISLJPJyi20f34iCILUolq4Qqs1M1eyKYFIlHT/Ps5iYkJkoYvdhXKjRCbzcsk2FPILzRKw0Do1RgDLZ1mMIXFgLAyLOQFGAk5hGM3gNGAWhjBaWArDLQxQLM3DWCllMAT5eKucHDycHTDKIOLzwGJ2cpWdv3L+nc4d+Vrm2OFL0WPaCwWvOuEJCQkA4OHhIRQKuRKBQODu7pGQkJCcnFy6ZnidZ72QVCol9w+j0QgAZrN51uw523fuKi4uLl2foemKRx0RHs79w91dxf3DYDDY3+CL4rHBpbe8vPyKg7FzpPWi65YdtnSh/fMTQRCkFtXCueapdG0xw2JiYXpBbnZBUUJSKm2iqRI1z2CY9+03IUqVuajYqDfy5c4lLE+DSUy4nAUHlpbQLG5iKYwgzGYLwRIMhdFmnA8yES7ngQMGYooGvUYPUsnN2Fg+a8YtJsZslEnEGFiKMrJMlx4m3LzD83Z9mFpkf7R0mRxW+hYgy/zjei/LMACA4/+Yq4LnNxQJ/B+3VP/vhxkrVq3W6XTff/vN1s2/z/t5jp0hvWKDLxrcRp2wMAAwGo0PHj60+enho0dc/x37R+ogl9tTaM/8RBAEqUU1vT/SmJkLOSZGKNBaTJGN67ft8Q4rkRAyKS7kOwvFQq0RKBMhFT0pzN9w8PAfZ67uPnpp9+HYP8/dT8zVW4AlcABgcZJPAXntTvzOg6d+2/jHnFU7f9t29OiFu0mpOTxSYM7I+GTS++1btyIAJCKhSCymGVwudZDTvHpeIQU5RauOxWqNlfTMzMrK6tKtR1Bo+MJFS7iS3OdnXY5yOQD4+/sDQEZmpsHw7ETNYDBmZmUBQGBggD2zYv+BAwDQ7Z2ukz/5qHOnjh4er/oOo+ptsNs7Xbl/WOcAx2QyfTJlapduPQYOHlqNI331+YkgCFIDavoK7aMCo5kBBiw8nHZ0lt28f7uev48hNzNPUzztixm+7j4sgR89eWL67F9NFtxgYXks0BiQONYoKnjW91OcpSKGZjCA3Jy8vw4dvnDjkZFmCYI0MbQYx/jAThrbf8L74+tGROzcfwTHCaW7l4Fickvy/MObmkQiXX6xp6+vs5PwTrGxhYpXQZxKpTIzM6ukpGTdhg3NmjaROTisWrMGACQSSXh4HQDo3avnjp27jEbjb8uXf/HZVABY+tsy7lJnn9697ZkVJMkDAO4hDYqiVq1ey5VrdXoAIMlnJ4IZmZXc5rSzwaqqVy+6S+fOfx87dvDQn+Pf/+C9sWPc3FwTE5MWL/n1zp278Hwyq2ukrz4/EQRBakBNZ82EHKMjxtOb9HLCLGMN4b7e+vx0BwdHF2fnjNw8E8krzsrMS8lcPO1ryowXq80UzQjFpFFfEBEZ6CiXsgyNsyzBsJ6O8mlTpty5/xQjRDQLForiOUhMOFOY/rioWCNxkyalpokdHEmhpCA9y9nVAyMxWbC/iRQbAMeMTHKupYWqojhxHP/6yy+mTP2soKCw74BB1vLPPp3C3Xjr2KH9gP799uzd98u8BXv37actluSUFAAYMXxom9at7JkV7du13b5j5+kzZwcOHpqamqZQKBo0qH/z5q3Zc+aUlBSPGf2ui4tzQUHhwkVLTpw49cP0aa/YYEhwsD1Rlfbbr4uGjXj32vXr+w8c3H/gYOmfPvpw0vBhQ6pxpK8+PxEEQWpAjWZNk5m+fSsRd3AS8RkRXbTut1k5j26LMSY6MiwsICgpJ0MvF4p5iomfT7l05cafpy9qMFFcYpqbowjT5JdQukEqpYgkGIZmSV6+1nD58dOT9+5SIlmxyaz08ebnZ0UqXHr16g0kbjQa07NyxC6uJgubnpYmN5tptck7L9PJK4jGMLOIf9/I0iwQts8o/sPwYUOcnByXLV/5+MkTvV4fGhIyYfx73NManGVLlzRq2GDrth1Pnj7FMKhfv96oESO4XGKPH6dPMxqNp06fuXX7TpfOnX6aNePqteuTp0zNycktKCwEgEUL5n/z3fc5Obk5uTlCgUBnsbxig1Xl6Oh46MC+bTt27t33x8OHj9RqtVzu0LBBg7FjRnfs0L7aR/qK8xNBEKQG1Og3T+4+yd1yPtVCkM5iuHN0W4CUDvNyS09Ni718GVjK3ct18aJfcJNOSBKZJVqHgKg7WSVfTZ/dpVnT93t3O7h6aYtIXx+Vi8VCsTgvKbfoSYGGdXJ3C607d9mKZh06TB0yIP/qWSee2VEmztaYOvUe6h8WqdcWh4UENW/e/HF28cbLSZO+nYEBWLQGS2HJyPahwX6KGpt2BEEQ5F+gRnsDaUmho4+H0EVG8JiCnBRTUVZJTpqfj2fDxo3iE5+mJaTyDUYBRRG0mWDZq7EXnYWSPu271AsIuX7mrK9KZaIsDE7gGIkDYCZzgKub2EThhYUdo+p2iohKuXe3IC9D5iDCWEqn12TmFRUVF6WnJjeuF5kcf1dAaUl1fkniQ0PKU0tqAp6VkZORW5PTjiAIgvwL1GjWzDMZNaSF7yQROUtNrIEU4X4B3udjzwAfL7GwRQYTAxgQOGOhHHmYB2vOjz1bX0g7Fae44UVCvFAsk7CEgMEwPoGJMAtbmCUsSacTbzVyZKgHZ/VJt10dxThtIvgYZdA5y6Xx8fGRdYIe37vtr1I5CcFNApg6V8KjBR6OUC8gX+5Yk9OOIAiC/AvUaNYsKlYLaROjL8FwwEUyb//g4ADfj8aOKMnP1luY+LT0CzfuAF/CAN+s1igEWAMfh4Y+0kYBLnyzRoyBg4jPshYaw00sQRN8M834enr4qVzqB/k0CvIJUMhJk4GiDHqzGhMLizVamqIUUrZd45ieHbr5eKgYjC/z8uP5+Jrd3Y0uLplQUR9aBEEQ5O1ipiwXr99lmPJvO+oNxtgb9159LDWaNXXxWfjTLEjLM6TmOuCSMN8QPo0d3L6NUhcH+3oqnBz3/bGHZUGrVpsMBiGBWYwaAqMpk0EqllAUTeIY0BaCwAHHMAwwYCVivsrNGSxGzGIkaJOIz9cXUwKe4ObNa35Boa5Kpc5Mn4u9lJKSERgYklZoosSqYkakZyUWVqIxo6yJIAjy76HV6bcfOLZ2x4GyiVNvMC5cu/3QifMvyqn2I3744YdXbMJ+V+KKWKGIIfkikciiLS5IfSIlmOyMtDoREclpGU0aRHspnEL9fBizTkDgNEXhOAE4jhOkiaKKSkriH8f7eHsTOG42ma9dveKqcHFVOBMEMAxFW0wCvgDDBBhFiKSC1JwCF89AvQkbPWJEckpCYWFhnoGOM4qjW7YHnOTRQOopgdnSIsD2418IgiDIW0okFAT5eR08fj4jJ7deRCj+/D1uXMrU6vSfTRguFYtecSw1eq5ZEOSa5e2sD/bMdpR4tW61+9K1/bFXHmflCsSiru1bJz9+lJeVidEW2mAEC80nSJwgTGaLhcVEDo73HsUHBgXz+UKaZmUyqbOzy6O4hziO0zTFIwmSJBiaxiwsibEmNatXG1ITH+CsxdM7JD0v+/TtS7uPXmrbrrWpJNeclQZpScK0JGFyQk1OO4IgCPK6hQT4fDJm0N1HCet2HKAZBriUuWYblzJdnauhO0uNnmvezKI0JpzG+RSLiyRChjXnZKfzRfzMzCyJSEoZjeFBAeqC/AAfTz6JszRrttASmaOJttx98CAoJMzfP4CmWQvNsoB7envn5ucDDjK53MLSLLAAJE4Dw9Dp2Xl3Hj4ICPaLu3v9we1YR5WLzCs4DxT1m3YEiiVpTIgTEpHEWS6qG6qssWlHEARBaoCLkzzIz+vg8QuZObkh/r6L123X6g3VlTKhhrPmkyxKY+bRDMHwSRMwvgG+iU8TcIadPO7jmMiYW1euDhk26OnjOKNe6+ggAwAaI0w0jfMFjxMTTWYqKTnVYDSZafbG7btavb6wuETu5OLo4myiaIFEZDGbGAuVmV10/f5llbcnn+SbtOkdO4bl6cm/bhR0n/gZLpKDQMQKBSY+X83DJS6Shj6VfAYLQRAEeetYE+ep2GsAUI0pE2o4az4tpLJ1DAsYDRiwLINDeFTUzXuPDhw5nlGsO3fxfHhoQFhoSHFRQXFxkclsysjJFUkc9CajSCQ+d/58/OMEg9HME0ruPnhwIfYKXygKi4w0WWiBWJyckp6aloyxTHxCemRMHYFUvnDRSgwraNet3rGr2QMmLytycGB4fAuBUSRhEQtomdjTTRrtbNcFbppmrt15uP3gsV1/njh27sq5K7dyC4q83ZVCAf91zzHOzkPHL1y706hunVsPHv+ycnPXNk0rrVkzgSEIgryZuMRZUFTy/oh+1ZgyoYbfqMcTMWbCRLCkxIIDYAQhNAHbYeR4g7pYpy0RJjwwYHxc4iBwcATKqFC558U9PX/xws07d+WOjkVFRQwDYpnUP8A/KTlFbzAlpaRu/H2zVCoJDPQXCHgeKueM/HxXT1cKI1i+5H5yZsvevVP1ZIfBo3KANOFSAAsfZwmWxYGlLKwDUdF3sqw0Ov2y3/conOUDu3fwUrmRJFGi0V24dvun3zZOHjvYU+X6umdalbRr3shiqeTznAiCIP8FIQE+IQE+1d5sjWZNH0fycraRb8J4RhYohqItDB9Ivkgqkzo6+5oatTl17ZqXt7vUVVWSnfokOY0UCnQG/fjx4/Lz8x0d5RhGOModMQzr2qUDjhG5ebkGg0EqlRQU5pUUF2GEoMhgjA52yypUp2sLxYFBrjE9U2kTy1eqab1FL8JNZh7D8DHgYRjgbHBQ5U+e0DSzZP3Otk0btGwcbS2UyyTd27fwVLmu2b5/+pTxWIUvs61hbi7omjOCIMhrVKNZs45MIH701GRiTECYBXxaKnFUeqpNZrFQotWZvAPCf/11VrfOHaiCLKVMxhh16SmpXt7eGAY6nTbh6ZPc3Gw+ybPQjFgk4ZF8mUwmkUpcnAMJlgWaETvIvMTBSck57r6+f1w+1aTHMK1LTKFJ6+CowNQs32S2ULl6o5bSGPh6g5CxBHXsVWnAx85d9vNyb9k4uqhEs37XobTMHBdHh/7d2q/csm/JD1OPnbvyNDkt2N8bAO7FJew7ejo3v8jdzWVgj46hAT4AcPnm/cOnY/OLih2kkk6tmnRo0QgAdv15Qm8w6gzGxNSMBd9Pnvnr+sbR4bHX73ooXSeO6Ps4MXXP4VNZufkCPr9Zw6i+XdrieBXS8s5Dx4tKNBNH9AOAcpva/ddJrc4glYgePU3WaPXNGkb169oWAMyUZe/hU7cfPtbqDD6eysE9O/l5ub/UQkYQBPk3q9GsKeCTPm6KJI1Z5CAjpFKTSFBstvAkEpPBTEj4Ep7XyMnf/rbtQO+2MR7eSp6+SGd6qk5LDw+PjGnSgmFok0FtMhgInkCnM/h6+eIEwVJmrVadnJBktjBZKel+vl6EVHo3IelGem73fh+UYCKTQJSjJSSkWISxlMQZp8U8RzOp0fvLBXx+JdPOsnDu6u2vJ40ymamfV2zq1Cpm6rhhOfkFi9ft8Pf2wDCsTpB/SkZ2sL93fmHxyi37RvXvVrdO0OVb93/buHvOVx9o9Yb1uw59+O6AiJCAxJSMRWu3B/p6+nm5kwRxLz6he/sWo/p1AwCSIC5cvT2i3zu+nqpitWbxuh1DenVq3qhuVm7Br+t3OkglnVrFvMSsflFTBI7fuBc3YVifgd07ZOXm/7BoTUx0uJe7257DJxNTMr76YJRUIj5w7OzSjbvmfPUhn1fTH5JDEAR5w9Xo85oAENEwhPLx1jg5aPm8Ir2Jh5N8Ey3HSZbS5ZsYeZ1WTfuP+37Z1u3HYw0CB7mbOykQZGZmmgwmHsaLPX9h65Ztvy1dfuL4aYqy6NTFWnXxvfv3KQy7fPuut08oRQn2nzn/9codzUZ8qperGJyWiiU8npxihRYLwxAyA89ZK3XTqfwCIiv/7mNaVo6DVCKXSc9cuqFUOHdo0RjDQOXq4uvpHujrBQACPs9C0wBw7c5DT5Vrk/oRIqGgXbOGw/t0oRnWzcV53ncfR9cJJgkiJMBH6eqckp7FtSzk89s3bySTirk/g/19wgJ9RULB5Zv3VW4urZvUJwnC292tZePoa3cevtx8rqApN4VT3TpBAODuppDLpFm5BSwLF6/d7d6hpbOjA59H9unSRm8wxiekvNyoEQRB/sVq+mQi2FVAJDKAsUYwSwV8XGNkjCa9hXLAMLPUkVJ58xXu01bvOPL7smlLNwzt3JJmWbNJe+/KKYWTU4iPf0RwhJmyMMA+ffxQoXAsVBenF+UWW+jgZo2PZxRu+uuKa0DkmOVLjDKXAqPRGUrAWIQTUhoT0kICLCwJgAHO4lDHTVhpqPmFxW4KJwB4mpJet87/smxuQWGrmGgAKFZr/L09ACC3oFhRqo9W0waR3D8u37x/8fpdrd6AYaDTG6jn/XRc/3n30c3l2bB5hcXubv/7eJmbwun0paKXms0VNcU91cPhkSRlodRaLWWxeCgV1kJHB1le4UuOGkEQ5F+sprOmAx9v6S26kqKVqI2Gojyj2Sx2lhMkBhZaxMc1RjWL0SzO7zv+k/T7VxeuWOglxiLrN3nyJFHP4NnZqfXqN7x69XpwSKCPt/udRw9v3r/LiKUSd+9rtx7ezLs17PM5QoGUJnBGq3Ek+XwKxFKnAoMJFzAW2kwwOImRGI618RbIeJWfZBuMRpFAAAA6vVEifpZlE1LSM7LzvNzdAODB46QOLRoDAI6X85nSc1duHTlzafLYwVxmnblknfUngvjH2InnvXnLdn/FXravUQVNlW2y3G63GLxJ3ZwQBEHeDDV9hRYAWns6WBKS9ZlZjiw4S4R6Rq+T4novuY7QK/gmAZhInCyhcI86jT+YNt/k4PXt/NUawiFDS0u9/O+lZXiHR1y79yAxM+tRYgoI5QVa2L7/jNA15P0p32IEzQOtQJ/hYsp1pIrFOF5UUIJjOGsxsRYDgQEAIyLoll52PabpIJUWlWgAwNdTeffRU4Zhk9OzTsXe4JEkQRB/n73soVS4OMkBQOHsmJWbbx3w2LkrOfmFCSkZ4cH+XMrUG4w5+YWVjtHVxTEzJ8/6Z3ZuwUv3ia1SU44OMpIkMrKf1TeazMVqjSvqjosgCFJGLXT3EPCIEe3qHbqcmJie7BkWJJSJtWJhgdl099y5+2fOanIKQCQDCwDQPJZi85N/+Gj0vjWLZSTWoGkThZtrRnZ6ibbk5u1bySmpiZn5oY3aPknVPMo+u3vXKVDIoLgIhGIws+CiGjx6fMNmLbMK8uVOMsAJjV4jEIrb+jkJCLvOogJ9PTfsOmQ0mbt3aLlpz+Hv5q3w93Yf2quLVCyauWR9sL/3qP7duJpN60cePH7uVOz1mOjwm/fjD5240KxBlIuT/Ma9OIPRZDJTu/487iR3KFZrKh5jTL2Iv05dvHDtTrOGUelZueev3endqdXLzeQqNUUQeEx0xOHTsQE+nmKRYN/R03KZNCzI9+VGjSAI8i9WO50k/X2ligekJjpUJyVxGvJvxu9duIoQSQgXuZOvB8PiDGXBgRJTxXlPrzUIdO//66wrJ4+k5hYbMjQEyzgSFhFYmjesP35SO9I1YPORq0r/OqyzyiSUsAQfcBIYGoy63Zu2P7xypf+o4fr0DJmLq1wkchHQMe6V39HkiEXCBlFhe4+cHt6ny6RR/a3lQ3t3HtC9PcMwAv6zdwM5yWVTxg7Zuv/vPYdPubspPnp3gEwqbt+i0dPktC9mL3WSywb26BAerNtx8JiDVFLBGN1cnD4Y0f/g8XM7Dx13dJB1b9+idZMGLzeHq9rUkF6ddhw8NnvpBspiCfT1/GzCcNK+t0AgCIL8p5RzQ65m6MzM8otP8rR6IUbO/PAbt+ZNQCjDKYzBSIzgUQYtrclxBW3Sqd07lk5vF6rimUs0RQa1RgcAIgcxi+NCZ7cSTLR4y6H1e44rG7bFnPxLWBmI5TSJwbB/AAAgAElEQVRjwgmaz8Mwlsk/d6L9O+27tmudV1js6qP8sG2I2I47mlYms3nJ+p0yibhr22Y+nioAyC8svvPwyanY64N7dqwfEfq65s7L2nnoeFGJduKIvrUdCIIgyL9TrWVNAMhSG7fczl6z+LfMHLU0NEqdX4BpdQyO84QiYCysoURoLoSC5CAHZnz/zjFh/h4SKQ8nLEAbGUuxXheXnH7pYeL15PzLjzIdQxqVmHi4wIXCcNpcwuNjmFjGU/hhlJmJuzJr5tcGdcnw9uGeztKqBknTzLkrt67cfpCbX8gCOMlloQG+LRtHv2nv0gMAM2VZvmmPi5N8ZL93ajsWBEGQf6fafIzd3UHYxlv24/04omETAhMwxWopbqIswFiMGIHxMIYUiXkKdxNJZYPT9LV7+Uatk9yBEPD0egMNrJuXd8seA3d/O0fkrNJqTXKpiDLmkwRJsCacYkrUDOEMEplztlr7MDFhcu/mL5EyAYAg8HbNG7Zr3rDaJ/+lnbhw7dCJ8+X+xOfxenduXcPxIAiC/HfU5rkmZ/XmQz+dScxSW6AoW0qpGWBZjGSABZYhwCTCaUN2WrPI4CmfT6EteqPRQBAEn0c6OjiygM+au+jytYdiZaAZF9GUnk/SBlwGABiOaYAUe9UhSMLy+MK2+VN7NI2q3clEEARB/gVqP2sCwJWEnF7Tfjfn5pC0hmGMDEPiuNjCMhhBg4UW4vyC9OSwAMWM6Z8r5CI+RpM4kZqeO3Per4+TMqVufizOE/CFlNkEwNIYj8UwGmP1JA+8op09fPYND24aGVDbk4ggCIL8G7wRWRMAUnJLRn657H5iIklSGPAtFI8geRSrF5EC2kjzMYtRnY5j5jbNYyLDgh4+eHDh3CUdIRW5eFlwIUOzPJKkKTPGMhhGsMAwGKMjhHWatPrzm77uckFtTxyCIAjyL/GmZE0AMFP02n2nFmzaW6wxYawQA8BJg1lvEALPQcQzU4UUYCWFBbqiPEe5o0LpaQS+kRVRQPKEIqNezycIFiw4EBgwcqnww1E9Jw3oyCdr4TUOCIIgyL/VG5RU+Dxi0uBON3Ys+HBQVzGfx5p17k7ihbO+cncS1PFXvjesvwAsOGVg1cWUXuMkE37x8Xh/lUMdf+XHYwdLSRpjTCxgAgF/8ohu13bOnTKkM0qZCIIgSPV6g841S8vIKTwReycwzC8i1O/WjSc+HkqlUvrRJ59vXreeBQYo8+jx7y9aPD85s0gklTg7Sw8cOn0u9mqTxvX7tY9xd3WsfAQIgiAIUnVvaNYsjQVgGDCZDd98/c3xY8fS0tIIgKZNm2zastnVVcVggL/0O84RBEEQpCregqyJIAiCIG8IdOcPQRAEQeyFsiaCIAiC2AtlTQRBEASxF8qaCIIgCGIvlDURBEEQxF4oayIIgiCIvVDWRBAEQRB7oayJIAiCIPZCWRNBEARB7IWyJoIgCILYC2VNBEEQBLEXypoIgiAIYi+UNREEQRDEXihrIgiCIIi9UNZEEARBEHuhrIkgCIIg9kJZE0EQBEHshbImgiAIgtgLZU0EQRAEsRfKmtUmIDjMVeW5dt2GaqyJVGzl6jWuKs+A4LDaDqR6Irl7737/gUP8AoLdvXyHDBtRXbG9ge7dv++q8nRVed67f7/Sytz2snL1mhoIrALWmB/FxdVuJLVIp9e3adfRVeW5es261z2uN2frtlHTWdNisXBr3k9zfrYW7t33B1dIUVQNx4PUpBmzZnMLuux/7l6+dSLr9h84ZM3a9VqttrYjrQU6nW7g4CHnzp/X6fUkSarVmtqOCEFsTZ4y9eGjR3379J4w/r3ajqXWkLUdAACAWCwGAD6fz+PxajuWl/fr4oVmMxUdHVW6sFuP3nHx8YlP4iqt+R9nsVjy8wvOnT9/7vz5ZStWbNm0MTIioraDqlE3b90qLCwCgHk/z3l31EgMw2o7IuQffLy9V61YDgCeHh61HUvt2LN334GDh9xcXX+eM7u2Y6lNb1DWlEgktR3IK+nRvZtNiclkunP3rkAgqLTmfwqO4w/v3bEpLFGXpKen/3X46O+bNmdkZA4ZOuJy7HmpVForEdaKvLx87h8DBw5AKfMNJJfL+/XtXdtR1BqtVjtt+g8A8O03Xzs5OdV2OLXpDcmaIgCQSt/urFnW7Tt3zWZz2ayJuLg4ly0J8Pdv3apVvei6n0yZmpObu3X7jvfHj6uV8GoFTdPcPwR8fu1GgiBlLV+xKj+/IDAgYMjggbUdSy17I3oDcWeZUsn/TixWr1nnqvJs274TAFy/cWPw0OFhEVF+AcEdOnXZvWcvVycxKWnSR59EN2js4e3XKKbZ7DlzzWZzxSN6b/z7rirPd8fYXpHfvHUbd3ft902bbX766JMprirP0WPHAcDde8+6A2i12vMXLrTv2MXbL/CXeQu4mqX7+OTk5rqqPHv06gMAGo2GG+q7af9Xtibn3THvWSucO39+0JBh4ZHRHt5+DWOafvPd99yFOxsnTp7qP3BIcFiEj39gm3YdV61ZS9P08RMnXVWebu5eLMtWPCs4xcXF8+Yv7NjlHf+gUKWHd1BoeM/efTf+vsm6B7cKCg13VXkePnKUZdlNm7d06totIDjM2y+wTbuOy1esZBjGntHZY8jgQUqlEgAuXbps5yDcmdn1GzdGjR4bEVXPw9uvXsPGn33+ZXZ2dtnKFotl05at/QYMDg2PdPfyDakT2b1nn+UrVur1hnIbP33m7NhxE6LqNfTw9vMPCm3Vtv30H2ZkZWXZGdvFi7Ee3n6uKs8fZ77wotb2HTtdVZ6TPvqE+9Pdy9dV5dmxc9eXiNk/KNRV5fn3sWOpqWlDho3wDwrt07+SfVylg2RkZE7/YUbLNu18/AN9/ANjmrb4/Muvnz5NKLe1p08TPv/y66YtWvv4B6o8fSKi6o0YNebU6TMVx2APDMNMJtOCRYtbtmnnGxDkHxTavWefvfv+KLdylWK2c1MqtzdQlbaLl9jMdXr98pWruvXoHRAc5uHtF1Wv4Zj3xp85e65szYqXY0JCwudfft2sZWsf/0BPH/8GjZsMHjr8j/0Hym7p5TKZTOs3bgSAsWNGEwRR+idudT30519Go3Huz/Oatmjt7RcYEBzWs3ffg4f+tGlnwKAhrirPr7/9HgC279jZpVuPgOAwH//AVm3b/7p02dvSr+UNOde0vUIrFAoAwGAwXLhwcfCwESzLikQinV5/9979SR99wjBMVFRk774DSkpKHB0dKYpKSU1dvGRpZmbWsqVLKhhRm9atDh768+q1azblFy/Gcv+IvXT53VEj//FTbCwAtGvbBgCEz88aHz9+MvLdsTqdDgC4/9vg83gNGtTPzc1NT8/AcbxevWgA8Pb2flFgz6ZXb/h90+bPv/yaIAhnJyeWZVNT09au23Dx4qXjfx8ufc66fMXK6T/OBAAcx729vDKzsr6fNv3s2XN9evcCAIFAYM8lvoSEhN79Bubk5ACASCRUuLjk5edfvnL18pWrh48c3br599K3mYUCQQmAXq//4MOP9+77QygUSqUSjUbz8NGj6T/OfPo0YeGCeZWO0R4Yhrm7q3JycopLSuwchCCIo38fG/PeeIvF4uzsRBBERkbmpi1bjxz9++jhP318/jfbi4uLhwwbeePmTQBwcHAICPAvKCi4eu3a1WvXNm3eunf3Tk/P/92yYln2i6++4Q6kBAKBr6+P0WiMi4uPi4v/fdPmTb+vb92qVcWBPXny9N2x4yiKGjig//99/+2Lqrm4uDRoUL+woDA5JQUAGjSoDwAhwcEvEbNQKNBqtRqNdsx74+7euw8AWk0lvYoqHuTkqdPvjX+fW8k9PDxomk5KTk5KTt6+Y+eypUu49c3qz78OT5g4idv3yWQyoVCUm5f397Fjfx879uUXn33x2dSKI6kYwzD9Bw6+cvWaUCgUi0WFhUXcTLj/4OH0ad+VrlmlmF9xU6rSdlHVzTw5JWXIsJEJCQkA4OTk5OHunpae/udfh//86/DECeNnzvjhH5G8eDmePnN2xKjR3EmFi4uzWCzOzc1LS0s/dfrM9h07bbb0ch0/cbKgoBDH8QH9+9nOAaFQq9UWFRf3Hzjk6rVrOI7L5fKioiJuTzJl8sffffN1qcoiANBoNDNmzV7623JuuvR6fVxc/MzZP506fXr3zu1vQe8WtmZRFKVQeiiUHrN/mlu63GAwmEwm659btm5XKD3CIqIaNm46b8FCnU7PsmxScnLTFq0USo8mzVt16Nx17LgJeXn5LMuWlJS8O+Y9rtnMzMwKxp6UnMxVe/r0aenyqHoN60TUDYuIqlu/Ueny1NQ0rn5ySgrLsgmJidyf49//oF7Dxr9v3nLm7Ll79+9zlf2DQhVKjzVr11sHX7FqtULp4R8UahNG2ZoffPixQunRscs73n4BS39bptVquXkyY9Zsbow7du6yVn78+Imbu5dC6dG3/6DsnByWZWma3rN3n5dvQLsOnRVKDx//wApmglWPXn0USo/AkDqnz5xlGIZlWZ1OP3P2T9wY163fULpy3fqNFEqP7j17h4ZHHj5y1GKxsCybk5s7YNAQrn5KSmqlY/xx5iyF0oM7fn8RmqZDwyMVSo/3P/iw0ga5OewXGFInou6HH0/Ozs5mWZaiqB07d6k8fRRKj2Ej3y1dn1tPfP2D9h84SNM0V3j23LngsAhu6rj5wFm9Zh03aXN/nsetgSzLPk1I6NjlHW6+5ebl2URSelnn5eU3bNxUofQYOHio2WyudFp27d7DjY6iqJeOOTK6Abd+evr4L1i0+NTpM+fPX6h4vBUMkpCY6OsfpFB6DBk2IiMjgyvMysoa+e4YhdJD5ekTH//Y2k5xcbFfYIhC6dGhU5fHj59YKw8ZNoKbroePHlkr3713jyu8e+9epXOG215imrYIi4j6++9j3LqXmprWu98ArpHbt+9YK1cp5iptStaYS09IlbaLKm3mJpOpddsO3ITfuHGTK9TrDXPm/sJV3rxlmz3LkWGY6AaNFEqP/gMHp6Wlc5WNRuO27Tu8/QLKbunlmvTRJwqlR49efV60dJo0axkeGX3y1GluN56amtarTz8uzps3b1krjxg1WqH0aNykuYe335q16zUaDcuyarX6m+++5yov/W2ZtfKL9p+17k3Jmja2bd/BVfvokymly3fs3MWVN2neqvTOxZoODxw8VHEA3I6s9ArH5cKhw0cOHjrcmiA523fsVCg9GsU04/5MSUnlxhIQHJaUnGzT8qtkzQ8/nsy1vGDR4tI1aZqOqtdQofT4ePKn1kJuDfP1DyosLCxdefOWbVwj9mTNzMxMrvLqNetsfurQuatC6dG7b//ShfUaNubqX75ytXT504SEshv8i9iTNTf+volrcOeu3ZU2yM1hhdKjV59+pZMHy7KzfprD/cSlUpZl792/z5X8vnmLTTv7Dxzkfoq9dJkrMZvNYRFRCqXHhImTbCqnp2d4ePsplB7zFiy0icS6rA0GQ9duPbkUwu0cK1Vu1qxSzOzzxeTh7bd33357RlrxIBMnfaRQejRv1ab0ES3LshaLpW37TjYzZ8/efVw8Dx4+LF05Ly/fyzdAofT4Zd4Ca+FLZE2F0uPc+fOlywsLC7kEOfXzL18u5iptSuVmzSptF1XazLkYPLz9EhITbWbIV998p1B6RNVrWHqdf9FytO4bb926bdPOsuUrBgwasmr1WrYyDRo3USg9ZsyaXfYn69KxOT4rKHi2dEpPFJc1FUqPuT/PK12ZYZh3uvdSKD0aNm5qLXxjs+YbcV+zAiNHDCv9Z3h4He4fw4YMJsn/XV728/XluhRlZ+dU3GCb1q0A4MrVq9aSi7GXAKB+vXoN6teHf95Oi710GQDatm1j00jnTh39fH2rPDGV4fF4E8b9454rjuNRUZEAkJmZaS08d/4CAHTs2MGmJ9uwoYNVKpWd43J3d89MS7576/qwYUNsfmrRrBkApKSmlh2qYYMGTWIaly4JDAjgLq1n2n2rr1wmkykuLn76jzO//PpbAAgLC7W5klax98aOsbmSNqDfs0tJF55ffj906C8AkIjFgwb0txm8e7d3HBwcAODo38e4kkuXL+fnFwDAmNHv2lT29PRo26Z16co2WJb98OPJ12/c8PXx2b5ty6t0Dq9SzFauroq+faow98odxGw2//nXYQB4b8xo/j87KBEEwW2Yfx87br0x1r9f35TEp9evXqoT9o/H0hUKl9CQYHjBGmW/0NCQVi1bli5xcnLq0KE9AFy4cPHlYq6WTQmquF3YuZnv/eMPAOjapXOAv79NC2PeHQUAWVlZt27dtvmp7HJkn9+XzcvPt6k86YOJu3dur/TJS7VanZqaBgBRkZEvqhMaGtKyZYvSJc7OTp06dQSA2NhLNpUxDBs7drRNyaCB/QEgJTU1IyMT3mxvetaM+OdDezKZ7Hl5uE1NmVQGAEajseIGW3NZ80qprHkxFgCaNGncpEkMAFy6fOV/P8XGAgC3iywtpnGjKkyD3YICA8s+ayF3cIBS08UwTGJiEgCUfZwRx/GyoVaAx+O5u7tLxGKbcm5rNxlNZQepXz+6bKFcLgcAo6GSOW/FMEzZtxx4+Qa0atue60ARXqfO9i2b+VXpSlp2iQQHB3HHVdY+IHfv3QOA8PBwoVBoU5kkyciIcAC4f//Bs8p37wEAhmH1ouuWHV103boAEBcXX25nipmzfzp46E+FwmXXzm2uCoX9U1FWlWK2atSwYVWfXSk7yIMHD7m1LjKynAdn60VHA4BOp0tOTrYWisUiXx+fsqN+tkaZylmj7BfTqJyNjjuMTk5J4W6mVinmatyUqrRd2LOZA8DNmzdfNCEhIcEikRAA7j+ofNH7+vj4+vgAwISJk1atWcsdC1ZJalqatakX1alg6aSlp9t08/H38yu7XVjPiBKTEqsaYQ17I3oDvQiGYTb7dBx7luYdHGS2lXEcSh1YvUirli0xDEtKTs7JzVW6uQFA7KXLJEk2atiIZRkcx63nmhkZmampaQRBtPrnMRQAuLm5vew0VcTRUV62EH82Xc/+1Gg03Cro5uZatnJQYGCVxnjq9Jmdu3bdu/8gLy+/uLi48gjljuVFiIEdc94eLVo0Hzp4UL++farUIwDH8bJnBjiOu7i45OTkFBY965qYk5MLAO7u5Z9DcB138/LySld2dnYqm64AQKl0AwCTyaRWq21OUzZv3cZ1c/jmqy/LniVUVZVitip33ahY2UGszXbv2aeCAbOysgOfr3Vms3nX7r1//vVXYmJSbl5euR3lXpqHZznvFnB1dQUAhmHUao2Li3OVYq7GTalK24U9m7lOp+M6SP805+fSr1GzkZVl20u87LTgOL5m1YrBw0YUFRV9P23699OmR0ZEtGnT+p2uXWIaN7Ln6MqaaLm5Xa5yl45CoQAAhmFKStQKhYs9lQGg3L7Eb5Q3PWu+xE8Vc3Z2qhsVeefuvStXrvbq2SMxKSkrK6thgwbcBd6oyIg7d+/l5OQolUruRLNB/frcdbDS5GVKqoU9E2U9Gi33MdAqXQz87PMvN23Zyo03ODgovE4Y12ZSUjLXmfPlIqwUjuM2L0vS6fXt2nfKzcuTSqSDB1X5aTCRSFRuuUDABwCT6dkc0xsM8IL5Zi03GAz/rFxOyizdiMFgKJ01dTrdF18+6zG4cPGS3r16ciccL61KMVvJHao80rKDaHV67h8qlYokiTJDPMOwzx6uUKvV/QcNuX37DgAIhcLgoCBHR0duwJu3bpfY3SP6RcRlLopAqWdbuaVcpZircVOq0nZhT2Xt8wMOJycniaScCefw+LYHl+Uu+vr16127fHHdho27du9NSEi4/+DB/QcPli1fERIS/NOsmdxNqwpYV7AXbWjwgqXDf37sazab7KjMf165kgcIa90bnTVfk9atW925e+/K1au9evbgbmo2a9aU+6lJk5g7d+/FXrrct0/v2EuXoLzLs1BNyePl8J6vW+U+21R2B/oie/bu41LmyOHDvvryc+6shfPLvAXzFix85UgrYrNLkkgkM36cPnHSR38fO7b/wMEq3dGEF29mJpMZnnd2BwCJWAQvvobPlVsD4y5yGI3lz09rIzYTwjCMUCic+eMPP839OSMj8/Mvv16zakWVpsVGlWK2eon1s+wg0uc7680b13OPTlVs+o8zbt++g+P4T7NmDBkyuPRVot59+8fa/fTti5hN5Sxl0/NFzy3lKsVcXZvS6yB9vkwnf/zhh5M+sH/AFy16uVw+dcrkqVMmJyUnnzhx6viJE+fOX3j8+MmgIcO2bv69Y4f2rxhwuUvH/HzG2hx9msu7Vm+mzM8rv+mvhXnT72u+Dm1atwaAy5evwPObms2tWTPmf7c2L168BABt21bh9kYNkMmk3IZRUFDO/YmnCeU/x13Wnr37ACAkJHjB/F9Kp0wAsF7SrEn9+/Vt0bwZAHz73TR7rhWXRlFU2VMZlmULCwuh1HuIuKu4ZS9qcbhXInCXXgFApVICQFFRsaG8+7VcpzORSGi90c4hSfLAvj3jx42d+9MsANh/4OCOnbuqNC02qhRz9VK5uz8bS04lPewAgGXZfX/sB4CRI4a/N3aMzY2Valmj8vJtL0QDQH5+PgCQJCmXO1Q15uralF4HiUTCrVqVdm+sKn8/v/Hjxu7ase1y7PmwsFCGYebMfeEVYI71FLOCI4lyl05BfgEAkCRpc1Ha+vLIf1QuqPw68Bviv5g1m8Q0FggE9x881Gq1F2MvYRjWtEnMs5+axADA5ctXsrOzk1NSZDIZ17H2zcHj8by9vQAgLv6xzU8Mw5T70pBypWdkAED9evVsDk5Zlj1dHW9yeQm/zJ1DkmRefv7//TCjqsPevnPXpiQhIZE7hwgNCeFKuM4gDx89LJsIzWbz/QcP4Xk3H2tllmVv3bbtpggAN2/dAoCoyCjudpSVSCTi3lEweNDA3r16AsDX337/osvd9qhSzNWrTlgod0/35s1bZX+16QZVWFjE3Ydr2MB2e0lPz4gvs66+hNu3bRcxAMTFxQNAYGAA98KaKsVcXZvSa1K/Xj0AuFmmlyzHYrFUqbWyXbH8fH0/nfwJADyKi6+4U4L1uLPsHXSrcpfOo7hHABAQ4G/zOqEnT5/q9Hrbyo+e3bUJCqpa54ya91/MmkKhsElMDMMw+/YfyM7OjoyIsJ4xKN3c/P384uLjT546AwAtWzQv/XxLVXF9l16x62BZ3Anx8RMnbPakO3buKt1zvWLczqXsUfaqNWsTk5Kg1LWvGhMSEvzBxAkAsH3HzvMXLlRp2M1bttqU/HHgAACU7szVq2cPANDrDTt32Z7//bH/APd5sl69enAlMTGNuVPwDRt/t6mclJx8/sLF0pXLNf+Xue7u7jqdbuIHH1V1H2dVpZirF4/H4z4zsGnLlqIyJ4uLf10aGd1g9py53J/cW2+gzBrFMMx30/6P2ym/4oZw7fp1LkdaabXaEydPAUC7Nm1eImaopk3pNenbpzcAXL12rezF7ctXrgaFho8eO67cCyE25s1fGBhS57Mvvir7E3egU+n7j3yev9TM2pm2rGvXr9scG6nV6mPHTwKAzfNCAGA2m/c8fzGqFfdyxLCw0Ffsdl4D/otZE54/tbl27XoodXmW06RJDMuya9eth+cv0ntpXH82s9l87PgJeMG7917C0CGDAKCgoHDyp1O5/SZ3feyrb75r1rSJnY1wj5edOn3GekytVqt/mvPzrNlzPp/6Kffni97b+fp8NvVT7v1wUz/70p49AkcsFp0+c3bBosXWG1QnT53+dekyAOjTu5e1t05oaEi/vn0A4IcfZ5Z+xvH4iZPffv9/ANCzR3frQwgkSX75xWcAsP/AwfkLF1lvnT5+/GT0mHEWi8XHx3vEsKEVROXo6Lhs6WIAuHHz5rz5L3mfuEoxV7vPP/tUJBIWFBQOGjrcmrF0Ot3iJUt//mV+Tk6O0u3ZtX2JRBIRHg4A6zZs5J7tA4CU1NRRo9979Chu6JDBAHD/wYNXSZxKpXLMuPHWMDQazQcffqzRaHAcHzXyf1/wtj9mqKZN6TUZOKBfaGgIALw3fsLxEye5Iw+GYQ4e+nPU6LE6nQ7DMO75k4pFRUWq1eqdu3b/NOdn6yOb3Mn0T3Pmgh2fYJLL5dxrKSv4hLi7u3vppVNcXDxx0kdarRbDMO7p0tI8PDym/zjz72PP1meKon6Zt4A7OBg3dkylU1Tr/ou9gQCgTetWM2cD9xbmZjZZMyZmx85d3INQbaryzFZZzZo2EQgEJpNp+Mh3SZKMiAg/8feRV2mQ06plyyGDB+3YueuP/Qf+OnzE19ensLCwoKBwxPCh0XXrln7etAKTJk7ctXtvcXHxwMFD/Xx9BUJBYmISwzBLFi1o0bz5wsVLGIbp1LWbn6/viWNHbC6wvD4SsXj2zBmjx45LTkn5ed78H/7v+4rrc2/HdnJymj7t+4mTPlq6dJmPj0+JWs2dKPj4eP/4w/+Vrj/v5zmZmZmXr1wd+e4YhcJF6abMzskuKCgEgCYxjRf981W6o0YMj4+PX71m3c+/zP/tt+W+vr4arSYtLR0AlErlpo3rK+1m2aply0kfTFy+YuXiX5e2a9fWeiOgSqoUc/UKDAhYu3rVuAnv3759p1Xb9iqViscjs7KyuVPnwYMGvlfqWfVvv/5y+KjR6ekZTVu0CgjwN5vMScnJCoXLrh3bHj9+sn3HzrS09EZNmrdt03rpkkVVCoNbylOnfLJ1+45Wbdv7+HiLxeKkpGQuB3/3zdfBwUEvF3O1bEqviUAg2Pz7hoGDhqakpg4bMcrR0dHJ0TE7J5s7moyKjJz/SyX3Izldu3QeM/rdDRt/X7Tk10VLfnVychKJRIWFhVxXsvA6daZPq2QrA4AmMTGpqWlXr9q+wdtqwrixe/ft55aOSCRKTk7hls7/ff8tl/tLa9igvrOz84nj7ykAACAASURBVIhRYxQKFzdXt/SMDLVaDQCdO3UcOWK4PRNVu/6j55pRUZHWU5CmTf5xUNms6bNdm4+P9ys+b6dUKlevXB4UFMjj8aRSaVR5Dyy/nCWLFvw8Z3ZUZCRJEnl5+YEBgatWLFu0YD53QIphlS9WT0+Po4cP9endy8XFOSMzU6vVvtO1y1+H9g8eNNDLy/PnObPd3d3NZjOOYzXcYbh7t3c6tG8HACtXreZeQl0BbsuXSqV9+/T+Y8+u5s2b5ebl5uXleXl5jntvzPGjR5T/fLLWwcHhj727Fy6Y16JFc5pm4uLjWZZt1bLl4oULDvyxt+xTIrNnztiza0eP7t2kMtnjJ0+Kioqjo+t+9eXnF8+d5k6tKvXdN19FhIczDPPBhx9xu4aqqmrM1atzp46XLpyfOGF8SEiwWl2SlZXt4uLS7Z2u27du/u3XxaXXjc6dO+3asa1F82Z8Pj8lJRXDsPHjxp74+2hUZGTvXj1HjRwhl8s1anUFTy+8CLeUXVxcDv6xb+qUyXw+Pzk5hcfjNW/WdNPG9Z98/OFLxwzVsSm9Pv5+fmfPnJw+7btGDRsyDJOaliYQCFs0bzb/l7l/H/mz7Of2XuSXuT9t27KpR/du/n5+FoslJydHLBa1aNF8zuxZx47+VfpJyhd5p2sXALhy9VrZ694cHo//58H9n0/9VCQSpaam8vn8Zk2bbNq4/qMPJ5WtTNP0/F/mLlm0IMA/ID0jw2w2h4WF/jh92qaN6206CryhavDtfchrt/S3ZQqlR0RUvdoOBEHebmhTKs1gMITUibB5ezaHew/tilWr7WmHew/tiFGjX0OMNedtSOxIeXLL688W//gJAHh5edV4OAjytkKbUqWEQuGYd98FgLXrN1Tjx3TfUihrvn32HzjoHxQaWbe+zSMNJSUlR47+DQAtWjSrpdAQ5G2CNiX7TfrgfWdnp4SEhJ27dtd2LLUMZc23T4sWzRmGZll2zNjx1s/KJyUnvzt2XElJiVAoHD3KttMagiBloU3Jfg4ODjN+mA4As3+aW9X3kPzLoKz59nFVKJYuWUyS5P0HD1q37RAcFhEUGh7TtMXFi7E8Hu/XxQu5Z7cRBKkY2pSqZPCggT17dM/Jzf3qm+9qO5bahLLmW6lXzx4njx8dMniQj4+3TqczGo1+vr7Dhw05efwo93A0giD2QJtSlSxdsii8Tp19f+xfs3Z9bcdSazC2Oj7whCAIgiD/BehcE0EQBEHshbImgiAIgtgLZU0EQRAEsRfKmgiCIAhiL5Q1EQRBEMReb1PWDAgOc1V5rl23odKa9RvFuKo8f5m3oAaietOMeW+8q8pz2Ii39enswsKiBo2buKo8d5f5Al91sX9Fqha5enrdXc34o3nNt2SErkn1W5lSf2N6xx2ZX54pOJKoN/9nXk+25o7aa3lK5LoXfqPxX2/skVyv5Sljj+TWdiDV4z+7m/2PfinMfg8ePlyxcnXspUs5ObkCgSAkOLhv395j3h3F5/NrO7SawzBMv4GDL16MdXZ2OnfmlM2HRKyW/rZ8xqzZALD59w1du3TmCrt063Hz5q2ylfl8vrOzc926UX179+rTu5f169/Ozk4b1q3t2q3Hp599ERoaWjcq8vVMU03I0NLzrxbvjdcyLACAl4wMdeaLSKzIxGRoLNsearc91HrLyG+aOfUKEpfbwk+XipbfUgOAAx+/NcZb8OIvtrEATTalZ2ppAJhU3+HbZk6vY4reIkaaDVqVWrZcSGDOIjzMmd/BTzQ4TCoka/STPtVu9py5i5csBYDUpIQKPrd55eq1Hr36AMCiBfNHDC/nu7D5+QV1IusCwIjhQxctmF9uIw1jmqamprVo3mz/vj3VE/3b6W3Kmr8uXmg2U9HRUaULu/XoHRcfn/gk7nWMccfOXZ9MmWp9pNVsNt+4efPGzZt79u7bs3P76/5I05sDx/HlS5e0ad+psLBoyqefbd+6uWyd+PjHc3+ZBwCjRgy3pswKmM3m7Ozs7OzsY8eOr1y9ZvvWzdZvuEfXjZr66eRf5i348ONPTvx9RCAQVO/klLsiVbt9j3Xfni3QUmxDlWB4uLSTn9hJ+L9LOwwLd/LM2x5odsdrJx3Lu5XjMK25E/7iHbjazBxL0vd8QXIFgNgMI5cy31gdfMVuYoJP1HKWMtJsppbO1BpOpRpW31Zv7an0k79Nu0EbPJLH/YPP51VQrVHDBnK5vKSk5MzZs+VmzbPnnn2d3vqZehsJiYnc98Y7dmj/ShHb58zZcwMHD50544eJE8bXwOiq5G26Qtuje7f/Z++8w5pKugZ+UoGETkIgoSNVVLoiCth7r2vvfe2uu6+vuuqqa6+Lbe1r712wF7oiKkVAegm9J6Tn+2MghpsAwcq+3/09Pj5hZu7cuXPnzpk558zM8GFD7O3sFCFCofDtu3ff6HYJiYmLliyTy+XdggIfPQjJz8n8mJy4c8c2XV3duLi3K1b+9o3u2zphs9noAOSHjx6fPIWVmhKJZP7CRSKRyM7Wdv3631Uv9+vU8UPCe+V/sTFR586cRufIv337btr0Bt/GwgXzLSw4Hz4kHz5y9Ks/i2pD+uoEv6la+LCEQiIc6cu8MdxstLOussgEACIBPEyp27qZ3BvFttQjH3lbtTOm0b09DbSIAHDpQ00Td7ySzAMAPWrrnTnZGZKHOND72TUq+L8RCzwN3k2zVPx7No5zcoBpX1saAGRVSRY9KvnO5fm6UKgUACAQCE0fHU8ikboFBQLAs+cv1B5a8uTpM/QjNzfv48c01QTP6qVpzx49vrDMmtDECdg/nH+T1FQl7u07kUj0jTLftHmLTCZr6+r6z6kT7du5USgUAwODiePH7dm1AwCuXb/x9t37b3Tr1snAAf3RKHXN7+vSMzKUo3bv3ff27TsSiXQweD+dpqZbJJMpJibGyv8sLS169uh+/OiR2TNnAEBkVHR4RKQivZaW1i/LlwHArj17P+8w5x/I5WTepohyK33y/dHsZoWEiwnl6jAzY23inleVsYVCtWm8zbTIRHiaU1vEVz+bFEjkd9J4ZCK0Z37lefn/ADpkgrE2UfHP3pDcw1rn737MEY50AHhdIMxr3XP0pqFSKACgicEIzRErKiri4t6qxqIpZpcu/qAkQZVBgRwO29nZ6cuKrBFRuNQEgGPHTzDNOI4ubpg9/NIzMphmHKYZZ9Yc7Knf585fYJpxnFzrLlF24igsKmKacZCmvrq6GuWwavUa5csJRIJcLj9x8lTP3n1t7B2tbO0Du/UMPnhIKm3+IykpKX30+AkA/LxgHqZFDh400N7eHgAuXtL0xJy0tLSVv63y6djZwtrOto3ToCHDzp47r3YvwydPn02bMauduxfb0sa2jVPXoO5rf1/P5XJVU0okkgOHDgd172Vla9/GybX/wCFNn+DD4/ODDx7qP3CInYMz29KmnbvX1OkzG9PGNMYfG9bb29nx+bXz5i9UVGN8QsKOnbsBYMXypR4e7i3KEAAWLlyAfkRERiqHDx821NjYqLq6+sy5803nEBkVjRrAw0eP1SboN2Aw04wzcvRY9Gdj3kDPnr+YNmNWB08fjpUtx8rW29dv8dJlKSmpLXqcjErJyqelBlrEC0NYHN264X9kvnDavSL34zltDmf3vpB/Mr5aDvAoq9YiOGvo1QJzXdKmQBM5wL7XlWrz1CIROrG1ZXK4lsJTm+B+Bp8nlnc01yY38kFXCGU7Yyr7X+I6H8m2OpDV9mjO8GsFpxOqpSptsO3RHIvgrPsZfDnAPwk1Ay5zXf7ObnMou9eF/ENxVbKG6WfcK7YIzlr7sgwAXuYKxt8qdD+eY3swy+903uoXZeWCBnMaVW+gxFKxRXCWRXBWpVBWKZRtjaoIPJvf5lC285HskdcLHmTWqj5IpVC2Ibzc/588+0PZnidy54YWfygTA8CAy1yL4KydMeorUC196gc0hTwJJkoigzOJNWNuFrY7lmNzMMvtaM7QqwWH4qpqJer3H32WI5gdUux9Mtf2YJbzkewe5/PXh5dzeZoK472vKy2Cs6wOZCk/8otcweyQYp9TuXYHsxyPZHc9k7fwYUk0FzuuolCoAEChNKWeRXTv3g39ePz0KSYq6cOHwsJCIyOjEcOGAcDTZ1ipKZFIXoaFA0CP7lj1bIu6WU0+sWUrVjLNOM9fvACA1Wt+R592ZWUL3uy35vtJzcCArgBQXl6OqaOw8Aj0IyIyCnMJigoMCCAQsHonKoXi6elhYcEBACKR6Onp4enpYWlpqZyGpqOzYOHiFSt/S05J1dbWqq0VJCYlrf19/S+//qfZ0kbHxKC33r1bkGpsj+5BAPDyZXiz+QDAzVu3u/fqc+z4icysLDKJVFNTExkVvWjJsgmTpihPlOVy+fJffh09dtyt23fKy8utra0MDQ0+fEgOPnjIzz8AtSEFMpls6vSZa9auS0hMJJHIpqbMj2lpCxYu/m3Vf1XrCgAys7J69Oq79vf1Ma9ekclktrl5UVHR7Tt3R435afWa3zV5CgSdRjt0MJhMJr+Ojd29dx8AiMXiBT8vlkgkvj4+ixf+rHlWCkyZTPTNV1Y0+DC0tLSGDhkCAOfPX2w6h46+Pmw2GwDu3L2rGpufn//q9WsAGDlieBOZrF23YeTosbdu3+FyuXp6uhQyOSs7+8zZ89179VE79G6MNS/KhFL5xgBjS706a9mfkRUjrxeEZtRqkQiuJtS8Gumq52WrX5TFFQkBwNNMCwAG2NPsDMkPMmsxkgYhkcv729GgcSXt5WQeykRtr55eIelxLn9nTMW7YpFEDiY6pCqhLJor/O1Z2aTbheKGN9QiEQCAL5YvfFjy67PS5FIxlUQQSOVJpeIN4eW/PittkJhMAIBaifx0Qs3Ym4UvcwUAIAfIqZYcf1896nqBsEnBoV1v48yvkY64VrD3dWUxX6pFJtSI5ZH5wql3i642HCWU1Mr6X+IeiqvKqpLokAk6ZMKdNP6gy9ywXEGVUAYALXLtqRTWPbk5vYFds0IoG36tYOXT0rBcgVQGtgYUIgFeFQg3hJf3vpCPMR7LAX57Vjb+VuGdNH65QGalTzHQIiaXiQ/HVQWezUMV0jQ3UnlboyoA4M9Ak142OihwV0zlTzcL76Txi3hSYx2SAZWYVSW5msIbfq1gV8ORATJnNm3URDAZjA4d2gPAkyfY9oxauI+Pt5eXBwCEhYWLxWLlBK9j39TU1ABAr55Y9azm3ayGn5iNtbWnpweRSAQACwsO6tsV3oKtge8nNe3t7VHXFhUdrRweFhYOAK4uLgUFBRmZmcpR4RERABAUGKCam5GRUcjd27NnzQQAOp0ecvd2yN3bGLvx7Tv3Hj56dPL40cy0lA8J79+9edW1SxcAOHX6n6xsNc51yiQmJQGAmZmZkZEaX0QnJycASElNbVY/nPThw+y58/n82pEjhr978yozPTUr/eO639cAQOiDh8j5DfH30ePIXrh86ZKUpISIl8/fvIqODH/h7t6Bx+dPmzG7uOSTAeb8hYv3Q0IBYMmihSlJ8eEvniUnvj95/Oi5cxdiXr3GlEEkEk2eMj0tLc3O1jbk7u2UpPhX0RGZaanLliwGgIOHj/xz5lzTT6FMh/btVv22EgC279j19u277Tt2JSQm0un04L/2Nm1ZaYySklL0iTLqvYEU9OndCwASk5KQG0JjEAiEoUMGA8D9kFBVm83N23cAQFtbG9lQ1fLi5cvgAwcBYOyY0Ynv335IeJ+Znhp6746tjY1QKFy4eKmGhoD4EtGT7Fp3U+pQBzoK2fu6cn9spR6V8Hc/ZtQki5sjzN5OtVzsbXDiffWlDzwA8GRpAQABoJcNDQAi89X0s1IZDGxDJxPhQ5k4vgRbkiK+9HlOLZkIA9vQ1ZZq+ZOSQr7UQIt4dhArdZbVmykWKbOsFngaAMCzHMHZxGrlxCQiAMDphOpn2bVH+5kmz7J6O9XyzRTLAEttADibWJNT/WlmhoRUQoloXVjZKj+jxBlWcVMtP8y0mu9pAAAfysS3PqqfHCvfCwD+87yUSiLcG2WeOMMyYbpl6Gg2W5cEANuiGth6f39ZllUlIRNhfy/G++mWYRM4UZMsfM21Fj8uqRDKAKAJdypVHmTyAaA9k2qu26DdrnhSGlsopFEIB/sw46dbPvmJ/W6a5fnBLEMtYkalZP6DYuWRyfH31acTqgFgsbdB/HTLZ+PYUZMsXozndDCl8sXy2SHFJbVNLS16VSBc8qgEAJb5GI5z1UWBGZUSZOSe464fP93q1WSLmMkWb6daznHXB4AdMRXJZZ9EGplMASWfoKbp1aMHALyOja2ubvDSnz59BgD+nf2cnZyYDAaPz4+JeaWagEKhdO3aBZOnht2s5p/Yzwvmhdy9TafTAWD2rJmob0d/thK+q10TyT/MnDI8IpJOpw8fNhQAIpQsWzk5uTk5udCI1NSEV69fnzx+rH+/vqg3Nzc337B+LYp6/Tq26Wu53AIA4LDZamNRuEQiKS5uxpVg2/adEomknZvbX/v2mJubAwCNpjNvzuxJEycAwKEjfyOBIRaLd+7eDQDDhw1d+ctyGq1uyGlvZ3fi6N9UKrWyslLZB+fY8RMA4OPt/Z/fVqKJGoFA6N+v7+9rVxcUFGDKcPHSlcSkJCqVeu7saU9PDxSoo6P968oV06dNBYCt23e06Oib+fPmdu3SRSKRTJk+Y8++/QDw56Y/rK2sNM9BmaPH6jSlSBuhjI+3F5o6x7x6hb2sIaj9lJSURqpoLG7evA0AfXr30tXVbezya9duAACDYbJrxzYGwwQFeni4/7FhHQAUFBS8UhmLqOVsYg0ATG+vj/5MLRfvjKkgAPzdt879BADIRFjua9iZo51bLQEAD1adJdLdVAsA0irEavIFMNYm9rRWP928nsKTyaGHNc1YW83nzOVJkVpvma9hgKU2Eis6ZMKvnQzbM6kAcPsjXzk9yiKGKzzaz7SPrQ6aDTJpxI0BddUSlf9JSYj0Gm+LRAu9DOZ66NMpBADQJhFWdjQ0p5MAIDyvqcmWQsilV4jPDma1Y9aZQlwZlEXehgCQUy1RGB3LBLIbqTwAmONuMNSBji41p5OO9jfVIhHUztERMjlIZJ/+VYnkMVzh3NDi0IxaQy3i5kAT5cSJJeJ76XwAWOtvPNCepihhFwvtP4NMUM0o1KRiGex5VQEAQx3oy30NdepnurYG5CN9TalEqBTK/kloIJ+UyayUTL1bJJLBhLa6S3w+OeRH5QvkAHQK4T9+Rgr3LiNt4n87Gw1zpPey0VE2b6NZJkWDuSYA9OjRDQCkUunzFy8VgUKhEPXJAV27EAgEJBefNFTSormgX6dOql4LGnazX+sTaw18V6mJukXluWZ6RgaXy3Xv0N7byxMaClQ00XRwaMNuRHQ1i4+3d6eOvsohbV1d9fX1AaCgsLDpa3k8HgDQ1Dm2KIcjrUVj1NYKQh88BICxY0YjhYOCWTOm/+e3lWtXrxIIBAAQERlZUlIKAFOnTMZkwuGw0bgBTS4BoLy8HDkiqZ7/N2rUSNV1GleuXQOAvn1629naYqKmTp4EAFwu982buCYeBAOBQAjev8fIyCg3N08qlQ4aOGDsmNGaX46orRW8j4//bdV/t+/cBQA9undD6iNl9PT0bG1sAOB9fELTuXVo3w75xN66c0c5nMvlIonbtHp2545tH5MTHz8IwSiC/Dv7oR/NKicQDzL4FCL0rheQB99USWQwwJ7mb4FdSNfFQhsAmDSSwvZpokMEgLLGe/8xLroAcC2Fh9GpXk6uAYBRzuoH4+Z0UsYc65jJFmOdsYOGThxtAMiuUiOnPVlaPuYNGpKtARkJxfwarBWQQoRp9QMFBJEAbZlUAOCqJFbLWBc9Q60GH0j7egmqyCE8T4BGdiOcGjypNokw272pNWA7YipsDmYp/rn+nT3sWsG9dP7Etnp3Rpl3MG3gtXA7jQcANAoBcxcA6GtL06cSASA0o26cEZUvKK2VAcAkNz1MYrYuqauljnJiDBVC2cTbheUCWW9bHcWIBIEeUyL7pENWsK8n43h/065KzQkNmqkUjZaPe3p4GBsbAcDjJ08VgZFR0QKBgMEwaevqCvW9tLLKtKqq6k1cHAD07KlmzYmG3ezX+sRaA99VaqJRTE5OrsK9BVkuO/r6enh4kMlk5bkmivrsiSYAeKrzTEETDowJTRUkzBqzFmjV+wfV1qpxWFCQlJQkFAoBoJ3KUn0nJ8clixZOmjhBT08PAN69ew8ABALBXUVyAECH9u0B4MOHZGRqTUn9iMLburpgUtJpNCdHB0xgbGwsALi5tVXN2dHRAa2Mjk9oRixhMDIyMjVlot9NzOEUvHj5Eln1Ff+sbO279+yDXHK8PD0P/LVP7YXW1lYAkJPT/IYyaAxx916I8rwZqWcNDQ171LtCNIaBgQFSBiij0Auh99g0BTwplydtx9RC0kUqr+uCx7pgu1Son2Z5sLCdXROrGbtZ6TB0iGUC2ZOsT60uqVScWCo20ib2sG7UWZdCBHM6iUbBZo3KKVT1CALAyBKEvhYRAAQqtlN7Q4quSuYGVCIACNRlrsnt9OuFqOJ26RViAKASoY0R9qvsZqWjyV2UkcjgakrNjuiKjMoGcj2+WAQALiZUbZU3QSaCK4MCAAn1SvL3xSIAIAC0V1ddKDC5TKxaByIZTL9blFEp8TLTCu7FxNzKj61NJIBQKh9ylXvrI1+1wpVBvooazjWJRGK3oCBo6O+DBGRA165IrxMYEAAA7969LysrRwmev3iJDB+91K050byb/fJPrJXwXU2sTAbD1cUlMSkpIjJ6+LAhUG/U9PPrRKPptGvn9uZNHJfLRTUbXic1Az/7dmi8g4FIJABAswpJbW1tABCJ1KvLhPUqeB2dpj5Xbr2ylKliscNQWFgEAMbGRui+GFgsUwAQCoVVVVVGRkalpXUeGUwmUzUxJpDH4/H5tQCwafOWTZu3NFpULlav2zTr/9iYnJyir69fVVV17vyFfn379Ovbp0U5AICOjranh8fIESPGjhnVmLWfxWIBQHFxcbO5DRs6ZPvOXfn5+W/exCkU0Ug9O3jQwGadDEtLy46fPPn06bPcvLzi4pLPWNGUVi4GAEfjuht9KBXxxHIiATqx1awGSSkTg5J6FgCQjlFfq9GBLJkIw510D8dVXUqu6W1b1/DQRHOoA53S5AD4abbgUnJNQomohC+tUJnBqGKgrhiN3UFtYqS81VDxr5qDQjWqyKC0VgoADJqacYWFHolKhMb2Jlzha7jI+9NkVCCRc3nShBJRcGzl1RReSAb/3GCWZ/2LKORLAQCpl1UxpZEBhCX1ClKkKTXSJqqK2PrEIJTKq0UyzEx6+eOSKK4QAHZ2Z6h6MNkYkDcHmvz2rDS9QjI3tJhKBG9z7UBLnf72NFuVDRlaNNcEgJ49ul+5ei07OyctPR2pZ5DNUmEf4XDY9vb2aWlpz54/RyNRJFatrCzbtLFXzVDzbvbLP7FWwvd2TAoKDEhMSoqKrpOa4RGRJBLJx8cbAPw6dnzzJi4iMmr4sKF5eflZ2dkUCsXfv/N3LiECjZV4fPW+DArFrJ5eU9MsxeiJRG7GTYZfWwsAWlrqN8RSKF1ra2uNjIzQPBgaGWBi1snU8OoewcjIiE5vfDqi2VgV8ejxE7T5wN+HD16+cvXipctLli339vZqYnDQ2a/TqRPHGpZTq4kNwBSgcQm/yTk9wtHRoa2ra0Ji4q07d5HU5HK50TEx0Jx6FgDex8ePGTse+VsZGxu5uroYGhigobfmDrTlQhkAMHTq3jXymmHrklW7RbEMnmTXQr0tE5GKhK5RU93faGfdw3FVDzP5FUKZoRZRJofrKTwAGKWifVVm5dPSM4k1AEAAaGNEcTahIEfZzEpJVpV6Dao6R+xGaVFi9TlokAZNubQamYzTKESRBqMBANAmE2wNyLYG5N62tDE3CmK4wkUPS56N4yA5XSuRNXEXhc8w+rMucSOOuwpRWiuWGyoNnJ5lCxTz+z/Cy473V7M/5XhXXX+O9qG4qrvpvNJaWXieIDxPsDmyPMhKZ2OAsbX+p34bSU0yRdOevHu3bgQCQS6XP336zN7OrrikJCExERpq9QIDuipLTbS/wRdubvBVPrFWwveWmgEBXYMPHoqKioZ6o6aHhzuyMHfs6Bt88FB4ROTwYUORUdPH20vtkvnvgAWHAwB5uXlqY5HCUEtLy7SRHVkRiploswph9JgCgXrZoBCTSJuhkItidVNhjNJYt14Bsujn+fPnzW26GJpQUlL688LFADBl8qRuQYGeHu7PX7wsKChYsnTFP6ca3Q+dRCJ/hw0Ihw0dkpCYePfuvbWrVwHArdt3AYDDYWPsLhjkcvnMWXOLS0pMmcw9u3d2CwpUdgZmmnE0vLtIKgcASv2lfLEcAHTUdamPsvhoZtmW8UlGvsytBXU6W2WcjSntmdR3xaLrKbwp7fRe5AoK+VJHI4rCCqjK1RQeEpnjXHWX+RqyaJ8ebUdMxa6WLHD8sVBIBAAQNyIZm1ZjqoVKhOnt9WO4xRmVksRSkRuDCgA0clOKZYFEBvWabQDQIatXWdclltaVFaMbF0rlFnrkSW56myLKH2TWnoqvVjWLQt2M03hToPHbItHjrNrQDH58iehpdu3Ay9wHY9hm9bPhul0ONFiviTA2NvL08HgdG/vs+Yvp06a+fBkGAG3a2Cu7jwQGdD12/ATyGMrOzkEWxy/ZSO9rfWKthO+9N5Bfp04UCiUxKamqqgpZLjv71VmDO/r6Qv1S97DwcAAICvp89ewX4urqAgCFRUXK6z0UxMcnAICzs1PTq4gUDbGktLSJZABgZsYCgPLyitpaNT6HBQWFAKCjo42MoMb1i2HU6i1z8xpIejqdjq5CmXw5CxcvKS4psbWx+X3tagAwMDBAO+2FhIaeOdvMdgSfARoEujsMMQAAIABJREFU0JrUhCtAQ+P0jAy0cOjmrVsAMGL4MLVrWBW8eROXlp4OAH9sWNezR3fl71lh2tEEQ20iAFTUu/MgrWOxym4+Aol8Y3g5AOhSCAqv14xKSVS+sBNby5TWjFpitLMuAKCFjNdSkB9QUxNNtDGCgxFlS5AJq2HmTfidtkJQfZYJ1KwAza+RamhAxaCQPdx6T10WnaT8J4ZCnhQATOvXd6LLKwQytYKzgCcFAG0yQY/aoJu1NSDfHmk+z0Mfvcr1YeVIzaAWAoC7KXWpj8H90eYXBrNoFEK5QHYo7tNuWcYmxr4+Pu3bt2BTZeRJGx4RKZfL0d4FGPeRLv6diURiTk5udnbOi5dhAKClpdXF31/zW2D4Wp9YK+F7S00aTcfH20sul0dFxyCjZudOHVGUiYmxvb19SkpqWVl5ZGQ0AAQFfL4r0Bfi16kj0ouGhDzAREkkkgePHgNAj27NOJg4OjigTFQXuqRnZEydPnPq9Jloazr3Dh0AQC6XI181DLFv3gBAO7d2yBHXvt66kJCYhElZWlqWnp6BCfRwdweA2Ea8ZCUSjbwcEX8fPf7g4SMCgbB/326FGqBnj+7jfhoLAKtWr2l6YeVnUFhYCOqWcqrFysrSy9MTAEJCHxQVF0fHNO89C0rjDHStMo8eq99sSC1mNDIAZNZ7l7RnahEAKoSyd8VKe1kA/PdFGTJCKpsw14WVyQHmejQ/HR/qSKcSIbZQWMCThmbUEgkwXMXbU5m8agkAdDDFblArB3iW3bzeu/Vga0ABAL5YnluNFWlPP/dBFApqhWG1g6kWACSVilQFoUgGiSUiUPLvbW+qBQBygLgiNSa6uEIhALgxqJhVpA7GFIYOEQA2dDW21icLpPL5D0owRlmxDFSHAf4W2sMc6Kh4ikAXZ+c7t65v+mODps9c79RTWVmZ9OEDWtGAkZr6+vqo04iKjkY2Dv/OfprYUxrja31irYQfsA9tYGAAALx+HRsRGUUgEDoqac/8OvkCwP2QkLT0dCMjI9WlCBiIBCJ8G+crPT29Af37AcD+v4KRN42CEydPFxQUEInE0aNHNp2Jjo422krjn7PneLwGJtLz5y/evnP3ydNnZiwzAPD19UFuL8dPnMRkkpGZiYZ7gwcPRCEsU1Nklr967Tom8YlTp1SX+aMZWHRMjPJGr4jIqOg2Tq5Tps1QO8fF8OFD8u/rNwDAgvlzfX18lKM2rFtrbm7O4/EWLFykdm/ozwaJYcyuT02AFm4+efI0JPSBXC53dXFxcXZu+hKFB1ZpQ5VARUUFOsUFlPy/msDJhKJLIURzkRoPmDRiDxsdAFj6qOR9sUggkccViSbdLrr1kbe9uwmRACV8aUalhFsjXfyo5GFm7UB7Wg/r5qfUhlpEtLJlz6vKKpEswFKH1eT0FFlVy1TW2v/9tgq5j4r+JZuwKlbCIM9kBQKp/MCbz9EzC6Vw9G0VANApBMVS0YFtaABQK5FfSsYuKruZyqsRywFgoH3dMMXHTAtV/sl47FbJmZWSsDwBQKNbT6D77uvFIBIgsUT0Z+SnKdfE20VOh7OuqBQA6k2qatX+mtOhQ3u0YjI09GFycgqJRPLvjHUfQc5B0TGv0MKtLzRqfsYnhmYIQkFrdKz9EVIzoCsA3L13Pz8/v62rq7K5Cylpj/x9DAACunbBrHFUBS1+EIlEaFkkRjJ9If/5baW2tnZaevrYceNfx8YKhcKi4uL9fwWv+X0dAEyfNkWTQzOWLV1MJBILCgomTJ6KppV8fu2Rv4+hzQFmTJ+KNjQgk8m/rFgGANdv3Ny+c5fCuywlJXXK1BkSicTKynLCuE/n+6BNEl69fr1m7Tr01LW1gqPHjm/fsQvtkavMqJHDnZwcAWD6zFkPHj5Cjm0ymezmrduTpkzj8XgEAqHZgaRQKJw1Z55QKHRxdv71lxWYWH19fbSpfURkFNoB5KtQU1ODKq2dumUzahkyZBCBQIh59frWrdugwUQTADw96vbr2rp9B49ft7ouMip6wOCh3l5ejo4OUL96p2lIBAiw1OGJ5TfqN8TZHGBirU/+UCbud4nb5nD2wMvcD6Wifway3BjUAEsdkQy6nsnzOZV7OZk3wJ62q4dG82kAGO2iCwDnk6oBYFSTE02oFzZPc2qf59QNjKpE8q1RFX9GViz2NgCAKpEsraIF+oYfhbU+2ddcCwB2x1SE1e9UV8CTzrhXTCYSDBv3Pa6VyMsEMsW/Ir40qVR8PqlmwKV8pAaY62GgkEOORhS0r9OG8PLQjE/D5UdZtWtelAHAAHsaWn8CAGQiLPU1BIBbH/m7X1Uq5oup5eKZ94skMrDUI//k0pT+3JOlhfx7D8dVvah/qDZGFJEMVr8ou5zMU0x5+WL5yfhqtM9Df7tPL/34iZPDR44ZPnKMRpUIAAAEAqF7t24AcPzkKQDw9vJUXTyGeunHT56kpn6EeqXuZ/MZnxjq2x8/ecLn10okEoVvR2vgB2zu596hg76+ftKHDwDg59dROQrNO9HawUANVmoiPapQKBw/cTKZTG7b1vVhyL2vVU5rK6ujhw9OnTErIjKqb/9BylG9e/Vcu/q/mmTi1rbt3t07Fy9d/vJlWEe/LjSajmLm2rNHd3SsB2LShPHJycmHjxzdsnX7/v3B1tbW1TXVaHckFot16sQx5T2lpk+dcu/e/YjIqAOHDh/++6iRkWFFRaVEIpk9c0atQJCWlqbs862lpXX65PFRo3/Kys4eN2GSoaGhkaFhQWEBml+2c3PbvrXRFSkK1m34I+nDBzKZ/Nf+PWoPWOgWFDhx/LjTZ85u3rKte/duri7YtaSfQcyr1+hBkJe1JrBMTf39O798GYYc89DUs2kYDJPZs2b+FXzg4aPHbu09rK2sSkpKCouKPDzct2zeuH7DxpSU1KvXbryPT5g2ZcqM6VObyGq2u/7ddP7umIq+tjQ6hWCuS3owhn05ueZdsUguB3cWdZRT3THIh/owTydUp5SJDbWJPa11OnNaoP4KtNRh0UiFfKkeldCnuTNVZrsbXEnmVQhl424VWuuTtUiEjEqxTA47ujP8ONp7X1fK5DDgUr6VAeXeKPMfffZlM2wMMBl6lVsjlo+5WciikehUQmalxECLeH4wa/ytRs32+2Mr98c2Ohmd1k5voVcDxfimQJP8Gkk0VzjtXpGJDpFFIxXwpGj3CR9zra1BDXYkGO+qm1ImOvquent0RfCbSmt9crVIjnZ9YtFIR/ub0lVWsmJY5GX4LFsQWyhc/LDk4Vi2kTZxma/hK67gTZFo8aOSZY/BRIcEAGUCKdJhDHWgj1Ta0eJjWtqLly8by7wxevbofvHS5fz8fGikp/X29qLRdJCmx87WVnWDlBbxGZ9Yt6DA1NSP4RGRNvYOBALh9IljvXv3+pIyfEV+wFyTRCJ1qV9P4tepk3KUrY0Nq94rtZsGKzVZLNbhg8Ft2thTKBRdXV3NZyQa0rt3rxfPHk8cP87KyhKdFNa1S5fg/Xv/OXVC86OSx4we9ejB/bFjRltYcCQSqa6uro+3964d28+cPokRPxs3rL988fzAAf119fRSUlPLyys6dGi/8pflYc+foG07FFCp1Ivnz/66coWjowOZTBYKRR3at9+za8cfG9Yh3x9BQ621rY3Ns6eP1q5e5e3lJZPJsnNytLS0/Tv7bd/6Z8i92yYmxk0/wsNHj5ECYMXype3csDs2KFi/bq2FBUckEs2bv/CrLMYKCX0AAC7Ozi3ark8hKf06deRwNNpYau3qVZs3/uHq4iIWi7NzcphM5trVq65fuWxoaLjyl+WBAV11dLTLysp0dZuZ2HmZaQ2wp2VUSpY8KkHenjQKYZKb3vZuJju6m0xsq6dYhUKnEOa46+/sbrK6s5FfS0QmAJAIdfvjDLSnq10pqAxbl3RrpPmgNjRjbWJ+jaRGLOtjS7s23HykE52jS9oYYGxOJ4mkcqJmyz9+LC4mlPuj2UMd6EwaqVwglcpgvKteyGh2WwYVDRI17M50KQRXBnVKO717o8zXdzXG2B31qYSLQ8y2Bpl05mhLZZBcJpYD+Ftob+9mcnmomerS0nVdjM8NZvW3o+lRiKnl4gqBtD2TutzX8PFPbFeT5l1byUTY25NBoxAK+dLlT0pR8a4MN98UYOzP0Tajk6pEsnKBlKlD6mtLO9rPdH8vxpe/qe7dghSaPNWdLAGASqUqOme1WwK1lJZ+Yr8sXzZ82BADAwMqlWpjba12bfqPgtCiDUhxcL4bQqGwg6d3aWnZurWr582d86OLoynVIvmgK9yP5WI/tvb27ibKS+swCKTye2n8v2Irl/oa9v/uZzX/j9HmcLZAIv8z0GRC2+Z3qsLB+RJa0fErODjKXLt+o7S0TFdXd7ySQbf1o0clXBtmNut+cUS+IPBs3lAHek8bWnsmlaFDIhKgVCAr4kvfFQmjucLHWfxqkZxOIahuN4rTGAKJXCwDvYYewbnVUmT/s9DDOzScbw7eyHBaIyKRaNuOnQCw6OcF32F7hK+LkTbx/BDWpQ81u2IqLifz0OGXqtgbUn720h3roqv2rBIcVQZe5r4tEo1wou9u6Dl18UMNAGiRCOiwUhycbwouNXFaI/v+Cs7OznF0dJgze2bzqVsfJAKMddEd7az7tlj0Mrc2u1JSKpBKZWCkTTTSJrmaUDuytawaV97iqKUjWzuuSHQ5medkTJ3aXk+bRBDJ4Gpyzf7XFQAwxkVXH7sqFQfn64PbNXFaHe/j4/v0G0ggEO7eutHsml2c/z/USuRjbxa+LhACAJkIDB1SEV8qkwMAeJlpnR3EatZhFQfny8GlJk7rory8vGefftnZOfv37h4zetSPLg5O60Isg38Sqm+k8pLLRDyxXJ9KdDahDG5DH+uK2bcOB+dbgUtNHBwcHBwcTcGHZzg4ODg4OJqCS00cHBwcHBxNwaUmDg4ODg6OpuBSEwcHBwcHR1NwqYmDg4ODg6Mp/wKpOXHyVKYZZ+r0f9lq97+PHmeacazt2vzoguD8K/Hw9mWacbZu2/GjC/Jv5dr1G4HdenKsbC1t7Hfu3gMABw8fYZpxHF0aPX7g+4CKYefQzLGv/8M4urgxzTh/BR/40QX5TPDdSXBwcP7XiHn1ataceeg3nU6vrlZzwjMOzufxA+aa/QcOadE4a/68uYcOBM+ZPevbFQkHR0OePnvONOMcPHzkRxcEpykePXoCAFQq9dGDkMy0lLWrVwFArx7dDx0I3rVj21e/Hd4q/l/xveeaQqHw7bt3mh9OCQCdOvp+u/Lg4LSI6OiYH10EnOYpLi4GABcX5/btPulj7e3t7e3tv8Xt8Fbx/4rvPdeMe/vuq5xXjIPzQ4jC+8d/A1KZFAC0qN/pCBS8Vfy/4vtJzcKiIqYZZ+DgoQBQXV3NNOMwzTirVq9BsbZtnJhmnJDQ0OzsnLHjJti2cRo6om4PUlVvoF179jLNOF2DugNARGTUuAmTnNu2Y1vaeHj7rvxtVXFJifJ9o2Ni0L3KyspzcnIXL13W3sObbWnj4tZ+yrQZb9+9V1va2Ng38xYs9PD2ZVva2Du6dOvRe8vW7VVVVWoT3w8JHTp8pL2ji5WtvX9A0LYdOwUCgSZ1wuPxrO3aMM04GzZuUptg5+49TDOOpY19dXW1IvDjx7RlK1Z29OtiZWtvaWPv5dtp/s+L3ryJw1y7ddsOphmnnbuXarY7du1uLOpLMvm8qlaljZMr04xz9959gUCwbcfOTp27WljbtXP3WrBwMZfLBQC5XH7q9D89evWxsXOwbeM0YtTYV69fq+YjkUhO/XNm+MgxTq5u5hbWji5uAwYNDT5wkM+vVU387PmLaTNmdfD04VjZ2tg5dOrcde78nyOjohUJlq1YyTTjPH/xAgBWr/kdPWllZaXaRzh2/ARyPMHsWJmekYEuVFjdFJw7f4FpxnFybXAJgUiQy+UnTp7q2buvjb2jla19YLeewQcPSaVS1Zvm5eWv/X19l8BuVrb2Vrb2vp38l//y68ePaZhkCYmJisJXVlZu2rzFr0uApY29bRunIcNGhISGqn0iZYYMG8E04/TtP0htbFR0XTN4+uy5IrC8vHzL1u09e/e1c3A2t7Bu2859/MTJ12/cxNRPWFg4ujY9IwOTbWRUdGNRyixYuJhpxjlz9jwoNci1v68Hdd5A797HowQ1NTUvXr7s3rOPpY29sgfW120VTSOXy2/cvDVuwiQXt/bmFtbObdsNHT7y1D9nZDI1x69KpdJ/zpwbNnK0k6ubGcfK2q5NUPdemzZvKS8vx6ScMGkq04yzZu06Pr92+S+/urp1sLFzQJ/A4SNHmWacoO69ACAtLW3BwsWox3Nxaz995uykDx++sJDl5eWrVq/x8u3EsbJ1deswYdLU/43hxffT0FIpFE9Pj6KiotzcPCKR6O7eAQAsLS1RrLa2Vk1NTXV1zdTpM969jweAGiU5gUFbWxsAqqurQ0JDJ0+dIZVK9fT0iERibm7eseMn7ty5e//ubQsLTn1iHfQjKSlp5uy5xSUlWlpa2traJSWld+7eCwl9cOrEsV49eyjnv2PX7j+3bAMAEolkaWFRVl4en5AQn5Bw+szZa5cvOjg0cIsNPnBw7boNAEChUKytrWpqeFu37Qh98HDYkMHN1gmdTh80cOCFi5cuXb666rdfiUTsIObmzdsA0K9vHz09PRRy8dLlhYuXok7TxtqaRCZnZmZevHT54qXL//3Pb4sWLmj2pt+Oz6hq9floaVUC1NTUTJ46/fGTp4aGhhKJpKCg4MLFS69jY589fvjrb6tOnzlLp9NlclltDf/5ixdR0dGPQu87OTkqMqmoqBg7buLr2FgA0NfXt7OzLS0tjY6JiY6JOXX6zJVLFzgctiLxth07UV9JIpGYTCaBQMjIzExLT7985eovK5atWLYUAGysrT09PeLi3spkMgsLjqmpKQCQyeq/oMCArgBQXl6ekpKqXKqw8Aj0IyIyCnMJigoMCCAQPh3cQdPRWbBw8cVLl7W1tel0WmlpWWJS0trf16elpe/YtkX58kePn0yfOZvH4wEAm82WSqUZmZkZmZnnzl/4a9+eoUqtUbvePpKXnz9n7oKkDx/09fW1tLQqKyvDIyLDIyIP/LVv5IjhTbygsWNGh0dEvo6NTUtLU9V53rx1CwDMzMwCunZBIe/j48eMHY+GsywWy9zcLC83L/TBw9AHD69cvfb34YMtMtk0jY2NtaenR1ZWVmlpGZ1OR5VvYWGhNrGiKlJSUidOnoZqD/0P36BVNIFAIJg+a05o6AMAoNF0rCwt8/Lzw8IjwsIjLl26fP7cGTqNpkhcWysY89M41ITIZLKJsXF5RUVCYmJCYuLFy5fv3rrBZn9q29raWgDA4/M3bt588tRpFCiXyxRRtbW1b97EjRg9trq62sTEmEwmlZSU3rx1+9Gjxw9D77dpY/95hSwuKenXf1BWdjYAMBkMQyPD5y+eP3z06GDwfsK//WQa+fflwKHDDBbbto0TJtytgyeDxZ45ey7HynbHrt2Pnzx98eIlipowaQqDxZ4ybQYmE2s7h7bt3JcsXZ6fny+Xy8Vi8Zmz58w4VgwWe+y4CYrE796/Z7DYDBa7o1+XfgMGJyQmSqVSuVweERnVzt2LwWI7ubrxeHxF+itXr6P0f2zaXFNTgwJjY9/4BwQxWGxvXz+BQKBI/DEtjcW2ZLDYo8eOKy0tQ4HxCQkdO3dFmVvZ2jddIS9fhqHbPXn6DBP1MS0NRYU+eIhC4t6+Q7cbP3EKl8tFgRUVFQsWLkYpnz57rrh8y9btDBbbrYOn6k2379zVWBSGFmXS0qpujPYe3gwWu0+/gZ27Br59914ul4tEon37/0KZz5m3wMbe8X5IiEwmk8lkz54/51jZMljspctWKGcyeep0Bottbdvm+o2bqBhyufzZ8+cOzm0ZLPaAQUNkMhkKTEtPZ5pxGCz22nUbqqqqUGBpadnadRvQHZOSPiiytW3jxGCxDxw6rOFTnDx1Wjlw9tz5DBY7IKgHg8VOz8hQjvLw9mWw2GfOnkN/unv5MFjsvv0HObq0vXP3nkQikcvl+fn5w0aMRqXKzMpSXJuWnm5t2wa1/Ly8PBTI5XInTp7KYLHNOFbJySmKxBmZmSiHAYOG9OjdN+7tOxT+Pj6+g6c3g8X29OnY9KPV1NRY2dqjbwQTJZPJ0Lteu26DIjF6lo6du8bFvUWBYrEYTXQYLPbGTX8qLld8Dmnp6ZicIyKjGotSZdGSpQwWu//AIcqBqN9wcG6rCElLT0d5zpw9193L5+Tpf54+e/4+Pl7+zVqFvJE+cOnyX1B3cfnKVdRcpVLplavX7B1dUJtXTrz5z62oDIcO/11bWyuXyyUSybXrN9CHMG3GLOXEqMlNnDyVY2W7cPHS0AcP74eEiMViuVz+z5lzDBbbuW27jn5d5sxbgLoUqVR689Zt1JH+vGjJZxdy3oKFDBabbWlz+85dFCIQCLZu22Hn4Iwaz/6/gjWprlZIa5Ga6LtiW9pcuXodE9WY1GSw2IOHDsck3rBxE4rKyclFIYqu3N7RRSHYEI+fPEVR5y9cRCFisRh1XouWLMXknJ+fjxrlydP/KALXrF2HuuaysgY5JyV9QJ9cs1JTJpN5+nRksNiz587HRO3cvQe1adTE5XI56gQ9fToqS265XC6RSLoGdmew2ENHjFIE/kCpqUlVNwFqDCy2JaZ/RBXFYLEvXrqsHD53/s8MFts/IEgR8j4+HqVUflmI6zduoqjwiEgUgvoOazsHhXBVMHvu/PETpyiPRTTvHxcuXqralbRz97K2c9i9Z5+ygJTL5dnZOahUCpmHKoHBYkdERinnEJ+QgMKvXL2mCJwzbwGDxe7cNVAoFConlkgkQd17MVjsWXPmKQKzsrJRDs5t25WXlyunP3n6H8zn0xjzf17EYLHbe3hjKi0qOhrlkJCYiEIOHj7CYLFNzS1SUlIxmaxY+Rv6fBRjqe8sNRVVYefgnJGZqZz4G7UKubo+8GNaGuouMA1bLpffvHUblTA19aMi0LeTP4PFnjx1Oibxmt/XM1hsjpWtcv+A3hTb0mbp8l8w6c+eO48yHzFqDCZq1px5mPFTiwpZXl6Oxveq46oZs+agxP9eqdm6djlgMhnDhjav2FQwfdpUTMiYUXXW0PCICEzUiOHDjI2NlEO6BQWaMpkAEB4RiUJiXr3OyckFgLmzZ2MuNzc379O7FwDcvXtPEfjk6TMACAoKNDJqkLOzs1NHXx9NHoFAIKAy3713r6amwaoypJ4dPmwoUvgIBIIHDx8BwLifxmI0WiQSaeyYUQAQFhZe3bhm+7uhSVU3Sxf/zna2tsohri4uAECn04c21H63dXUBgIKCQkXIrVt3AIBOo40eOQKT7YD+/fT19QHgfkidAU8ulwOARCKpqMCaow4G7//n1HGkbm0p6Kqo6E82sPSMDC6X696hvbeXJzRU0qLm6uDQRlm3BgA+3t4YH/K2rq6o/AWFdc8rEolu37kLANOnTqFSqcqJSSTSxAnjACAk9IGqKXTcT2MNDQ2VQzq0rzsDPJ+b3/TT/TRmNADk5+e/DAtTDkeNtq2rK3pZAHDr1m0A8O/cGWPaAIDxP40FAB6fj8nk+9O7V08ba2vlkG/UKtRy7foNuVzOZDBGDB+GiRo4oD+DYQIA9+6HKAIjwp4nxb/bsW0rJrG/XycAEAqFhYVFmCiRSLRg/tzGCjBv7hxMCDoNPj+f+3mFfBkWjtrbsKFDMIknTRzfWDH+LbQuqent5UVoic7b18cbE9KmjT2FQgGA9HSsy4BqYgBwcXEGgPT0dPTn69evAYBKpTo6Oqgmdu/QAQDi4xPQnzKZLC09HQDaurqqJvZwd9fwKcaMGQUAtbWCGzdvKwLT0tPjExIAYPTIkSgkKemDRCIBAC9PT9VMUH8nl8sTk9TY8L8zmlR1s7Rt2xYTgoy7Tk6O6BVjwpU9sN69fw8Arq6uyASuDJlMdmvrCkrv0d/fj0gkCoXC/oOGXL9xs7ZWI0+uZunatQsA5OTkIg8mqLdcdvT19fDwIJPJEUoDCBQVFBiAycTTQ00r0tXVBYDK+t48ISERPbubG7bGoL7R8ni8zMxMTJRqEzUw0Ec/mnVn69zZz8rKEgDOX7ikCJTL5Tdv3wGA0aNGKELex8cDgJeXh2omrq4uaESImvoPRLXFfqNWoZbXr2MBwNXVRdWzgUAgoE87PiFeEUgkEhkMExMTY0xiOp2OfgiFQkwUg2Fia2PTWAE83DtgQgz0DQBAIpEoBlstKmRKaioAkEgkJ0dHTGLUIP/VtK69gUxNmZonJhKJZmZmmEACgWBiYlJQUFCm4kuGGcUjGAwGACgSFxeXAIBIJDI1V+8+AACFRUUymYxIJFZXV6NVNEwmQzUZk6nps1hbWXX26xQeEXnh4sXx48aiwJu3bgOAg0MbNOhD90U/zFWeGgBYLFb9IxRreN9vhyZV3Sx6erqYEPS56tc7RikgEIlQPzlAoLG2ubmaioL6ulJUlK2Nzbatf6745de0tLSZs+dSqVQfH+/uQUEDBvSzt7PTsLSqMBkMVxeXxKSkiMjo4cOGAEBYWDgA+Pl1otF02rVze/MmjsvlmpubA0B4ndQMxGSCppUYiESC8vMqHmTAoKFNlIfLLcB47hgaGGBzJtR1iM2eVY90JNt27Lxz9y6Ptxn11zGvXnG5XCKRqJiO1NTUIHdNtY2WQqEYGxkVFRf/8EaLvHiU+UatQi3o8Z89f8E04zSWhsstUP4zJSX12ImT0dExhYWFJaWlal1YlTFlYh9QGYzKAerbGKg0Mw0LWVpaCgDGRkYkEgmTRk9PT1tbW8NVBq2T1iU10QBHQ3R0dNSGU6kUABCJsKMtmpJ/l1JiKgCIhHVLSGt4PAAgEolstnkTt64VCOg0muLFUyhU1TRULTWBjfH/BVl2AAAgAElEQVTT2DHhEZERkVFZ2dnWVlZQr+lSTDQBQLFeQktbjcOhQmdbW6tmWcV3RpOqbpbGtA6aaCP4tbWgVCcYULhyRU2aML5rF/+/gg/euXu3pKQ0LCw8LCx8w8ZN3bsFbflzE0Z3pzlBgQGJSUlR0XVSMzwikkQi+fh4A4Bfx45v3sRFREYNHzY0Ly8/KzubQqH4+3f+jLvU8Pjoh5mZGZmM7aQUyOTYjrVFeh1VxowZtW3HTj6/9uat2z+NHQP1jTagaxfFGI5fX8laWthJf124NvZd/BAM1I1OvlGrUAW9QRpNx9gYO31UoKc0WDx/4eKSZSuQ5snCguPl6amrSweA8oqKuLi3ai9XaBHUoklLaFEhBbUCAKBQ1feBVCoVl5pfjRZ9xo3tliASiUHdV6oqRxWZKOSQLp0OADra2m9eRasmxqCwIYnFakpSq25RYGMMGjTw199W8fj8K1evLV28KD0jA+mslBcA0Ol1owSBOmWRohUqtDRNIG92KqEBTWSiSVV/U+g0HWhczYjCMRVla2Ozfeuf27Zsjot7+/DR4/shIe/exz9+8rRPvwHPHj9U1WpoQkBA1+CDh6KioqHeqOnh4Y688zt29A0+eCg8InL4sKHIqOnj7UVXN9poFl163VWnTxxzV1G1fTusraz8O/uFhUdcvnLtp7FjlNSzn4Z6iicSCNR/Dqgxf7dG2xiN9TzfolWogt6gf+fOZ/851WzizKyspct/kUgk3l5eO7ZvUdiPASAsLFyxzB3DF46QWlpINGcQN9JF//BB0hfSuuyaLUIsFqtdTVxWVgbqtKZI+4oBaRIU2lQzczMA4PH5mvjU6OnpIf2D2pxz8/KazUEBnUYbNGgg1I/Wr12/AQD+/p0Vq04BwIxV94lyCwpUcygorAtksepUMeg7UdvXVJRXaFiwz8tEk6r+pqDuDKPUUlBQUABKFaUMgUDw8HBfsXzpowchVy9foNNoZWXlwQcOfV4x/Dp1olAoiUlJVVVVyHLZ2c8PRXX09QWAiMhIAAgLDweAoCCselZDzMzr9CIK/6DvxtgxowHgZVhYaWlZVHQMl8ul02gD+vdXJNDV1UUSUW2jFYlESGPPMq2bmyo6d9UmV1GhaaP96nzdVqGKmZk5NHRna4Jbt+6IxWIikXjs70PKIhNaYv74DFpUSGMjY1QeVR+0ouJisVj81Yv3PfkXS00AiHv7DhOSlpaG5jQObbAOe2p1F0lJH5QTe3rU+SzEqmy1AwBIJaKATCbb2NgAQEJiomrimJhXzT+AEsgpMSExMS09/crVawCA8f90cXFGs1u1++DExsYBAIlEcnWpc01CidVuFvE69o2Gpfq8TDSp6m8K8jhITEpUdeIQiUTxCYmg5C8KAGKxWPXz7tqlC7LPJSQmfV4xaDQdH28vuVweFR2DjJqdO3VEUSYmxvb29ikpqWVl5ZGR0QAQFIB1BdIQF2cn5PQUq+6NqN1F6GsxaNBAOo0mk8nu3LuHGu2AAf1ptAamE/cO7QHg1etY1cvfvX+Piqcw3ivsGjUqp5SgDSu+J9+oVaji6ekOACmpqRgvegSm20HDcTbb3Nwca0V69Pjx1yqSKi0qJLKgS6XS5JQUTMqWdoytkO8tNZG7gaqL1+dx5uw5TMiVq9cBgEAgdO7sh4m6dOUK5r5hYeHIxaZrF38U4uPthaZ3e/bux4x25XL52HETugR2QxNBRBf/zgDw5OnTsrIGo7zIqOjEpJZ9VH5+nZBFc8vW7ampH7W1tQcNHKCcgEql9uvbBwDOnjuP0T2KxeJzFy4CQO9ePXV06lTTZmYsAODx+WlpDfZUe/X6tVq5q5bPy0STqv6mDB40EAD4/NoLFy9ioq5dv4E++8GDB6KQseMm2Ng7Xrx0WTUfZJZTtqAjjyShQNMGHBgYAACvX8dGREYRCISOSstI/Dr5AsD9kJC09HQjIyOF5GgpFApl4ID+AHDqn39UN1TbvXefWwfPjZv//LzMm0ahI7l+/eat27ehoXoWMWTwIAAID49ITsZ2oKdOnwEABsOks18nFKJQqLx912BAXFlZee7cha//AI3zTVsFBrSSSigUqp6aUllZ6e7pM3jocEV/gkZI5WXlGA+g2Ng3Fy9dQb+F6kwkX0iLCunfue6ForGUMseOn/zqZfvOfG+pibxkRSJR6IOHoLR51WdAp9EeP3m6c/cexXz/fkjo3v1/AcDQIYOZDKyGViaTz547XyHeUlJSFy9dDgAcDrtvn94okEgkrvrtVwB48fLlgoWLS0pKUXheXv6cefOfPX+RmvpRednZxAnjAYDPr50+a3Z+fj4AyGSyx0+ezpg5W3knKk0gEAhjRo+CevWs8i56CpYtXUyhUHJz82bPnV9aWoYCy8rK5/+8KC0tjUwmr1i+VJG4U/205tf//Bc9iEwmCw19MGnyNM2Pkfm8TDSp6m+Kk5Pj8GFDAeD3dRsU6zIB4MHDR//57xoAGDRwgFv9yhaHNm1EItFvq1ZfuHhJMTfl8fnHjp9A72LggH6KHFADfvzkCZ9fK5FImnVqQKv67t67n5+f39bV1UDJbRUpaY/8fQwAArp2UXXo15zly5bo6GiXlpaN/mn8hw/JdY/A4+3es2/L1u2FhYUKFehXB+lIXrx8WVpaZmZmpjoqGjN6tK2NjVwunzJ9hqJsYrF43/7gc+cvAMDypUsUS4ksLDiWlhYAsHP3HkUXnJCYOGrsODs7W/iOfNNWgcHO1nbC+J8AYNv2nQcOHVZc/uZN3LARowuLijKzshVrl9FCcB6fv2PnbsWi0ouXLo8c85Pi81erdfhCWlRIFovVp3dvAAg+cAhtJAQAJSWlS5etiE+Ix6xu/9fxvb2B/Dp11NLSEgqF4ydOJpPJbdu6Pgy51/xl6tDS1tr0x4Z5Cxbu3bvfysqqvKIC2ausrCw3/rFeNf2GdWuXrVjp2q6DnZ2tVCJFe0BraWkF79+nvP5v5IjhaWnp23fuunjp8pWr1yw4HIFAgOZJRCJx25bNbkrrCDu0b/fzgnn79ge/fBnWwdPHxMSYz+fX1go8PNynTZmM9qPS/InGjB61dXvdztGjVJbnA4CLs/Nf+/bM/3nR3Xv3Q0If2NvbyWSyjIxMqVRKoVD2793dzu3TztTWVlbjfhp79tz5p8+eu7i1ZzBMeDxeba1g2NAhffv0iYyKljZUqqjl8zLRsKq/Kdu2bM7Pz4+Mip44eSqDYcIyZRUUFqChRkdfH+VDFlf+sjz61avY2DcLFi5etGQZw8QEAErLypDSafiwoWg0g+gWFJia+jE8ItLG3oFAIJw+cax3715NFMO9Qwd9fX20EbafX0flKDTvRG5fgSorNVuEvZ3d34cPzZg1Oy7ubdeg7mZmZhQKmcstQI8wZvSo6dOmfEn+TYB0JGi70RHDh6nKfhpN5+SJo6PGjPv4Ma1rUHdrKysajZaVnYV8wmdMnzptaoOy/frLivk/L8rLyw/s1hMNMiorKx0dHfbu2okObJBKvqHOWcE3bRWqbNywgcstePT4yZq16zb/ucXczLysvByZco2MjE4cPaJYedyndy8vT8/XsbFbt+84cfIUk8nMzsmprq6eNGH8kkULz5+/mJ6RsfK3VcdPnNq6ZZOPt5qV05+N5oUEgE1/rH/z5k1RcfHc+T8vWbYC7aJMIpEOHwze9OdWtCnVVyzb9+R7zzVZLNbhg8FoLwJdXd126tZla4hUKhsxfNi1K5e6dOlSXFJcWlpqYcGZMX3qw5B7qhNNALC3t3sUen/c2DG1tbU5ubkMhsmggQNC799RaIcUrPxl+f27t0aOGG5ubsYtKKiorLSztZ00Yfyzxw8nTZyASbzmv6sOBu/39fGh0+l8Pt/CwmLZksU3rl4xMTEBAEFLlDZWVpb+nf0AgMEw6daIb8iwoUNePH00aeIEK0vL7Oyc3Nw8G2vrKZMnvXz+BM2ulNm5feua/65ydnbS0tKqrRXY29n/uemPg8H7kTucULMj2z4jE82r+tuhr69/7cqlnTu2+ft3lkplH5KT5XJ51y5ddu/ccePaFeU5n66u7q3rV7f+ualLF39zc7Oq6qqy8nImk9m/X99TJ44dOvCXsv/hL8uXDR82xMDAgEql2lhbN+vcRCKRutSvJ/Hr1ODxbW1sWPXLBLuprNRsKb179Yx4+WLOrJmOjg5VVZVcboGJiUn/fn3PnTm9f+/uL3ehbAyFjgSUNjfA4OLs/PLZ4xXLlrZzcyspLf2YlqavbzBk8KBrly9u3vgHpmyjR408efxop46+dDpdIBAYGxktmD/vzs3raA4K30b9qMo3bRWq0Gg6586cPnwwuGeP7nQ6PSs7WywWt3NzW7ZkccTL556en/aIIJFIly+emzNrpqWlRVl5eWFRYft2bocPBu/YvhUA9u7Z5ezshFaTq10A9iVoXkgAsLKyfPTg/qQJ49FZAgQCoXevnteuXBo8aCBaii34Sna67w/h3yjwDx4+snrN73p6eumpze+D8z4+vnvPPgDw+GGI8lSsdTJ+4uTQBw/nzp61ft3aH12WFvPvqmqcrwU69qd9O7dHD0KaT42D8y/n3+1D+z9GaupHtNOs6owWB6d1IpFIDv99FAAmT570o8uCg/M9wKVma0Eul6/5fZ1cLu/bp3dLPYlwcH4UwQcO5eXlmzKZqhvl4+D8T4JLzVZBeXn5z4uWPHz0mEKh/Pc/v/3o4uDgNI9IJDp4+Aha0/Lrr7+obpSPg/M/SevaUe//ITdu3lr13zWKndk3b9yATp/HwWm1FBQU9Ozdr7yiAu0oMnzY0Injx/3oQuHgfCdwqfmDIRKJxSUlFArF1cV52dIlaB8DHJzWDIFIrKyqkkgk1lZWkyZOmD8PezojDs7/MP9KH1ocHBwcHJwfAm7XxMHBwcHB0RRcauLg4ODg4GgKLjVxcHBwcHA0BZeaODg4ODg4moJLTRwcHBwcHE3BpaZGTJw8lWnGmTh56o8uCA4ODg7Oj+R7r9d89PjJ2HHqN1klEAj6+vr29nYBXbtMmjBBccQBhvCIyJOnTkfHxBQXlxAIBJapqY+P9/ifxnbR7Ljj9X9s3Lc/WDWcRCIZGOg7Ozn17NFj4oRxhoaGmj/U5/F5VTFn3gLVg14bY8zoUfv37gYAsVjMtrQBgAXz561dvepLi46Dg4Pz/5VWNNeUy+WVlZWxsW9279nnHxB4+cpVTAKZTLb8l1+HDBtx9dr13Nw8oVAoEAiysrMvX7k6bOTonxctQWeffh5SqbSsrDw8InL9Hxv9uwZFx8R82dN8Ec1WRUtRnGpJ/V7HW+Lg4OD8T/LD9gY6c/qkl6encohAIMjLz4uMjN73V3BFRcX8nxfZ2doqn9m2ecvWk6dOA4Czs9PMGdMdHRxkUumH5OTDR46mpaefv3DRgsNZ+ctyTe5OJBIT379VDhGJhDm5uXfu3Dty9FhRcfG4CZMjw14wGCZf41mboUVVsXHD+v/8ulI5cXRMzNz5PwPAoQPB3l4N8qHT6YrfZDJZIpFQqLjUxMHBwfl8fpjU1NfXNzExxgRyOGxfH5++fXr36N1XIBDs3rvv1IljKIrL5e7/6wAA9O7V8/TJ44oj4zt39pswftzI0WMjIqMOHDq8ZPFCKpWqSQFU725ubu7r49Oxo+/kqdMrKyuPnzy5YtnSL3pIzWhRVZiYGGMSZ2Rmoh8sU6aVlWVjd6FSKRKJhErRqHJwcHBwcNTSijS0ChwdHfr36wMAEZFRisDbd+5JJBIA2Ll9q0JkIqhU6qKFPwMAj8f7kJzyhXfv368vOqgrIiKq6ZSVlZXbtu/s2aefbRsnM46VW3uPvv0HHTx8pLKy8gvLoEBtVXweFAoVAPC5Jg4ODs6X0Ep3bzc3ZwOAsvgxNzebN2e2sbExi8VSTW/B4aAfPB7vy+9uweF8/JhWWVnRRJq8vPyBQ4bm5uYBgL6+PofDLisrfx0b+zo29tDhI7dvXOdw2F9eElBXFZ8Hsmjidk0cHBycL6GVSs3MzEwAUBaQAwf0Hzigf2PpP6aloR9Wlo2qKDUnn8sFAAaD0USajZv/zM3NY7PZx/8+jCyOcrk8IjJq4aIlWdnZa35fd/TIoS8vCairis+DTKGAklsQDg4ODs5n0Bo1tIlJSSGhDwCge7cgTdKLxeLtO3ah9F8+w3vx8mVKSioABAZ0bSJZWHgEAMyaMU3hr0QgEDr7ddqza4dfp45fa+FKS6uiCai41MTBwcH5YlrRXFMqlRYUFN4PCflz63aJREKj6SxauKDZq6qrq2fMmhOf8H/s3Xd8HMXdOP6Z2Xp7/U53p5NOXbKKi9x7wTbFpoQeElrCk4T05IHUJ70R8k2e5EmBhJAGpBBIQjXFFfeCu2VbVu/ldL3sbZ/5/eH8CMjGCAO2Seb90h/Wafezs7Pn/ezszs4c83q993z3O2e9dcMwhoaHX3hx7Q9/9GMAQDAQuO3WW86w/MkZ1mLxxLjPFy1a+Myit/qiyNlVxZmdfKI5wa5SFEVR1Gmdt6x51dXXnuGvHo/nd795oLqq6sxBDh06/OE7P9bX319WFvnjw3842YtnIjDGgeLS1/trKBj80yMPOZ3OM0RYtnTJXx97/P5f/sow9A/efntdXe0EN32qt6Uq3tDJ3rO0rUlRFPVWXEBtzZNqqqtvufn9t9z8fp/Pe+Yln3/hxQ/f+THDMC695OL7fv5Tr/cNln9DDMM01NdfcfnqD3/ojjeM9u1vfuPYseMtR48++JvfPfib30UipcuWLrn0kktWrlguCMJbLMlJE6+KiaBtTYqiqLfuvGXNvz326JzZs179yYfv/NiGjZsKivLBD9x25nYeAKC7p+dkyvzgB27/f/feM+5dlDeEEGpvPfrqTxiGcTgcE4/g83nXvfjcP5548uFH/rRv//7BwaE//+Wvf/7LX30+7+fvvvsjH/6viYd6i1UxQRzLAQBY9oK7TqIoinoXOW+9gURRtL/Wvd//niAIIyMj3/ne999w9ft/+YBhGA0N9ffe8903mzJPcr/Wm0qZJ7Ese9N7b3x+zdMnjrX86v5fXHftNQ6HI5lMfeVrX7/n3h9MPM5brIoJ4v/Z1qR3aCmKos7eBdSHtrKi4rOf/hQA4KGHH9nz8hsMA9vR0SFJtitWr74QGk8+n/eG66/79a/ubzm0/5qr3wMAuO/+X6VSqbMO+KaqYoKmTZ06d84cn2/8IEQURVHUxF1AWRMA8OlPfaKyogIAcNfnPq/r+hmWfOapJ/q6O7/8pS+cq6Kdhqqq4z5xOBzf+863AACmabZ3dL6V4BOvign67ne+9dyzT02ZPPmth6IoivqPdWFlTVEUf3DvPQCAjo7On/zfz853cV7XuvUbps2YvWTZilNnWSkoysl/2Gy2t7KJd0tVUBRF/Ue5sLImAGDliuVXXL4aAPCzX9x34kTb6y32vptvve6Gm379m9+ew6L9S3PztHQ61dvX94E7PtzxqjbliRNtn/jkZwAAFeXlUyY3vcWtTLAqJkIuFK674abrbrjpscf/9hZLRVEU9Z/sgsuaAIB7vvsdSbKZpvnfd38eY3zaZbZt3/HKID7nXigY/L8f/y/LsmvXrVu4ZFlVbf30WXOq6xqWXLRi3/79LpfrgV/dd3Z9lMaZSFVMhGkY27Zv37Z9e19f/1svFUVR1H+sCzFrlpaWfP7uuwEA+w8c+O3v/nC+i3N611937aYNa2+/9Zb6+kk8z42ORgkhzdOm/vdnP71rx9bZs2a9cYgJeFdUBUVR1H8OeHJkOIqiKIqi3tCF2NakKIqiqAsTzZoURVEUNVE0a1IURVHURNGsSVEURVETRbMmRVEURU0UzZoURVEUNVE0a1IURVHURNGsSVEURVETRbMmRVEURU0UzZoURVEUNVE0a1IURVHURNGsSVEURVETRbMmRVEURU0UzZoURVEUNVE0a1IURVHURNGsSVEURVETxZ7LjY0kMudycxRFURR1WmG/++xWhISQt7coFAUAGElkzvpLSVEUdcGid2gpiqIoaqJo1qQoiqKoiaJZk6IoiqImimZNiqIoipoomjUpiqIoaqJo1qQoiqKoiTqn72v+4qHHW050nfw3w6CAz3vx4jlL5814veW3vXyopiJSEip6W7ZuWfj5l3Zetmwez3FvS8AJOrnX93/vCxz7r9resvvAn59a+8WP3VpbWfa57/2sNBS4+yM3n8tSURRFUWfhPLQ1r1110Q2Xr7hy5WJCyJ+efLGtu/+0ixUU9S9PrR0Zi79d2z3W3v3shm26brxdAd+KpknVH73l2uLg23NBQFEURZ0b57StedLFi+ecbHWVlxT/4qHHu/uH6qvLh6Pxvzy1tndwxO1y3Hz1pSWhwJfuvQ8A8Os/P7lo9rQd+47813uvmj9zyp+fWrtl94Fbrrls2fyZT764ecP2vT/79t1j8dSr1508qRoAsGbj9m0vH5ILyswpDbddv3p/y4nfP/YsAODu7/7sM3fcFPB7/vLU2u7+YY5l5s2YfMMVKxl0Ti8gjrd3v9LWfOXDbS8f+uMTL/zXTVfNnzFlXPk5lo3Gk+e3zBRFUdR5OO0mUplEKjMaS+w5dBQAUBoKYEx++cjfE+nM5z96S11l2a///KTA8++98mIAwHWrl7/nkqV2ydY3NAIA6Owd8LicXX1DAIDewZGq8hIE0bh1Nd3YdaDlmfXbFs1u/vQdNx081r5u656p9TXzZkwGANz14ffXVJQ+9uyGZDr72f967/vec+mOfUcOH+849/UwTu/gyKNPr7tkydz5M6acWn4AwAVYZoqiqP8056Gt+Y0fP/jPbbPMqmXzpzXWDgxHxxKp1RctqIyEL1s2b+f+I8c7eoJ+LwAg4PN43c6aitK+oVFF1YajsetXr9iy5yAAoG9odPmCWUOjY+PWbTnRdeBoGwBg9fIFHMtObah++dDxK1YscjnsAICycNAmChjjnFwYGBlrrK38+bc/d+4rYRxZUR/40xMVkeLrV68AAJy2/Bdamd85aj7fuXNn7PgRNR3LjcaBBkJllULA5582uWL2HN5uP7uwmqbFo9FsOp3KpI+2tHR2diLEeNzuGbNmX7RiuSCKZxfW0rXRlgOp+OCXv33P8hkLP3rFqpFoe1uh4J08a9GySwDkzy6sqmkn2ruPt3fFUqlcNgks3e12e7yBxvr6yZNqbKJwdmEVVTl86Mgjjzza1dUfjSV0rVBa4n/vjVc1NU2ZNm2m0+U8u7DvkFwu9+yaNU8//cxA/4Bpmu973/vy+Xw4HK6vr5s9a5Z0tt+EbC6/YeOOzdu2VlQFK8vDNpYJB/ySxBUFSjz+CMOcZb+Hgixv2bhu26b1A90diVgUQlgUCpVX1i5eeeniZSvtzgurbqmzdh6y5p03X8sw6MkXN+fkwurlCwEABUUFAKzbtmfjjn0nl0mmM8UB/yur1FaWPbdxe0fvgNNuXzBz6t+f39QzMFxQ1LqqstOue/LDu779UwCAZVkMw4wrww2Xr3jo7889+vQ6AEBpceATt98Q8Hne6R0/g4HhKMMg3TA1XbeJwmnLf6GV+Z0gp1MbH/njjieflRhUWlHs83tMlkMQqaqW6+45tnsb/9uHpl95Rf3qVfybOb9nMpn29s5jx44d2r/v4KFD/f0D2WyWEIIQhBAyiOE54c6P3fn5L35efDO5Mx6P/fLnPz3w0pqlVRVV1ZPu/9pXvA6hreXwkda2xgULnSinJx9mbNWMbR6AjomHzcmFLTtfPnhgn5rPd3R1j4yNWnoBYsPpdIXLaluOtxGGmT+j+ZJlC12ONxM2n336+TUHjrYMdg8e2N8i2pz1DY35XCadGm3r6t6wacOB/W0f+/idt99+a6Do/D9uV1V1+/btP/3pT1tbW6PRqGmafr//yJFDxMJ9Pd0vPr+G5bnLLlt1/fXXu91vYrjjWDx+3/2/f/TRJ/WCzomAE7BoE8vLKm68/j2VFf5E9iDf1xoMVYbDNRz3Jq5Lstns7r07//Tgr4Z7ui1ds4m82+2qqa56ee++0aHBXVs3/ULgVl938813fMTrP/91S71F5yFrNjfVcixLCH7gT08+t2nHDZev8LidAICl82asXDTn5DJ2m3jyNuxJdZURTTd27D1SWxlxOqSAz7Npxz4IYU1FaTqbP3XdvqFRCOHXPnMHep0nf5Fw8Cuf/GBOlo+19/zpyRfWbtl967Wr3tndPqOyktDNV1/2/371yPMv7bx+9XKPy3lq+S+0Mr/tBg/se/HnPxkeS2AENUEyba7hvNrT08Oz4sc/cmUuOQa7BNMEQ0daOnftmXPbLZFZr9v7+tVSqfS2bdvvuuuufD6PECMIYl5WOF40TdO0LNM0IbQwAr/45X0bNq5/7PHHQ6HQRMJu3LTps5/9ajIzYhdTH33vNZfOW5kf6e84enDtvgPYFtn/5PpVl86sqy/GagvWD0NpNcs3TiTs8Y6ex596gZgFOTl6aOfmnFzgbTbGMi1dSSTHhrp7J8+YV9bQtHn7rm27Xv7A+66fMWVCYVuOt2zY+dK+A4fCxSWKoVfUVFZU1DIsW1wSxLhCMUwk2L1FgUf+8vhvHvnjz3/8o0tXrphI2HdIMpncv39/NBqtqanJZ3PFocDhw4cz6WRvT1cwGMTYJIDIsvbUU09s2rTpM5/5zNy5cycSdsOGzXd/6ksMNEM2jpck1dBMxOkK390ef+yxtZ/8zG0OhwQBScQGY7Gh2toZbveEMtyOrZv/9tyToeKgaeoAGzOnTx0aGli6aEF5efnw8BDDcoNDw6apP/X4wy889+T/fOveRctWvrXqoc4z5lvf+tY529jLh46NxVNXrFjEIFQcKDrS2nGktXP+zClFPs/BY20j0fik6vKjbV1rNm5vrK0yLWv3gaM8xxUHfCXFgbVbd4+MxRfPaa6pKO0dHNnX0loWDi1fONtuE09d10AgkRQAACAASURBVOWU9h1plWyiQ7I9vmZDMpWdUl/T2TvY0TPgdjl9Htf373u4pa2rvLSYQejg0ba6yrLGuqp3dK8Fnu/pH+7qG+rqG0IIZXL5lhNdi2ZP83nc67bu8XvcV6xYNByN79rfMn/mFMkmjCv/5EnV3/zJb85Zmd+6vKI5pQm32wjpX7eu79kn7ZJkcbzKMK6SisOtrc+sf1ElxOb1eUPBUGnpzNkzamc0h2uqJY+7/8gRbBre8nIA4RkCDwwM9vcP/PKXv+zv79d1nUCIEDR1XeQFyzJ1XWc5lkCim6qmq4lE4qVNL1100UVer/eMhSUP/Pahr37/B94Qvvm6uTddMn9+3eSeY8c6u9v+vnHz+kMdps2XiA6nh9uWXdzM8ogwlqEdwcRiuUoAzlTabXsO/u3Z9cTUdDnV235k7uTaqY2Tli9ZMHVSbSTg87udAst2dXZyNofH67FMvGPvAb/fX15afObS/uqhB//vt/cXBYuHhkfsdqfX7uZZbmCgHxtWPpvNJBIMAJLNTgDIyoVEMv3UmmcFkZs7axY8Y92+Q4aGhqLRKMMwPT09HMeVl5cihIaGhkzTVBSlpCSCCQAQmRbABFiWtWXbZo7lGhubzlBaQsh9P3ngR1//UUOkuDroqCl21BcHw26X1+nBBmPqMJNM+V3ipNoyhgAGMgSDTDoJEHI4ztSQJYQ8+Kv7fvjjnwSrqgSeT46M6LnUjddfu2jh/PJIqcDz9Q31U6c2Hz16NCfnNQzzmrl+7QsshM0zZ5+XuqXeFucta0IIvG7X7oNHc7I8a2pDY21lZ+/guq17hqPxixbMbG6qcznsx9u7W7t6baLYVFd1rL0nmc5cc9kyj8uZzctHWjvnNDdOnlQNITx13XCwiOO47XsP7dh32O91X7fqIskm2m3i4eMdR9s6J1VXNDfVHTzWtnbL7sOtHdMaaq+/fAXLjr+L+/bu9YnO3uMdPSd/An4vx7Kvzpouh33BrKllJaGXdu1LZ/NXrlx8avnDoaJzVua37k1lzZGDB8ZeWu/1uZDAJXXdEO2PPb+us6erorzs8iuvuubGG6dOb355946tmzclUwnRxpeUlVQ31HkkUcOYc7zurdpEItHb2z8yMvLwww8nk0lRFJGpQ1NHpiEhBAxNYJFlGcTSCcYMghDAeCwh5/PTp08/wxO+AydOPPTMby+/ZNI3Pn97Y02RnBkZO9zFOpgxhtF8DSVNi1taDjeWe6tD7rnLJiMWQwQIIIbVDaGdYUtfL+yx9q71W/doms4A88ThPbffePWK+bNmNU+rqaquKiurKY9EQsUEAJblDrW21VTXYAwwAClZdbucxUW+1wv71Itrvvb/vqfpliBISl5VcnK0pz+XSBX7vHaOExE0FUVADAOQzWEvLi7NZfOEWPsOvdzY1FBdca4vy0ZHR+PxOMMwo6OjGOPS0tJAkb+3t1eWC2OxhG5YDodblByWBVXN0nRT4EWCccvRI6FgcVXV65b2qb898YefPDBvSmNDpKjYgYrtrF8Q3XbR6/K6HJ5sPO1gkVcADRVhm9OJEAsJAgipqsrxos0mvV7YPfv3bt6+p6apOVI3SeD5aXU1KxfOddhFj8vp8Ti9Pi/DsCYhJaURf0m5pzhSUjnJX1LePzjg9/nKyyvemSqk3nF0fk3qHTHx+TXTQ4Prf/CNSDgY8LpH07m/b97ekcgd7RusDAQ+c8cHFy5c6AoUMTwHObTzmafSg4OJeNLldpdVVYVKS73BgKt5DnO685qiqEeOtAAAnn322T/+8Y+FQgEB4oTmRQsX5VOZ1FhMluVEJq0DrGFTsYiFMWRYnhcV1fjCl/7ns3d/xnW6xNnV03fVtVd+5wcfnjx9iiYjHg+k+tfxfYGSphn7R7QthzMBb1nXwbX57r3LZtbfftclvB0T1jCAjomBrYLd8ymGPc0d4Hgq/du/PI0JyGUzREm3H9j69bs/HnQ7JLtLMzCwsJxNx+OxE509+46eeGnfkeY5C4ojlbJuRSpqEMPc+f73FHlPU9sdPV0r33etppkcQsWBYpHhnYL4nqXLZ06bZupaQZaTiUQmk8kVCnKh0D40yHBSa2tnQc04vdzMOdM//6kvVVVUTuQgvi1SqdTOnTsNw4AQEkL6+/urqqoCRb6Wo8ceeODBru4+lhUam6ZOqm+KRCIsK3R2tm3ZsoFFuG5SlcgLv/jFLyKRyKlhu7s6b7zs6osXL/eLggMZnJnlgAmASHjeYHgNSMeO9uST6WmNZUuWzHA21Ygup2FZhOEgxwOGra1r4NjT9A8aGB7++P98xS24/cXhSG25hyd+S3UxenGR3+1xWpZlYWARaFgknSuMpvPb9x82kA1DFhJTzuXu/dbXS4rPdJOAumCd07Ym9Z9j4m3NrQ/+TM7HAmG/w+OIZrMv7tjVEY2aiEypqbxk3jyfTWIgAgge3LWDB1jEeknI73Q5Orvae3v7ctkcC6H3dGf27u5uVdUQQocOHTp+/LimaTzLLGiounrl8lKve3JlRcjtlHjGLjIcJAhxEENsWoQAjhP7BgYWzF8YKTtNu/Br3/jCB+5YOWfGQs5iCe7CoIu18Ws3t2w51Nc5aioGq6iZ7tYDajIWLnLPWljNiZAgEwOCAQAEYyPG26afGvb5l7YnMzlMkKFr+eSYnh1bPGeaw+biRIdpItPECAIEmbymj4zF+0eihIBAOGJi4PL4IEJZuTC57jSVcNc3v9I10GeaFjEBMK1if+CDN9+6ctEij9PudTnKSgJNjXUzmqdOmdxUVV3Ji8LYaHywb5gQIxLxRyKhXbv3XXbxpRM5iG+Lhx56KJVKxWKxcDhcKBRqa2tbW1tTqaTkcEHEaTr++CfvmjJtVlEwItm9DpunKBDUdPV461FdVYIBfywWX7p06alhv/zlb5omVFW1IOcFjhM5iWEcMrYlC1pW1yDHQQvaAFMVDM+eNs1dXowRMEyMGJbleIblEctKNtupYX/76GOJbM4uOl1Ol93Oi0QV1JxL4gEEhXwhJ8uaZugmtggEkCEMm86rso5Fu5MgBkOYluW5zdPe+Uql3n7noTcQRb1Cz2aGjrzsiARYt8h77P37R1Jy3oQwkU7n0sn48NBoV1fexMtXX9Z54kRleSgmx+rqGwKhkkhjXXfXQGmkXDAVQ1G4157XTMNMJtMAIQaidDoDIJJsdoFYU2urWEt1cUBTNQ8HyrwOO0/sAuNSYSKbT2byed0ADCaWpSiarus8/5r3RuLxhM15eMnSSqB36IaNF4YYEC+oyF0fyfW5d65rqW+sFb1iRXl5S08X4iTLMgAkJx9lIggJZiz9BLYyiHlNu1AuKB09/QAyBBACCAAkMRa1dJ1hBU2zAGQQw+uGdvRE677Dh+PpnEsSU8kEg155MAY7evrzBcUhvaYS4snk5j07GYZhGOx0OKrCZaWBcFm4VNcUDgJRQDyPEMQW0SU7F+KLZk2f2tMxyGAMGGATeJ/b/fja58ZisWAg8PYf+FOk0+k1a9ZMnz597ty5kiTZ7fbh4eHS0lJFVRLJpL8oIIh2hhMYRmIAixCrKxrH2qZOmXnwwMtjY9GqyrJ9+15OpVLjnkknkulte455naLHK8aymUxPvqmy1s7bOgaiWTXJ2QDDZUv9pXyB1FVOkjNakBfzisULEgaQQQxkGEM3yCmPo/OyPJZKR0rLWAsiSHQ5q8MCx6NCQUmlkjzPm6ZpWgSxPGR5u9OlW6CstERHScLxBNhESegbiZ56yKh3BTq4DHU+9R86lIKMLPF6kTvGM4OKkjFMVTWABQSG52xc+9hA0+yZWk69+X23zL/0ouoZdf7GSmd9vb24urioKuwJ2d220aH2cWGzibQOocqxhoVSqQJjc/BQqJICEV+xYRqJfCqv501N5g3DiRifwAd4s1iCAbfAQgyxFQgUsSyMnTKaY+uxnR++aZWkZ0XSKzL9IoNZk3OyuD5oasrozTff7EFo3qS6VDROOOQJ8IBTLKAwAAsA8pgwFkYEmeqxcWHbe/ogBBhgAi3T0gkACLJytrBp49q//PG3ba0HdC1z4OC+3S/vJYZZJNk9EueSBI4TCWARQIhYDCTtPeNHplyzaT0riALD2nhGFKBd4gJuJ6OqiBgswqaimgVDL2jAJKZh6JrCWoylq7yAAbT8/oBlQks3tm3Z9vYe8deza9cuSbQXCuqJtg7LIvmsDC3gc3skm93psIsiJwhcLiczrGAQYkJMEFYNS9FwZWU9ZIS+/kGE+D27944Lu2XX3oqKYNDNmWqKd3K607G9c2Bza7/hEnmfqypSVVFX3wesDLHqGxuEsiKdFzXI6hgAhgUE8ZDjAcSmOS7s8a5uUbS77C7RaQc8FDnIQoaXXB6Xp7S4tNgfCAWCkZLSkuKwjeML+cJYXlYAcAV8Drfd6bSHgkG/L9DWM3Bu6pZ6e9GsSZ1PO7bvGCYoK3DAJTF2cWB4WFdUkWEFSNRCxiYwn/rohydPqpNjqcGO7mQ0qXGY8Yicx55WZbvPDZxcjlOiua5xYVOxBECAIViwrIjHg3QdYOPG669zu4osixNEl2URWVYszSQGNjRDNwyGZW02iWFZHVuzZs/RDXMslhgX9sjxp3xhYKIcFPKQS0ImBzkDcGYgaCZSXQcP733/zR88sL8lnhwGbKx+uovYsI6ICrAGiAEBYVnE8Hrh6Liwxzt6AYAAEAiATZQEThB4gWF4m8A7JBvPQIFjO9vamuonzZw2vSQUDBcX87xoGCY82QQiAIDTZM2XNm80kkmkK0GPa+VFS2dOnxqPj3ACg3UTG5aAWIgJMAnRDY5heYbV1EImHbeIaWKTl6RUNq8a5uZtp8+asqbmNeXN9opIK3JSzp12nW1bN+uG0t/fa1r64ZZDspI3idHR0cZzbGlJWM7nJUnEmGiazjBMdHREEAVN1/K5PM8LTpdrLBZTlMKePXvGhd25dev8KY2V3qJqf0lQdIfsrrpIaSTgZRHgWUZiWQbDyU1N9bU1fR2d4dKwIAosgxjIAAARQhBCACE2rXFhD7d1AobBgAAIESDAMkqCwXAo6PP5fH6/2+d3u71Op9PucJSVlxcVFZWVlmJsGSbWDGxgoBqmYRonunvfVO1RFwh6h5Y6n46OZYYAwxrGmCIzudjQUL/I8Sbkiv0ep13avWuHXeBryyd5RXZ0aMhvLzE4mJbzBMRSyVR5IJRDal5QRtXx1+xZRYEQI9WQVNAUDLyo5MLh4lBJkRyLd/YOBos8vM0j2ZWslhY5BHXTAIasaQbhAGQIwfWNTQTCVCY3LmxpSQERYuP8mooZyBKAAfZiC2NkmzevfGQkuObFdSaBLpsUckRKi6rYXIRRRYRYBjCIEFPRLF0DFgSvveU5Gs8AgBAhGBAGwGAwULpseTBU3FhfWygUCACGUrALIrAsn9ftcruODwxxot20CAEQQHIybQ5FY+NKO6upzi+xwWAQ8azT49FkjUPk+JGDei7PElAWLomUhnPZXE9fr+SS/MUhxPHpVEIp5FVi+APBaGwMM9yR1tMM3DiUivMsxyCYyGcr/G/weuvJzAoh/MehbZ/4288Ny/z+lR/62OIrxy12vPUYBpZukK3bd1gWqaoomz5tqtfjAQR0drYfPXp4yuTZxLQMTYWmhQjQdd2yzGwua5hGVWVl24n0yMjwida2cWHLfNJYV3/E6cknc3bOLhtawOfIZXLEYbeJLgdAlihU1tZcdtV7Y1t3qKYOLRESwrHIwhYA3MnyW6bJgdcMejAYi2EAACEIEgBMgeWrykudkCCWUeQCgNiwTAAYXuJF0eEvLk0pakYxk0MJyNsMQ4fYAgAPRkfPXHXUhYlmTep8qmycaQxzohtkFXW4tVUu5DHBDGJzspwu6P0j0dHBwSLepmpGKFwUiISHR0e99qLuIx0hVwlCSGVIIp/rHewDc14TVrVMjLATkdZdO92WsWz6ZCLyJ04c0VSQNciuDZv9dtHHcTaeUw0jZ1kFk2gWAhyLWCboC9TU1BgYjG9fADC/cqE9JzIW4iGPCdZM3TChkifdg6ne7kxZRXlbdO+85ik+zLswEpPNJOeGrAgAsiyATYILpllQdUV1zHxNWMPEgCBILEQAwRhCpqpukm4RlkE2gctlZQhAkc+zY8cup91hczll3XT7/YjliGkAQAAkBEDjlPZQOOTnGFxaWmpBCCHShAKqrHSz3GAmZzEok0xMbWzIJFPpRDyZAoW8XFFdNad5WmlZ2ZpN60SOT6dymmZqBh4X1sIYQRhwugEAiqE/cWg7w5zpllVSzv390JY7F1757RceGZMzAIDvrf3T7fMukV47+M7Le/fWVNc7Xb6ScKS6ptY0tHhC7u4ZItiAEJeURAABLMMYhpFLZooCPsPUFEUhhOiaFgx5HA5HMpk0jPEzGs1orjuhKtneBDKwpsgCzzKmEnQLg5kMUoDFC4BjSgK+5OhoNpFgow4kAWzqvGAzTQwsfJJlntI8JiYCSGBYjC3DNKc0NSv5bDqVkHVTluWCLANAIGIgw4kOFyuITqczEi7tj+Vk3YAEQwIgJBY+9StGvQuc66yZUvEPdqfW9hSyGg472JnFwhfnecqc/yxGb8b86b70ziF1rGD5RGZJRPzvOZ4q97s+tZ9hr295NrplQD11lWVl4p+vmtAgNe9qbperGlU4fKbEWOl4Ss4rigF5HjKM/WjXoFbI13b18FgXPU7OZsW6TW+gpHVvmws4fILDAhBDNpvRzOz4F8YtAAABLCaF+Fh1SXGJ1+UtLe461jGaUjxB/2g6oWq8q7x8LJ/vj47kDF0pqBAxnI1AjKc21TMQKIbJCuNfh01tiSBPscg7AMYAEs3AWU2Na/mozhCNtB09VllR3Hro8KqG5V6jiB8NIQ4zggAhAy0ADQAUi8kLHD7NMHgEEAZCQgixIOG5ggkNhhsdiyViUY/Tk06nhweH3G73WDzmsCze5ghX1OQNbGFCMEEMxACc+vIu55REwyXYHRhAYFq8ABzhSE2wJOh0KYrMMiyxzHAoYDU18gIfLA4Zprl4zpydhw6HvH6XZM+nshzk0CkndgiBSfAr5RZZPlPIF7v9qUKOYxi7KDEAapZZ7gtIvAAASBXy6UJuakmVV3ICQgCELlFi0fjS1tVM7u0fmj6jYsqUuSwnCCIPicVy0ehIr24YumEIok6AKtpEt8dtmoZu6ghBQeAVpVBaMik6Ejhx/LiFx2dNHauaqbI2VjQsBvMG1lRN1hUsAuTgBTvHMDY+VOQ/+LcX3elMoiVVU7IUAcvQCojhEAKGYbCcoFvmuBFvc7ERiGEBMBgCu8QODgxyak6ORTWGKeTykigG/H4Lg+FYnKSziBd4BvmyBQeH0skEQpAAYgGgqcqp3wTqwndOE5Jikiv/PtKX/eej9b6s2Zc1dw6qG99f4hFQf9a8+omRhPLP/5BjBesf7fLGPmXj+0tC0oX7Ov8bOvNen9+ynXeWlsokR3z+ALSInNV0HTOcqOgqhwTB4c5qFssLiVTSYWeLfd6UDrSuuM1kAgEfQkRlcVotZNOa65Q3IAVWVBXVwIYo8vv37bFJqDZSWu7wHu8a6B0dCLjtRR6n02nXNS2dzysQIMRACCHAXre9qqw0n4nzDg/HjT86TtUnxh0cz0FiAACxRVhcgDh1+Yr5sVR64+YNR/fsKeGcPiiU2z085g3DtE5GxgiagBgAmByxjR/P3SGJ+ZwGASEAWAAakBlKpCUbU+5Egs2umobT5Zkxa/b6lzZlCwXB7eElh0kYDKBumv//g01oP+WlVSjaTSZXIJBggDDUZVXC2ONyOp22XDZrmRYDiWTjqyvKIIJuny+WSHIcGx0dFXjeZrMZhuHxeAOB8aPKIYgkXhxIxgAEAsNNj9Qm5KxTtHkLDkyIQ7SZpmlgq9jpYxCCEJZ7g82l1QCAX9302S8+/aBqGN+74g6eGX/mKYlEDJOZN38pLzgRI1gWwZbu9hXbbFI8ESUAi6LLMBiGZVkWyYpsmpamqdlsRtM0WZZDoUDrMcJzp4yVj8TB0RE35gk2AWR5gRNZHlmEh5BlCAtIkcftdzvjY8PFLnf9onk6zyqyBiHA2DJNgyCoahpGaNxgUWPtrYlYkuXFUKSMKw509fRwhuoWuLScC/j8fo8HWBZCsDhcOhSPa7qBERjo6zEJSg+PIAg0yxLdRUXh07xdSl34zmnWfKgldzJ5/PLSwNIy8bmuwpc2J6IF6x9t8oemOX/0cjqhYI+Afn95cJKPe6Jd/sa2ZFrDT7XLH53uOpflfHudea/vvzSgW/+6/2NhcOPTo70Zc3nF645I8u8E8oqsxQHwmpqlFwzTAIRBBBCesXRETIADgeDCaU1MOIDDVfJwurjchrJZloEFttCRGB0sZDOqVuwdf/axC5KsKYauQZ51eJyVdeUOQbR7bJ56wcNZJQ6uOBgsC0f2vLzfhlgAIWEgsCyELQLAxrVrrrz6PaqherzjB8e3+4JclIHYRMggFoMAY3fDqTUBDac8Llh+1cUbi1xde9rskCOaZnICQByADEEAAIgNCxgYmhD4xp/ZQwF3PpcCBBAALQBUixCWHUhky/xFFraghSEBdpdbkCRvINA/MjowPGYPVhZUFb/qFl/RKaX1O4vHxjKQtSuqwrNsStftTkdCzSNdHRkeQgjanIKiFAxVDQaDhJgmIA6v92h7m93nyatKMpfBCNY31p161Px2p09yAAAghK2jA7FcOp5PM4hBAOimIWsqgFAzjLymuERpduWkk2s1FVes+eg9p77FcVJtbc3AUIwXeBNbCFoAAEIINqy8YrG8EyICEOfyuDFBuqFZll4oKJlMdmRkJBQKHj58sK623Ofz+f3jx0gimC9kFJ+DMXEhl1ewxSGT5aHIOSDPgSKPN5dLE2woilzV3MwhIOsqC4EFMDZNw8RIgLqJIXdKjnc5OvfvwwwfDAZtgoiByTvcBbVAGFazzFg8ITAcZFgTQUGymapKAIaWsX/HjlR0xNA0HXHTFq6smrvgdDVBXejOadbULLKsTKxwc++plQAAtzQ5vrMjKRukL2MAAC6tlOaGhSo3NzcsAABum+z85rYkAUA99aHCu8qZ93pcc/O+A5nejFnn5T445T9iXqHqSRX9ueM6lOV0vlDQWMhZFmFYwEETs2BSXV1JJOL0FOWQFEtpgPOGyiOokCgkB3riXQdHOuOmruVwc928cWF9bqmvr0PXMm6/S2KKbXYJWgRaxMPCdH8fsbTKxibOxEYq6xMkBSHMIsPQOR6lstlQsCQ+MuDwBcPB8c0srtKH+/IE6gwHIGYBy5hQi6d7Jc3vcroEjrt65cXa9GWgM6+OYRZACeoMMTEDGACxbhLVYnTA1I0fxKeyJNTd3XuyF61pWQRBBnLDifgzz+9/79VX2VjB0s3syEhJpCytyJ29fUeP9fpKqnib29T/dUOyprxkXNjSQPHO3XtfXLvZHwxOnzFtYCzaEW+9YeXK7PAAC4GhmwO9vR6PWxD4jo521dSTBvjqd788nEzOX740U8in8mkAxLlzZ4LTeWUY1cbissbistMuc/oVX+fzUKgomYoRYLIssrBpWTidSWJs2gQHz7I8zyYSSbmQtNnsspIFwCQEEIA1XZ80qTZ1aKR/YKiionLO3DnjwhaHInZRYhBEDCwN+hnkICrPEl5nchhoBsE2BrafaPX7PfaQHxtaLqcZAGkmEe1uTDAkeHB4pJQZf1k2bfrMl555SgUsskyGZUWbo5BLQ8MiAGfTWU2WpzY1pdLZgbExwelmRZHjufjwcF97K2NqiAAgOp0Oqa6ifOL1Rl04zmnW/O/ZbgD+dcoYylsFgwAAgnYGAHBV7b9aVxkN/6ElRwBAEFxS+e5udZ15r1+tL2v+dG8GAPDtxT72P+PebX1dw5a+P1pelBlLDIx0swjxvEOGwCDAxvNefzDJikNIwJhPpZJNM+ex2McHQG9h73H5YBKNxdWEquPamv8ZF1bgrc0PfAdx2GuT/JJrimMGEKSYVjhwcF9c1+fNmQc5+1gymcjlWYSInA/5vRphZE2TAJCwueHxP6tK4cd/f3582MlOc+0wB4CJBA0xGBQSiaGBkQ6fvbe8vMnmLUFW3mkH3Ay3PozTPTlWsRk8ayEEdQwKGKiMmrLsDePbQ9XlkY1wn2kRACDExCpoXV2j0eHB5kq7ZnE2lvO4JIDx8NjowdYWVmC9bv+2jS8FQiUlkXKIEUaQYHxq1vQ63bwkSR730ZYT4Uh1f0zmC4aq46JI6WhXnwdJTmQHCrAADpQEOYlvebkjmlEyuiE6XbmsYmmWKDEL5pw+a77tLrv00m9++57Nm9dddNGlLGczDCzwNpblMMGGjglgs5m83++HQOcQUDWzoBaGRoc4m0gYW03djAP7tjdPCa84ZaqWiprKpJ4URD/HiwzgsKGbpipA1snhLEOGgbqgquLEpi1hp013I7vPjtPDqqFjxBqAJwyvW4pgY8vKxmfNBSsu/d5Xv2ghxgCWYmJd1QvZlBMaTk7QCgW/QywLBwAxB0dN0zAsAPO57LqnnjI1q6BhgXAmRAaH6qrpULTvSueto41qkY+vjREAJA5eN+k1/SOm/2EgrmAAwPwS4a7Znqais5wk9gJ0hr0GANy7K6VaZH6JsLTsLGdIftcJuCNLZi1PKgP9BztEh001Uy6nw2t3XbJiVVHAOzjU3TRvgdPtKmTzzTUhu00yADA4kCQ5f6VdUsO+tDfibwp4w+PCesOlU+fMPrRni8zyRjJdaxg2gZimOjgysvqSVZCA4aGR1hMnRsaimBCeY4lpENMgpi5yjI1jsarMXrjYHxoflgtLuNqG+9KmRQDDQ9OSsG2wPdrKDvXGh6vKqos8XpvAiaLL7iwONHvNgaw+yoi5IkZnda2gqznY5EaB8Xdo/V53VVlJd+8wIaS3p3egt09RNJfT5RTYJgAAIABJREFU0TUQtXuLcqnYWGw4l0kfOtoiq5rN5TOsMU3TotHRTDa3YOFCCGBdVZnbOf7r5HG7KsKhbbu3q4qiymoylVXHRg8fPj6nuTpcUc5pABLgC/kFl5hXs8lM+tkXn8sqOcFuD5eU9fcN6gpYdfGy0vD4SniH1NXVzZ87e90LzykFdcbMeQwjuj2+bCaXTiXdHrecT6taYSym2+12TdNM0ywoajqT8fn9lmm5XK58Xl66ZElFxfg85PL4brrt1qG2jp6jHappQB1AC0IWKSYGPGdYustuc9RUORl+JJbkFBm4WIGHFoE8IoalIsjWVpQ4T5lQumZSw+LlF2/atBFCSDAhmAACeFGQJGdZJAKIpRumy+2a1FCf00xZ0Y51Hs+ncxzPyaqGMbZYrrlxivfNzAxKXTjOzzi0WZ3cvia6b1QDAPzgIv+CktckiQcOZQsmAQAwEJa7uRmhs5y2/kJz5r1uienf3J4CAPx4eVG5613fbXji49AGHGVR5ejBnQcSA9lc0hLtgcuvvmn1e947d9HikbFoWWV5WVWVu6SEdbp0hAzOIAZOREckuyn4kOB1rW74JIdOs6FwTcOul14EgkMzYKS0DCGczSa7evqSiZSmaoZhRseiACGAoGYaiBDVKACIWQYEinymqX/uZ7+znW7OZ1hmN3cOYwZAADgTsBhoqtk+1NbT19bXe2x4uDuTShumiYluoTRbyooCb0QLXJ6gvGkWNMfdzUg6zcENB4sOHWs3TWv9+o2mbnAcbxoWAGQsHpszb7ZFjIKuHWvvLC6rGRxNdnaPsIINAMRy3PQZ03mev+k9lwj8aS4uw0UBE2E5LUejqf2HD5mKYocw6Hc47XbIMIwksE5JB1YilcjllbXbX1YxUCxravOsro6+TDL7uwd+5nDYTw37Dpk7Z/bDDz/S293V1tbGsiiVSORzGbuNS6diAFuapiiKksvnGIbVdF1R9NGR6LQpUzPpZDw+0t3R+tAffiNJp7kvFQpH0tH+6NBoNpUtyIpmWIaFC5alYezxOr1O+4LVq42CNppRelM5d8CHGF4QJWxagGCWBWU109ApfZcAAFNnzPrHX/9cWlkja4Zdsuly1lBkluULqooYVpBsBU2NJVIWxrJcSAyPjPUNsTyraBrAwB0K/eCHP35TU6BTF47zkDVHZeump0cPx3QIwPeX+m5pGn8d94GprtsnO/029FxX4aV+JSix04KndI17t3nDvf7SlkR32pxSxH9lwZkmd3y3mHjW5JCELG7z1mf72mJyBlRXT1156erS+hq3V4IQTp7WjFleB6yqW4psaMOJzQ8+P7i+o6G83HTJk0suLxKqTxvW7vZC0fmd7/1AlvUFc2abWl7Opxne1lDfiC2cSqYQg8Zi8bFkQrAJgBiAYL/fY7eL2NQ/9I0f1M88/UTHyMEBiTMOx1mMOB0xBguACEzCQRxLj3QO9vRHU0ND8WR0yFRSyIQ2h10nVjqpkbhou62Bm3z6x9WSTXQ67Cc6e48cbjF1w+l0xWIJxNnH4qm8LNdMquvo6SOshDjXS1v26hgJok3TddFma25uvvLSJWUlp39JSRRFuyB09/Rt2b5TtwhWterisN/GKLm8zW7nJEHFVjQWTY6NhYpCWw8cy2q64HRPnTFz967d3/jy3fPmzJrIEXy7+P3+SGnp7l27LcPgOYaBxGEXIdHlfDaXz1iGEU/GJbvdZpMAgIlYGgJQXVURiw5t37Lxl/f9eMGC+acNywuiaLMf2L41n8krBc00sYGxCqBFTKOQlTjU0Dj5WEf3A4891ZOQu4ZHyqrr03lddLoNAEoqG6TXmWLT6y8qLi7dt3//8dZWh12UOJSKxz1eL8NzqXS6b3Agk88hhgUIxRMxBsPhzh7JbpOVPNbwT3794JRpze9kXVLvoHOdNRMKvv7J0c60aefgg6uC104afyWLCeAZ6OTR3LD4Up8yKltpDb+v8TRX/e8ib7jXI7L11a1JAsCHprlOdoZ6t3tT82t6pFLTwE/9/WlTYafUN0fCxaEimyJni8simLdpGnl57YFdD29I7+hRjo4VJdl6eyQZS9TOXRzxnz63nVRd36SbQMvlpjXUW6psGgpvc+qaoRQK3d3d0VhMVlWTYAwJtrDD5bBJAgPJVR/59GW3fOgMYZlyJy5gcjRrqaYBYJ5YmqZUVAb8YUkzlWCoVJEVniVDAyfig31dqaHnOw4+f+Rw6Map1dc2nCFsKOADADz7/HqCMcfxqmpgbGNYfmh4+MDhI4l0YWg0vW3nIblguTxeTddNbPI8/+lP3DF3xuQzhC3y+iEmR461y5rukiS/YJtSWZqIRmPRWDweHx4Z0QqFslDYbXPvOdaTVU2HtyhQHF4yd8aHbnv/GQ/aO2LatGmGoe3cubNQyC9YMFfOZQAxw+GQKPBdXR0cx6lKIRaLKqqaTKSbGiZJIvPk3x+9+66PffaznzpDWJeviGBroK0dQQQgRDyDWeiwCaxlAkI6evuf3LR1y+ETWRNt2XMgKWuPPvFsKq9MntJcVXX6a7KTGqdO7e7u3rxpQ9DrLinyKYrsdLsZhjGxaWHMMKxoEwcGhwzDcIqu9pajgohMQ/3U575yy0c++nbXHHXunNOsaRHw/meirQnDJ6LHri5eUPqvs6qJwfJHh+/ZlUoo1vKKf84D8I82eShvOXn0gXdzh9Iz7PUrnmiXN/YpAIB7l/m94r9DR6A3lTUBAI11s+vqpu7ctH321CnFbkHUk26n3VMS6Y3nvvG1H3VsPFw+Qiar9p54qrihqFCkVFy/uKTqjSdaWnzRRVNnzlSGR7CumNhiEI8gI8vy4OBQPJkEDKtjUzdNThSLgkGGZz79o1+uuOHWNwzLNXpQWFKPxGI4k3BqOThm8pmSUvuMyfVzps1cOHdheUWFPxQaHBjZ1Tu04VjnXd//2kXXXfSGYSvLwk31tRs2bWMYrlBQBcFumZZp4mQ6y3C2Y61diLGxnGQRrBu63WG//6f3rFhy+gbWq1VXVTZPbty6ay/WDRdETRXFTlG080JlZVVNdWVJcVhAHDFB31iudyjqC5V85kO3Xrv64jcM+w5ZtGhRQ0P9li0vxWKjoijs2L4tlUkGQ8GKygoWAYIxwZZhag6HKxTyDQ50f+dbX7zzzjNd5ZxU2dBUUlnZffgQhBhxkOUJMnQBwmSu0D4W393WEZc1wvCyiQdGRhHLfvrO2xfOe+Om9uKlSxvqG5T0iJ1HhXxWkGwQQoZlTBMLNgkxbGdnFy+KRYFg7/FjLqftR79++IYPfvjtqCfqvDmnWfP3LblHW/MAgHuX+ScX8bJBTv7oFrBzcG1PoTtttiaNOi/n5NEL3crvW3IAgIvKbKur38XdaM+w1zb2n/3wf30o2540QhLzpfnj37p7l3qzWRMAUFfXcPX11/e1tfhYoyLscrs8OQONZg1XoGzvjj0Rh5NltLFymZ/pWXDbFd7QRAdO8gdDJQ2NajaXHosWFC2ZSGUyGQAAgFDRdVlTMQQMb1u8atUX/u+BmimnmfzytFCJxM4rUnC+ckmdzCadYdtYerS1vWPH1n1b1u3bvfH40Il8bWieUlf5owfun9480dtx1ZVl11x16eBQtL2jm2UAJNjCFoYwk5M13cSAsByDLbJy5aKHfv3j6VObJhi2OBS48pLlvT29AiZFLptTkkxNE3nO7rBjDBnEYAAJZ7cQ+eE9X6mrehNvkrwT6uvrr7nmmv379+7evTOVTicS8f7+vqIif1lZmV0S5VyWRbCqtlayoW98/XOzZ0/0NnJRSWnzkiXJ0aFEtJ9DGo8tiJHKCMdHYi19AwzHW7qBibFi6bw/PvDDaVPOdGPg1eom1S9cslzNJY4e2u90OjHGhACOFwzT0nVTLigMx9U3NdZX1371f+9raD5HfZKpdw58s7MWvBWL/zzUmxk/5w4AYGqAf+HG8KEx/YYnR1XrNeWxsXDNDeF637u4G+2Z9/rkvy/+6/CJpLGwVHz86n+TUfRGEpmw/yy7CMb6OomSFBmhe1De25uWyqs3r3/Ri9WZ9eVX3HSp0zH+NcoJUrLZtl3bD2/b2nHsWE9nZ15RBI+ntKZm0vQZs5Ysm7t4ydmF7e7qUBNjT/71ka7OI5mR0Sr/pGXNqyKBSSWTasQGj3tS8dmF3bu/ZdfuvcdPdPb0Do3EkoLN7naJpeHAzGlNC+bNmjvrLCc07u3qifZ1kXxeSyaBrruLfK5gSHQ6WcmJHK6i8IX19du+ffuOnTv27tvb09U9NDS8atWqKU1TeZ4vjUQmNTRMndJ4dmF7j7f0tR4cPX4iOZI+3je2rvWEFA5VVVQumDl90aJ5Cxec6bb/GXSdaImODvZ0dWQy2XQ2TSDr8wdF0RapqJw/f6HTSXvM/ps4p1lz3iODQ/nTDFj8Sv5oTRj/tze9a1jNaNgrogUl4n/P8TS8m1MmmMBeAwBmPTQYLVirqqTfrj4XMwCfA28la1IURV2wzmnWpP5z0KxJUdS/pX+HjicURVEUdW7QrElRFEVRE0WzJkVRFEVNFM2aFEVRFDVRNGtSFEVR1ETRrElRFEVRE0WzJkVRFEVNFM2aFEVRFDVRNGtSFEVR1ESd07GBRhKZc7YtiqIoino9Zz14GR1Rj6IoiqImit6hpSiKoqiJolmToiiKoiaKZk2KoiiKmiiaNSmKoihqomjWpCiKoqiJolmToiiKoiaKZk2KoiiKmiiaNSmKoihqomjWpCiKoqiJolmToiiKoiaKZk2KoiiKmiiaNSmKoihqomjWpCiKoqiJolmToiiKoiaKZk2KoiiKmiiaNSmKoihqothzuTFCyAubd+3YeziVzZWFQ7deu6qsJDRumT88vmbXgZZXfvW4HD/8yqcBAMPR+ONrNvQMDDMMs2RO8zWXXQTha1bM5OQv3PPzV351SLbq8tIbrlhRHPADAL7+v79OpDL/+7XPSDbxlWX2HTnx4F+evHz5wmsuWzbBXYgl0489u76jZ4BlmMn11TddebFdsj3xwksvbtn96sVKQkXfuusj49Zt7+l/ftPO/qHRgqq6HPY5zU3XXLaMY9/SIdB04x8vbDp4tF3T9YpI+KYrL46EgwAAC+O/P7fp4LE2RdXqKstuuXaV1+08uUrPwPBvH33a5XR86eO3vRKnoKiPPrPu0LF2hNDsaY03XXUJz53T7wZFUdS7wjk9M27edWDDtpc//P6rQ0W+l3bt//kfHvveFz4u8Nyrlyko6iVL5l68eO7JXxFCAADdMH72+7821VXfdt3qRCrz+8efddilS5bMPXUTn/7ge0+mjUwu/+yGbT/93V+/87k7eY4DAIiisO9I69J5M15ZeM+ho69Oom+IEHDfQ38rDvj+55Mf0HTjob+t+euz6z9003tWL1+4fOHsVxZ77Nn1r6SoV4zGEj/73WOrLlpw67WrRIEfHI098o/nC4r2gRsun3gBTvW35za2d/d/7NbrXA7pqXVb7nv4b/d+6RMQwuc37TzW3v3RW651SLan12/99Z+f/PInbgcAbN1z8PmXdkbCQbmgvjrO7x97FiL41U/foWr6X59Zv+fg0SVzp7+VglEURf1bOqd3aPcfPXHRgllNdVV+r/v61StYlj3S2gEAeGHzrq/+8Fcnlymoqs/j9rqdJ3/cTjsAoHdgJJuXb7nmMr/XPam6/KqLl2zdc/C0m3A6pJMrVkbCd7z3qmQ62zswcvJPjbWVuw8ee2XJgqK2dfXVVkQmXv5sXv7/2rvPuCivfA/gZ5heKAMDDAxlqFJFmoIgRQTFAqhY0NgSQ4p6s0n2s9mUzc2Wz6a4N9UY471u7BqxBVFBdBFBaaKAIEXK0DtTmWHqc19MnGUB8VHB0fj/fngxz5kzh/+ZF/445ynacixfWp7ItbZy5nEXRIbea2lHCNFpVEPBQyJJU2tnUnzUmM82t3VSqZRlCyI5lhYsJsPLzTl9XYrfDFf9uwNDou/2n3j7L1+/9cmX+45nyhUjCKHyO3Xvf747r6j8L9/s+92fv9p3PFOj0Y4ZFsOwtOQEN2eetRU7ZWHMkEgyKBQjhK4Wly9bMM/F0d7air02KaGlvbOzpx8hRCSafLRji4uj/ehBevoH65oEW1Yt5Vpb8R3s/vjmRohMAACY0FNda2q1WvL9fT8CAZmxmO1dvaEBPh58B/1yECEkV4w0CtpLblcPisQuDvZrkuKtLS00Wq0JwYRIJOr7WJixegeGVGq14VMT0m9+anU6/aG/l9vh09mDQrEV2xwhdLOq1tudbxgTD3NT5psbVxoORRIZh20xps+xzEvJCVF0GnVMu72ttWxYfq3kdkRIAJFoghDiO9jxHewQQhiGfbc/w9ud/9r65SqVet/P505kXd68aqmJiYlILBWKJB+/9YpSpfr0+wMX8m4kxc8bPeyGFYmG12KJlEwimZkyRRKpVCZ3cbTTt7MYdI4lW9DRzeNaR4QEjJ9Xo6CDx7XJLSi9WnyLaGISHuyfkhCtLxIAAMBoT/VfRi83/vWySv1iqPLuvc6ePplcgRBy5zvGRfy6w0khk7VaXVpywo7Nq3UY9uX/HlVrNHwHOyLRJCe/CMMwuWIkr6gcIaRfkD2IUqU6nZ3HYjL0yYQQolIogb6exber9YclFTVhQX6PPZf27r5L10qSEv4jwypr78mG5eFB/uP78x3sXlq+6GxO/jt//XrXgYxL10oGhkT6txoFHX0DQysSYylkMovJSIqfV1JRo9FqEUJanS4hOkxf/JxAv8q7DQ+qRzGiPHwme0lcBIVMlg0rEEJMBt3wLotBlw3LH/RZoVja0d2HEPr7H97Ytim1qPzOv27cfKRvAwAAXhBPda25KCasd2Dww50/kIgkHw8XX0/X8Uu997dtMrx+NS353b99c7ehJcDHY+va5EOnL2bmFjAZtISosKraRqLJBMvEnXsOEwgEhJBKreZaW725YeXoZV94sP/xzNwl8yOGRJLu3gF/L/eyytrxg3z4xQ8DQjFCKCFqzsrE2PEd6ptafzx6dn3KIk8Xp9Ht2VeL4+fNftAqLWpOYERIQFNbR0Nz2+2ahtPZecsXxiyMDusfEmp1uu1/2jm6s0gsRQjRqBTW/fCzMGOJJLIJRx4SSb796ecZrs6LY+caGjEMm/D1eBiGUamU5IQohJCLo/38iJCbVbUTnjYGAIAX3FNNTSqFkr5uuVqj0Wp1NCrls90Hne8vBCdEp1EtzEyFEilCaKa3+84PdwzLFXQara5JQCIRR6+lDLamJfO41gghFoM+/kofb3f+iFIp6Oiua2oNnulNesD27H+9vEZ/BpHFZIx/t6Si5nhm7qtpyT4eLqPbh0SS5raO9HUpk8yISDTxdHHydHFaGhd5reT2kbM5ESEzySQynUb95pN3xnRu7+7TanWGQ50OQwQ0XmdP/9f7js+fG5x4PzJNWQyEkEyuMHwD0mG5KYv5oKrMTZmj/7awtDATSaSTzAIAAF5YT3WHtrOnv765jUwi0agU6bC8taPbnf8fF+MoRpSHTl8cEkkMh0KxhMO20Gi1JRU1I0oVk0E3MSHcqWtyc+KZmEyQIWxzUxsrto0Ve8KLYwkEwpxAv/I7daUVNWGBD9yeteVY8rjWPK61/lqk0apqG0+cu/zO1rQxkYkQqrjb4MC1GX/1rN6layVXi2+NbnF14mEYJh2W23DYihGlYdZKlVp6fzdVrdEY1peDQjHb3GzMsINC8df7ji1fFJM4apVpbsoyN2U1t3XqD0US2aBQ7Opkjx7AzpYzJBQbfmlv/5D+1C8AAIAxnmpqdvT07Tl8urmtc0gkOXDyvKO9rQffCSHUKGi/cv0mQohOo7Z29hw4eb6nf7BvULg/I4vDtvB25xNNiFmXC09dzJPK5BV3G/JLbsVHzXm8GsKD/EsralQqtZsz71E/O6JUHTx1ITkhisVkCMVS/Y9h81PQ0W1txX7QZxl02olzl3MLSnv6B0USWUNz25GzOQ52NlxrjjOPy3ewO56ZK5MrFCPKo2dz9h45o/8UiUQ8d7lApVb3DwpvlFcF+nqOGfboLzm+nq7e7nxDPSq1BiEUEx6Udbmwpb2rb1B47JdLXm7O+vtWRRKZUCxVjCi1Wq2+v06HefAd7Ww5B09eGBgS1TYK8orKI0JmPuqXAwAAL4KnukM7Z5ZvV0//rv0ZKrXax8N126ZU/ZMK7gk6Cksr9BcEbduYejwz97PdBzUazQw357e3pulPE6avX37o1IX3Pttlbspan7Jwppf749Vgb8sxYzEDfDwe47MNLW0S2fDhM9mjG7/801v6jVyJdNiG88DUjAwNoJDJeUU3z//r+ohSaW7K8pvhlpIQrf8G0telHP3l0h8//Z5MJnm5OW9N+3Wbl0alujrxPtr5o0wuD/b3WhgdNnpMpUp9p64JIXSj/N/PhXht/fJgf6/EmLlyxci3P51Qq9U+Hq6v3t83/u8v9ypGlPrX7326CyH0+fvb2eam2zamHjp98eMv99Kp1EUx4XODJ7jUFgAAAGHy60SAEd2uaTh46sJXH//O2IUAAAD4FdyTBwAAAOAFqQkAAADgBTu0AAAAAF6w1gQAAADwgtQEAAAA8ILUBAAAAPCC1AQAAADwgtQEAAAA8ILUBAAAAPCC1AQAAADwgtQEAAAA8ILUBAAAAPCC1AQAAADwgtQEAAAA8ILUBAAAAPCC1AQAAADwgtQEAAAA8ILUBAAAAPCC1AQAAADwIhm7AKTRakViqUqtIRAQgUCgkMnmZiyiCcQ5eL4NCsUsJp1KoRi7EADAVDJmag6JJGdz8m9V16s1GjKJiGEIQ5hGo6VRKcH+XskJ0RZmLCOWB57Q7er67PzivoEhjhU7Yd7s0AAfhFBZ5d1LBaUDg0IbjmViTPgsX09jlzldjp/L9fN0jQ4LMnYhAICpZLTUbO3s+WbfcW8Pl/fe2OBgZ0MgEPTtWp2uvas3J7/4r9/ue/uVNAc7G2NVOIUUI8ofDp1yc3ZITojSt+zPOH+zqtbQwcyUOW/2rEXR4fe/hufeletlWZcLUxZG8x3tBe1dxzJze/uHEAFduX4zJSHKxYnX3NZ54NSFQZE4LiLU2MVOC51Op9Nhxq4CADDFjJOaI0rVrv0ZcZGhS+ZHjHmLaGLCd7B7bf3yzNyCXQcy/vxOOpVCxjNmfvGt7Pxi2bDc2cEuLSmBx7UeEkmOns1paGmjUihzAn1XJsYSjBFKihHl1/uOt7R31TW1qjWa1MXzEUKpS+bHz5tt6DMoEh8+nc2gUfEvTQpKKy5eLZJIhx3tbdclJzja2w6JJIfPZN9raWMy6BEhAcsWRE7LfHAQiqVnsvPfTV/n4miPEHLmcT1cnD7bfQAh9N4bG3lca4SQk72tM4/7P3uPBvl5sc1NHzrm+Pm+9v5nGPbvWJozy/eVtUnTNicAAEAIIeInn3zy9H/r5etlYons5TXLJukzw825tOKuRqN1c+Y9dMCG5rYfj5xxdeKFBviUVdbWN7fGhAXtO555t7Flw4rFNCrlyvUyGyv201+5KkaUX/3fMRaTYWlhNtPb42ZVnUgi9fV0pZDJZiym4ceWY0mlkG9V14cH+eMZtq2zZ9eBDHtb64jQmRU1DTUNLbFzg3cfPNnc1rUwOmxEqbpRXsXj2tjZcKZ7ghMqulWt0WoXxYQbWkxZDLa5qb+Xm4+Hi6GRbW56T9COIUwfrpOYcL5kMsnLne/tznd3drgnaPfxdBk9uNGVVtTYWFnqpybo6CYQTGhUOMcJwHPPOBfd1NQ3hQc/PB7Cg/yr65vwDKjRauPnzd66NmlpXKSvp2tX7wCGofbuXmced06g78LoMIRQe3fvk9b96IRiqYuj/ZsbV5LJJFuO5R9ef0k2rJiwJ5NBH1aM4Bx2WDESNSfw5dVLF8fO9fV07ekf1Gi0fEf7jSsTl8ZFrlq6ACHU1ds/ZdN4RFLZsBXbfExjWJB/2Li/CdjmphLp8EMHHD9frVa3KDosMSY8MSZcp9NRKeSFUWFTNoGplnW58FZ1nbGrAABMAePs0Iqlw5xx/6qOZ2VpLpLI8Azo4+Hi4+EikysaBR0t7Z3e7nwCAbk42tc3t/UNChsF7Qihhy5opoO9LSctOcFwyLG02LJ66ZMP6+3O93bnI4RkckVDcxuPa00iEVcmxup0WP+gsKi8ikBAXm78J/9Fj8fMlCno6MbTUyiWOvG4D+02fr5E4q9/8A0MiXKuFS+ZH2HKYjxByVNDpVaTSeTx5wEwhCE4xQnAb4Jx1pp0GnVY/vB1lWxYzmTQ8Q976kLeF3sOmbGYm1KXIITWJiXQadSPdu7Zn3E+NMAnZKb341f8TJLJFd/+8+dhuWLNsnh9i1gq+3Dnnryi8tTFce58B2MV5sF3bBR0KFWqybup1OpGQYe7M946x88XIZR1pZBMIs2fG/L45U6dn05k3SivMnYVAIBpZJzU9HBxrKy999But2saZrg64R92/tzgjSsXy0eU/9h7RK3R7D16VqvVbt+8as2y+LLKuzn5xU9Q8jNHIhv+4odDXb0Dr29Y4eXmrG9kMemvv7Q8IiQg4/yVgtIKY9XmYGdjw2HfuHln8m6FZZU2HLwnmyecr0yuKL5dPXuWL4NOe9Kip4JKrVap1MauAgAwjYyTmrHhwXfqGqtqGyfpU9soqGtsjZoTiGfAW9X1Geev2NlyIkMDwoP8+weFza0djYJ2X0/XmV7ucREhdBoVT04/L7Q63Xc/nRBLZe+mrwvw9kAIyeSKXy5dq2loDvLzSktOIBBQVd1kX+90WxoXkXWlUCaf+CQuQmhYrjh/5frScRdRT2j8fPUqahp0OmyWz2/2pk8AwLPGOOc1rdjmW1Yv23v0bFxkaNTsWeOvHLnX0r7n8Om1SQvw3JOAEBJLZLkFpb39Qy5O9gWlFVQK2dGea8ZiVtc33aquHxgSKUaUPO4zeusHIaB+AAADLElEQVRnVW2jlzvfcNgoaOdYWliYTTbxgtKK1s4eTxenuqbWuqZWhFBYoF9hWUVekTYuoq+nfwDDkINR5xvoO6OwrHL/iaxtm1LH3/CDYdiBk+f5jvaBfjPwjDZ+vpEhAaYsRlNrJ0LIGceZUQAAmBJGe8pBkN8MK7b5meyrH1wtIhJNomYHrk2KRwhptbqsK4U514rXLouPCAnAOVp0WJBIIi0oq7zb2GJnw9m8agmDTtu2KfVE1uV//nyOQiHPnuWTcv8JA0ZBIhI1Wu2Eb10rvX3pWsncEH+EUElFzaFTF99NXzd5auqvj21oaWtoadO3+Hm67ti8+sjZnAt51xl02rzZsxJjwycZ4SnYlLrk77v2n8m+uiIxdsxbZ3Py27p6P9yxBedQE87XlMUQiiVEExMW0/jXAQEAXhCE0feJG4VSpcq+WtzW1bNj8+qO7r6fTpxTqTUvr1lmlEtep09OfvHNqtp3Xl1Hp1HHvKVSa3YfPNnc1olhGIZhb2xY6evpapQip1xnT/8/9h6JDA1YsShWv+DEMHQ6O6+wrPL36ev1jzv4Lflu/wk/T7fYucGTvAYAPNeM//R2KoVixmJqNNrM3ILsq0Ux4UEpC2MoZOMXNrXiIkPvtbS/+7dvzFhMQ6ObM+/VtBQKmbR906ofDp+qa2zdvnmV96jd2ucdj2v9+/T13x/I6OodeGn5IoTQ4TMXu3sHfpORCQB4ETwr4VTbKBBLZe+mr8fzJKDnEYlI3L55Ve/AkFgiM6zuDY+nJ5GIb25MFUtklhZmxqpwmvC41h/s2HLsl0sffL4bIRTs7/XB9i0s5iPcUAQAAM8O4+/QIoQ6e/prGprnR4SQiERj1wKmy6BQTCAQfnt/Fox2reS2E4/Ld7Ab87qgtMLR3lb/GgDwXHsmUhMAAAB4LsB//gwAAADgBakJAAAA4AWpCQAAAOAFqQkAAADgBakJAAAA4AWpCQAAAOAFqQkAAADgBakJAAAA4AWpCQAAAOAFqQkAAADgBakJAAAA4AWpCQAAAOAFqQkAAADgBakJAAAA4AWpCQAAAOAFqQkAAADgBakJAAAA4PX/q+ihT8yk7UQAAAAASUVORK5CYII=" alt="tweet" width="400">
</div>
</div>
<div class="paragraph">
<p>Most of the books I&#8217;ve looked at which claim to teach programming begin with
some strong assumptions about the reader already knowing how to program, and
teach the specific syntax of some language. That&#8217;s no good if this is your first
language, so I&#8217;m working towards teaching the concepts, the language, and the
syntax (warts and all).</p>
</div>
<div class="paragraph">
<p>The book is currently available under the Manning Early Access Program (MEAP)
which means if you buy it you get the draft of the first three chapters right
now. If you find something you still don&#8217;t understand, or you don&#8217;t like how
I&#8217;ve written some/all of it, then jump onto the forum and let me know. I make
more edits and write more chapters, and you get updated versions. Lather, rinse,
repeat until the final version and you get a polished book which (if I&#8217;m any
good) contains what you want it to.</p>
</div>
<div class="paragraph">
<p>I&#8217;m genuinely interested in getting this right; I want to help people learn R. I
contribute a bit of time on Stack Overflow answering people&#8217;s questions, and
it&#8217;s very common to see questions that shouldn&#8217;t need asking. I don&#8217;t blame the
user for not knowing something (a different answer for not searching, perhaps),
but I can help make the resource they need.</p>
</div>
<div class="paragraph">
<p>To show that I really want people to contribute, here&#8217;s a discount code to
sweeten the deal: use <code>mlcarroll</code> for 50% off here:
<a href="https://www.manning.com/books/data-munging-with-r?a_aid=datamungingwithr&amp;a_bid=1dc44480" class="bare">https://www.manning.com/books/data-munging-with-r?a_aid=datamungingwithr&amp;a_bid=1dc44480</a></p>
</div>
<div class="paragraph">
<p>Chapter 1 is a free download, so please check that out too! At the moment the
MEAP covers the first three chapters, but the following four aren&#8217;t too far
behind.</p>
</div>
<div class="paragraph">
<p>I&#8217;ll document some of the behind-the-scenes process shortly, but for now here&#8217;s
an excerpt from chapter 2:</p>
</div>
<div class="sect1">
<h2 id="storing-values-assigning"><a class="anchor" href="#storing-values-assigning"></a>1. Storing Values (Assigning)</h2>
<div class="sectionbody">
<div class="paragraph">
<p>In order to do something with our data, we will need to tell <code>R</code> what to call
it, so that we can refer to it in our code. In programming in general, we
typically have <em>variables</em> (things that may vary) and <em>values</em> (our data). We&#8217;ve
already seen that different data <em>values</em> can have different <em>types</em>, but we
haven&#8217;t told <code>R</code> to store any of them yet. Next, we&#8217;ll create some <em>variables</em>
to store our data <em>values</em>.</p>
</div>
<div class="sect2">
<h3 id="data-variables"><a class="anchor" href="#data-variables"></a>1.1. Data (Variables)</h3>
<div class="paragraph">
<p>If we have the values <code>4</code> and <code>8</code> and we want to do something with them, we can
use the values literally (say, add them together as <code>4 + 8</code>). You may be
familiar with this if you frequently use Excel; data values are stored in cells
(groups of which you can opt to name) and you tell the program which values you
wish to combine in some calculation by selecting the cells with the mouse or
keyboard. Alternatively, you can opt to refer to cells by their grid reference
(e.g. <code>A1</code>). Similarly to this second method, we can store values in <em>variables</em>
(things that may vary) and <em>abstract</em> away the values. In <code>R</code>, assigning of
values to variables takes the following form</p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r">variable <span class="tok-o">&lt;-</span> value</code></pre>
</div>
</div>
<div class="paragraph">
<p>The <em>assignment operator</em> <code>&lt;-</code> can be thought of as storing the value/thing on
the right hand side into the name/thing on the left hand side. For example, try
typing <code>x &lt;- 4</code> into the <code>R</code> <code><strong>Console</strong></code> then press <kbd>Enter</kbd>:</p>
</div>
<div class="imageblock" style="text-align: center">
<div class="content">
<img src="data:image/png;base64,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" alt="Variable" width="150" height="150">
</div>
</div>
<div class="paragraph">
<p>You could just as easily use the equals sign to achieve this; <code>x = 4</code> but I
recommend you use <code>&lt;-</code> for this for reasons that will become clear later.</p>
</div>
<div class="paragraph">
<p>You&#8217;ll notice that the <code><strong>Environment</strong></code> tab of the <code><strong>Workspace</strong></code> pane now lists
<code>x</code> under <code><strong>Values</strong></code> and shows the number 4 next to it, as shown in <a href="#fig-x_eq_4">Figure 2. 1.</a></p>
</div>
<div id="fig-x_eq_4" class="imageblock" style="text-align: center">
<div class="content">
<img src="data:image/png;base64,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" alt="fig x eq 4" width="400">
</div>
<div class="title">Figure 2. 1. The <em>variable</em> <code>x</code> has been assigned the <em>value</em> <code>4</code>.</div>
</div>
<div class="paragraph">
<p>What happened behind the scenes was that when we pressed <kbd>Enter</kbd>, <code>R</code> took
the entire expression that we entered (<code>x &lt;- 4</code>) and evaluated it. Since we
told <code>R</code> to <em>assign</em> the value <code>4</code> to the variable <code>x</code>, <code>R</code> converted the value
<code>4</code> to binary and placed that in the computer&#8217;s memory. <code>R</code> then gives us a
reference to that place in the computer&#8217;s memory and labels it <code>x</code>. A diagram of
this process is shown in <a href="#fig-assign">[fig-assign]</a> Nothing else appeared in the
<code><strong>Console</strong></code> because the action of assigning a value doesn&#8217;t <em>return</em> anything
(we&#8217;ll cover this more in our section on functions).</p>
</div>
<div class="paragraph">
<div class="title">Assigning a value to a variable. The value entered is converted to binary, then stored in memory, the reference to which is labelled by the variable.</div>
<p>![figures/assigning.png]</p>
</div>
<div class="paragraph">
<p>This is overly simplified, of course. Technically speaking, in <code>R</code>, names have
objects rather than the other way around. This means that <code>R</code> can be quite
memory efficient since it doesn&#8217;t create a copy of anything it doesn&#8217;t need to.</p>
</div>
<div class="admonitionblock caution">
<table>
<tr>
<td class="icon">
<i class="fa icon-caution" title="Caution"></i>
</td>
<td class="content">
<div class="title">On <em>"hidden"</em> variables</div>
<div class="paragraph">
<p>Variables which begin with a period (e.g. <code>.length</code>) are considered
<em>hidden</em> and do not appear in the <code><strong>Environment</strong></code> tab of the
<code><strong>Workspace</strong></code>. They otherwise behave exactly as any other variable; they can be
printed and manipulated. An example of one of these is the <code>.Last.value</code>
variable, which exists from the moment you load up <code>R</code> (with the value <code>TRUE</code>)&#8201;&#8212;&#8201;this contains the output value of the last statement executed (handy if you
forgot to assign it to something). There are very few reasons you&#8217;ll want to use
this feature (dot-prefixed hidden variables) on purpose at the moment, so for
now, avoid creating variable names with this pattern. The exception to the
<em>hidden</em> nature of these is again the <code>.Last.value</code> variable which you can
request to be visible in the <code><strong>Environment</strong></code> tab via
<span class="menuseq"><span class="menu">Tools</span>&#160;&#9656; <span class="submenu">Global Options&#8230;&#8203;</span>&#160;&#9656; <span class="submenu">General</span>&#160;&#9656; <span class="menuitem">Show .Last.value in environment listing</span></span>.</p>
</div>
</td>
</tr>
</table>
</div>
<div class="paragraph">
<p>We can retrieve the value assigned to the variable <code>x</code> by asking <code>R</code> to print
the value of <code>x</code></p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r"><span class="tok-kp">print</span><span class="tok-p">(</span>x <span class="tok-o">=</span> x<span class="tok-p">)</span></code></pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre>#&gt; [1] 4</pre>
</div>
</div>
<div class="paragraph">
<p>for which we have a useful shortcut&#8201;&#8212;&#8201;if your entire expression is just a
variable, <code>R</code> will assume you mean to <code>print()</code> it, so</p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r">x</code></pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre>#&gt; [1] 4</pre>
</div>
</div>
<div class="paragraph">
<p>works just the same.</p>
</div>
<div class="paragraph">
<p>Now, about that <code>[1]</code>: it&#8217;s important to know that in <code>R</code>, there&#8217;s no such thing
as a single value; every value is actually a <em>vector</em> of values (we&#8217;ll cover
these properly in the next chapter, but think of these as collections of values
of the same type).<sup class="footnote">[<a id="_footnoteref_1" class="footnote" href="#_footnote_1" title="View footnote.">1</a>]</sup>
Whenever <code>R</code> prints a value it allows for the case where the value contains more
than one number. To make this easier on the eye, it labels the first value
appearing on the line by it&#8217;s position in the collection. For collections
(vectors) with just a single value, this might appear strange, but this makes
more sense once our variables contain more values</p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r"><span class="tok-c1"># Print the column names of the mtcars dataset</span>
<span class="tok-kp">names</span><span class="tok-p">(</span>x <span class="tok-o">=</span> mtcars<span class="tok-p">)</span></code></pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre>#&gt;  [1] "mpg"  "cyl"  "disp" "hp"   "drat" "wt"   "qsec" "vs"   "am"   "gear"
#&gt; [11] "carb"</pre>
</div>
</div>
<div class="paragraph">
<p>We can assign another variable to another value</p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r">y <span class="tok-o">&lt;-</span> <span class="tok-m">8</span></code></pre>
</div>
</div>
<div class="paragraph">
<p>There are few restrictions for what we can name our data <em>values</em>, but <code>R</code> will
complain if you try to break them. Variables should start with a letter, not a
number. Trying to create the variable <code>2b</code> will generate an error. Variables can
also start with a dot (<code>.</code>) as long as it&#8217;s not immediately followed by a
number, although you may wish to avoid doing so. The rest of the variable name
can consist of letters (upper and lower case) and numbers, but not punctutation
(except <code>.</code> or <code>_</code>) or other symbols (except the dot, though again, perferrably
not).</p>
</div>
<div class="paragraph">
<p>There are also certain <em>reserved words</em> that you can&#8217;t name variables as. Some
are <em>reserved</em> for built-in functions or keywords</p>
</div>
<div class="paragraph">
<p><code>if</code>, <code>else</code>, <code>repeat</code>, <code>while</code>, <code>function</code>, <code>for</code>, <code>in</code>, <code>next</code>, and <code>break</code>.</p>
</div>
<div class="paragraph">
<p>Others are <em>reserved</em> for particular values</p>
</div>
<div class="paragraph">
<p><code>TRUE</code>, <code>FALSE</code>, <code>NULL</code>, <code>Inf</code>, <code>NaN</code>, <code>NA</code>, <code>NA_integer_</code>, <code>NA_real_</code>,
<code>NA_complex_</code>, and <code>NA_character_</code>.</p>
</div>
<div class="paragraph">
<p>We&#8217;ll come back to what each of these means, but for now you just need to know
that you can&#8217;t create a variable with one of those names.</p>
</div>
<div class="admonitionblock caution">
<table>
<tr>
<td class="icon">
<i class="fa icon-caution" title="Caution"></i>
</td>
<td class="content">
<div class="title">On overwriting names</div>
<div class="paragraph">
<p>What you <strong>can</strong> do however, which you may wish to take care with, is <em>overwrite</em>
the in-built names of variables and functions. By default, the value <code>pi</code> is
available (&#960; = 3.141593).</p>
</div>
<div class="paragraph">
<p>If you were translating an equation into code, and wanted to enter the value
<em>p<sub>i</sub></em> you might accidentally call it <code>pi</code> and in doing so change the default
value, causing all sorts of trouble when you next go to use it or call a
function you&#8217;ve written which expects it to still be the default.</p>
</div>
<div class="paragraph">
<p>The default value can still be accessed by specifying the package in which it is
defined, separated by two colons (<code>::</code>). In the case of <code>pi</code>, this is the <code>base</code>
package.</p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r"><span class="tok-kc">pi</span> <span class="tok-o">&lt;-</span> <span class="tok-m">3L</span> <i class="conum" data-value="1"></i><b>(1)</b>
base<span class="tok-o">::</span><span class="tok-kc">pi</span> <i class="conum" data-value="2"></i><b>(2)</b></code></pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre>#&gt; [1] 3.141593</pre>
</div>
</div>
<div class="colist arabic">
<table>
<tr>
<td><i class="conum" data-value="1"></i><b>1</b></td>
<td>Re-defining <code>pi</code> to be equal to exactly <code>3</code></td>
</tr>
<tr>
<td><i class="conum" data-value="2"></i><b>2</b></td>
<td>The default, correct value is still available.</td>
</tr>
</table>
</div>
<div class="paragraph">
<p>This is also an issue for functions, with the same solution; specify the package
in which it is defined to use that definition. We&#8217;ll return to this in
<a href="#SS-Scope">Scope</a>.</p>
</div>
</td>
</tr>
</table>
</div>
<div class="paragraph">
<p>We&#8217;ll cover how to do things to our variables in more detail in the next
section, but for now let&#8217;s see what happens if we add our variables <code>x</code> and <code>y</code>
in the same way as we did for our regular numbers</p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r">x <span class="tok-o">+</span> y</code></pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre>#&gt; [1] 12</pre>
</div>
</div>
<div class="paragraph">
<p>which is what we got when we added these numbers explicitly. Note that since our
expression produces just a number (no assigment), the value is printed. We&#8217;ll
cover how to add and subtract values in more depth in <a href="#SS-math">Basic
Mathematics</a>.</p>
</div>
<div class="paragraph">
<p><code>R</code> has no problems with overwriting these values, and it doesn&#8217;t mind what data
you overwrite these with.<sup class="footnote">[<a id="_footnoteref_2" class="footnote" href="#_footnote_2" title="View footnote.">2</a>]</sup></p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r">y <span class="tok-o">&lt;-</span> <span class="tok-s">&#39;banana&#39;</span>
y</code></pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre>#&gt; [1] "banana"</pre>
</div>
</div>
<div class="paragraph">
<p><code>R</code> is <em>case-sensitive</em>, which means that it treats <code>a</code> and <code>A</code> as distinct
names. You can have a variable named <code>myVariable</code> and another named <code>MYvariable</code>
and another named <code>myVARIABLE</code> and <code>R</code> will hold the value assigned to each
independently.</p>
</div>
<div class="quoteblock">
<div class="title">On variable names</div>
<blockquote>
There are only two hard things in Computer Science: cache invalidation and naming things.
</blockquote>
<div class="attribution">
&#8212; Phil Karlton<br>
<cite>Principal Curmudgeon Netscape Communications Corporation</cite>
</div>
</div>
<div class="paragraph">
<p>I said earlier that <code>R</code> won&#8217;t keep track of your units so it&#8217;s a good idea to
name your variables in a way that makes logical sense, is meaningful, and will
help you remember what it represents. Variables <code>x</code> and <code>y</code> are fine for playing
around with values, but aren&#8217;t particularly meaningful if your data represents
speeds, where you may want to use something like <code>speed_kmph</code> for speeds in
kilometers per hour. Underscores (<code>_</code>) are allowed in variable names, but
whether or not you use them is up to you. Some programmers prefer to name
variables in this way (sometimes referred to as 'snake_case'), others prefer
'CamelCase'. The use of periods (dots, <code>.</code>) to separate words is discouraged for
reasons beyond the scope of this book.<sup class="footnote">[<a id="_footnoteref_3" class="footnote" href="#_footnote_3" title="View footnote.">3</a>]</sup></p>
</div>
<div class="admonitionblock important">
<table>
<tr>
<td class="icon">
<i class="fa icon-important" title="Important"></i>
</td>
<td class="content">
<div class="title">Naming things</div>
<div class="paragraph">
<p>Be careful when naming your variables. Make them meaningful and
concise. In six months from now, will you remember what <code>data_17</code> corresponds
to? Tomorrow, will you remember that <code>newdata</code> was updated twice?</p>
</div>
</td>
</tr>
</table>
</div>
</div>
<div class="sect2">
<h3 id="unchanging-data"><a class="anchor" href="#unchanging-data"></a>1.2. Unchanging Data</h3>
<div class="paragraph">
<p>If you&#8217;re familiar with working with data in a spreadsheet program (such as
Excel), you may expect your variables to behave in a way that they
won&#8217;t. Automatic recalculation is a very useful feature of spreadsheet programs,
but it&#8217;s not how <code>R</code> behaves.</p>
</div>
<div class="paragraph">
<p>If we assign our two variables, then add them, we can save that result to
another variable</p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r">a <span class="tok-o">&lt;-</span> <span class="tok-m">4</span>
b <span class="tok-o">&lt;-</span> <span class="tok-m">8</span>
sum_of_a_and_b <span class="tok-o">&lt;-</span> a <span class="tok-o">+</span> b</code></pre>
</div>
</div>
<div class="paragraph">
<p>This has the value we expect</p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r"><span class="tok-kp">print</span><span class="tok-p">(</span>x <span class="tok-o">=</span> sum_of_a_and_b<span class="tok-p">)</span></code></pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre>#&gt; [1] 12</pre>
</div>
</div>
<div class="paragraph">
<p>Now, if we <em>change</em> one of these values</p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r">b <span class="tok-o">&lt;-</span> <span class="tok-m">2</span></code></pre>
</div>
</div>
<div class="paragraph">
<p>this has <strong>no impact</strong> on the value of the variable we created to hold the sum
earlier</p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r"><span class="tok-kp">print</span><span class="tok-p">(</span>x <span class="tok-o">=</span> sum_of_a_and_b<span class="tok-p">)</span></code></pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre>#&gt; [1] 12</pre>
</div>
</div>
<div class="paragraph">
<p>Once the sum was calculated, and that value stored in a variable, the connection
to the original values was lost. This makes things <em>reliable</em> because you know
for sure what value a variable will have at any point in your calculation by
following the steps that lead to it, whereas a spreadsheet depends much more on
its current overall <em>state</em>.</p>
</div>
</div>
<div class="sect2">
<h3 id="assigmnent-operators-code-code-vs-code-code"><a class="anchor" href="#assigmnent-operators-code-code-vs-code-code"></a>1.3. Assigmnent Operators (<code>&lt;-</code> vs <code>=</code>)</h3>
<div class="paragraph">
<p>If you&#8217;ve read some <code>R</code> code already, you&#8217;ve possibly seen that both <code>&lt;-</code> and
<code>=</code> are used to assign values to objects, and this tends to cause some
confusion. Technically, <code>R</code> will accept either when assigning variables, so in
that respect it comes down to a matter of style (I still highly reccomend
assigning with <code>&lt;-</code>). The big difference comes when using functions that take
<em>arguments</em>&#8201;&#8212;&#8201;there you should only use <code>=</code> to specify what the <em>value</em> of the
<em>argument</em>. For example, when we inspected the <code>mtcars</code> data, we could
specify a string with which to indent the output</p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r">str<span class="tok-p">(</span>object <span class="tok-o">=</span> mtcars<span class="tok-p">,</span> indent.str <span class="tok-o">=</span> <span class="tok-s">&#39;&gt;&gt;  &#39;</span><span class="tok-p">)</span></code></pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre>#&gt; 'data.frame':	32 obs. of  11 variables:
#&gt; &gt;&gt;  $ mpg : num  21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
#&gt; &gt;&gt;  $ cyl : num  6 6 4 6 8 6 8 4 4 6 ...
#&gt; &gt;&gt;  $ disp: num  160 160 108 258 360 ...
#&gt; &gt;&gt;  $ hp  : num  110 110 93 110 175 105 245 62 95 123 ...
#&gt; &gt;&gt;  $ drat: num  3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
#&gt; &gt;&gt;  $ wt  : num  2.62 2.88 2.32 3.21 3.44 ...
#&gt; &gt;&gt;  $ qsec: num  16.5 17 18.6 19.4 17 ...
#&gt; &gt;&gt;  $ vs  : num  0 0 1 1 0 1 0 1 1 1 ...
#&gt; &gt;&gt;  $ am  : num  1 1 1 0 0 0 0 0 0 0 ...
#&gt; &gt;&gt;  $ gear: num  4 4 4 3 3 3 3 4 4 4 ...
#&gt; &gt;&gt;  $ carb: num  4 4 1 1 2 1 4 2 2 4 ...</pre>
</div>
</div>
<div class="paragraph">
<p>If we had used <code>&lt;-</code> instead of <code>=</code> for either argument, then <code>R</code> would treat
that as creating a new variable <code>object</code> or <code>indent.str</code> with value <code>mtcars</code> or
<code>'&gt;&gt; '</code> respectively, which isn&#8217;t what we want.</p>
</div>
<div class="admonitionblock warning">
<table>
<tr>
<td class="icon">
<i class="fa icon-warning" title="Warning"></i>
</td>
<td class="content">
<div class="title">Assigning to variables.</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r">score <span class="tok-o">&lt;-</span> <span class="tok-m">4.8</span>
score</code></pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre>#&gt; [1] 4.8</pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r">str<span class="tok-p">(</span>object <span class="tok-o">=</span> score<span class="tok-p">)</span></code></pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre>#&gt;  num 4.8</pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r">fruit <span class="tok-o">&lt;-</span> <span class="tok-s">&#39;banana&#39;</span>
fruit</code></pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre>#&gt; [1] "banana"</pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r">str<span class="tok-p">(</span>object <span class="tok-o">=</span> fruit<span class="tok-p">)</span></code></pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre>#&gt;  chr "banana"</pre>
</div>
</div>
</td>
</tr>
</table>
</div>
<div class="paragraph">
<p>Note that we didn&#8217;t need to tell <code>R</code> that one of these was a number and one was
a string, it figured that out itself. It&#8217;s good practice (and easier to read) to
make your <code>&lt;-</code> line up vertically when defining several variables:</p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r">first_name <span class="tok-o">&lt;-</span> <span class="tok-s">&#39;John&#39;</span>
last_name  <span class="tok-o">&lt;-</span> <span class="tok-s">&#39;Smith&#39;</span>
top_points <span class="tok-o">&lt;-</span> <span class="tok-m">23</span></code></pre>
</div>
</div>
<div class="paragraph">
<p>but only if this can be achieved without adding too many spaces (exactly how
many is too many is up to you).</p>
</div>
<div class="admonitionblock caution">
<table>
<tr>
<td class="icon">
<i class="fa icon-caution" title="Caution"></i>
</td>
<td class="content">
<div class="paragraph">
<div class="title">Watch this space!</div>
<p>An extra space can make a big difference to the syntax. Compare:</p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r">a <span class="tok-o">&lt;-</span> <span class="tok-m">3</span></code></pre>
</div>
</div>
<div class="paragraph">
<p>with</p>
</div>
<div class="listingblock">
<div class="content">
<pre class="pygments highlight"><code data-lang="r">a <span class="tok-o">&lt;</span> <span class="tok-o">-</span> <span class="tok-m">3</span></code></pre>
</div>
</div>
<div class="listingblock">
<div class="content">
<pre>#&gt; [1] FALSE</pre>
</div>
</div>
<div class="paragraph">
<p>In the first case we assigned the value <code>3</code> to the variable <code>a</code> (which returns
nothing). In the second case, with a wayward space, we <em>compared</em> <code>a</code> to the
value <code>-3</code> which returns <code>FALSE</code> (I&#8217;ll explain why that works at all, later).</p>
</div>
</td>
</tr>
</table>
</div>
<div class="paragraph">
<p>Now that we know how to provide some data to <code>R</code>, what if we want to explicitly
tell <code>R</code> that our data should be of a specific type, or we want to convert our
data to a different type? That&#8217;s an article for another day.</p>
</div>
<div class="paragraph">
<p>If you&#8217;re interested in seeing more, and hopefully providing feedback on what
you do/don&#8217;t like about it, then use the discount code <code>mlcarroll</code> here
<a href="https://www.manning.com/books/data-munging-with-r?a_aid=datamungingwithr&amp;a_bid=1dc44480" class="bare">https://www.manning.com/books/data-munging-with-r?a_aid=datamungingwithr&amp;a_bid=1dc44480</a>
for 50% off and get reading!</p>
</div>
</div>
</div>
</div>
</div>
<div id="footnotes">
<hr>
<div class="footnote" id="_footnote_1">
<a href="#_footnoteref_1">1</a>. In technical terms, <code>R</code> has no <em>scalar</em> types.
</div>
<div class="footnote" id="_footnote_2">
<a href="#_footnoteref_2">2</a>. This is where the distinction of <em>weakly typed</em> becomes important - in a <em>strongly typed</em> language you would not be able to arbitrarily change the type of a variable.
</div>
<div class="footnote" id="_footnote_3">
<a href="#_footnoteref_3">3</a>. This syntax is already used within <code>R</code> to denote functions acting on a specific class, such as <code>print.Date()</code>.
</div>
</div>