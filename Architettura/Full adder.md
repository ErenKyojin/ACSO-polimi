# Full Adder

A | B | C in |  Sum |C out 
--- | --- | --- | --- | --- 
0 | 0 | 0 | 0 | 0
0 | 0 | 1 | 1 | 0
0 | 1 | 0 | 0 | 1
0 | 1 | 1 | 0 | 1
1 | 0 | 0 | 1 | 0
1 | 0 | 1 | 0 | 1
1 | 1 | 0 | 0 | 1
1 | 1 | 1 | 1 | 1 

Sum = (A xor B) xor C_in
C_out = AB + C_in(A xor B)

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
%primo half hadder
\node[and port, xscale=-1] (ANDa) at (-2,-1){};
\node[xor port, rotate=270] (ORa) at (2,-4){};
\node (A) at (1.5,1){A};
\node (B) at (2.5,1){B};
\node (C) at (3, 1){Cin};
\node (Acr) at (1.5,-1){};
\node (Bcr) at (2.5,-1){};
\node[above left] (Cout) at (ANDa.out){AB};
\node[below left] (Sum) at (ORa.out){A xor B};

%secondo half hadder
%nodes
\node[and port, xscale=-1] (ANDb) at (-2,-7){};
\node[xor port, rotate=270] (ORb) at (2.5,-10){};
\node[above] (Coutb) at (ANDb.out){C(A xor B)};
\node[below] (Sumb) at (ORb.out){Sum};
\node[or port, rotate=270] (OR) at (-3, -10){};
\node(Abcr) at (2, -6.5){};
\node(Ccr) at (3,-7.5){};
\node(Cfin) at (OR.out){Carry out};

%connections
\draw (ORa.out) |- (ORb.in 2);
\draw (C) |- (ORb.in 1);
\draw (Abcr) |- (ANDb.in 1);
\draw (Ccr) |- (ANDb.in 2);
\draw (ANDa.out) -| (OR.in 2);
\draw (ANDb.out) -| (OR.in 1);

%connections
\draw (A) |- (ORa.in 2);
\draw (B) |- (ORa.in 1);
\draw (Acr) |- (ANDa.in 1);
\draw (Bcr) |- (ANDa.in 2);


\end{tikzpicture}
\end{document}
```