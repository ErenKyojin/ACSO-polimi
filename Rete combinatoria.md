# Rete combinatoria
Una rete combinatoria è un circuito digitale con $n \geq 1$ ingressi in uscita, formato da porte logiche elemntari [[AND]], [[OR]] e [[NOT]], e privo di retroazioni


```tikz
\usepackage{circuitikz}

\begin{document}
\begin{tikzpicture}
%nodes
\node[or port] (ORa) at (3,-1){};
\node[and port] (ANDb) at (0, -2){};
\node[and port] (ANDa) at (0,0){};

%connections
\draw (ANDa.out) -- (ORa.in);

\end{tikzpicture}
\end{document}
```

