# XNOR

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{tikzpicture}
%nodes
\node[xnor port] at (0,0){};

\end{tikzpicture}
\end{document}
```
A | B | AB & !A!B
--- | --- | ---
 0| 1 | 1
 0 | 1 | 0
 1 | 0 | 0
 1 | 1 | 1

E implica l'uguaglianza tra **A** e **B**.
