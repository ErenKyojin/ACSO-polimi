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
\node[latch] (Dms) at (0,0){};
\node[above](master) at (Dms.north){Master};
\node[latch] (Dsl) at (4,0){};
\node[above](slave) at (Dsl.north){Slave};
\node[circle] (clock) at (-3,-0.85){CLK};

\node[flipflop D] at (8,0){};
\path (2,-3) coordinate (mid){};

\node[not port](NOTa) at (2,-3){};

%connections
%\draw (ANDa.out) |- (ORa.in 1);
\draw(Dms.pin 6) |- (Dsl.pin 1);
\draw (clock) to[short, -*] coordinate (A) (Dms.pin 3);
\draw (A) |- (NOTa.in);
\draw (NOTa.out) -| (Dsl.pin 3);

\end{tikzpicture}
\end{document}
```
Il master campiona l'ingresso durante l'intervallo alto del clock, lo emette su $Q$ e lo manda all'ingresso D dello slave.
Lo slave campione l'ingresso D durante l'intervallo basso del clock e lo emette su $Q$ che varia solo durante il fronte di discesa del [[clock]]


Per quanto riguarda la trasparenza:
- Nell'intervallo alto del clock il master è in trasparenza
- Nell'intervallo basso del clock lo slave è in trasparenza

Visto che l0uscita del master non cambia nell'intervallo basso del clock, non si verifica la trasparenza sulle uscite.


>[!convenzione]
> ```tikz
\usepackage{circuitikz}
\usetikzlibrary{calc}
>
>\begin{document}
>\begin{tikzpicture}
>
>\ctikzset{
>logic ports/scale = 1,
>logic ports/fill = darkgray,
>}
>
>%nodes
>\node[flipflop D,dot on notQ] (FFDa) at (-2,0){};
>\node[flipflop D,dot on notQ] (FFDb) at (2,0){};
>\node at (FFDb.bpin 3)[ocirc, left]{};
>
>%connections
>%\draw (ANDa.out) |- (ORa.in 1);
>
>\end{tikzpicture}
>\end{document}
>```
>Con la prima si indica che il clock controlla sul fronte di salita, con la seconda sul fronte di discesa?


Il flipflip D ci fornisce una nuova relazione [[relazione stato uscita]]
