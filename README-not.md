
<!-- README.md is generated from README.Rmd. Please edit that file -->

# aeolus

<!-- badges: start -->

[![R-CMD-check](https://github.com/maelle/aeolus/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/maelle/aeolus/actions/workflows/R-CMD-check.yaml)
[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://lifecycle.r-lib.org/articles/stages.html#experimental)
<!-- badges: end -->

The goal of aeolus is to fix Markdown files that have no semantic
linebreaks. aEOLus, get it? :wink:

## Installation

You can install the development version of aeolus like so:

``` r
pak::pak("ropenscilabs/aeolus")
```

## Why have semantic linebreaks?

For any Markdown parser the two following code chunks are the same:

``` md
This is a sentence. This is another
sentence.
```

``` md
This is a sentence. 
This is another sentence.
```

However, the second one will make your work easier when you use version
control. Git treats code by **line** so if lines are logical units as
opposed to random units or units of a certain length, the Git diff is
better.

If you change one sentence in a paragraph, and that paragraph is a
single line, the Git diff is less readable.

With semantic linebreaks, code suggestions in GitHub Pull Requests are
easier to make and use.

More information: <https://sembr.org/>.

## How to add linebreaks at the end of sentences?

1.  You can start doing it manually and make it a habit.
2.  You can use RStudio IDE’s Visual Markdown editor with the correct
    wrapping option:
    - Either run `aeolus::use_sentence_linebreaks()` for the current
      user (or `use_sentence_linebreaks("project")` for the current
      project);
    - Or, manually in the project/global options, choose “sentence” as
      value for “Automatic text wrapping (line breaks)” under “R
      Markdown”.

## How to fix a file that has no linebreaks at the end of sentences?

1.  Open it with RStudio IDE’s Visual Markdown editor with the correct R
    Markdown options (see previous section), then save.
2.  Use aeolus.

## Example

This is a basic example which shows you how to solve a common problem:

``` r
library(aeolus)
markdown_file <- system.file("example.md", package = "aeolus")
readLines(markdown_file)
```

    #>  [1] "This is a **sentence**."                                                                                                           
    #>  [2] "This is another [sentence](https://github.com)."                                                                                   
    #>  [3] ""                                                                                                                                  
    #>  [4] "In this paragraph I made random line breaks."                                                                                      
    #>  [5] "How annoying is it?!"                                                                                                              
    #>  [6] ""                                                                                                                                  
    #>  [7] "``` md"                                                                                                                            
    #>  [8] "This is a sentence. This is another"                                                                                               
    #>  [9] "sentence."                                                                                                                         
    #> [10] "```"                                                                                                                               
    #> [11] ""                                                                                                                                  
    #> [12] "This is a very long paragraph very very long without any breaks whatsoever which is sad, because who wants to get such a git diff."
    #> [13] ""                                                                                                                                  
    #> [14] "1.  thing"                                                                                                                         
    #> [15] "2.  other thing"                                                                                                                   
    #> [16] ""                                                                                                                                  
    #> [17] "-   item 1"                                                                                                                        
    #> [18] "-   item 2"                                                                                                                        
    #> [19] "-   item 3"                                                                                                                        
    #> [20] ""                                                                                                                                  
    #> [21] "**What is wrong with bold text?** What?"                                                                                           
    #> [22] ""                                                                                                                                  
    #> [23] "The [difference between working openly and transparently](https://wiki.mozilla.org/Working_open#Open_vs._Transparent)."            
    #> [24] ""                                                                                                                                  
    #> [25] "This is a footnote [^example-1]."                                                                                                  
    #> [26] ""                                                                                                                                  
    #> [27] "[^example-1]: Some more information."

``` r
unleash(markdown_file)
readLines(markdown_file)
```

    #>  [1] "This is a **sentence**."                                                                                                           
    #>  [2] "This is another [sentence](https://github.com)."                                                                                   
    #>  [3] ""                                                                                                                                  
    #>  [4] "In this paragraph I made random line breaks."                                                                                      
    #>  [5] "How annoying is it?!"                                                                                                              
    #>  [6] ""                                                                                                                                  
    #>  [7] "```md"                                                                                                                             
    #>  [8] "This is a sentence. This is another"                                                                                               
    #>  [9] "sentence."                                                                                                                         
    #> [10] "```"                                                                                                                               
    #> [11] ""                                                                                                                                  
    #> [12] "This is a very long paragraph very very long without any breaks whatsoever which is sad, because who wants to get such a git diff."
    #> [13] ""                                                                                                                                  
    #> [14] "1. thing"                                                                                                                          
    #> [15] "2. other thing"                                                                                                                    
    #> [16] ""                                                                                                                                  
    #> [17] "- item 1"                                                                                                                          
    #> [18] "- item 2"                                                                                                                          
    #> [19] "- item 3"                                                                                                                          
    #> [20] ""                                                                                                                                  
    #> [21] "**What is wrong with bold text?**"                                                                                                 
    #> [22] "What?"                                                                                                                             
    #> [23] ""                                                                                                                                  
    #> [24] "The [difference between working openly and transparently](https://wiki.mozilla.org/Working_open#Open_vs._Transparent)."            
    #> [25] ""                                                                                                                                  
    #> [26] "This is a footnote [^example-1]."                                                                                                  
    #> [27] ""                                                                                                                                  
    #> [28] "[^example-1]: Some more information."                                                                                              
    #> [29] ""                                                                                                                                  
    #> [30] ""

## Caveats

`aeolus::unleash()` uses the tinkr package under the hood, which means
it suffers from the same limitations: for instance, files after editing
only use “-”, not “\*“, for lists. Refer to [tinkr
documentation](https://docs.ropensci.org/tinkr/#loss-of-markdown-style).
We recommend using aeolus together with version control and reviewing
changes carefully before committing them.
