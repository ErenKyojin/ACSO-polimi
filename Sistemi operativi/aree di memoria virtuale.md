Le aree di memoria virtuale sono diverse aree in qui salvare diversi dati di un processo.


è un sistema che porta diversi vantaggi rispetto a salvare tutti i dati nella stessa area indiscriminatamente, ad esempio è possibile:

- Gestire diversi [[pagina#Diritti d'acesso|diritti d'accesso]] delle aree:
	- **READ_ONLY**
	- **READ_WRITE**
	- **EXECUTE**

- Consentire crescita diverse e indipendente di aree (ad esempio pila ed heap)
- Gestire un'area di memoria condivisa tra processi



