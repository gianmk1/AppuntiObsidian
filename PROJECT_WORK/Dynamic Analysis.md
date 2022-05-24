# FRIDA
### Installation on Android
1. Download di **frida-server** per la piattaforma specifica della simulazione android
2. Riavviare la connessione con adb in **modalità root**
3. Spostare il file **frida-server** nella memoria del cellulare 
```adb push frida-server /data/local/tmp/```
4. Dare i permessi al file
```adb shell "chmod 755 /data/local/tmp/frida-server"```
5. Eseguire il file
```adb shell "/data/local/tmp/frida-server &"```


##### Alcuni comandi
```bash
# Vedere le app installate
frida-ps -Uai
frida-ps -D emulator-5554 -ai

# Vedere le app in esecuzione
frida-ps -Ua

# Vedere i processi in esecuzione
frida-ps -U

# Collegare frida al processo
frida -U -n 'Secret Cat Forest'
frida -U -n air.net.ideasam.games.cat

# Lista device collegati a Frida
frida-ls-devices

# Avviare uno script JS senza python
frida -U -l script.js air.net.ideasam.games.cat

```