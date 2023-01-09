Fa una scansione per vedere i ref bit e gli access bit e modifica le liste


#### Controlla_lista
Inoltre definiamo una funzione Controlla_lista (attivata da kswapd) che esegue una scansione di entrambe le liste:
1. scansiona **active list**  partendo dalla coda ed eventualmente sposta alcune pagine inattive.
	1.  A = 1
		- azzera A
		- ref = 1 $\implies$ sposta P in testa alla active
		- ref = 0 $\implies$ ref = 1
	2. A = 0
		- ref = 1 $\implies$ ref = 0
		- ref = 0 $\implies$ P in testa alla inactive con ref = 1

2. scansione **inactive list** partendo dalla testa spostando eventualmente alcune pagine alla active (non scansiona quelle appena spostate).
	1. A = 1
		- azzera A
		- se ref = 1 $\implies$ sposta P in coda alla active con ref = 0
		- se ref = 0 $\implies$ ref = 1
	2. A = 0
		- se ref = 1 $\implies$ ref = 0
		- ref = 0 $\implies$ P in coda alla inactive

La pagina viene scansionata solo utilizzando **A** e **ref**