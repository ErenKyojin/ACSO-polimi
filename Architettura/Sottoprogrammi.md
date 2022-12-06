# Sottoprogrammi

### Chiamante (caller)
- Predispone i parametri da passare tramite i registri a2-a7
- Trasferisce il controllo al sotto programma tramite jump and link `jal`


### Chiamato (callee)
- Allocazione dell'area di attivazione su stack
- esecuzione
- Memorizza il risultato in a0/a1
- Restituisce tramite jr ra, ret


>[!esempio]
>
>#### chiamata:
>```armasm
>jal ra, label ;# jump and link, ra <--- PC + 4, ossia l'indirizzo di ritorno, terminato il sottoprogramma l'istruzione va al comando successivo al caller. PC <-- label
>
>```
>
>#### ritorno da sottoprogramma
>```armasm
>jr ra
>```


Tuttavia non può essere così semplice il sistema, infatti in questo modo si creano svariati problemi:

```mermaid
flowchart BT
	 subgraph MAIN
	 direction TB
	 C[jal ra, A]
	 end
	 C --> A:
	 
	 
	 subgraph A:
	 direction TB
	 a1[jal ra, B]
	 a2[jr ra]
	 a1 --> a2
	 end
	 a1 --> B:
	 
	 
	 subgraph B:
	 direction TB
	 b1[jal ra, C]
	 b2[jr ra]
	 b1 --> b2
	 end
	 b1 --> C:
	
	 subgraph C:
	 direction TB
	 c2[jr ra]
	 end
	 c2 --> B:
	 b2 --> b2
	 b2 -.-x A:
	 a2 -.-x MAIN
```

Se salviamo ad ogni chiamata nel [[registro]] ra, già dopo due chiamate non è possibile tornare indietro al chiamante originale, la soluzione è semplice, salvare gli ra precedenti in memoria.


## Utilizzo della [[memoria]]
Ogni chiamata crea un'area di attivazione sullo stack, quando il sottoprogramma termina l'area viene rilasciata:

```mermaid
classDiagram
   class main
   main: A
   main: B
   main: C
   main: indirizzi bassi()
```
I dati vengono inseriti con push ed estratti con pop

>[!def] Push
>```armasm
>addi sp, sp, -16
>sd t1, 8(sp)
>sd t2, 0(sp)
>```

>[!def] Pop
>```armasm
>ld t2, 0(sp)
>ld t1, 8(sp)
>addi sp, sp(16)
>```
