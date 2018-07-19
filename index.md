---
title       : Slidify 
subtitle    : A little bit more sysadmin oriented tutorial
author      : Goyo Ambrosio
job         : Jul. 18 2018
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : zenburn       # {zenburn, tomorrow, solarized-dark, ...}
widgets     : bootstrap     # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
logo        : goyologo.png  # Graphic files will be in ~/myDeck/assets/img
biglogo     : goyologo.png
license     : by-nc-sa
github:
  user: goyoambrosio
  repo: SlidifyTutorial
  branch: "gh-pages"
assets      : {assets: ../../assets}       # Add an assets directory
libraries   : {libraries: ../../libraries} # Add a libraries directory
ext_widgets : {rCharts: [libraries/nvd3, libraries/leaflet, libraries/dygraphs]}
---


<!--
If you want to enable automatic prompt generation use
{bash ,prompt=TRUE, eval=FALSE}
{r, prompt=TRUE, eval=FALSE}
-->


## R presentations

R presentations are presentations coded as Rmarkdown and then translated to HTML
using the R programming language framework.

Rmarkdown is a markdown based R syntax that helps make documents in many different formats.

There are many different ways to make *r presentations* in RStudio (`oslides`, `Slidy`, `Beamer`, ...)

Slidify exists as a package with a huge online community and popularity.

Slidify has the most options and flexibility but you mustn't to use it until you
are more comfortable with R packages and general syntax.

*** =pnotes

R presentations are presentations coded as HTML created with the R programming language framework.

Rmarkdown is a markdown based R syntax that helps make documents in many different formats.

In RStudio, you simply create a new rmarkdown file, write your text/code, and
runs `knitr` and `pandoc` to turn your raw text into a complete HTML, named *r
presentations*, or PDF document.

There are many different ways to make *r presentations* in RStudio but three main
choices: `ioslides`, `Slidy`, and `Beamer`.

On the other hand, Slidify exists as a package with a huge online community and popularity.

Slidify has the most options and flexibility. This package is clearly aimed at
the intermediate to advanced R community and you mustn't to use slidify until
you are more comfortable with R packages and general syntax.

