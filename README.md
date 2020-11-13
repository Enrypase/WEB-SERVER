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
