Tabella con indirizzi NPF in cui inseriamo gli [[NPV]] delle [[Memoria virtuale#VMA|pagine virtuali]]. Alcune osservazioni:
- La pagina NPF = 00 è detta **ZeroPage** e si indica con **\<ZP>**
- Memoria fisica di 12 pagine
- La pagina **n**, nell'area virtuale **A** (che indica un area virtuale con [[Memoria virtuale#Codice: C]]) del processo **P** si indica come **PAn**
- L'allocazione è on demand ed usa sempre la prima pagina disponibile (ossia la 01)
- Se una pagina è condivisa o mappata su file, glli utilizzi diversi si indicano come: PC1/X