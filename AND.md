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
\usetikzlibrary{calc}

\begin{document}
\begin{tikzpicture}

\ctikzset{
logic ports/scale = 01,
logic ports/fill = darkgray,
}

%nodes
\node[and port] (ANDa) at (0,0){};
\node[or port] (ORa) at (2,0){};

%connections
\draw (ANDa.out) |- (ORa.in 1);
\draw (3,3) -| (ORa.in 2);

\end{tikzpicture}
\end{document}
```