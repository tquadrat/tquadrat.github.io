# References in a Document
To add a reference to another part of your document, add the following new commands to the preamble of your document source:

```tex
\usepackage{nameref}
\usepackage[colorlinks=true]{hyperref}

\newcommand*{\tqfullref}[1]{\hyperref[{#1}]{“\ref*{#1} \nameref*{#1}”}}
\newcommand*{\tqfullvref}[1]{\hyperref[{#1}]{“\ref*{#1} \nameref*{#1}”} on page \pageref{#1}}
\newcommand*{\tqref}[1]{\hyperref[{#1}]{\ref*{#1}}}
\newcommand*{\tqvref}[1]{\hyperref[{#1}]{\ref*{#1}} on page \pageref{#1}}
```

These are for a document in English language, for another language you have to adjust the commands accordingly; for the German language, the will look like this:
```tex
\usepackage{nameref}
\usepackage[colorlinks=true]{hyperref}

\newcommand*{\tqfullref}[1]{\hyperref[{#1}]{„\ref*{#1} \nameref*{#1}”}}
\newcommand*{\tqfullvref}[1]{\hyperref[{#1}]{„\ref*{#1} \nameref*{#1}”} auf Seite \pageref{#1}}
\newcommand*{\tqref}[1]{\hyperref[{#1}]{\ref*{#1}}}
\newcommand*{\tqvref}[1]{\hyperref[{#1}]{\ref*{#1}} auf Seite \pageref{#1}}
```

Because the `hyperlink` package redefines several other LaTex commands, it should be loaded always as the last package.

The destination for the reference will be marked with the `\label` command, like this:

```tex
\section{<headline>}\label{sec:<label>}
…
See chapter \tqfullref{sec:<label>}
See chapter \tqfullvref{sec:<label>}
See chapter \tqref{sec:<label>}
See chapter \tqvref{sec:<label>}
```

- `\tqfullref` adds a reference like ***“\<number> \<headline>”***
- `\tqfullvref` adds a reference like ***“\<number> \<headline>” on page \<page>***
- `\tqref` adds a reference like ***\<number>***
- `\tqvref` adds a reference like ***\<number> on page \<page>***

Both, the number/headline and the page number will be generated as hyperlinks. So the resulting output would look like this:

> ### 1.2.3 \<headline>
> …\
> See chapter <ins>“1.2.3 \<headline>”</ins>\
> See chapter <ins>“1.2.3 \<headline>”</ins> on page <ins>42</ins>\
> See chapter <ins>1.2.3</ins>\
> See chapter <ins>1.2.3</ins> on page <ins>42</ins>
  
The `hyperlink` package provides also the commands `\url` and `\href` that allow to integrate references to websites or an email address into the generated document. The code:
  
```tex
Send me an email: \href{mailto:thomas.thrien@tquadrat.org}{thomas.thrien@tquadrat.org}
Or see my GitHub page: \url{https://tquadrat.github.io/}
```
results in:
> Send me an email: <ins>thomas.thrien@tquadrat.org</ins>\
> Or see my GitHub page: <ins>https://tquadrat.github.io/</ins>

## Links
- [hyperref – Extensive support for hypertext in LATEX](https://ctan.org/pkg/hyperref)
- [Hypertext marks in LATEX: a manual for hyperref](https://ftp.gwdg.de/pub/ctan/macros/latex/contrib/hyperref/doc/hyperref-doc.html)
- [nameref – Make reference to section names, etc](https://www.ctan.org/pkg/nameref)
- [Section name references in LATEX](https://mirror.dogado.de/tex-archive/macros/latex/contrib/hyperref/doc/nameref.pdf)
