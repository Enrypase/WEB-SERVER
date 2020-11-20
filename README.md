# WEB-SERVER

## PROCESSO DI INSTALLAZIONE
Installazione di **ssh** *apt-get install openssh-server*.<br>
Installazione del **webserver** *apt-get install apache2*.<br>
C'è la possibilità di creare **più siti** sulla stessa macchina aggiungendo file di configurazione in */etc/apache2/sites-avaiable/...*. Da modificare sono le opzioni rappresentanti il nome del sito, l'URL per raggiungerlo e la destinazione dei file di log<br>
Ora bisogna **creare un nuovo sito con le configurazioni appena modificate** *a2ensite*.<br>
Modifica dell'**indirizzo IP** tramite file presente in */etc/netplan/...*.<br>
**Comando** *netplan try*.<br>
Applicare la **modalità bridge** da VirtualBox.<br>
Installazione di programma **FTP** tramite comando *apt-get install vsftpd*.<br>
Modificare il **file di configurazione** */etc/vsftp.conf* come da consegna.<br>
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
