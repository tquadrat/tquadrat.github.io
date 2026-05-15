# Integration of Source Code Listings
To integrate 'listings' – source code of programs, scripts and alike – into a document, use the package `listings`. It allows syntax highlighting for several programming languages.

To integrate the package, put the line `\usepackage{listings}` to the preamble of your document.

The configuration of the package is done with the `\lstset` environment.

```tex
\lstset{
language=Java,                    % The programming language
backgroundcolor=\color[gray]{.9}, % The background color

basicstyle=\ttfamily\footnotesize\bfseries,
                                  % The basic style
commentstyle=\color[gray]{.2}\bfseries,
                                  % The style for the comments if different
                                  % from the basic style
identifierstyle=,                 % The style for identifiers
stringstsyle=,                    % The style for String constants
keywordstyle=\color[gray]{.2},    % The style for the keywords of the selected
                                  % programming language if different from the
                                  % basic style
showstringspaces=true,            % A special character is displayed for the
                                  % blanks in a String

frame=single,                     % The listing should be surrounded by a frame
framerule=0.2pt,                  % The width of that frame

xleftmargin=.2cm,                 % additional indentation for the source code
xrightmargin=.2cm,                % right margin

breaklines=true,                  % source code lines can be broken at the
                                  % margin
breakatwhitespace=true,           % lines are broken at whitespace

inputencoding=utf8,               % the input encoding
extendedchars=true,               % allows non-ASCII characters
literate=                         % the mapping of extended characters to
                                  % TeX/LaTeX constructs; required for nearly
                                  % all non-ASCII character in the source code
  {á}{{\'a}}1 {Á}{{\'A}}1 {à}{{\`a}}1 {À}{{\`A}}1 {ä}{{\"a}}1 {Ä}{{\"A}}1 
  {â}{{\^a}}1 {Â}{{\^A}}1 {ã}{{\~a}}1 {Ã}{{\~A}}1 {æ}{{\ae}}1 {Æ}{{\AE}}1
  {å}{{\r a}}1 {Å}{{\r A}}1
  {ç}{{\c c}}1 {Ç}{{\c C}}1
  {é}{{\'e}}1 {É}{{\'E}}1 {è}{{\`e}}1 {È}{{\'E}}1 {ë}{{\"e}}1 {Ë}{{\"E}}1 
  {ê}{{\^e}}1 {Ê}{{\^E}}1 {ẽ}{{\~e}}1 {Ẽ}{{\~E}}1
  {í}{{\'i}}1 {Í}{{\'I}}1 {ì}{{\`i}}1 {Ì}{{\`I}}1 {ï}{{\"i}}1 {Ï}{{\"I}}1
  {î}{{\^i}}1 {Î}{{\^I}}1 {ĩ}{{\~i}}1 {Ĩ}{{\~I}}1
  {ñ}{{\~n}}1 {Ñ}{{\~N}}1 
  {ó}{{\'o}}1 {Ó}{{\'O}}1 {ò}{{\`o}}1 {Ò}{{\`O}}1 {ö}{{\"o}}1 {Ö}{{\"O}}1 
  {ô}{{\^o}}1 {Ô}{{\^O}}1 {õ}{{\~o}}1 {Õ}{{\~O}}1 {œ}{{\oe}}1 {Œ}{{\OE}}1    
  {ø}{{\o}}1 {ő}{{\H{o}}}1 {Ő}{{\H{O}}}1
  {ß}{{\ss}}1
  {ú}{{\'u}}1 {Ú}{{\'U}}1 {ù}{{\`u}}1 {Ù}{{\`U}}1 {ü}{{\"u}}1 {Ü}{{\"U}}1
  {û}{{\^u}}1 {Û}{{\^U}}1 {ũ}{{\~u}}1 {Ũ}{{\~U}}1 {ű}{{\H{u}}}1 {Ű}{{\H{U}}}1 
  {€}{{\euro}}1 {£}{{\pounds}}1 
  {«}{{\guillemotleft}}1 {»}{{\guillemotright}}1 
  {¿}{{?`}}1 {¡}{{!`}}1
  {©}{{\copyright}}1
  {…}{{\dots}}1
}
```
The format for the `literate=` entries is `{<source character>}{{<replacement sequence>}}<effectice length of the replacement sequence>`. To print the copyright symbol in the listing, the `literate` sequence would be `{©}{{\copyright}}1`.

The list above is not exhaustive, it just contains those characters that I have used within a source code file at some time in the past.

The package is used basically in two ways:

- As environment: `\begin{lstlisting} … \end{lstlisting}`
- Inline: `\lstinline|…|`

The environment allows to overwrite some of the settings provide with `\lstset`: `\begin{lstlisting}[language=python, numbers=left] … \end{lstlisting}`.

`\lstinline|…|` works similar to `\verb`: the vertical bars are just the delimiters for the value; any character that is not part of the value can be used for that.

## Links
- [listings – Typeset source code listings using LaTeX](https://ctan.org/pkg/listings)
- [LaTeX/Source Code Listings](https://en.wikibooks.org/wiki/LaTeX/Source_Code_Listings)
- [The Listings Package](https://texdoc.org/serve/listings.pdf/0)
