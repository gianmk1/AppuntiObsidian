# Encoding
### Perchè si usa l'Encoding?
- **Trasformare i dati** affinchè possano essere opportunamente **utilizzati da altri tipi di sistemi**
- L'obiettivo NON è mantenere le informazioni segrete
- Si può fare facilmente reverse sull'encoding
- L'operazione è inversa è l'**encoding**

### Base64
- Molto comune nella comunicazione web
- La lunghezza del messaggio finale è sempre un multiplo di 4
- [A-Z, a-z, 0-9, +, /, =]
- **può finire con = o ==**

### Esadecimale
- Simile al base64
- [A-F, 0-9]
- Utilizzato soprattutto per:
	- Indirizzi MAC
	- Registri di memoria

### UUEncoding
- **Inizia** con il tipo e il nome del file
- Finisce sempre con " ' "

