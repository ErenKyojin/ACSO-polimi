# Ritardo di propagazione

I [[Bistabili]] e le [[porte logiche]] soffrono di ritardi di comunicazione dell'uscita rispetto all'ingresso, che possiamo rappresentare come:
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
\node[nor port] (NORa) at (2,0){};
\node[genericshape,centered] (Tau) at (4,0){$\Delta\tau$};
\node[left] (A) at (NORa.in 1){A};
\node[left] (B) at (NORa.in 2){B};

%connections
\draw (NORa.out) |- (Tau);

\end{tikzpicture}
\end{document}
```

Risulta in
![[Pasted image 20221010181712.png|300]]
