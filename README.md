# DOCUMENTAZIONE-VM

## PROCESSO DI INSTALLAZIONE
Installazione di **ssh** *apt-get install openssh-server*.<br>
Installazione del **webserver** *apt-get install apache2*.<br>
C'è la possibilità di creare **più siti** sulla stessa macchina aggiungendo file di configurazione in */etc/apache2/sites-avaiable/...*.<br>
Ora bisogna **creare un nuovo sito con le configurazioni appena modificate** *a2ensite*.<br>
Modifica dell'**indirizzo IP** tramite file presente in */etc/netplan/...*.<br>
**Comando** *netplan try*.<br>
Applicare la **modalità bridge** da VirtualBox.<br>
Installazione di programma **FTP** tramite comando *apt-get install vsftpd*.<br>
Modificare il **file di configurazione** */etc/vsftp.conf* come da consegna.<br>
Aggiungere un **utente** *useradd -s /bin/bash -d /var/www/... -m nomeUtente*.<br>
Impostare la **password dell'utente** *passwd nomeUtente* --> *Inserimento della password*.<br>

## PROCESSO DI CONFERMA
Si può verificare l'effettiva installazione di openssh provando a connettersi tramite "PuTTy" o da altre shell ssh.<br>
Si può, inoltre, verificare quella di apache inserendo l'indirizzo IP della macchina virtuale nel browser e visualizzare la pagina default di apache in risposta.<br>
Allo stesso modo, una volta creati i diversi siti tramite apache, basterà inserire il loro indirizzo nel browser per verificarne l'effettiva visualizzazione.<br>
Si può, invece, verificare l'effettiva applicazione dell'indirizzo IP tramite i comandi ifconfig o ip addr.<br>
Ora, si può verificare se la macchina è raggiungibile tramite comando *ping*.<br>
Una volta modificato il file di configurazione per FTP si può verificare l'effettiva funzionalità provando a connettersi tramite *filezilla* o altri programmi che supportano FTP alla macchina virtuale.<br>
