---
title: 'Manta Structural Variant Caller'
subtitle: '(Document from [Manta GitHub repository](https://github.com/Illumina/manta))'
date: '2021 12_Dec 02'
output:
  bookdown::pdf_document2:
    latex_engine: xelatex
    pandoc_args:
    - "--listings"
  
header-includes:
# wrap code blocks using the listings package (run with pandoc command that includes `--listings` command). looks cleaner. but makes highlighting mistakes, e.g. mistakes any '#' symbol as the start of a comment
- \usepackage{fontspec}
- \setmainfont{Optima}
- \usepackage[fontsize=14pt]{scrextend}
- \usepackage{xcolor}
- \lstset{breaklines=true}
- \lstset{language=[Motorola68k]Assembler}
- \lstset{basicstyle=\small\ttfamily}
- \lstset{extendedchars=true}
- \lstset{tabsize=2}
- \lstset{columns=fixed}
- \lstset{showstringspaces=false}
- \lstset{frame=trbl}
- \lstset{frameround=tttt}
- \lstset{framesep=4pt}
- \lstset{numbers=left}
- \lstset{numberstyle=\tiny\ttfamily}
- \lstset{postbreak=\raisebox{0ex}[0ex][0ex]{\ensuremath{\color{red}\hookrightarrow\space}}}
- \lstset{commentstyle=\color{red!50!black}}
- \lstset{keywordstyle=\color{blue!70!black}}
- \lstset{stringstyle=\color{green!50!black}}
# prevent floating figures (insert them where they are in the .md file)
- \usepackage{float}
- \let\origfigure\figure
- \let\endorigfigure\endfigure
- \renewenvironment{figure}[1][2] {\expandafter\origfigure\expandafter[H]}{\endorigfigure}

---

Manta Structural Variant Caller
===============================

Manta calls structural variants (SVs) and indels from mapped
paired-end sequencing reads. It is optimized for analysis of germline
variation in small sets of individuals and somatic variation in
tumor/normal sample pairs. Manta discovers, assembles and scores
large-scale SVs, medium-sized indels and large insertions within a
single efficient workflow. The method is designed for rapid analysis
on standard compute hardware: NA12878 at 50x genomic coverage is
analyzed in less than 20 minutes on a 20 core server, and most WGS
tumor/normal analyses can be completed within 2 hours. Manta combines
paired and split-read evidence during SV discovery and scoring to
improve accuracy, but does not require split-reads or successful
breakpoint assemblies to report a variant in cases where there is
strong evidence otherwise. It provides scoring models for germline
variants in small sets of diploid samples and somatic variants in
matched tumor/normal sample pairs. There is experimental support for
analysis of unmatched tumor samples as well. Manta accepts input read
mappings from BAM or CRAM files and reports all SV and indel inferences
in VCF 4.1 format. See the [user guide][UserGuide] for a full
description of capabilities and limitations.

[UserGuide]:docs/userGuide/README.md

Methods and benchmarking details are described in:

Chen, X. *et al.* (2016) Manta: rapid detection of structural variants and
indels for germline and cancer sequencing applications. *Bioinformatics*,
32, 1220-1222. [doi:10.1093/bioinformatics/btv710][bpaper]

...and the corresponding [open-access pre-print][preprint].

[bpaper]:https://doi.org/10.1093/bioinformatics/btv710
[preprint]:https://doi.org/10.1101/024232


License
-------

Manta source code is provided under the [GPLv3 license](LICENSE.txt).
Manta includes several third party packages provided under other
open source licenses, please see [COPYRIGHT.txt](COPYRIGHT.txt)
for additional details.


Getting Started
---------------

For linux users, it is recommended to start from the most recent
[binary distribution on the Manta releases page][releases], this
distribution can be unpacked, moved to any convenient directory and
tested by [running a small demo](docs/userGuide/installation.md#demo)
included with the release distribution. Manta can also be installed
and run on OS X. Please see the [installation instructions](docs/userGuide/installation.md)
for full build and installation details of all supported cases.

[releases]:https://github.com/Illumina/manta/releases


Data Analysis and Interpretation
--------------------------------

After completing installation, see the [Manta user guide][UserGuide]
for instructions on how to run Manta, interpret results and estimate
hardware requirements/compute cost, in addition to a high-level methods
overview.


Manta Code Development
----------------------

For manta code development and debugging details, see the
[Manta developer guide][DeveloperGuide]. This includes details
on Manta's developement protocols, special build instructions,
recommended workflows for investigating
calls, and internal documentation details.

[DeveloperGuide]:docs/developerGuide/README.md
