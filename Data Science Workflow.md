# Data Science Workflow

I completed three data science projects for my doctoral dissertation in epidemiology. 

During this time I developed my personal workflow for projects in academic clinical research. 

The consistency allows me to locate files efficiently at any stage of the project.

Whenever I start a new project I create seven empty folders with the following names:

* [`0 Data`](https://github.com/dgrisafe/rookie-researcher/blob/main/Data%20Science%20Workflow.md#0-data)
* [`1 Programs`](https://github.com/dgrisafe/rookie-researcher/blob/main/Data%20Science%20Workflow.md#1-programs)
* [`2 Media`](https://github.com/dgrisafe/rookie-researcher/blob/main/Data%20Science%20Workflow.md#2-media)
* [`3 Reports`](https://github.com/dgrisafe/rookie-researcher/blob/main/Data%20Science%20Workflow.md#3-reports)
* [`4 Discussions`](https://github.com/dgrisafe/rookie-researcher/blob/main/Data%20Science%20Workflow.md#4-discussions)
* [`5 Drafts`](https://github.com/dgrisafe/rookie-researcher/blob/main/Data%20Science%20Workflow.md#5-drafts)
* [`6 Talks`](https://github.com/dgrisafe/rookie-researcher/blob/main/Data%20Science%20Workflow.md#6-talks)

Throughout all of the above folders I name files with the prefix `YYYYMMDD`. 

For example `20230130 Data Science Workflow.md` would be the name of this file on my local machine.


## `0 Data`

This data folder has varying utility, as often data is protected in a database that requires special permissions to access. 

This is a great place to store publicly available data.


## `1 Programs`

I create a shortcut/alias with this name that links to the specific repository within my GitHub folder in my Documents on my local computer. 

I use [GitHub](https://github.com/dgrisafe/rookie-researcher/blob/main/Git%20and%20GitHub.md) to manage all my code.

I create the following set of standard files when beginning a new project.

* `.gitignore.R`
* `directories.R`
* `formats.R`
* `data_wrangling.Rmd`
* `analysis.Rmd`

### `.gitignore.R`

This hidden file tells R to ignore certain file types that are not necessary for reproducibility. 

In addition to the template files to ignore, I add lines to ignore all `.html` and `.pdf` files. 

I also ignore the `.Rproj` file. 

The asterisk tells Git to ignore any file with the following ending or suffix type.

```
.Rproj.user
.Rhistory
.Rdata
.httr-oauth
.DS_Store
*.html
*.pdf
*.Rproj
```

### `!workflow.R`

Think of this file as the *spine* of the project. 

Other files are the *ribs* that project of this main organizational file. 

This can also be thought of as the table of contents, or a "hub".

I ["abstract"](https://en.wikipedia.org/wiki/Abstraction_principle_(computer_programming)) or separate additional `.R` scripts using the function [`source()`](https://bookdown.org/yihui/rmarkdown-cookbook/source-script.html) and `.Rmd` files using the function `rmarkdown::render()`. 

The latter function can then output the PDF or HTML reports into the folder `3 Reports`.

Note, the file name begins with an exclamation point so it always floats to the top of the folder for ease of access.

```
# packages
library(knitr)
library(markdown)

# R scripts for directories and formats
source("directories.R")
source("formats.R")

# Rmd file and output for data wrangling
rmarkdown::render(
  input = paste0(dir_programs, "/data_wrangling.Rmd"),
  output_format = "html_document",
  output_dir = dir_reports
  )
  
# Rmd file and output for data analysis
rmarkdown::render(
  input = paste0(dir_programs, "/data_analysis.Rmd"),
  output_format = "html_document",
  output_dir = dir_reports
  )
```

I use this `!workflow.R` file to tell R to output the .Rmd [`data_wrangling.Rmd`](https://github.com/dgrisafe/rookie-researcher/blob/main/Data%20Science%20Workflow.md#data_wranglingrmd) and [`analysis.Rmd`](https://github.com/dgrisafe/rookie-researcher/blob/main/Data%20Science%20Workflow.md#analysisrmd) files to the `3 Reports` folder. 

### `directories.R`

This simple R script assigns the directory locations of the folders that are called by the program files. 

I find having this in one dedicated file helps maintain organization.

```
# assign directories
dir_home      <- "/Users/dgrisafe/Documents/rookie-researcher"
dir_data      <- paste0(dir_home, "/0 Data")
dir_programs  <- paste0(dir_home, "/1 Programs")
dir_reports   <- paste0(dir_home, "/3 Reports")
```

### `formats.R`

Formats can become cluttered within the data wrangling .Rmd file. 

I separate out the formats, especially for factors, so I can quickly and consistently modify them throughout the project.

### YAML Headers in Rmd

There are many options in the YAML header at the beginning of a new Rmd file. 

I like to use HTML output because it is universally read by any internet browser.

I use the following stock header for my analysis reports.

Note, the spacing is important in the YAML header, unlike in R; they are different programming languages.

```
title: "Rookie Researcher Analysis"
author: "Dom Grisafe"
date: "`r Sys.Date()`"
output: 
  html_document:
    keep_md: FALSE
    toc: TRUE
    toc_float: TRUE
    toc_depth: 2
csl: chicago-note-bibliography.csl
bibliography: references.bib
```

#### Referencing in R Markdown with Styles (.csl) and BibTeX (.bib)

Make sure the names in the last two lines of the YAML header above match the file names of the `.csl` and `.bib` files that we'll save in the folder [`1 Programs`](https://github.com/dgrisafe/rookie-researcher/blob/main/Data%20Science%20Workflow.md#1-programs).

##### Styles (.csl)

Download a .csl file from the [Zotero Style Repository](https://github.com/dgrisafe/rookie-researcher/blob/main/Zotero%20%7C%20Citation%20Management%20Recommendations.md#zotero-style-repository-formatting-bibliographies) by *Right Clicking* and *Save Link As...*.

For example the [Chicago Manual of Style 17th edition (note)](https://www.zotero.org/styles/chicago-note-bibliography).

Place this `.csl` file in the folder [`1 Programs`](https://github.com/dgrisafe/rookie-researcher/blob/main/Data%20Science%20Workflow.md#1-programs)

##### BibTeX (.bib)

In Zotero, create a folder with all the references for a project. 

Highlight all references, right click, export items as BibTeX file.

Save this `.bib` file to the folder [`1 Programs`](https://github.com/dgrisafe/rookie-researcher/blob/main/Data%20Science%20Workflow.md#1-programs).

To find the key for each reference, open the `.bib` file in a text editor. 

In the `.bib` file, the key is the first line of each section, between the open bracket `{` and the comma `,`: `@article{authorLastName_titleFirstWord_Year,`

Throughout the `.Rmd` document, call a unique reference by typing `[@`, the specific key, `]`: `[@authorLastName_titleFirstWord_Year]` 

### `data_wrangling.Rmd`

Most of the time spent on data analysis seems to be cleaning it into a *tidy* dataset. 

Separating the wrangling code from the analysis helps maintain clarity.

### `analysis.Rmd`

This analysis file generates a .html or .pdf report. 

Sometimes there are multiple analysis folders. 

For example, one for multiple imputation and another for epidemiological analysis.


## `2 Media`

Sometimes I include images or other media in a report. 

Keeping media files in a separate folder is useful when creating a presentation towards the end of a project.  


## `3 Reports`

I use R markdown files often to generate PDF and HTML reports that I share with collaborators during meetings and internal presentations. 

Keeping them organized here allows me to access them while communicating my work during meetings.


## `4 Discussions`

I take notes during project meetings in MS Word. I often reference these meetings later while working on my code.


## `5 Drafts`

This is where I keep manuscripts that I eventually plan on publishing in a journal.


## `6 Talks`

I give formal and informal presentations throughout the life of a project. 

I usually use Google Slides for ease of access. 

I also often use [bitly.com](https://bitly.com/) to produce shortened, custom HTML addresses for a talk that I can quickly share with others.
