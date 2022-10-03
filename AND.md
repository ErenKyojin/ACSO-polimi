# AND




# AND A 3 INGRESSI

A | B | C | AND3
--- | --- | --- | ---
0 | 0 | 0 | 0
0 | 0 | 1 | 0
0 | 1 | 1 | 0
1 | 0 | 1 | 0
1 | 1 | 0 | 0
1 | 1 | 1 | 1

Cascata di AND tra A e B con l'AND di C
![[Pasted image 20220928094912.png]]


>[!oss]
>Un AND ad n ingressi si può sempre realizzare come [[circuito a cascata]] di altri AND, e per n pari come circuito ad [[circuito ad albero]] di AND

```tikz
\usepackage{circuitikz}

\begin{document}
\begin{tikzpicture}
%nodes
\node[and port] (ANDa) at (0,0){};
\node[or port] (ORa) at (2,0){};
\draw (ANDa.out) |- (ORa.in 1);
\end{tikzpicture}
\end{document}
```