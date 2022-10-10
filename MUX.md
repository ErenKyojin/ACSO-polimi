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
\node[and port] (ANDa) at (0,0){};
\node[muxdemux] (ORa) at (2,0){};

%connections


\end{tikzpicture}
\end{document}
```