Description
-----------
This script transforms a SRU-query from muscat.rism.info/sru/sources into a LaTex-file, provided by XSLT.

SVG-graphics of the musical incipit are generated by verovio; then these incipits are included via the SVG-package.

Currently an index of personal names is added to the corpus.

![Example](example.png?raw=true "Example page")

Requirements
-------------
This software works under Ubuntu 16.04

Packages and required software

1. Latex and all included packages
```bash
sudo apt install tex-common texlive-base texlive-binaries texlive-extra-utils texlive-font-utils texlive-fonts-recommended texlive-generic-recommended texlive-latex-base texlive-latex-extra texlive-latex-recommended texlive-pictures texlive-pstricks
```
2. inkscape
```bash
sudo apt install inkscape 
```
3. verovio (called from commandline)
see: https://github.com/rism-ch/verovio/wiki/Building-instructions

4. Ruby and Nokogiri

5. Increase the main memory size of texmf.conf:
* find the correct texmf.conf: 
```bash
kpsewhich -a texmf.cnf
```
* increase the size:
```latex
main_memory = 7999999
extra_mem_top = 7999999
extra_mem_bot = 7999999
```
* rebuild the configuration files
```bash
sudo fmtutil-sys --all
```

Basic usage
-----------

Transformation of Marcxml to LaTex is done by calling the ruby script:
```bash
&> ruby pdf.rb
```
Input file is defined at the top of the script. Please consider also generating the input file using the sru-downloader in the related repository.

All temporary files are build in /tmp/.

Background
-----------

1. XSLT

The process is called from the pdf.rb-script. Main target of the script is the build of a related .TEX-file in prepartion for pdftex. At the current state the XSLT also defines the order of the resulting document.

2. PDFtex

During the next step the .TEX-file is calling some subroutines:
* Creating textfiles with the Plaine & Easy-code.
* Calling verovio in the subshell to generate the SVG-files.
* Calling \includesvg to insert the graphics into the document.
* Completing the PDF-export.

Hint: The pdftex-command MUST be called from within the output-directory (eg. /tmp/)

Output
------
Result will be look alike example.pdf in this repository.

Indices
-------
Indices can be build also by using the preprocessing and transforming via XSLT. Currently the index of personal names is incuded in the corpus.

Additional indices could be:
* Title and Text
* Watermark
* Shelfmark
* Literature

For implementation see the example code in the index_names*.xls

Localization
--------------

If you like to modify the values of some fields (e.g. to have a special localized version), consider using the help of related software (e.g. Nokogiri with ruby).


