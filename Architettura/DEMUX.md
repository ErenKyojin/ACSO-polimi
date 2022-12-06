---
alias: demultiplexer
---

# DEMUX
Il contrario del [[MUX]] .Seleziona un'uscita su cui mandare l'ingresso

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
\node[muxdemux, xscale=-1] (ANDa) at (0,0){};

%connections

\end{tikzpicture}
\end{document}
```

I | S1 | S0 | O0 | O1 | O2 | O3
---|---|---|---|---|---|---
D | 0 | 0 | D | 0 | 0 | 0
D | 0 | 1 | 0 | D | 0 | 0
D | 1 | 0 | 0 | 0 | D | 0
D | 1 | 1 | 0 | 0 | 0 | D