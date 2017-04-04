Description
-----------
This script transforms a SRU-query from muscat.rism.info/sru/sources into a LaTex-file, provided by XSLT.

SVG-graphics of the musical incipit are generated by verovio; then these incipits are included via the SVG-package.


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

Basic usage
-----------
1. XSLT

The process is called from the pdf.rb-script. Main target of the script is the build of a related .TEX-file in prepartion for pdftex.At the current state the XSLT also defines the order of the resulting document.

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
Indices can be build with the resulting .TEX file. All entries are having the schema:
@creator:::entry:::number, eg.
@creator:::Beethoven, Ludwig van:::128

Indices are:
* Composers
* Names
* Title and Text
* Watermark
* Shelfmark
* Literature

