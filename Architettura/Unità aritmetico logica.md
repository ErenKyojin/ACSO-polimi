---
alias: ALU
---

# ALU
L'alu è l'unità aritmetico logica, si occupa di eseguire le operazioni , nella foto un ALU ad 1 bit

![[Pasted image 20221010150920.png]]


Una alu ad $n$ bit è semplicemente una serie di $n$ alu ad 1 bit


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
\node[ALU] (ALUa) at (0,0){};
\node[ALU] (ALUb) at (0,-4){};
\node (a0) at (ALUa in blpin1){d};

%connections
%\draw (ANDa.out) |- (ORa.in 1);

\end{tikzpicture}
\end{document}
```