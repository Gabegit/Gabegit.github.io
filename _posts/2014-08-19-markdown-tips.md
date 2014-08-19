---
layout: post
title: markdown tips
---

% Markdown syntax cheatsheet
% Li Guomin

# syntax cheatsheet

## Phrase Emphasis #

* `*italic*` 
* `**bold**`
* `_italic_`
* `__bold__`

## Links #

Inline

`an
[dingus](http://http://daringfireball.net/projects/markdown/dingus)
`

Reference-style labels (titles are optional):

`an[example](id).Then,anywhere else in the doc,define the link:`

`[id]:http://example.com/ "Title"`

	
## Images #
Inline (titles are optional):

`![alt text](/path/img.jpg "Title")`

Reference-style:

`![alt text][id]`

`[id]: /url/to/img.jpg "Title"`

## Headers #

Setext-style:

`Header 1`

`========`

``

`Header 2`

`--------`

atx-style (closing ##'s are optional):

`## Header 1 #`

`### Header 2 ##`

`####### Header 6`

# show,hide,move the level

    -`Tab` show

    -`Tab Tab` hide

	-We can cut the level(C-w) when the level is circed,then yoke to
	the place we want it to be.

# using pandoc #

## the basics

* in Emacs, when you finish a md file, using shell command:alt+!,
  input:
  
  `pandoc -o output.html input.md`
  
  * input format can be specified using the `-r-/--read or -f/--from`,
    the output format using `-w/--write or -t/--to`.
	
  * to convert hello.md from markdown to Latex,type:
  
  `pandoc -f markdown -t latex hello.md`
  
  * to convert `hello.html` from html to markdown:
  
  `pandoc -f html -t markdown hello.html`
  
* Pandoc uses the ** UTF-8**  character encoding for both input and
  output. If your local character encoding is not UTF-8, you should
  __pipe__ input and output through `iconv`:  
  
  `iconv -t utf-8 input.txt | pandoc | iconv -f utf-8`
  
## tranfer command using pandoc

pandoc ʹ��utf-8��ΪĬ�ϵ�����������룬��������md �ĵ�����Ҫת��utf-8��ʹ��icovn.exe���÷����£�

* �ֲ�����

  - `iconv.exe -c -t utf-8 he.md > he.md` % �ⲽ����û�ɹ�

  - �Ƚ�he.md��Ϊutf-8��In Emacs��
  
     `c-x ert f utf-8`

  - ʹ����������

  `pandoc -N -o he.tex --template="mytemplate.tex" -f markdown he.md`

  `xelatex he.tex`

* Ҳ���Խ�he.tex ת��utf-8��ʽ��û����ɹ�

   `iconv.exe -c -t utf-8 he.tex`

* ���input �� output ������ utf-8��ʹ�ã�û����ɹ�

   `iconv.exe -c -t utf-8 he.md | pandoc -o he.tex --template="mytemplate.tex" -f markdown he.md | iconv.exe -c -t utf-8 he.tex`


## creating a pdf
  pandoc can now produce pdf output itself. just specify an output
  file with a `.pdf` extension.
  
  `pandoc test.md -o test.pdf
  
 
# producing slides with pandoc #

- In Emacs, create a md file,like he.md. Seemly it must be saved as utf-8 format,and not support chinese at least in Emacs,but works well in other compilers like Rstdio.

- In Emacs, switch to *scratch buffer, write some pandoc command for pasting later in shell command minibufer,

  pandoc -t beamer he.md -0 he.pdf

- In Emacs, Alt+! call the shell command window, paste the above pandoc script from scratch buffer.

- Up to now, the md file will transfer into the basic beamer pdf file. If you want to create more functional beamer pdf, you can use a beamer template.

- View the beamer pdf, Alt+! input
  
  `sumatrapdf he.pdf`


