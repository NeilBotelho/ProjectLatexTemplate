# Requirements
* A LaTeX compiler. I use `latexmk`
* A LaTeX package manager. I use [tllocalmgr](https://wiki.archlinux.org/title/TeX_Live#tllocalmgr)

* LaTeX packages used(These might come included with your LaTeX install, otherwise use the LaTeX package manager to install them):
	* geometry
	* bibLaTeX
	* graphicx
	* float
	* array
	* caption
	* amsmath
	* ragged2e
	* listings
	* titlesec
	* hyperref

# Compilation
```bash
latexmk -pdf report.tex
```

# A couple notes for clarity
## Chapters
I've broken up the report into chapters(available in the chapters folder) for ease of access and for compilation speed(see next section)


## \includeonly and \include
Since this is a pretty massive report with a lot if images, compiling it to a pdf takes like 1 minute which is kinda a long time to wait between seeing your changes. So LaTeX's solution to this is the \include function. 

This function allows you to break up your document into separate sections(here chapters). The function takes one arguement, the path to the LaTeX file with the content of that chapter (without a preamble aka the \usepackage and \begindocument parts). This function uses the intermediate compiled files(.aux files) of that chapter instead of recompiling.

The \includeonly function is run once before the start of the actual document in report.tex. This specifies which chapters to ignore the compiled files for and always recompile. To speed up compilation, youll want to make sure that only the chapters you're currenty editing are mentioned in this function. \includeonly takes a comma separated list of files/chapters as arguements

**Important**: If you are using the \includeonly function then \include does not compile chapters that do not have intermediate compiled files(.aux files). So run the compilation for the full document at least once with \includeonly commented out. For safety, \includeonly has been commented out in report.tex but once you compile it once uncomment it and add only the chapters you're currently editing to it to see your changes when you recompile

## Citations
The citations are made using bibtex. See [this tutorial](https://www.overleaf.com/learn/latex/Bibliography_management_in_LaTeX) for a detailed explanation. But essentially, you add all you're citations in a particular format(bibtex format), that is available on all the sites where you get papers, i.e. researchgate, arxiv etc. allow you to download bibtex files for citations. See my citations.bib file for reference. 

The first thing after the @ is the type of document it is, i.e. article/ paper published in proceedings/ book / collection etc. After the open curly braces is the name you will use to refer to that citation. If you refer to any chapter where I made a citation you will note the \cite function that mentions one of these names. Latex then automatically cites these papers and orders them for you. 

## Intermediate files generated
LaTeX compilation generates a lot of intermediate files. These tend to clutter up your working directory. These are required to shorten the compilation time while editing but if you aren't going to recompile for a while or you don't mind a longer compilation duration for the next compilation you can use the following command to clear out intermediate files.
```bash
rm *.log *.fls *.toc *.out *.synctex.gz *.fdb_latexmk *.aux *.dvi *.synctex\(busy\) *.bbl *.bcf  *.run.xml *.blg *.lof *.lot 2> /dev/null 
```

I add an alias in my .bashrc to lc i.e. LaTeX clear to avoid having to type out the whole command:
```bash
alias lc="rm *.log *.fls *.toc *.out *.synctex.gz *.fdb_latexmk *.aux *.dvi *.synctex\(busy\) *.bbl *.bcf  *.run.xml *.blg *.lof *.lot 2> /dev/null "
```
