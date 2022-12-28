Quando bisogna deallocare una pagina fisica scritta ([[dirty bit|dirty page]]) il suo contenuto deve essere salvato su disco:
- se SHARED nel file di [[backing store]] 
- se ANONIMA o PRIVATA e duplicata in memoria fisica a seguito di [[Copy on write]]

Tenendo a mente che una pagina fisica PFx è Dirty se
- Il suo descrittore è marcato D a seguito di un TLB flush
- Una delle pagine virtuali condivise in PFx è contenuta nel TLB ed è marcata D


# Deallocazione delle pagine
Il meccanismo di swapping permette di deallocare pagine e salvarle su disco,