Quando bisogna deallocare una pagina fisica scritta (<[[dirty bit|dirty page]]) il suo contenuto deve essere salvato su disco:
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
>Un processo swappa d0 nel page slot 1, nella TP ci sarà <d0:s1>


### swap_in
Quando un processo accede ad una pagina virtuale precedentemente swappata
- Genera un [[page fault]]
- Il gestore del [[page fault]] attiva l'allocazione (**swap_in**)
- Una pagina viene allocata in [[memoria]] fisica
- Il page slot viene copiato da disco nella pagina fisica
- La PTE viene aggiornata inserendo l'NPF della pagina fisica al posto del SWPN identificatore del page slot


#### Comportamento delle [[PFRA#Spostare pagine tra le liste|liste LRU]] in caso di swap-in
Se avviene uno swap in: la NPV allocata in memora fisica viene inserita in testa alla lista active con ref = 1
Altre NPV condivise con la stessa pagina fisica da parte di altri processi vengono inserite in coda alla lista inactive con ref = 0


## Altra ottimizzazione dello swapping
Spesso dopo uno swap_in è necessario deallocare di nuovo la pagina, per limitare quindi i trasferimenti tra disco e memoria fisica linux non cencella immeadiatamente la pagina dalla swap area dopo lo swap_in, così in caso di swap_out se la pagina non è stata modificata non è necessaria scriverla su disco (perchè la abbiamo lasciata presente)


### swap cache
Introduciamo quindi una swap cache che è:
- l'insieme delle pagine rilette da swap file e non modificate
- Alcune strutture ausiliare (swap_cache_index) per gestirla come se tali pagine fossero sulla swap area 

Una pagina appartiene alla swap cache se è 
- registrata nel swap_cache_index 
- presente sia in memoria sia su swap_area 

Consideriamo una pagina swappata nella swap area:
- Se la pagina viene letta si deve eseguire uno swap_in, la pagina viene copiata dallo swap file in memoria fisica ma la copia nella swap area non viene eliminata
	- La pagina letta viene marcata in sola lattura R
	- Nel swap_cache_index viene inserito un descrittore che contiene i riferimenti alla pagina fisica PFx che al page slot SWPNx
	- Finchè la pagina viene solamente letta la situazione non cambia e se la pagina viene deallocata non è necessaria riscriverla su disco
- Se la pagina viene scritta si verifica un [[page fault]] che causa:
	- La pagina diventa privata (viene allocata una nuova pagina fisica)
	- La protezione diventa W
	- Il contatore swap_map_counter viene incrementato
	- Se il contatore è 0 il page slot viene deallocato dalla swap area

