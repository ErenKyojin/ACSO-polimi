---
alias: multiplexer
---

# MUX

Il mux è un componente che "seleziona" un ingresso:

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
\node[muxdemux] (ORa) at (2,0){M};

%connections


\end{tikzpicture}
\end{document}
```
A sinistra abbiamo $2^n$ ingressi, a destra l'uscita e lateralmente $n$ selettori, la tabella di un MUX sarebbe:

SEL | I0 | I1 | U
--- | --- | --- | ---
 0 | 0 | 0 | 0
 0 | 0 | 1 | 0
 0 |1 | 0 | 1
 0 | 1 | 1 | 1
 1 | 0 | 0 | 0
 1 | 0 | 1 | 1
 1 | 1 |0 | 0
 1 | 1 | 1 | 1

Il selettore dice quale ingresso mandare in uscita