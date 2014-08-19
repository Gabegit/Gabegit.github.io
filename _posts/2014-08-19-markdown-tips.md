---
layout: post
title: markdown tips
---


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

# Pandoc Use's Guide #

## 安装pandoc程序和相应模式 ##

* 下载pandoc程序，安装在`c:\Users\gabe\AppData\Roaming\pandoc`
* 安装`pandoc-mode.el` 和 `markdown-mode.el`,其中前一个设置pandoc的格式， 后一个方便markdown 输入。

## 配置 Emacs ##

重点是配置 `pandoc` 程序路径。方法为：
	options - customize Eamcs - specific option > pandoc TAB - pandoc
	binary 输入pandoc 的路径


## Using pandoc ##

* Two ways to using pandoc compiling
  * 在pandoc 菜单进行相应的设置，然后点击编译，即可。
  * 输入shell 命令，方法：alt-！ 进入shell命令行，输入相应的编译命令。

* output to a file, use the -o option

the input-files are concatenated (with a ank line between each) and
used as input.

The `-s` option says to create a “standalone” file, with a header and footer, not just a fragment.

	pandoc -o output.html input.txt

* specify th input format and output format

	pandoc -f markdown -t latex hello.md

* Convert hello.txt from markdown to LaTeX

To create a LaTeX document, you just need to change the command slightly:

	pandoc test1.md -f markdown -t latex -s -o test1.tex
	pandoc test1.md -s -o test1.tex

* HTML with smart quotes, table of contents, CSS, and custom footer:

	pandoc -s -S --toc -c pandoc.css -A footer.html README -o
    example3.html

* From LaTeX to markdown:

	pandoc -s example4.tex -o example5.text

* Converting a web page to markdown:

	pandoc -s -r html http://www.gnu.org/software/make/ -o example12.text

* PDF with numbered sections and a custom LaTeX header:

	pandoc -N --template=mytemplate.tex --variable mainfont=Georgia
	--variable sansfont=Arial --variable monofont="Bitstream Vera Sans
	Mono" --variable fontsize=12pt --variable version=1.10 README
	--latex-engine=xelatex --toc -o example14.pdf

* HTML slide shows:

	pandoc -s --mathml -i -t dzslides SLIDES -o example16a.html
	pandoc -s --webtex -i -t slidy SLIDES -o example16b.html
	pandoc -s --self-contained --webtex -i -t s5 SLIDES -o example16c.html
	pandoc -s --mathjax -i -t slideous SLIDES -o example16d.html

* TeX math in HTML:

	pandoc math.text -s -o mathDefault.html
	pandoc math.text -s --mathml -o mathMathML.html
	pandoc math.text -s --webtex -o mathWebTeX.html
	pandoc math.text -s --mathjax -o mathMathJax.html
	pandoc math.text -s --latexmathml -o mathLaTeXMathML.html

* Pandoc uses the UTF-8 character encoding for both input and output 

If your local character encoding is not UTF-8, you should pipe input and output through:


## creating a pdf ##

Pandoc will create a latex file and use pdflatex (or another engine,
see --latex-engine)

	pandoc test.txt -o test.pdf

## General options ##
	
Specify input format

	-f FORMAT, -r FORMAT, --from=FORMAT, --read=FORMAT

Specify output format

	-t FORMAT, -w FORMAT, --to=FORMAT, --write=FORMAT

Write output to FILE instead of stdout

	-o FILE, --output=FILE

Specify the user data directory to search for pandoc data files.

	--data-dir=DIRECTORY


