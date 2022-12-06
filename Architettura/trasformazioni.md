# Trasformazione di una [[funzione logica]]


>[!esempio]
>F(a,bc) = !a!bc + !abc + !ab!c
>
>**Applichiamo idempotenza**
>!a!bc + !abc + !ab!c = !a!bc + !abc + !abc +!ab!c
>
>**Applichiamo distributiva**
>!a!bc + !abc + !abc +!ab!c = !ac(!b+b) + !ab(c+!c)
>
>**inverso**
>!ac(!b+b) + !ab(c+!c) = !ac1 + !ab1
>
>**identità**
>!ac1 + !ab1 = !ac + !ab
>
>**distributiva**
>!ac + !ab = !a(c+b)

Così abbiamo trovato una funzione equivalente ma che avrà bisogno di meno operazioni, che si traduce a livello di circuito in semplicità e riduzione del consumo
