# Bistabile SR sincrono
In questo tipo di bistabile c'è un terzo ingresso oltre ad S ed R, chiamato [[clock]], che se uguale a 0 "blocca" gli ingressi, questo fornisce un "intervallo" in cui è possibile cambiare i valori


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
\node[and port] (ANDa) at (-1,0.28){};
\node[and port] (ANDb) at (-1, -2){};
\node[nor port] (NORa) at (2,0){};
\node[nor port] (NORb) at (2,-1.72){};
\node(CLOCK) at (-3,-1){};
\node(S) at (ANDa.in 1){};
\node(R) at (ANDb.in 2){};
\node(notQ) at (NORa.out){};
\node(Q) at (NORb.out){};


%connections
\draw (ANDa.out) |- (NORa.in 1);
\draw (ANDb.out) |- (NORb.in 2);
\draw (NORa.out) -\ (NORb.in 1);
\draw (NORb.out) -/ (NORa.in 2);
\draw (CLOCK) node[left](In1){CLOCK} -| (ANDb.in 1);
\draw (CLOCK) -| (ANDa.in 2);
\draw (S) node[left](In2){S};
\draw (R) node[left](In3){R};
\draw (notQ) node[right](Out1){$\bar{Q}$};
\draw (Q) node[right](Out2){$Q$};

\end{tikzpicture}
\end{document}
```

Non filtra per clock alti, quindi usiamo il [[Bistabile D sincrono]]
