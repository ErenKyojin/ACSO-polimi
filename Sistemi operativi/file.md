Un file è una sequenza di byte che rappresenta un insieme di formazioni, ha un nome simbolico (ed univoco) all'interno della directory e degli attributi (tipo, locazione nel dispositivo, dimensione, protezione, proprietari). In linux ci sono diversi tipi di file:
- **File ordinario o normale**: dati o programmi
- **Directory**
- **File speciale**

Il file è visto dal file system come una sequenza di blocchi logici nymeratii in sequenza a partire dal bloco 0, le operazioni di read e write si riferiscono alla posizione (byte) all'interno del blocco


| blocco 0 | blocco 1 | blocco 2 | ... | blocco 512 |
| -------- | -------- | -------- | --- | ---------- |
| 0        | 512      | 1024     |     |            |
