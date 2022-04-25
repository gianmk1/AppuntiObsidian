	**ES1**. 
130.192.0.0 -> 1000 0010 (130). È di classe B, ed è una rete
192.168.0.0 -> 1100 0000 (192). È di classe C, ed è una rete
80.45.0.0	 -> 0101 0000 (80).  È di classe A, non è una rete
112.0.0.0     -> 0111 0000 (112). È di classe A, 
198.0.1.0     -> 1100 0110 (198). È di classe C, 
134.188.1.0  -> 1000 0110 (134). È di classe B
224.0.0.3    -> 1110 0000 (224). È di classe D, non è rete
241.0.3.1      -> 1111 0001 (241). È di classe E, non è rete
235.0.0.0     -> 1110 1011 (235). È di classe D, non è rete

Una rete non termina mai con numero dispari.
L'indirizzo di rete broadcast è dispari.
Host sono pari.
...


**ES2**. (diverso)
Utilizziamo un piano classless 
(vedi sul foglio)

**ES6**:
Ipotizzando di avere un indirizzamento classless e l'address range 192

Numero Host | Rete 		| Indizirro broadcast
------------|-----------|--------------------
1540		|2^11, prefisso 32-11=21, 192.168.0.0/21,  | 192.168.7.255
1010		|2^10, prefisso 32-10=22, 192.168.0.0/22,  | 192.168.3.255
2			|2^3, prefisso 32-3=29, 192.168.0.0/29
300			|2^9, prefisso 32-9=23, 192.168.0.0/23	   | 192.168.1.255