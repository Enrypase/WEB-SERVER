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

- **checkpoint:** <br>
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

> ***systemctl status vsftpd.service*** <br>
_Questo comando permette la visualizzazione dello stato del processo relativo a vsftpd (FTP). Altri comandi utili potrebbero essere ***netstat*** oppure ***ps***_


### **Passo 5:**
**(Opzionale ma fortemente consigliato)** Per l'installazione di un Web-Server è preferibile che ogni utente abbia a disposizione una determinata zona del File-System della macchina.
Per fare ciò bisogna creare degli utenti i quali possiedono una determinata home (diversa da quella del root) contenente tutti i file dei quali l'utente potrebbe necessitare. In questo caso i file di Log e i vari HTML, CSS, Script, file multimediali eccetera eccetera;

- **Comandi:** <br>
Per l'eseguzione dei seguenti comandi è necessario che l'utente sia **root**.

> ***useradd -s /bin/bash -d /var/www/... -m nomeUtente*** <br>
_Comando che permette la creazione di un utente. Con **-s** diamo a disposizione dell'utente la **bash**; con **-d** diamo all'utente una **home directory**; con **-m** diamo il **nome** dell'utente

>



C'è la possibilità di creare **più siti** sulla stessa macchina aggiungendo file di configurazione in */etc/apache2/sites-avaiable/...*. Da modificare sono le opzioni rappresentanti il nome del sito, l'URL per raggiungerlo e la destinazione dei file di log<br>
Ora bisogna **creare un nuovo sito con le configurazioni appena modificate** *a2ensite*.<br>
Aggiungere un **utente** *useradd -s /bin/bash -d /var/www/... -m nomeUtente*.<br>
Impostare la **password dell'utente** *passwd nomeUtente* --> *Inserimento della password*.<br>

### NOTA: <br>
è fortemente consigliato creare prima l'utente con il comando sopra specificato, della directory, in modo tale che i vari permessi siano già settati in automatico. Altrimenti, dobbiamo eseguire i seguenti comando: *chown -R nomeUtente:nomeUtente directoryCartella* e *chmod +rwx directoryCartella* <br>

## PROCESSO DI CONFERMA
- Si può verificare l'effettiva installazione di openssh provando a connettersi tramite "PuTTy" o da altre shell ssh.<br>
- Si può, inoltre, verificare quella di apache inserendo l'indirizzo IP della macchina virtuale nel browser e visualizzare la pagina default di apache in risposta.<br>
- Allo stesso modo, una volta creati i diversi siti tramite apache, basterà inserire il loro indirizzo nel browser per verificarne l'effettiva visualizzazione.<br>
- Si può, invece, verificare l'effettiva applicazione dell'indirizzo IP tramite i comandi ifconfig o ip addr.<br>
- Ora, si può verificare se la macchina è raggiungibile tramite comando *ping*.<br>
- Una volta modificato il file di configurazione per FTP si può verificare l'effettiva funzionalità provando a connettersi tramite *filezilla* o altri programmi che supportano FTP alla macchina virtuale.<br>
- Si prova prima di tutto la connessione, per vedere se è possibile accedere alla macchina, in seguito bisogna provare a passare un file dalla macchina virtuale al pc e, infine, dal pc alla macchina virtuale. Se tutti questi passaggi vanno a buon fine, possiamo dire di aver installato il client FPT con successo. <br>

# AGGIUNGERE COMANDI NEI RIQUADRI, ESEMPI DI RISULTATO E FILE DI CONFIGURAZIONE (presenti sul pc in etc e var (desktop))
