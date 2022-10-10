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
\node[above left] (a0) at (ALUa.blpin 1){a0};
\node[above left] (b0) at (ALUa.blpin 2){b0};
\node[above right] (o0) at (ALUa.brpin 1){result0};
\node[above right] (Cin0) at (ALUa.btpin 1){Carry in};
\node[above right] (Cout0) at (ALUa.bbpin 1){};

\node[ALU] (ALUb) at (0,-4){};

%connections
%\draw (ANDa.out) |- (ORa.in 1);

\end{tikzpicture}
\end{document}
```