# DOCUMENTAZIONE WEB-SERVER

## PROCESSO DI INSTALLAZIONE


### **Passo 1:**
Il primo passo per portare a buon fine la configurazione di un server web è quello di assegnare a esso un IP statico, in modo tale che si possa raggiungere facilmente;

- **Comandi:** <br>
Per l'eseguzione dei seguenti comandi è necessario che l'utente sia **root**.

> ***apt-get install net-tools*** <br>
_Questo comando permetterà l'installazione di tools utili per la verifica dello stato del network_

> ***nano /etc/netplan/00-installer-config.yaml*** <br>
_File di esempio: [File](https://github.com/Enrypase/WEB-SERVER/blob/main/00-installer-config.yaml)_

> ***netplan try*** <br>
_Questo comando darà anche il relativo esito dell'operazione. Se positivo, verrà chesto di dare l'OK per applicare le modifiche_

- **Checkpoint:** <br>
I seguenti passi saranno utili per confermare l'effettivo esito dei passaggi sopra eseguiti.

> ***ifconfig*** <br>
_Con questo comando verranno visualizzate tutte le interfacce di rete. Basterà quindi verificare che quella interessata abbia l'indirizzo IP inserito in precedenza per vedere se le impostazioni sono state applicate correttamente e definitivamente. Potremmo utilizzare anche il comando **ip addr**_

> ***wget www.google.com*** <br>
_Questo comando è preferibile a quello di Ping essendo che i pacchetti ICMP potrebbero essere scartati da certi router, mentre quelli FTP no. Se la richiesta del sito (in questo caso Google) va a buon fine, significa che l'indirizzo statico sopra-inserito ci permette di navigare in internet_


### **Passo 2:**
In questo passo andremo a installare un client che permette l'accesso SSH alla macchina. Così facendo questa sarà raggiungibile da tutte le altre macchine presenti in rete;

- **Comandi:** <br>
Per l'eseguzione dei seguenti comandi è necessario che l'utente sia **root**.

> ***apt-get install openssh-server*** <br>
_Una volta fatto questo il servizio dovrebbe già essere attivo e, di conseguenza, la macchina dovrebbe già permettere l'accesso tramite SSH_

- **Checkpoint:** <br>
I seguenti passi saranno utili per confermare l'effettivo esito dei passaggi sopra eseguiti.

> ***systemctl status ssh.service*** <br>
_Questo comando permette la visualizzazione dello stato del processo relativo a SSH. Altri comandi utili potrebbero essere ***netstat*** oppure ***ps***_


### **Passo 3:**
In questo passo effetueremo l'installazione di Apache Server;

- **Comandi:** <br>
Per l'eseguzione dei seguenti comandi è necessario che l'utente sia **root**.

> ***apt-get install apache2*** <br>
_Con questo comando verrà installato il web-server Apache_

- **Checkpoint:** <br>
I seguenti passi saranno utili per confermare l'effettivo esito dei passaggi sopra eseguiti.

> ***systemctl status apache2.service*** <br>
_Questo comando permette la visualizzazione dello stato del processo relativo ad Apache (Web-Server). Altri comandi utili potrebbero essere ***netstat*** oppure ***ps***_


### **Passo 4:**
In questo passo installeremo il client FTP in modo tale da permettere tale accesso sulla macchina e, di conseguenza, poter modificare e trasferire files da macchine in rete alla macchina soggetta;

- **Comandi:** <br>
Per l'eseguzione dei seguenti comandi è necessario che l'utente sia **root**.

> ***apt-get install vsftpd*** <br>
_Con questo comando verrà installato il client FTP vsftpd_

> ***nano /etc/vsftpd.conf*** <br>
_File di esempio: [File](https://github.com/Enrypase/WEB-SERVER/blob/main/vsftpd.conf)_

> ***systemctl reload vsftpd.service*** <br>
_Con il comando sopra stante potremo riavviare il servizio, così facendo verranno applicate le impostazioni appena modificate senza dover per forza fare un reboot_

- **Checkpoint:** <br>
I seguenti passi saranno utili per confermare l'effettivo esito dei passaggi sopra eseguiti.

> ***systemctl status vsftpd.service*** <br>
_Questo comando permette la visualizzazione dello stato del processo relativo a vsftpd (FTP). Altri comandi utili potrebbero essere ***netstat*** oppure ***ps***_


### **Passo 5:**
**(Opzionale ma fortemente consigliato)** Per l'installazione di un Web-Server è preferibile che ogni utente abbia a disposizione una determinata zona del File-System della macchina.
Per fare ciò bisogna creare degli utenti i quali possiedono una determinata home (diversa da quella del root) contenente tutti i file dei quali l'utente potrebbe necessitare. In questo caso i file di Log e i vari HTML, CSS, Script, file multimediali eccetera eccetera;

- **Comandi:** <br>
Per l'eseguzione dei seguenti comandi è necessario che l'utente sia **root**.

> ***useradd -s /bin/bash -d [homeDirectory] -m [nomeUtente]*** <br>
_Comando che permette la creazione di un utente. Con **-s** diamo a disposizione dell'utente la **bash**; con **-d** diamo all'utente una **home directory**; con **-m** diamo il **nome** dell'utente

> **passwd [nomeUtente]** <br>
_Una volta  dato l'invio verrà richiesto all'utente di assegnare una password all'utente inserito. Quindi, è necessario re-inserire la stessa password due volte di seguito accertandosi che siano uguali e corrette_

- **Checkpoint:** <br>
I seguenti passi saranno utili per confermare l'effettivo esito dei passaggi sopra eseguiti.

> ***Accesso tramite FTP-Client*** <br>
_Per verificare che l'utente sia stato creato effettivamente si può tentare l'accesso tramite client FTP, nel caso in cui ci fossero dei problemi con dei permessi nel trasferimento, bisogna tornare sulla macchina e digitare ***chown -R [nomeUtente]:[nomeUtente] [directoryCartella]***.
Se nonostante questo ci fossero comunque dei problemi con dei permessi bisogna eseguire il seguente comando: ***chmod +rwx [directoryCartella]***.
Se ci fossero comunque problemi bisogna controllare il file di configurazione di vsftpd (FTP)_


### **Passo 6:**
Qui finiremo la configurazione del Web-Server andando a configurare Apache;

- **Comandi:** <br>
Per l'eseguzione dei seguenti comandi è necessario che l'utente sia **root**.

> ***nano /etc/apache2/sites-avaiable/default-ssl.conf*** <br>
_File di esempio: [File](https://github.com/Enrypase/WEB-SERVER/blob/main/000-default.conf) <br>
Modificare il file in base alle proprie necessità. Le tre voci principali da modificare sono ***ServerName*** che contiene la URL del sito, ***DocumentRoot*** che contiene la posizione del sito nel FileSystem, ***ErrorLog*** dove deve essere indicata la posizione per i file di log relativi agli errori e ***CustomLog*** dove deve essere indicata la posizione per i file di log relativi agli accessi, richieste e altre operazioni. <br>
***ATTENZIONE, è preferibile, però, lavorare su un altro file e non direttamente su quello di default_***

> ***a2ensite [nomeFile]*** <br>
_Con questo comando si abilita il sito_

> ***systemctl reload apache2*** <br>
_Con questo comando verrà riavviato il servizio di Apache, in modo tale da rendere i cambiamenti effettivi <br>
Se il riavvio andrà a buon fine non verrà visualizzato alcun messaggio di errore, altrimenti sarà segnalato un problema_

- **Checkpoint:** <br>
I seguenti passi saranno utili per confermare l'effettivo esito dei passaggi sopra eseguiti.

> ***journalctl -xe*** <br>
_Con questo comando sarà possibile vedere i log del sistema che comprendono anche il riavvio di Apache. In caso di problemi, tutti i possibili errori che impediscono l'avvio di Apache verranno segnalati qui_

> ***Raggiungere la pagina dal browser***
_Per verificare se il sito è raggiungibile, il modo più semplice e rapido è quello di provare a raggiungerlo da un browser qualsiasi. Se il sito comparirà significa che tutte le operazioni sono andate a buon fine. In caso di errori bisognerà controllare nuovamente i file di configurazione del sito_


### NOTA: <br>
*Si consiglia di effettuare tutte le operazioni rispettando l'ordine con le quali sono state esposte* <br>


# AGGIUNGERE COMANDI NEI RIQUADRI, ESEMPI DI RISULTATO E FILE DI CONFIGURAZIONE (presenti sul pc in etc e var (desktop))
