L'esecuzione di una exit causa molteplici effetti sulla memoria:
- VMA del processo
- Eliminazione della PT del processo
- Deallocazione delle NPV del processo con
	- **Se** *ref_count = 1* deallocazione delle pagine fisiche occupate da questi NPV
	- **Altrimenti** riduzione del loro ref_count di uno
Se il processo terminato ha dei thread attivi vanno anch'essi eliminati