# Linux
![[scaricare slide da classroom]]

Linux ha 3 fondamentali da ricordare:
1. Nucleo o kernel
2. Shell
3. Filesystem

![[slide 02_]]

#### Kernel
- ci mette a disposizione le risorse
- ...
- ...

Passa i comandi ad una shell

#### Shell
![[slide parte 08]]

![[link sito paolo morettin]]

Ci permette di eseguire dei comandi

#### Filesystem
Rappresenta il modo nel quale vengono organizzati i file.
Windows considera uan stampante come diversa da video, tastiera
In unix si rende trasparente il tipo di oggetto e dire che tutti gli oggetti vengano visti come dei **file** (non come l'oggetto stampante in se).

=> periferiche sono viste come **file**

![[slide parte 03]]
Se c'è un dispositivo che non viene riconosciuto bisogna oltre a installare i driver anche **montarlo** nel file system per fare in modo che venga visto come un file

bin : dove ci sono file di configurazione
etc : ??

##### Mount
...


![[slide parte 04]]

#### Filtri sui file
![[slide parte 06]]

Dobbiamo sapere dei comandi per filtrare i nostri risultati


### Comandi linux
Il prompt dei comandi essendo linux una piattaforma multiutente visualizziamo il nome utente, nome della macchina, il percorso corrente e il $

ls -la : vedo anche 
d > directory
- > file
l > link

r > read
w > write
x > eseguibile

questi ultimi 3 sono riferiti all'utente stesso, poi al gruppo e poi a tutti gli altri

.file		questo è un file nascosto


**pwd** per stampare la directory corrente

**tac** per stampare file con ordinamento al contrario

**head -1 nome_file** per stampare prima riga di un file
**tail -1 nome_file** per stampare ultima rida di un file

## Shell
*dal sito vedere "redirezione", "pipe"*



