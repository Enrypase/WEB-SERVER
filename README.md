# DOCUMENTAZIONE-VM

## PROCESSO DI INSTALLAZIONE
Installazione di ssh *apt-get install openssh-server*
Installazione del webserver *apt-get install apache2*
C'è la possibilità di creare più siti sulla stessa macchina aggiungendo file di configurazione in */etc/apache2/sites-avaiable/...*
Ora bisogna creare un nuovo sito con le configurazioni appena modificate *a2ensite*
Modifica dell'indirizzo IP tramite file presente in */etc/netplan/...*
Comando *netplan try*
Applicare la modalità bridge da VirtualBox
Installazione di clietnt FTP tramite comando *apt-get install vsftpd*
Modificare il file di configurazione */etc/vsftp.conf* come da consegna
Aggiungere un utente *useradd -s /bin/bash -d /var/www/... -m nomeUtente*
Impostare la password dell'utente *passwd nomeUtente* --> *Inserimento della password*

## PROCESSO DI CONFERMA
Si può verificare l'effettiva installazione di openssh provando a connettersi tramite "PuTTy" o da altre shell ssh
Si può, inoltre, verificare quella di apache inserendo l'indirizzo IP della macchina virtuale nel browser e visualizzare la pagina default di apache in risposta
Allo stesso modo, una volta creati i diversi siti tramite apache, basterà inserire il loro indirizzo nel browser per verificarne l'effettiva visualizzazione
Si può, invece, verificare l'effettiva applicazione dell'indirizzo IP tramite i comandi ifconfig o ip addr
Ora, si può verificare se la macchina è raggiungibile tramite comando *ping*
Una volta modificato il file di configurazione per FTP si può verificare l'effettiva funzionalità provando a connettersi tramite *filezilla* o altri programmi che supportano FTP alla macchina virtuale
