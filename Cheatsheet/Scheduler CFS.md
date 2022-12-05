## Senza pesi

- **NRT**: **n**ume**r**o di **t**ask in runqueue
- **PER**: **Per**iodo di schedule = max(*LT*, *NRT* * *GRT*)
- **Q**: **Q**uanto di tempo = *PER*/*NRT*
- **RB**: coda dei task
- **LT**: **L**a**t**enza (6ms)
- **GR**: **Gr**anularita (0,75 ms)


## Con pesi (LOAD)

>In questo caso ogni task ha un peso diverso, e quindi ogni task ha proprietà diverse che indichiamo con t.PROPRIETÀ

- **RQL**: **R**un**Q**ueue**L**oad, la somma dei pesi della runqueue
- **LC**: **L**oad**C**oefficient = *t.LOAD* / *RQL*
- **t.Q**: quanto della task t = *Per* * *t.LC* = *PER/RQL* * *t.load*


## con tempo virtuale

- **VRT**: **V**irtual**R**un**t**ime, misura del tempo consumato da un processo, corrisponde al tempo reale modificato da alcuni coefficienti ed è utile a scegliere il prossimo processo come quello con il VRT minimo
- **RB**: ordinata in ordine di VRT
- **LFT**: **L**e**ft**most, primo elemento della RB
- **DELTA**: Tempo di esecuzione di una task
- **SUM**: tempo di esecuzione, *SUM* = *SUM* + *DELTA*
- **t.VRTC**: **VRT**_**C**oefficient = 1 / *t.LOAD*
- **t.VRT**: *t.VRT* + *DELTA* ** *t.VRTC*
- **VMIN**: minimo *VRT* tra tutte le task nella runqueue: tmin(*curr.VRT*, *LFT.vrt*) ^[1]


>[!tldr] #### TLDR
>1. Il primo task della coda *RB* viene estratto e posto uguale a CURR
>2. CURR eseguito fino a quando no scade il suo quanto Q
>3.  CURR sospeso e posto in fondo a *RB*


# Gestione di eventi

## wakeup di un processo `tw`
Quando un processo viene risvegliato potrebbe avere o un VRT basso se in attesa da molto tempo o abbastanza alto (se in attesa da poco)
Il nuovo VRT è:
`tw.VRT = MAX(tw.VRT, (VMIN - LT/2))`


^[1]: dfd