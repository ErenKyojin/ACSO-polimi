# Circuito ad albero
Preferibile per quanto riguarda ai tempi di propagazione, composto da una serie di operatori che hanno per ingresso altri operatori, eccetto la prima "fila" di operatori che hanno ingressi diretti.

```tikz
\usepackage{circuitikz}
\begin{document}
\begin{tikzpicture}

%nodes
\node[and port](ANDa) at (0,0){};
\node[and port](ANDb) at (-2,1){};
\node[and port](ANDc) at (-2,-1){};

%connections
\draw (ANDb.out) |- (ANDa.in 1);
\draw (ANDc.out) |- (ANDa.in 2);
\end{tikzpicture}
\end{document}
```
