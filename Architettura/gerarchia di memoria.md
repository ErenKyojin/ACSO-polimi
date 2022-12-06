Una gerarchia di memoria è un sistema di [[memoria]] composto da più livelli, con aumento della velocità e riduzione delle dimensioni più si sale nella gerarchia.

```mermaid
graph BT
	A[Disco] --> B[Memoria principale] <--> C[Cache] --> D[Registri]
```
>[!oss]
>Un livello può comunicare solo con i suoi adiacenti, la [[Cache]] è più piccola rispetto alla memoria principale
