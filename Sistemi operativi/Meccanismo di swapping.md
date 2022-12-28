Quando bisogna deallocare una pagina fisica scritta ([[dirty bit|dirty page]]) il suo contenuto deve essere salvato su disco:
- se SHARED nel file di [[backing store]] 
- se ANONIMA o PRIVATA e duplicata in memoria fisica a seguito di [[Copy on write]]

Tenendo a mente che una pagina fisica PFx è Dirty se
- Il suo descrittore è marcato D a seguito di un TLB flush
- Una delle pagine virtuali condivise in PFx è contenuta nel TLB ed è marcata D


# Deallocazione delle pagine
Il meccanismo di swapping permette di deallocare pagine e salvarle su disco, è richiesto che sia definita almeno un'area di swap sul disco (o un file o una partizione, swap file o [[swap area]])


## Regole generali di swapping

### Swap_out
Quando [[PFRA]] chiede di deallocare una pagina fisica (swap_out):
- Viene allocato un page slot dello [[swap area|swap file]] su disco
- La pagine fisica viene copiate nel page slot nello swap file e viene poi deallocata
- Allo *swap_map_counter* viene assegnato il numero di pagine virtuali che condividono la pagina fisica
- In ogni PTE che condivideva la pagina fisica viene registrato il SWPN identificatore del page slot al posto del NPF (il bit di presenza in memoria fisica viene azzeratto)

Negli esercizi lo SWPN delle pagine swappate è indicato nella TP preceduto da una **S** per distinguerlo da un normale NPF

>[!esempio]
>Un processo swappa d0 nel page slot 1, nella TP ci sarà 
