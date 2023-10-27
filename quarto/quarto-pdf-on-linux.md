I want to render a CV pdf using [Quarto] on a fresh linux machine, but got an error 
> xelatex not found.

Quarto transforms *.qmd* to *.md*, and then to *.pdf*. Quarto uses `xelatex` as the default [TeX] pdf engine for a [pandoc] call. TexLive is installed on many Linux distributions, but the version may be outdated. Check in the terminal via `which tex && tex --version | head -n 1`. [TinyTex] is an (optional) internal TeX used in Quarto.

To render PDFs using Quarto;

1. [download](https://quarto.org/docs/download/tarball.html) the Quarto CLI.

```
~$ quarto list tools
[✓] Inspecting tools

Tool         Status            Installed     Latest  
chromium     Not installed     ---           869685  
tinytex      Not installed     ---           v2023.10
```

2. run `tlmgr init-usertree`
3. check `tex --version`, update if <2020, via [repairTeX]
4. install `rmarkdown` via `Rscript -e 'install.packages("rmarkdown", repos="https://cran.r-project.org")'`

[TeX]: https://tug.org/texlive/
[Quarto]: https://quarto.org/
[pandoc]: https://pandoc.org/chunkedhtml-demo/2.4-creating-a-pdf.html
[latex]: https://www.latex-project.org/
[repairTeX]: https://puttym.github.io/update-texlive
[TinyTex]: https://quarto.org/docs/output-formats/pdf-engine.html