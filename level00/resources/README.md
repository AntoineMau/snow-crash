On cherche les fichier de l'user flag00 auquels on a accès :

<pre><code>$ find / -user flag00 -print 2>/dev/null
/usr/sbin/john
/rofs/usr/sbin/john</code></pre>

Ces deux fichiers sont identiques

<pre><code>$ cat /usr/sbin/john
cdiiddwpgswtgt</code></pre>

Ce mot de passe ne fonctionne pas avec flag00, il est sans doute chiffré. Il s'agit d'un rot15 qui après déchiffrement donne :

<code>nottoohardhere</code>

<pre>
<code>$ su flag00
Password: nottoohardhere
$ getflag
Check flag.Here is your token : x24ti5gi3x0ol2eh4esiuxias</code>
</pre>
