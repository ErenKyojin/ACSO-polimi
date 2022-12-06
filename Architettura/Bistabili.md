
Elementi di memoria fondamentali, sono caratterizzati da due stati stabili, rappresentati con $0$ e $1$, i bistabili mantengono lo stato memorizzato finche uno o più segnali d'ingresso non ne modificano lo stato.

I bistabili soffrono di [[ritardo di propagazione]]
# Latch

## Bistabile SR asincrono

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
\node[nor port] (ORa) at (0,1){};
\node[nor port] (ORb) at (0,-1){};
\node[left](S) at (ORa.in 1) {S};
\node[left](R) at (ORb.in 2) {R};
\node[right](nQ) at (ORa.out){$\bar{Q}$};
\node[right](Q) at (ORb.out){$Q$};
%connections
%\draw (ANDa.out) |- (ORa.in 1);
\draw (Q) -- (ORa.in 2);
\draw (nQ) -- (ORb.in 1);

%bistabile
\node[flipflop SR] (FSR) at (5,0){bistabile SR};

\end{tikzpicture}
\end{document}
```


Abbiamo gli ingressi S (set) e R (reset) e 2 uscite $Q$ e $\overline{Q}$, che sono rispettivamente lo stato memorizzato ed il suo negato.
Quindi se S = R = 0, l'uscita Q ammette 2 stati stabili:
- Se lo stato presente $Q_{T} = 1 \implies Q_{T+1} = 1$
- Se lo stato presente $Q_{T} = 0\implies Q_{T+1} = 0$
- Se S = 1, R = 0, $Q_{t+1}=1$ a prescindere
- Se S = 0, R = 1, $Q_{t+1}=0$ a prescindere
- Se S = 1, R = 1, il sistema non è definito, in teoria dovremmo avere $Q = 0$ e $\overline{Q} =0$

>[!oss] ritardo di propagazione di un bistabile SR asincrono
>![[Pasted image 20221010183149.png|200]]

>[!error] Problema
>Hazard, ossia segnali non voluti casuali, possono cambiare i valori mantenuti nel bistabile, la soluzione è l'introduzione del'[[clock]], che ci  introduce il bistabile SR sincrono
>![[Pasted image 20221010183827.png|300]]


## Bistabile SR sincrono
In questo tipo di bistabile c'è un terzo ingresso oltre ad S ed R, chiamato [[clock]], che se uguale a 0 "blocca" gli ingressi, questo fornisce un "intervallo" in cui è possibile cambiare i valori.



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


\node[flipflop JK] at (7,-1){};

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


Se il clock vale 0, gli ingressi sono chiusi (opaco), ed il bistabile mantiene lo stato corrente, se il clock è 1 gli ingressi sono efficaci, ossia il [[latch]] è trasparente, ed il funzionamento è analogo ad un SR asincrono


## Bistabile D sincrono

- 1 Ingresso D
- 1 ingresso di sincronizzazione
- 2 uscite: $Q$ e $\overline{Q}$ 

Se il clock vale $0$ l'ingresso $D$ è inefficace (Il latch D è opaco)
Se il clock vale uno l'ingresso $D$ è efficace e il bistabile memorizza il valore presente sull'ingresso $D$


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
\node[and port] (ANDa) at (0,0.28){};
\node[and port] (ANDb) at (0,-2.28){};
\node[nor port] (NORa) at (2,0){};
\node[nor port] (NORb) at (2,-2){};
\node (D) at (-3,0.56){D};
\node (CLK) at (-3,0){CLK};
\node[not port,rotate=270](NOTa) at (-3,-1){};

\node[latch] at (6,-1){};
%connections
\draw (ANDa.out) |- (NORa.in 1);
\draw (D) |- (ANDa.in 1);
\draw (CLK) |- (ANDa.in 2);
\draw (D) |- (NOTa.in);
\draw (NOTa.out) |- (ANDb.in 2);
\draw (CLK) -| (ANDb.in 1);
\draw (NORb.out) -- (NORa.in 2);
\draw (NORa.out) -- (NORb.in 1);
\draw (ANDb.out) |- (NORb.in 2);

\end{tikzpicture}
\end{document}
```


>[!oss]
>I [[latch]] (ossia i bistabili con [[relazione stato uscita]] basata sul livello del clock) sincroni, presentano durante l'intervallo di tempo in cui il clock è attivo, un fenomeno detto "trasparenza delle uscite".
>Ossia durante ogni ciclo di clock se gli ingressi si modificano anche le uscite possono cambiare, per questo si introducono i [[flipflop D master-slave]]


# Flipflops

## [[flipflop D master-slave]]

## [[flip flop edge triggered]]

>[!tldr]
>
|         | Livello         | fronte                   |
| ------- | --------------- | ------------------------ |
| fronte  |                 | flip-flop edge triggered |
| livello | latch con clock | flipflop master slave                         |

