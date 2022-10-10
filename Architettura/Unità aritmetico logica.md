---
alias: ALU
---

# ALU
L'alu è l'unità aritmetico logica, si occupa di eseguire le operazioni 

```tikz
\usepackage{circuitikz}
\usetikzlibrary{calc}

\begin{document}
\begin{tikzpicture}

\ctikzset{
logic ports/scale = 1,
logic ports/fill = darkgray,
}

%nodes
\node(A) at (-5, 0.5){A};
\node[and port] (ANDa) at (0,0){};
\node[or port] (ORa) at (0,-2){};

%connections
\draw (A) |- (ANDa.in 1);

\end{tikzpicture}
\end{document}
```
