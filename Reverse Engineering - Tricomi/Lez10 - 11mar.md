# Overview di C
- **C è un linguaggio STRUTTURATO**
- fu il primo ad introdurre i commenti
- È un linguaggio a **basso livello**, quindi è molto potente

Le LIBRERIE riprendono un file .h dove sono state scritte le funzioni.

La **funzione MAIN è l'entry point** di ogni programma.

### Data Type in C
- **Primitive data type**
	- int, float, double, char
- **Aggregate data types**
	- array
- **Strutture definite dall'utente**

**NB**. Bisogna sempre **definire il tipo della variabile**.

### Input e Output
**INPUT:** 
- scanf("%d",&a);
- il **gets** NON controlla il dato inserito

**OUTPUT:**
- printf("%d", a);
- puts prende la stringa contenuta nella variabile e va a printarla nello schermo

### Placeholde
%f	float
%d	decimali
%x	esadecimale
%c	caratteri

### Ciclo FOR
for(inizializzazione; controllo condizione; incremento) {
	// corpo del for
}

### While loop
while (condizione) {
	// corpo del while	
}

### Do While
do {
	// corpo del ciclo
} while(condizione);

A differenza del while, il do while esegue il corpo del ciclo **almeno una volta**.

### Switch case
switch (variabile) {
	case 1:
		// nel caso sia uno
		break;
	case n:
		// nel caso sia n...
		break;
	default:
		// nel caso le condizioni precedenti non siano verificate
		break;
}

Corrisponde ad una serie di if-else.

### Operatori
- Logici (&& and , || or)
- Relazionali
- Aritmetici
- Compound assignment
- Shift

### Le stringhe
**strlen(str)** -> per trovare la lunghezza della stringa
**strrev(str)** -> per rovesciare la stringa
**strcmp(s1,s2)** -> per verificare se le due stringhe sono uguali
**strcmpi(s1,s2)** -> string compare ma **case sensitive**

### Procedure
La **procedura** è una funzione che ritorna un dato **void**.
Per ritornare qualcosa si utilizza **return**.

**Dichiarazione funzione:**
tipo_dato_di_ritorno nome_funzione (parametri);

**Definizione della funzione:**
tipo_dato_di_ritorno nome_funzione (parametri) {
	// corpo della funzione
}

**Richiamo della funzione:**
nome_funzione (parametri);

### Parametri
I parametri possono essere:
- **FORMALI**: quelli che noi scriviamo e di cui non sappiamo il valore, ma vengono utilizzati all'interno della funzione
- **ATTUALE**: parametro di cui sappiamo il valore

### Array
- Possono contenere solo dati dello stessso tipo
- int a[5] è un array che stora 5 interi
- int a[5][5] è una **matrice**

### Strutture ???
Le **strutture** vengono utilizzate per **definire dei tipi** che possono essere utili agli utenti.

struct persona {
	int id;
	char name[5];
} ...

### Puntatori
**Sono delle variabili che puntano ad altre variabili**.

Il puntatore salva al suo interno l'indirizzo di memoria di quella variabile, diventa in pratica un **alias**.

Per definire il puntatore di tipo intero:
int *ip;

Assegnare un indirizzo:
int *ip = &a;

### Chiamate 
- **Call by value**: quando richiamiamo una funzione **viene creata una copia della variabile**, che poi verrà utilizzata all'interno di una funzione

	Il contenuto della variabile originaria NON sarà intaccato da ciò che faremo all'interno della funzione.

- **Call by reference**: es. fun(&a) , in questo modo tutto ciò che accadrà all'interno della funzione avrà poi effetto sulla variabile stessa.
