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

\node (Operation) at (5,0){};

%alu1
\node[ALU] (ALUa) at (0,0){};
\node[above left] (a0) at (ALUa.blpin 1){a0};
\node[above left] (b0) at (ALUa.blpin 2){b0};
\node[above right] (o0) at (ALUa.brpin 1){result0};
\node[above right] (Cin0) at (ALUa.btpin 1){Carry in};
\node[below left] (Cout0) at (ALUa.bbpin 1){Cout};
\node[below right] (Oper0) at (ALUa.bbpin 2){OP};

%alu2
\node[ALU] (ALUb) at (0,-4){};
\node[above left] (a1) at (ALUb.blpin 1){a1};
\node[above left] (b1) at (ALUb.blpin 2){b1};
\node[above right] (o1) at (ALUb.brpin 1){result1};
\node[above right] (Cin1) at (ALUb.btpin 1){Carry in};
\node[below left] (Cout1) at (ALUb.bbpin 1){Cout};
\node[below right] (Oper1) at (ALUb.bbpin 2){OP};

%alu63
\node[ALU] (ALUc) at (0,-9){};
\node[above left] (a2) at (ALUc.blpin 1){a63};
\node[above left] (b2) at (ALUc.blpin 2){b63};
\node[above right] (o2) at (ALUc.brpin 1){result63};
\node[above right] (Cin2) at (ALUc.btpin 1){Carry in};
\node[below left] (Cout2) at (ALUc.bbpin 1){Cout};
\node[below right] (Oper2) at (ALUc.bbpin 2){OP};

%connections
\draw (ALUa.bbpin 1) -| (ALUb.btpin 1);
\draw (ALUb.bbpin 1) -| (ALUc.btpin 1);

\end{tikzpicture}
\end{document}
```



![[Pasted image 20221010170633.png]]