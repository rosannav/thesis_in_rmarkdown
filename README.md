Note: these are old blog posts that I wrote in 2016

Writing your thesis with R Markdown (1) – Getting started
=========================================================

Looking to use R Markdown to create your thesis? You have come to the right place. R Markdown is a great tool for integrating data analysis and report writing, but it can be a bit daunting to get started. I wrote my thesis with R Markdown last year, and sure spent quite some time browsing the internet figuring out how to get my text, code, and figures to work together and turn into a coherent thesis. But it was worth the struggle (and an excellent way to procrastinate), and I’d love to share with you what I’ve learned.

This will be a series of blog posts discussing how to write a thesis with R Markdown. We’ll start with the very basics: installing the necessary software and getting familiar with the various markup languages you’ll need. Then we’ll prepare an R Markdown document that will represent one thesis chapter. When I wrote my thesis, I wanted to do the following things in each chapter:

*   Writing text
    *   Spelling check this text
    *   Comment on this text
*   Writing equations
    *   With references
    *   And captions
*   Including figures (non-R creations)
    *   With references
    *   And captions
*   Citing stuff
    *   And add a bibliography
*   Adding R code
    *   Render R code
    *   Add figure captions to R rendered figures + references
*   Including tables
    *   Really difficult tables

In the next blog post, I will explain how to do each of these things in a thesis chapter (_UPDATE: I have decided to split the chapter contents blog post into to blog posts, 1: text, citations and equations and 2: figures, R code and tables_). Then, I’ll show how to use multiple documents together, and get the fiddly layout bits like page numbering, title pages and table of contents stuff working to create a full thesis document. But first, let’s get started with the basics.

**Getting started: What do we need?**

