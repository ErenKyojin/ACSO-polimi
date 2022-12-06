# Circuito a Cascata
Meno efficiente per quanto riguarda i tempi di propagazione, costituito da una serie di operatori che hanno un input diretto ed un input di un altro operatore, eccetto il primo nodo della serie.



```tikz
\usepackage{circuitikz}
\begin{document}
\begin{tikzpicture}

%nodes
\node[and port] (ANDa) at (0,0){};
\node[and port] (ANDb) at (2, -0.5){};
\node[and port] (ANDc) at (4,-1){};

%connections
\draw (ANDa.out)|- (ANDb.in 1);
\draw (ANDb.out) |- (ANDc.in 1);
\end{tikzpicture}
\end{document}
```
