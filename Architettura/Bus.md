# BUS
Un BUS è una linea di uscite e ingresso, o "di trasporto", del segnale.

Un bus a 4 segnali è un collegamento a 4 bit


## Linee di uscita condivise
Ipotizziamo di avere due o più componenti, entrambi connesso allo stesso BUS, come si può garantire la non interferenza del segnale? Ci sono degli opportuni elementi funzionali che, se il BUS è impegnato, generano uno stato di alta [[impedenza]] $\mathcal{Z}$ che essenzialmente genera un circuito aperto tra i componenti ed il BUS (eccetto il componente in uso, questi componenti si dicono [[buffer tri-state]]