**Languages and tools:** R, [Markdown](https://daringfireball.net/projects/markdown/), [Rmarkdown v2](http://rmarkdown.rstudio.com/), [Latex](https://www.latex-project.org/), YAML, [BibTeX](http://www.bibtex.org/) **Software:** [R](https://cran.r-project.org/) & [RStudio](https://www.rstudio.com/products/rstudio/download/), pdflatex ([MikTeX](http://miktex.org/download) on windows, [MacTeX](https://tug.org/mactex/mactex-download.html) on mac), [Mendeley](https://www.mendeley.com/download-mendeley-desktop/) **R Package:** knitr, use this code:

    install.packages("knitr")
    library(knitr)
    

Don’t worry, it sounds way scarier than it actually is. **Markdown** is a very simple and straightforward language. No need to worry about it now, but if you’d like to get more familiar with it have a look at [this reference guide](https://daringfireball.net/projects/markdown/) or [learn it here](http://markdowntutorial.com/). **R Markdown** is almost the same as Markdown, but has the added feature off embedding and dealing with R code in your documents. **LaTeX** is another markup language, that is not as easy to read and write as Markdown but allows for much more flexibility in creating your document. The code that is placed at the top of document is called **YAML,** and it explains how the document should be rendered. **BiBTeX** is an excellent reference management system (if you are used to the horror of inserting references with MS word add-ons, you are going to be really happy using this :). BiBTeX files can be created with Mendeley, more on this later.

Here is an example of an R Markdown document, and how each of the languages are used:

[](https://rosannavanhespenresearch.files.wordpress.com/2016/01/repro_res_ex1_decorated.png)

![repro_res_ex1_decorated](https://rosannavanhespenresearch.files.wordpress.com/2016/01/repro_res_ex1_decorated.png?w=584)

  
_Click on the image to enlarge._

You can see there’s quite a few different languages used in the same document. In the next blog post we will go into the details of each of these parts of the document. For now, (once everything is installed and communicating with each other – if you are having problems, feel free to leave a question in the comments), I recommend to just play around with R Markdown for a bit to get a feel for it. You can do this by going to _Rstudio > File > New File > R markdown… > OK_. This opens a standard R Markdown file (.rmd) with some instructions.

Good luck!

_You may find yourself worrying about this at some poin (probably not yet, but when you do, you’ll know where to look): there are multiple types of markdown, which are called flavours. Examples are ‘github markdown’, ‘multiple markdown’ and ‘pandoc markdown’. The markdown we are using here is called pandoc markdown._

Writing your thesis with R Markdown (2) – Text, citations and equations
=======================================================================

_This is the second post in a short series of tutorials to write your thesis in Rmarkdown. You can find instructions on how to get started in [the first post](https://www.rosannavanhespen.nl/2016/02/16/writing-your-thesis-with-r-markdown-1-getting-started/). Note that these tutorials were written by a Windows user, so if you are using a different operating system some details may differ._

Welcome back to part two in this short series of tutorials! In the last post we looked at setting up all software and what an R Markdown document looks like. Now we will look at including text, citations, and equations in your thesis chapter. First up, writing plain text and headings:

Step 1: Writing plain text and headings
---------------------------------------

Take your standard Rmarkdown file (Rstudio > File > New File > R markdown… > OK) and remove all the text except for the YAML header (the bit between the three dashes). Now write a little bit of text. Click on ‘knit’ to see what the output looks like (Note: I’ll be using pdf output in the examples). You can try adding some headings by using #-signs to structure your text. Below is an example that uses different headings:

[![heading_example](https://rosannavanhespenresearch.files.wordpress.com/2016/02/heading_example.png?w=584)](https://rosannavanhespenresearch.files.wordpress.com/2016/02/heading_example.png)

Left: Writing headings in R Markdown. Right: .pdf output. _Click on image to enlarge._

Step 2: Citing someone
----------------------

Make sure you have Mendeley installed (you don’t necessary need to use Mendeley. You can also check if your preferred reference manager provides BibTeX output or [make your own bibtex file](https://www.economics.utoronto.ca/osborne/latex/BIBTEX.HTM) if you like. For the sake of speed and easiness, I’m going to use Mendely in my example).

If this is your first time using Mendeley and you don’t have any articles added yet, simply find a paper on you computer and drag and drop the pdf file into Mendeley.

Open Mendeley and select _Mendeley > Tools > Options > BibTeX_. Select ‘_Escape LaTeX special characters_’, ‘_Enable BibTeX syncing_’ and ‘_Create one BibTeX file for my whole library_’. Choose a path to sync your bibtex file to. Make sure you choose the same folder as where your R Markdown document lives. If you don’t want to do that, you can copy and paste the file into the R Markdown document directory, but realise that it is not longer automatically synced if you change something in Mendeley, so you’ll have to do update the bibtex file manually.

Now go to the R Mmarkdown document we made in step 1. In the YAML header, write ‘_bibliography: library.bib_’ (unless your .bib file has a different name), so your header will look like something this:

    title: "Untitled" 
    output: html_document 
    bibliography: library.bib
    

In Mendeley, check the citation key of the paper you want to cite (in the Document Details tab). In your R Markdown document, write the citation key in square brackets, for example . Below is an example of the output.

[![citation-example](https://rosannavanhespenresearch.files.wordpress.com/2016/02/citation-example.png?w=584)](https://rosannavanhespenresearch.files.wordpress.com/2016/02/citation-example.png)

Left: Using citations in R Markdown. Right: .pdf output. _Click on image to enlarge._

For information more information on citation syntax have a look at [here at the official R Markdown website](http://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html).

You can also change the citation style. Have a look at [this online .csl file database](https://github.com/citation-style-language/styles), chances are your preferred journal is on there (these files are usually correct, but check with the actual journal to make sure). Download the file and add it to the same folder as where R Markdown document lives. In your YAML header, add ‘_csl: your-preferred-citation-style.csl_’.

Step 3: Adding an equation
--------------------------

Inline equations can be added by writing dollar signs around an equation: ‘_$ a + b = c $_’. If you want to add an equation on it’s own line, simply add the LaTeX code for the equation (R Markdown will recognise the LaTeX automatically):

    \begin{equation}
    \label{eq-abc}
    a + b = c
    \end{equation}
    

The ‘_\\label{}_’ bit is used to give the equation a name, that you can use to refer to the equation in text, for example by writing: ‘_see equation `\ref{}`_’ or ‘_see `\autoref{}`_’ .I recommend choosing a label name that’s easy to remember and clearly explains what the equation is about. Below is an example of the equation in R Markdown and .pdf output.

You can find some excellent documentation on how to write latex equations [here](https://en.wikibooks.org/wiki/LaTeX/Mathematics).

[![equation-example](https://rosannavanhespenresearch.files.wordpress.com/2016/02/equation-example.png?w=584)](https://rosannavanhespenresearch.files.wordpress.com/2016/02/equation-example.png)

Left: Writing equations in LaTeX/R Markdown. Right: .pdf output. _Click on image to enlarge._

_That’s it for now! In the next post we will look at including figures, tables and R code. If you have any questions, feel free to post them in the comments._

Writing your thesis with R Markdown (3) – Figures, R code and tables
====================================================================

_This is the third post in a short series of tutorials to write your thesis in R Markdown. You can find instructions on how to get started in [the first post](https://cocky-elion-5880fb.netlify.app/2016/02/03/writing-your-thesis-with-r-markdown-1-getting-started/). These tutorials were written by a Windows user, so if you are using a different operating system some details may differ._

Welcome back to part three of this tutorial! In the [previous post](https://cocky-elion-5880fb.netlify.app/2016/02/17/writing-your-thesis-with-rmarkdown-2-text-citations-and-equations/) we looked at including text, citations, and equations in the thesis chapter. This time we’ll look at including figures, R code and tables. Let’s start with the figures:

### Step 4: Including a figure

You can include a figure in an R Markdown by writing `!(name_of_figure.jpg)` in the document. To make sure a caption shows up underneath your figure, we need to turn on the captions option, as in R Markdown it is turned off by default. You can do this by writing this bit in your YAML header:

    output:
      pdf_document:
        fig_caption: yes
    

The indentation of the above bit of text is important, knitr will not understand it if it is not written exactly like the above.

To refer to the figure in-text, a label needs to be added to the figure. This can be done by writing: `!(filename.png)` (what you are actually doing here is adding a LaTeX label to Markdown text). Then, you can write, for example, _see figure `\ref{}`_, or as you may remember from the previous post, _see `\autoref{}`_.

[![figure-example](https://rosannavanhespenresearch.files.wordpress.com/2016/02/figure-example.png)](https://rosannavanhespenresearch.files.wordpress.com/2016/02/figure-example.png)

Left: Adding a figure. Right: .pdf output. _Click on image to enlarge_

_Note: figures are seen as ‘floats’ by LaTeX, and therefore are not placed immediately where you call them. If you want to get more specific with how to place them and what height and such, I recommend you use latex syntax to include the figure instead of using the R Markdown syntax. You can read more [here](https://www.sharelatex.com/learn/Inserting_Images). I generally did not find it necessary in my thesis, but it requires some playing around to figure out what works best for your thesis._

### Step 5: using R code

This is where we get to the real magic of using R Markdown: including R code and data anlaysis directly into your thesis!

Here is how you include R code in your story. It’s called a code chunk:

    ```{r}
    plot(iris)
    ```
    

There are a bunch of values you can you give your code chunks. For example, if you don’t want to include code in your text, but just the output, you can write `{r include = FALSE}`. You can also suppress warnings by writing `{r warning = FALSE}`. If you don’t do this and something is wrong with your code, a warning message might be printed in your thesis. Anyway, there’s a whole list of things you can do with knitr chunks. I only discuss the ones I found necessary here, but if you’re interested, Yihui Xie, the developer of knitr, provides some [great documentation on his website](http://yihui.name/knitr/).

There are probably some things you want most of your code chunks to do, so you can set your own defaults for your thesis using:

    ```{r include=FALSE}
    knitr::opts_chunk$set(fig.path = /figures/, echo = FALSE, warning = FALSE, message = FALSE)
    ```
    

Basically what you are saying here is firstly, you want the figures to be saved in the folder ‘figures’, secondly, the R code itself won’t be printed, just the output, thirdly, warnings won’t be printed and finally, messages (similar to warnings) won’t be printed either.

_Note: If you are making rather big calculations in the code chunks, this can make it slow to render your thesis (i.e. knitting). You can cache files with `cache=TRUE`. Note that you will need to turn this off if you want to update your calculations._

One of the great things about including R code directly in your thesis is that you can generate and change figures as you go. To create a figure in your thesis using R code, just write the R code as you would normally when making a figure, for example:

    ```{r fig.cap = "figure caption. \\label{figurelabel}", fig.height=12, fig.width=10}
    plot(iris)
    ```
    

As you can see, I’ve added some info to the R code chunk about how to render the figure. I defined a figure caption with `fig.cap` and added a LaTeX label for in-text reference. Don’t forget to write the double backslash when adding a label name.

You can also refer to stuff in your text, that you calculated inside a code chunk. For example, if the code chunk says:

    ```{r include = FALSE}
    variable_t = 3 * 4
    ```
    

you can refer to that in text by simply writing: `` `r variable_t` ``.

Below is image that compares the .rmd file and the .pdf output to show what kind of output each code chunk produces.

[![rcode-example](https://rosannavanhespenresearch.files.wordpress.com/2016/02/rcode-example.png?w=584)](https://rosannavanhespenresearch.files.wordpress.com/2016/02/rcode-example.png)

Left: Using R code in R Markdown. Right: .pdf output. _Click on image to enlarge._

### Step 6: Including a table

Sometimes you find yourself needing to include a table. [Markdown](http://rmarkdown.rstudio.com/authoring_pandoc_markdown.html#tables) and [kable](http://www.inside-r.org/packages/cran/knitr/docs/kable) can do the trick, but I do not recommend using it for ‘serious, thesis-grade’ tables. In a thesis, you will almost always find yourself wanting more flexibility than Markdown and kable can offer. I therefore highly recommend using LaTeX when including tables.

This is some simple LaTeX code for a neat-looking table you might want to use in your thesis:

    \begin{table}
    \centering
    \caption{}
    \label{table-paramvalues}
    \begin{tabular}{ p{4cm} p{4cm} p{4cm} }
    \hline \\ 
    colname &amp; colname &amp; colname \\ 
    \hline \\ 
    Info & info & info \\ 
    Info & info & info \\ 
    Info & info & info \\ 
    \hline
    \end{tabular}
    \end{table}
    

I will not go into great detail about LaTeX tables here, but if you’d like some more information, have a look at this [Wiki](https://en.wikibooks.org/wiki/LaTeX/Tables). If you’re finding LaTeX tables a bit confusing, you can also write your table in excel and then upload it to [this website](http://www.tablesgenerator.com/): it will make a LaTeX table for you. Also, I had to use a couple of multi-page tables in my thesis. If you find you need to do the same, have a google search for ‘latex longtable’.

_Note: References are note translated to LaTeX, but into plain text. This means that you cannot add any R Markdown references (i.e. ) in a LaTeX table. If you want more information, it got me quite confused as well, so I wrote a question and then an answer about it on [tex.stackexchange.com](http://tex.stackexchange.com/questions/272475/citations-in-tabular-environment-not-working/290915#290915)._

[![table-example](https://rosannavanhespenresearch.files.wordpress.com/2016/02/table-example.png?w=584)](https://rosannavanhespenresearch.files.wordpress.com/2016/02/table-example.png)

Left: Including a LaTeX table. Right: .pdf output. LaTeX automatically places tables at the bottom of the page. Click on image to enlarge.

And that’s it! Of course this is only one chapter, so in the next post we’ll have a look a writing multiple chapter in multiple .rmd files, how to put together and turn it into a pretty thesis. If you have any questions, feel free to post them in the comments or shoot me an email!

Writing your thesis with R Markdown (4) – Putting the thesis together
=====================================================================

March 29, 2016 Categories: RMarkdown

_This is the fourth post in a short series of tutorials to write your thesis in R Markdown. You can find instructions on how to get started in [the first post](https://cocky-elion-5880fb.netlify.app/2016/02/03/writing-your-thesis-with-r-markdown-1-getting-started/). These tutorials were written by a Windows user, so if you are using a different operating system some details may differ._

Welcome back! You have arrived at the fourth part of this tutorial. In [the previous post](https://cocky-elion-5880fb.netlify.app/2016/03/18/writing-your-thesis-with-r-markdown-3-figures-r-code-and-tables/) we looked at including figures, R code, and tables IN the thesis chapter. This time we’ll be looking at making multiple chapters, putting them together and turnING them into a thesis. In the next (and hopefully last) post I will show you how to adjust the thesis layout. Let’s get started!

**Step 1: Merging multiple chapters into one thesis**

You may have found that writing your whole thesis in one document can quickly get confusing. If you are like me, you have probably written multiple chapters in multiple documents. So let’s make a ‘parent document’ called THESIS.rmd that contains all the ‘child’ chapters. In R Markdown you can easily do this using this bit of code (assuming you keep chapters in the same folder as the THESIS.rmd file) in your THESIS.rmd file:

    ```{r child = 'chapterxx.Rmd'}
    ```
    

You can add as many child documents to the parent document as you like. If you want to make sure that chapters start on a new page, use the LaTeX command `\newpage` between the chapters you add to make each chapter start on a new page. Similarly, you might want to add the LaTeX command `\FloatBarrier` between chapters to make sure that figures, tables and such that belong to one chapter are not accidentally moved to another chapter (this happens sometimes as LaTeX is a typesetting system that is designed to allow the author to write without having to worry about the layout of the document; LaTeX tries to figure out the best spot to place figures and tables, which depends on the space that is available). To ensure the \\FloatBarrier command works, you need to load a LaTeX package. You can do this very easily by adding this bit of code to the YAML header (the bit between the dashed lines at the top of the document):

    header-includes:
    - \usepackage{placeins}
    

**Step 2: Adding a Titlepage, Declaration, Abstract and Acknowledgements**

The same way you added chapters to your thesis, you can also add a titlepage, declaration page, abstract and acknowledgements. LaTeX has some fancy syntax to do this (for example [see here](https://www.sharelatex.com/blog/2013/08/02/thesis-series-pt1.html)), but I didn’t look into this, as I found just straight up adding the pages as child documents was nice enough. Basically, I treated each of these pages as I would treat the chapter documents. For example, I added:

    ```{r child = 'titlepage.Rmd'}
    ```
    

to include the titlepage (for an example of titlepage you can write in R Markdown/LaTeX, see [here](https://raw.githubusercontent.com/rosannav/thesis_in_rmarkdown/master/titlepage.rmd) for the .rmd file and [here](https://github.com/rosannav/thesis_in_rmarkdown/blob/master/titlepage.pdf) for the .pdf example..

By now, the THESIS.rmd parent file will look something like [this](https://raw.githubusercontent.com/rosannav/thesis_in_rmarkdown/master/thesis-step2.Rmd), which produces [this](https://github.com/rosannav/thesis_in_rmarkdown/blob/master/thesis-step2.pdf) pdf file. I’ve given the chapters a little bit of text so they wouldn’t look so empty :).

**Step 3: Adding the Table of Contents, List of Figures, List of Tables, References**

R Markdown automatically places all references at the bottom of the document, but doesn’t not give it a title. To do this manually, just write _#References_ at the bottom of THESIS.rmd document. The references will be placed below this.

LaTeX offers some inbuilt functionality to automatically generate the Table of Contents, List of Figures and List of Tables. It is fairly simple: wherever you want to include one of these, you just type: `\tableofcontents`, `\listoffigures` or `\listoftables` in the THESIS.rmd file. To change the Table of Contents depth to for example headings and subheadings only, write `\setcounter{tocdepth}{2}`. You can play around with the number for a bit to see what depth you prefer. This is probably also a good moment to add some section numbering, so chapters and sections will be shown as e.g. _1\. Introduction_ and _1.1 Things_ instead of _Introduction_ and _Things_. We can do this easily by adding `number_sections: yes` to the YAML header:

    output:
      pdf_document:
        fig_caption: yes
        number_sections: yes
    

This is what the table of contents will look by now (see here for the full .rmd and .pdf files):

![Table of Contents with numbered sections.](https://cocky-elion-5880fb.netlify.app/post/2016-03-29-writing-your-thesis-with-r-markdown-4-putting-the-thesis-together/thesis-step3A.png)  
_Table of Contents with numbered sections._

As you can see, the titlepage, declaration, abstract, acknowledgements, list of figures and list of tables are not shown in the table of contents. This is because these pages don’t have chapter headings (i.e. for the abstract page I just wrote _abstract_ instead of _#Abstract_ – see [here](https://github.com/rosannav/thesis_in_rmarkdown) for the child documents I used in my examples – you might have to click on _Raw_ as Github automatically renders any markdown in documents). You can include them by writing _#Abstract_, but that way they will appear numbered in the table of contents as well. To avoid this, you can instead write `\section*{Abstract}` at the place where you’d like the title to appear. Using the `\section*{}` command will not automatically add the section to the table of contents, you can do this by writing this bit of code:

    \addcontentsline{toc}{section}{Abstract}
    

Similarly, you can write `\addcontentsline{toc}{section}{List of Figures}` to add the list of figures to the table of contents.

_Note: Although I’ve been talking about chapter headings here, officially they are called section headings. You can read more about it [here](https://en.wikibooks.org/wiki/LaTeX/Document_Structure#Sectioning_commands)._

By now, the THESIS.rmd parent file will look something like [this](https://raw.githubusercontent.com/rosannav/thesis_in_rmarkdown/master/thesis-step3.Rmd), which produces [this](https://github.com/rosannav/thesis_in_rmarkdown/blob/master/thesis-step3.pdf) pdf file.

**Step 4: Global R code chunk options**

As we saw in [tutorial #3](https://cocky-elion-5880fb.netlify.app/2016/03/18/writing-your-thesis-with-r-markdown-3-figures-r-code-and-tables/) that you can set knitr options that apply to all code chunks in your document. If you define your defaults in the parent document, these will be applied to all code chunks in the child documents (unless a code chunk has its own settings I’m pretty sure they won’t be overridden). The R code chunk options I’ve found useful are:

    ```{r include=FALSE}
    knitr::opts_chunk$set(fig.path = 'figures/', 
                          echo = FALSE, warning = FALSE, message = FALSE)
    ```
    

Just add this chunk at the top of the document, right below the YAML header and you’re good to go.

_Note: all the stuff you define in the parent document (i.e. YAML header, global R code chunks settings) will not be included if you try to render a child document seperately. So if you have a THESIS.rmd file that includes the package ‘placeins’, chapter1.rmd will not have this, unless you are rendering chapter1.rmd as a child document of THESIS.rmd._

By now you have pretty much got your whole thesis put together. All that is left now is the layout! If you found anything confusing, don’t hesitate to leave a comment or email me, and hopefully I’ll see you again in the last post.

Writing your thesis with R Markdown (5) – The thesis layout
===========================================================

March 30, 2016 Categories: RMarkdown

_This is the fifth and last post in a short series of tutorials to write your thesis in R Markdown. You can find instructions on how to get started in [the first post](https://cocky-elion-5880fb.netlify.app/2016/02/16/writing-your-thesis-with-r-markdown-1-getting-started/). These tutorials were written by a Windows user, so if you are using a different operating system some details may differ._

Hi there, you’ve made it to the last post! Today we’ll be looking at making the thesis extra pretty.

**Step 5: Organising the document layout with the YAML header**

As you may remember, you can write a bunch of commands in the YAML header to tell knitr and LaTeX how to render the document. There are a [whole range of things](http://rmarkdown.rstudio.com/pdf_document_format.html) you can define here to adjust your layout. Here’s what I did:

    ---
    output:
      pdf_document:
        fig_caption: yes
        number_sections: yes
    bibliography: library.bib
    csl: methods-in-ecology-and-evolution.csl
    urlcolor: black
    linkcolor: black
    fontsize: 12pt
    geometry: margin = 1.2in
    header-includes:
    - \usepackage{placeins}
    - \usepackage{setspace}
    - \usepackage{chngcntr}
    - \onehalfspacing
    - \counterwithin{figure}{section}
    - \counterwithin{table}{section}
    ---
    

We’ve already looked at number\_sections in step 3 in [the previous post](https://cocky-elion-5880fb.netlify.app/2016/03/30/writing-your-thesis-with-r-markdown-5-the-thesis-layout/2016/03/29/writing-your-thesis-with-r-markdown-4-putting-the-thesis-together/), and as you may recall from [tutorial #2](https://cocky-elion-5880fb.netlify.app/2016/02/17/writing-your-thesis-with-rmarkdown-2-making-a-chapter/), we used this bit:

    bibliography: library.bib
    csl: methods-in-ecology-and-evolution.csl
    

to define what library to use for the citations, and define the preferred citation style. The statements

    urlcolor: black
    linkcolor: black
    

are to indicate what colour the external (urlcolor) and internal (linkcolor) links should have. By default the linkcolor is magenta. Here I went a little crazy and opted for green and cyan:

[](https://rosannavanhespenresearch.files.wordpress.com/2016/03/ex-step4-6.png)

![](https://rosannavanhespenresearch.files.wordpress.com/2016/03/ex-step4-6.png)

  
Left: External links are now green, and internal links cyan. Right: pdf output.

The following arguments are pretty straightforward as well:

    fontsize: 12pt
    geometry: margin = 1.2in
    

to set fontsize at 12 points, and create a margin of 1.2 inches (30 mm).

All the stuff that is included under `header-includes:` are LaTeX arguments, such as packages that need to be loaded. So far, we’ve used the package `placeins` for the `\FloatBarrier` in step 1 of [the previous post](https://cocky-elion-5880fb.netlify.app/2016/03/29/writing-your-thesis-with-r-markdown-4-putting-the-thesis-together/). The argument `\onehalfspacing` is used to set the line spacing (more info on LaTeX’s line spacing can be found [here](http://tex.stackexchange.com/questions/65849/confusion-onehalfspacing-vs-spacing-vs-word-vs-the-world). The `\onehalfspacing` argument is part of the `setspace` package. I used the arguments `- \counterwithin {figure}{section}` and `- \counterwithin{table}{section}` to have LaTeX number the figures and tables according the section they belong to (e.g. the third figure in the thesis, but the first figure of the second chapter, will be named ‘figure 2.1’ instead of ‘figure 3’). To use these arguments, we need to use the package `chngcntr`.

**Step 6: Headers, footers and page numbering**

You’ll probably want to add some headers, footers and page numbering to the document so your reader doesn’t get completely lost. Page numbering is straightforward. You can use `\pagenumbering{gobble}` for pages without numbering, `\pagenumbering{roman}` for roman page numbering and `\pagenumbering{arabic}` for normal page numbering. Just include the argument wherever you want the have the page numbering changed. Default page numbering is arabic.

For headers and footers we can use the package ‘_fancyhdr_’. You can do some really cool stuff with it, see [here](http://texblog.org/2007/11/07/headerfooter-in-latex-with-fancyhdr/) for some info. Here’s what I did with it:

    \pagestyle{fancy}
    \fancyhead{}
    \fancyhead{}
    \renewcommand{\headrulewidth}{0.4pt}
    \renewcommand{\footrulewidth}{0pt}
    

This bit of code states that from now on pages have fancy headers (`\pagestyle{fancy}`). Lines 2 and 3 state that headers on the left even (LE), right odd (RO), left odd (LO) and right even (RE) pages are empty by default. I set the line below the header to a 0.4pt width (`\renewcommand{\headrulewidth}{0.4pt}`), and removed the footer line by setting it to 0pt. I then manually set the header title for each page by writing, for example, `\fancyhead{Abstract}` (CO, CE means centrally displayed on odd and even pages).

When pages are fully covered with a picture, graph or table, you might prefer to turn off page numbering and headers or footers. You can do this by adding this bit of code under the header-includes in the YAML header:

    - \usepackage{floatpag}
    - \floatpagestyle{empty}
    

If you’d like to know what the files should like by now, you can see what the [THESIS.rmd](https://raw.githubusercontent.com/rosannav/thesis_in_rmarkdown/master/thesis-step6.Rmd) and [THESIS.pdf](https://github.com/rosannav/thesis_in_rmarkdown/blob/master/thesis-step6.pdf) files will look by now.

**Spelling checking and commenting**

One thing we did not look at is spelling checking and commenting. There various ways to do this, but none of them are as elegant and easy to use as the ones in editors like MS Word. I tried a bunch of things, but decided that the best for me to deal with this was to convert .rmd to .pdf files as usual, and then use a pdf to word converter (it is also possible to create a .doxc file with knitr, but because I didn’t optimise the .rmd file for conversion to word it creates quite messy word documents. This makes it hard for others (supervisors) to get an idea what the final document is supposed to look like).

If you are working with the sublime editor, you can turn the spell checker on in there: [http://juristr.com/blog/2014/11/enable-spell-check-sublime-markdown/](http://juristr.com/blog/2014/11/enable-spell-check-sublime-markdown/).

If you need to comment to yourself while you’re writing in the .rmd file, you can use this syntax `<--your comment here-->`. It works alright, although you have to be careful with it: if you accidentally remove the last bit of the comment (the `-->` bit), but leave the first bit, and then try to compile your thesis, some bits may dissappear as knitr thought they were still part of the comment. I recommend making sure you’ve removed all comments when you compile the final thesis.

**A note on pandoc**

You might have heard some people talk about pandoc, and you might be wondering what it is. There is actually no need to undertstand what pandoc does, but if you’re curious: knitr depends on pandoc for its .md to .tex conversion. Basically what happens, is that knitr convert your .Rmd file to a .md (markdown file). That means that nothing changes, apart from the R code chunks, that are rendering and transformed into plain markdown. This includes creating the figures and storing them. Pandoc and pdflatex than come into play to convert the .md file to a .pdf, .doxc or .html file:

[](https://rosannavanhespenresearch.files.wordpress.com/2016/03/pandoc1.png)

![knitr, pandoc, pdflatex](https://rosannavanhespenresearch.files.wordpress.com/2016/03/pandoc1.png?w=584)

  
The role of knitr, pandoc and pdflatex in converting R Markdown to a pdf file.

**That’s it!**

I hope these tutorials were helpful! If you’d like some more examples, I’ve uploaded an example thesis to github. See [here for all the files](https://github.com/rosannav/thesis_in_rmarkdown/tree/master/example_thesis), and [here for the final pdf output](https://github.com/rosannav/thesis_in_rmarkdown/blob/master/example_thesis/THESIS.pdf). Good luck!