Slidify also uses `knitr` but renders HTML pages using [Whisker](Slidify uses
[whisker](https://github.com/edwindj/whisker)

References:

[Comparisons between ioslides and Slidify in R Markdown Presentation](http://yintingchou.com/others/2017/05/26/ioslides-slidy.html)

[Introduction to Presentations in Rmarkdown](http://data-analytics.net/cep/Schedule_files/presentations_demo.html**

---

## What is Slidify

Slidify is a tool that makes it easy to create, customize and publish,
reproducible HTML5 slide decks using R Markdown.

Slidify helps create, customize and share, elegant, dynamic and interactive
HTML5 documents using R Markdown.

It is is an almagamation of other technologies including knitr, Markdown, and
several javascript libaries

It allows embedded code chunks and mathematical formulas

You can view slidify presentations with any web browser and share them easily
on Github, Dropbox, or your own website

*** =pnotes

Slidify uses [whisker](https://github.com/edwindj/whisker) to render the final
html by passing the parsed data to the layout file.

Whisker is a [{{Mustache}}](http://mustache.github.io/) implementation in R
confirming to the Mustache specification. 

Mustache is a logicless templating language, meaning that no programming source
code can be used in your templates.

--- .segue bg:grey

# Set up your workspace

---

## Things you need 

To work with slidify you need the right environment:

- A language and environment for statistical computing and graphics:
  [R](https://www.r-project.org/)
- An integrated development environment (IDE) for R:
  [RStudio](https://www.rstudio.com/)
- Optionally a powerful more-than-an-editor like
  [Emacs](https://www.gnu.org/software/emacs/) customized with
  [Spacemacs](http://spacemacs.org/), [ESS](https://ess.r-project.org/) and
  [Polymode](https://github.com/vspinu/polymode).
- A way to install R packages under development (i.e. slidify):
  [devtools](https://github.com/r-lib/devtools)

Preferably in Linux!

*** =pnotes

[Spacemacs](http://spacemacs.org/) is an open source Emacs distribution, aimed
at providing a bridge between Emacs and Vim.

[ESS](https://ess.r-project.org/) (Emacs Speaks Statistics) is an add-on package
for Emacs. It is designed to support editing of scripts and interaction with
various statistical analysis programs such as R.

[Polymode](https://github.com/vspinu/polymode) is an emacs package that offers
generic support for multiple major modes inside a single emacs buffer. It is
necessary to allow the mix of modes present in Rmd files, specially `markdown`
and `R` modes but also other major modes.

---{class: smaller}

## How to install R

The Ubuntu archives on CRAN are signed with the key of “Michael Rutter". To add
the key to your system run:

```sh
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
```

edit the `source.list` file

```sh
sudo vim /etc/apt/sources.list
```

and add the corresponding source to your operating system version [Ubuntu 16.04|17.10|18.04]

```sh
deb https://cloud.r-project.org/bin/linux/ubuntu [xenial|artful|bionic]-cran35/
```

Finally, to install the complete R system, run:

```sh
sudo apt update
sudo apt install r-base
```

---

## How to install RStudio

[Download](https://www.rstudio.com/products/rstudio/download/) RStudio.

Install it (`rstudio-xenial-1.1.453-amd64.deb` in this case) from command prompt 

```shell
# For Debian based
sudo dpkg -i rstudio-xenial-1.1.453-amd64.deb
# install dependencies
sudo apt install -f
```

Or click deb file through the file manager. Ubuntu will install it and its dependencies.

---

## How to install Emacs and Spacemacs

As usual, run this command

```bash
sudo apt install emacs
```

Download [SourceCode Pro
font](https://github.com/adobe-fonts/source-code-pro/archive/2.030R-ro/1.050R-it.tar.gz),
uncompress and install. (it takes some seconds ... don't suspect, it's working)

```bash
sudo mv ~/Downloads/source-code-pro-2.030R-ro-1.050R-it/OTF /usr/share/fonts/opentype
sudo fc-cache -f
```

To install Spacemacs type

```bash
git clone https://github.com/syl20bnr/spacemacs ~/.emacs.d
```

The first time you run Spacemacs you must to answer three initial configuratation questions.


---{class: smaller}

## How to install ESS and polymode major modes for Emacs

Edit `.spacemacs`, usually under your home directory.

1. Activate `ess` configuration layer  
```
dotspacemacs-configuration-layers
'(ess)
```

2. Add `polymode` package as additional package  
```
dotspacemacs-additional-packages '(polymode)
```

3. Add extension associations  
```
dotspacemacs/user-config ()
(add-to-list 'auto-mode-alist '("\\.Rmd$" . poly-markdown+r-mode))
```

---

## How to install devtools

Previously you need to install some libraries in your system:


```bash
$ sudo apt-get install build-essential libcurl4-gnutls-dev libxml2-dev libssl-dev
```

Now run R as `sudo` and install the package

```sh
$ sudo -i R
```


```r
> install.packages('devtools')
```

---

## How to install slidify 

Now you are ready to install Slidify

Slidify is not on CRAN and needs to be installed from github using the `devtools`
package. 

```r
pkgs <- c("slidify", "slidifyLibraries", "rCharts")
devtools::install_github(pkgs, "ramnathv")
```

If you are brave, <http://slidify.github.io> recommends installation of the
package `dev` version but I don't recommend it.

```r
devtools::install_github(pkgs, 'ramnathv', ref = 'dev')
```

Now you are ready to create your first slidify presentation.

--- 

## Create a new Deck

Each presentation is called a 'deck'. To create a new deck open R, set
your working directory and use the `author` command.

```r
setwd("/path/to/")
require(slidify)
author("myDeck")
```

`/path/to/myDeck` is created.

Create a R Project from Existing Directory

```
File -> New Project -> Existing Directory -> /path/to/myDeck -> Create Project
```

A file called `myDeck.Rproj` will be created under `/path/to/myDeck`.

*** =pnotes

Then, automatically:

- A directory with the name of your project is created inside of your current directory.
- Inside of this directory an assets directory and a file called “index.Rmd” is created.
- The assets directory is populated with the following empty folders: css, img, js, and layouts.

---{class: smaller}

## Add version control with Git 

If git is installed, then the `author` command also initializes a git repository,
switchs to a `gh-pages` branch and commit all changes.

Before uploading your deck to your favourite Git cloud provider create
`.gitignore` to avoid version control for non essential files.

```sh
cd /path/to/myDeck
touch .gitignore
vim .gitignore
```

Add your [ignored extensions](.gitignore)

```sh
# RStudio files #
.Rproj.user
.Rhistory
.RData
.Ruserdata
# ...
```

---

## Upload the new repository to BitBucket or GitHub

Create an empty Repository, e.g. `myDeck` in BitBucket or GitHub. With an empty
repository a default branch called `master` won't be created. Then `push` the
local `myDeck` repository to the remote `myDeck` repo. Note that a new branch
called `gh-pages` has been created.

```sh
cd /path/to/myDeck
git add .
git commit -am "Initial commit"
git remote add origin_github https://github.com/username/myDeck.git
git remote add origin_bitbucket https://username@bitbucket.org/username/myDeck.git
git push -u origin_[github|bitbucket] --all
git push -u origin_[github|bitbucket] --tags
```

Now you can work with your new repository as usual

---

## Cloning your repo


To clone the repo on your machine take in account that you'll need to clone `gh-pages` branch

```sh
git clone -b gh-pages https://github.com/username/myDeck.git
```

or

```sh
git clone -b gh-page https://username@bitbucket.org/username/myDeck.git
```

---

## Editing with Emacs and RStudio

index.Rmd is the only file you need to edit and for that you have two ways:

- Using RStudio opening the project file, e.g. `/path/to/myDeck/myDeck.Rproj`
- Using Emacs with ESS/Polymode major mode.

To take advantage of their editing capabilities RStudio and Emacs can be used simultaneously.

You can enable Emacs keybindings within RStudio using the Code section of the
Global Options dialog.

Changes made to the edited files will be updated in real time both in Emacs and RStudio.

--- 


## Slidify it !

```r
slidify("index.Rmd")
browseURL("index.html")
```

and don't forget to update your git repository

``` shell
git status
git commit -am "Updating my repository"
git push
```

--- .segue bg:grey

# Edit slides

---

## index.Rmd = YAML + R Markdown

index.Rmd is the R Markdown document which you will use to compose the content of your presentation.

It's composed of a YAML section and a body section.

[YAML metadata](https://github.com/ramnathv/slidify/wiki/Page-Properties)
includes the `title`, `subtitle`, `author`, and `job` of the author. Also
includes what slide `framework` you wish to use, which code `highlighter` you
wish to use, and any `widgets` you want to include.

In addition it can include other fields like a `logo` to appear in your title
slide under logo, the path to your `assets` folder and the paths to any other
folders you may be using under url, and the specific theme for your code
highlighter of choice under `hitheme`.

Under YAML you can include your slides just using R Markdown to write them.

[R Markdown](https://rmarkdown.rstudio.com/) is a file format for making dynamic
documents with R. An R Markdown document is written in
[markdown](https://en.wikipedia.org/wiki/Markdown) and contains chunks of
embedded R (and other languages** code.

*** =pnotes

YAML is a superset of JSON.

---{class: smaller}

## How YAML looks

    ---
    title       : Slidify 
    subtitle    : A little bit more sysadmin oriented Tutorial
    author      : Gregorio Ambrosio
    job         : Apr. 17 2018
    framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
    highlighter : highlight.js  # {highlight.js, prettify, highlight}
    hitheme     : zenburn       # {zenburn, tomorrow, solarized-dark, ...}
    widgets     : bootstrap     # {mathjax, quiz, bootstrap}
    mode        : selfcontained # {standalone, draft}
    knit        : slidify::knit2slides
    logo        : goyologo.png  # Graphic files will be in ~/myDeck/assets/img
    biglogo     : goyologo.png
    license     : by-nc-sa
    github:
      user: goyoambrosio
      repo: SlidifyTutorial
      branch: "gh-pages"
    assets      : {assets: ../../assets}       # Add an assets directory
    libraries   : {libraries: ../../libraries} # Add a libraries directory
    ext_widgets : {rCharts: [libraries/nvd3, libraries/leaflet, libraries/dygraphs]}
    ---

---

## Slides

Your first slide begins under YAML and looks like this:

```markdown
--- .myClass #myId &myLayout 
or 
---{class: myClass, id: myId, tpl: myLayout}

## Slide Title

- Whatever you put after `##` will be the title of the slide.
- Each slide needs to be preceeded by an empty line followed by `---`
  this denotes the beginning of a new slide and the end of the previous slide.
- `.class #id` are `CSS` attributes you can use to customize the slide.
- Whatever you put between `##` and `---` is up to you! As long as it is
  valid R Markdown or `HTML`.
```

---

## Blocks

Blocks are slides nested within a slide, identified by three stars. Just like a
slide, they can contain properties, title and content.

There are two types of blocks - named and unnamed. A block can be named by
specifying the property `{name: block1}` (or using the symbolic shortcut
`{=block1}`).

A block with the name `block1` can be accessed in a slide layout as
`slide.block1`. The title and content of this block can be accessed as
`slide.block1.title` and `slide.block1.content**. Unnamed blocks are aggregated
into the namespace `slide.blocks**.

---

<img style='margin-top: -40px' class="center" src='assets/img/slide_properties.svg' width=960px height=250px></img> 

---{class: [segue, dark]}

# Slide Customization

---

## Slide customization

- **Properties**. They are implemented as *css*. You can find them in
  `libraries/frameworks/io2012/css` or write your own css files under
  `assets/css`. Your css files will be loaded when open you slidify
  presentation.
- **Layouts**. They are implemented as *html* files conforming mustache
  specifications under `libraries/frameworks/io2012/layouts`. Also you can write
  your own layouts and locate them under `assets/layouts`.
- **Widgets**. A widget is a collection of stylesheets, javascripts and layouts
  that add additional functionality to a slide deck.

With io2012 framework you have two layouts: `twocol.html` and `vcenter.html`
besides the default `slides.html`. Be careful with the examples because they
often use their own layouts.

This presentation also uses its own files as `assets/css/app.css` and
`assets/layouts/carousel.html`.

---{class: [segue, dark]}

# Properties

---

## Slide properties

Slide properties, i.e. attributes, are key-value pairs that are passed to the
layout.They are valid YAML and are written after `---` as follows

```
.class_name_1 .class_name_2 #id_value
class:[class_name_1, class_name_2] id:id_value
{class: [class_name_1, class_name_2], id: id_value}
```

The three lines are equivalent. The first one follows symbolic css style
prefixes where a dot indicates class, a hash refers to id and an ampersand
identifies a layout.

e.g.

```
.segue #myId bg:blue 
class:segue id:myId bg:blue
{class: segue, id: myId, bg: blue}
```

For clarity we will use the third option

---
## Slide properties table

| VARIABLE       | DESCRIPTION                           |
|----------------|---------------------------------------|
| slide.title    | The title of the slide with no markup |
| slide.header   | The title of the slide with markup    |
| slide.level    | The title header level (h1 - h6)      |
| slide.content  | The contents of the slide sans header |
| slide.html     | The contents of the slide with header |
| slide.num      | The number of the slide               |
| slide.id       | The id assigned to the slide          |
| slide.class    | The class assigned to the slide       |
| slide.bg       | The background assigned to the slide  |
| slide.myblock  | The slide block named myblock         |
| slide.blocks   | The slide blocks which are not named  |
| slide.rendered | he rendered slide                     |

---

## Slide to parse

```
--- {class: class_name, id: id_value, bg: color_name}

## Slide Title

Slide Contents
```

---{class: smaller}

## Parsed slide

```
$html
[1] "<h2>Slide Title</h2>\n\n<p>Slide Contents</p>\n"

$header
[1] "<h2>Slide Title</h2>"

$level
[1] "2"

$title
[1] "Slide Title"

$content
[1] "<p>Slide Contents</p>\n"

$class
[1] "class_name"

$bg
[1] "color_name"

$id
[1] "id_value"
```

---{class: [segue, dark]}

# Layouts

---

## About layouts

Slidify uses [whisker](https://github.com/edwindj/whisker) to render the final
html by passing the parsed data to the layout file.

Whisker is a [mustache](http://mustache.github.io/) implementation in R
confirming to the mustache specification. 

A layout is a *mustache template* that specifies
the markup to render a slide.

To identify a layout you can use an ampersand (&) or `tpl` as key. e.g.
`---&layout_name` or `---tpl:layout_name`

Slidify combines the parsed slide plus the layout to render the HTML.

--- 

## Creating a layout

To create a new layout you must to make a new `.html` file conforming the mustache
specification under your `assets/layouts` directory.

Insert your code and reference it as a slide property, i.e.

```sh
cd /path/to/myDeck/assets/layouts
touch myLayout.html
vim myLayout.html
```

and then use it in your slide as follows

    ---&myLayout

or

    ---{tpl: myLayout}

---{class: [RAW, smaller]}

## Carousel layout

	 ---
	 layout: test 
	 ---
	 {{{ slide.content }}}
	 <div id="{{slide.id}}-carousel" class="carousel slide {{slide.class}}">
	     <!-- Indicators -->
	     <ol class="carousel-indicators">
	         {{# slide.blocks }}
	         <li data-target="#{{slide.id}}-carousel" data-slide-to="{{num}}" class="{{class}}"></li>
	         {{/ slide.blocks }}
	     </ol>
	     <!-- Wrapper for slides -->
	     <div class="carousel-inner">
	         {{# slide.blocks }}
	         <div class="item {{class}}">
	             <img src="{{img}}" alt="{{alt}}">
	             <div class="carousel-caption">{{{ content }}}</div>
	         </div>
	         {{/ slide.blocks }}
	     </div>
	     <!-- Controls -->
	     <a class="left carousel-control" href="#{{slide.id}}-carousel" data-slide="prev">&lsaquo;</a>
	     <a class="right carousel-control" href="#{{slide.id}}-carousel" data-slide="next">&rsaquo;</a>
	 </div>

--- {tpl: carousel, class: span12}

## Carousel

*** {class: active, img: "assets/img/apply.svg"}

Image 1

*** {img: "assets/img/split.svg"}

Image 2

---

## Vcenter layout

vcenter layout presents content in the slide center.

Use vcenter layout as follows

    ---&vcenter
    
or

    ---{tpl: vcenter}

---&vcenter

<q>Slide contents</q>

---.smaller

## Two columns Layout

Two columns layout presents content distributed in two columns.

Use layout as follows

    ---&twocol w1:40% w2:60%

    ## Using twocol layout

    This slide has two columns

    *** =left

    - point 1
    - point 2
    - point 3

    *** =right

    - point 1
    - point 2
    - point 3

---&twocol w1:40% w2:60%

## Using twocol layout

This slide has two columns
    
*** =left
    
- point 1
- point 2
- point 3
    
*** =right

- point 1
- point 2
- point 3


---{class: [segue, dark]}

# Playing with code


---

## Code hightlighting

We want that our code blocks look good. Syntax highlighting let us to make code clear and understable.

Usage:

    ```<language>
    ... code
    ```

---

## Using Hightlight.js ##

Highlight.js is a syntax highlighter written in JavaScript. It works with pretty
much any markup, doesn’t depend on any framework and has automatic language
detection.

Main features

- 176 languages and 79 styles
- automatic language detection
- multi-language code highlighting
- available for node.js
- works with any markup
- compatible with any js framework

[hightlight.js demo](https://highlightjs.org/static/demo/)

[CSS classes reference](http://highlightjs.readthedocs.io/en/latest/css-classes-reference.html)


---

## Knitr

The [knitr](https://yihui.name/knitr/) package was designed based on the idea of
[“Literate Programming” (Knuth
1984)](http://www.literateprogramming.com/knuthweb.pdf), which allows you to
intermingle program code with text in a source document.

When knitr compiles a document, the program code (in code chunks) will
be extracted and executed, and the program output will be displayed together
with the original text in the output document.

<!-- Example of using triple backticks by means of unicode characters coded as decimal inside markdown. --> 
<!-- <code></code> html tags are used to hightlight triple backticks --> 

For instance, for an R Markdown (Rmd) document, we write code chunks between
<code>&#0096;&#0096;&#0096;\{r\}</code> and <code>&#0096;&#0096;&#0096;</code> and inline R code
is written in <code>&#0096;r \<expr\>&#0096;</code>. Chunk options are written
before the closing brace in the chunk header.

knitr support a lot of computer languages that are implemented in [knitr language
engines](https://yihui.name/knitr/demo/engines/).

*Note that knitr converts `{<language_name> ...}` to `<language_name>` but the
language name in knitr corresponds to the engine that executes the code but
does not have to correspond to the name used by hightlight.js.*


---{class: smaller}

## Running bash scripts

    
    ```r
    # should exist
    Sys.which('bash')
    Sys.which('sh')
    ```

Does `bash` work?

    
    ```bash
    echo hello world
    echo 'a b c' | sed 's/ /\|/g'
    # number of lines
    awk 'END{print NR;}' 027-engine-bash.Rmd
    ```

How about `sh`?

    
    ```sh
    # run wc on all engine examples
    ls | grep engine | head -n8 | xargs wc
    ```

---{class: [segue,dark]}

# Recipes

---

## Section

```md
---{class: [segue, dark]}

## Section name
```

```md
---{class: segue, bg: green}

## Section name
```

---

## Table

```md
## This is a table

| **Variable**    | **Description**                       |
|-----------------|---------------------------------------|
| `slide.title`   | The title of the slide with no markup |
| `slide.header`  | The title of the slide with markup    |
| `slide.level`   | The title header level (h1 - h6)      |
| `slide.content` | The contents of the slide sans header |
| `slide.html`    | The contents of the slide with header |
| `slide.num`     | The number of the slide               |
| `slide.id`      | The id assigned to the slide          |
| `slide.class`   | The class assigned to the slide       |
| `slide.bg`      | The background assigned to the slide  |
| `slide.myblock` | The slide block named myblock         |
| `slide.blocks`  | The slide blocks which are not named  |
| `slide.rendered`| The rendered slide                    |
```

---{class: green}

## Changing page number color

```md
---{class: green}

## Slide Title

Slide Content
```

---

## Corner banner: `example` class

```html
<a class='example' href="http://your.url">click here</a>

## Slide Title

Slide content
```

<a class='example' href="http://goyoambrosio.com">click here</a>

---

## Corner banner: `definition` class

```html
<a class='definition' href="http://your.url">click here</a>

## Slide Title

Slide content
```

<a class='definition' href="http://goyoambrosio.com">click here</a>

---{class: smaller}

## Image inclusion

To include an image in your slide you must insert html code as follows:

```
<img style='margin-top: 5px' class="center" src='assets/img/slide_properties.svg' width=500px></img> 
```

<img class="center" src='assets/img/slide_properties.svg' width=500px></img> 

---

Also sometimes you will find the following code

```
<iframe src='assets/img/slidify_banner.png'></iframe>
```
   
<iframe src='assets/img/slidify_banner.png'></iframe>

---

## Quoted text

Use `<q>...</q>` html tags

    <q> Slidify helps __create__, customize and share, elegant, dynamic and ...</q>

<q> Slidify helps __create__, customize and share, elegant, dynamic and interactive HTML5 documents using R Markdown.</q>

---

## Inserting text file content

Sometimes you'll need to include raw code or text in your slide.

You can to create a text raw file and insert it as follows

	 ---{class: RAW}
	 
	 ## Slide
	 
	 ``` {r results = 'asis', echo = F}
	 writeLines(paste('\t', readLines('assets/includes/myfile.txt')))
	 ```

---

## Slide with custom background

Two options:

```
---{bg:url(assets/img/<my_image_file>)}
```

or

```
---{id:custbg}

## Slide with custom background

<style>
#custbg {
  background-image:url(assets/img/<my_image_file>); 
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
}
</style>
```


---

## Presenter display and presenter notes

You can define speaker notes within any slide by adding the line `*** =pnotes`
before it. Here is an example of a slide with speaker notes.

You can view speaker notes by pressing the key `p` which acts as a toggle and
automatically opens the presenter view. 

For `io2012`, you need to add `?presentme=true` to the presentation url, which
will then open the presenter view.

You can also include an image in the presenter display using markdown syntax,
e.g.
`![](http://codingsomething.files.wordpress.com/2013/02/screenshot.png?w=652)`

    *** =pnotes
    Presenter notes
    ![](http://codingsomething.files.wordpress.com/2013/02/screenshot.png?w=652)



*** =pnotes

Presenter notes  
![](http://codingsomething.files.wordpress.com/2013/02/screenshot.png?w=652)

---


## Comment out a slide

Change 

    ---
    Slide 1 content
    ---
    Slide 2 content
    ---

by

    ---
    <!--
    Slide 1 content
    -->
    Slide 2 content
    ---

--- #stackedit

## Using `iframe`

 <iframe src = 'https://stackedit.io' height='600px'></iframe>

---{class: [segue, dark]}

# CSS related

---

## Changing background in all slides at once

Include this in your `/assets/css/mycss.css`:

```css
slides > slide {
  background: #hex !important;
}
```

---{class: smaller}

## Changing the font type on slides

```css
@import url(http://fonts.googleapis.com/css?family=Baumans);

.title-slide hgroup > h1{
font-family: 'Baumans', cursive;
}

.title-slide hgroup > h2{
  font-family: 'Oswald', 'Calibri', sans-serif;
}

/* Fonts and Spacing */
article p, article li, article li.build, section p, section li{
  font-family: 'Open Sans','Helvetica', 'Crimson Text', 'Garamond',  'Palatino', sans-serif;
  text-align: justify;
  font-size:22px;
  line-height: 1.5em;
  color: #AA7139;
}

...

```

*** =pnotes

```css
@import url(http://fonts.googleapis.com/css?family=Baumans);

.title-slide hgroup > h1{
font-family: 'Baumans', cursive;
}

.title-slide hgroup > h2{
  font-family: 'Oswald', 'Calibri', sans-serif;
}

/* Fonts and Spacing */
article p, article li, article li.build, section p, section li{
  font-family: 'Open Sans','Helvetica', 'Crimson Text', 'Garamond',  'Palatino', sans-serif;
  text-align: justify;
  font-size:22px;
  line-height: 1.5em;
  color: #AA7139;
}

slide:not(.segue) h2{
  font-family: 'Calibri', Arial, sans-serif;
  font-size: 52px;
  font-style: normal;
  font-weight: bold;
  text-transform: normal;
  letter-spacing: -2px;
  line-height: 1.2em;
  color: #AA9A39;
}

/* Reduce Space between Title and Body */
slides > slide > hgroup + article {
  margin-top: 15px;
}

slides > slide {
    background: #303E73;
}

.title-slide {
  background-color: #303E73; /* #EDE0CF; ; #CA9F9D*/
  /* background-image:url(http://goo.gl/EpXln); */
}

.title-slide hgroup > h1, 
.title-slide hgroup > h2 {
  color: #AA7139 ;
}

```

---{class: [segue, dark]}

# Other stuff

---

## Tutorials and resources

1. [Introduction](http://slidify.github.io/workshops/tutorials/01)
2. [Frameworks](http://slidify.github.io/workshops/tutorials/02)
3. [Layouts](http://slidify.github.io/workshops/tutorials/03)
4. [Widgets](http://slidify.github.io/workshops/tutorials/04)
5. [Slidify on GitHub](https://github.com/ramnathv/slidify/wiki/Page-Properties)
6. [Ramnath Vaidyanathan on Github](https://github.com/ramnathv/slidify/wiki/Page-Properties)
7. [Slidify.org](http://slidify.org/)

--- {
 tpl: thankyou,
 social: [{title: www, href: "https://goyoambrosio.com"}, {title: e-mail, href: "mailto:contact@goyoambrosio.com"}]
}

## Thank You

For more information you can contact.


