Hanno una struttura più complicata rispetto ai master slave, limitano il problema di dover mantenere stabili gli ingressi al flipflop per tutto il tempo in cui il livello del clock è alto, l'evoluzione del flip flop è controllata dal fronte del clock: detto [[fronte attivo]], che agisce come segnale di campionamento. Gli ingressi e l'elemento di stato vengono campionati, memorizzati e presentati in uscita in corrispondenza di questo segnale.

Considerati
- $T_{sp} =$ tempo di setup
- $T_{prop} =$ tempo di memorizzazione dello stato



La lunghezza del clock deve essere almeno:
$T_{clock}= T_{sp} + T_{prop}$