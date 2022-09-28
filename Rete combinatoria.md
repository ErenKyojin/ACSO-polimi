# Rete combinatoria
Una rete combinatoria è un circuito digitale con $n \geq 1$ ingressi in uscita, formato da porte logiche elemntari [[AND]], [[OR]] e [[NOT]], e privo di retroazioni


```tikz
\usepackage{circuitikz}
\usetikzlibrary{calc}

\begin{document}
\begin{tikzpicture}
%nodes
\node[or port] (ORa) at (3,-1){};
\node[and port] (ANDb) at (0, -2){};
\node[and port] (ANDa) at (0,0){};

%connections
\draw (ANDa.out) -| (ORa.in 1);
\draw (ANDb.out) -| (ORa.in 2);
\draw (ORa.out) -- (4,-1)node[right](Fout){F out};

\end{tikzpicture}
\end{document}
```



## Forma canonica
Le forme canoniche sono due:
1. Somma di prodotti (SoP)
2. Prodotto di somme (PoS)

Data una forma booleana esistono una ed una sola forma canonica SoP ed una e una sola forma PoS che la rappresenta


>[!esempio]
>Ricaviamo la SoP 1 dalla seguente funzione:
>
> a | b | f(a,b)
> --- | --- | ---
> 0 | 0 | 0 
> 0 | 1 | 1
> 1 | 