# Level00

On cherche les fichier de l'user <code>flag00</code> auquels on a accès :

<pre>$ find / -user flag00 -print 2>/dev/null
/usr/sbin/john
/rofs/usr/sbin/john</pre>

Ces deux fichiers sont identiques

<pre>$ cat /usr/sbin/john
cdiiddwpgswtgt</pre>

Ce mot de passe ne fonctionne pas pour <code>flag00</code>, il est sans doute chiffré. Il s'agit d'un <code>rot15</code> qui après déchiffrement donne :

<code>nottoohardhere</code>

<pre>
$ su flag00
Password: nottoohardhere
Don't forget to launch getflag !
$ getflag
Check flag.Here is your token : x24ti5gi3x0ol2eh4esiuxias
</pre>

https://www.dcode.fr/chiffre-rot
