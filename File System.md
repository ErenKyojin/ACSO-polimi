Linux gestisce i file system a livello logico attraverso dispositivi logici detti [[volumi]], un [[file]] è visto dal file system come una sequenza di [[blocco#Blocchi logici]]

Per mappare da blocchi logici a blocchi fisici e viceversa utiliziamo la tecnica di [[i-node]]


# Strutture dati del file system

## Tabella dei descrittori dei file aperti per processo

Esiste una tabella per ogni [[processo]] attivo nel sistema. Indi


- Tabella globale dei file aperti
	- Tabella globale del sistema operativo con una riga per ogni file aperto nel sistema

- Tabella degli i-node (detta in-core i-node)
	-  Tabella globale del sistema che contiene una copia in memoria degli i-node relativi al volume