# Servizi di sistema

>[!tldr] Tabella di definizione delle [[system call]] e mappa delle funzioni
>#todo lezione 7: 5/8/12
>
> glibc libreria [[gnu]] per il C


>[!esempio] Invocazione del servizio read()
>1. Programma -> read(fd, buf, len)
>2. read(fd, buf, len) -> syscall(sys_read, fd, buf, len) 
>3. syscall():
>	1. pone sys_read nel [[registro]] rax
>	2. pone fd, buf, len nei registri rdi, rsi, rdx
>	3. esegue istruzione [[SYSCALL]]
>
>4. inizia la unzione del kernel system_call che a sua volta invoca system call service routine opportuna per eseguire il sevizio e sys_read
>5. esecuzione sys_read (codice del [[sistema operativo]])
>6. il servizio ritorna alla funzione system_call
>7. la funzione system_call ritorna eseguendo l'istruzione [[SYSRET]]


Passiamo da modalità U a modalità S dopo la SYSCALL (maiuscola)

## Wake Up

>[!esempio]
>```c
>void wake_up(wait_queue_head_t * wq) {
>	for each task in waitqueue wq {
>		//risveglia e cambia lo stato della task da attesa a pronto
>		//elimina il task dalla waitqueue
>		enqueue_task() //inserisci nella runqueue
>		if(flag == EXCLUSIVE) break //esci dal ciclo scansione wq
>	}
>	
>	check_preempt_curr(){
>		//verifica se il task deve essere preempted per modifica
>		//insieme dei processi pronti nella runqueue
>		//se necessario invoca reached
>	}
>} //wakeup
```


