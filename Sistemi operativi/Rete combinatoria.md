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
> 1 | 0 | 0
> 1 | 1 | 1
> 
> È abbastanza intuitivo che si possa ottenere dall'[[OR]] delle seguenti funzioni:
>>[!multi-column]
>>
>>>[!F1]
>>>a | b | f1(a,b)
>>>  --- | --- | ---
>>>0 | 0 | 0
>>>0 | 1 | 1 
>>>1 | 0 | 0
>>>1 | 1 | 0
>>
>>>[!F2]
>>>a | b | f2(a,b)
>>>--- | --- | ---
>>>0 | 0 | 0
>>>0| 1 | 0
>>>1 |0 |0
>>>1 | 1 | 1
>
>f(a,b) = !ab + ab  è la forma canonica SoP
>
>```tikz
>\usepackage{circuitikz}
>\begin{document}
>\begin{tikzpicture}
>%nodes
>\node[not port] (Na) at (0,0.285){};
>\node[and port] (ANDa) at (3, 0){};
>\node[and port] (ANDb) at(3, -2){};
>\node[or port] (ORa) at(5,-1){};
>
>%connections
>\draw (Na.out) -| (ANDa.in 1);
>\draw (ANDa.out) -| (ORa.in 1);
>\draw (ANDb.out) -| (ORa.in 2);
>\draw (ANDa.in 2) |- (-2,-0.5)node[left]{B};
>\draw (Na.in) |- (-2, 0.285)node[left]{A};
>\draw(ANDb.in 2) -| (-1,-0.5);
>\draw(ANDb.in 1) -| (-1.5,0.285);
>\draw(ORa.out) -- (7,-1)node[right]{f(A,B)};
>\end{tikzpicture}
>\end{document}
>```





