# Level01

On cherche a regarder si l’on peut trouver des informations dans le fichier <code>/etc/passwd</code>

<pre>$ cat /etc/passwd
***
flag00:x:3000:3000::/home/flag/flag00:/bin/bash
flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash
flag02:x:3002:3002::/home/flag/flag02:/bin/bash
***</pre>

On observe que <code>flag01:42hDRfypTqqnw</code> est en clair

## Depuis la machine hôte

On install <code>John The Ripper</code>

On enregistre le mot de passe précédemment trouvé

<pre>$ echo "flag01:42hDRfypTqqnw" > passwd</pre>

On lance john sur le fichier passwd pour le décrypter

<pre>$ ./john passwd --show
flag01:abcdefg</pre>

On a plus qu'a essayer

<pre>$ su flag01
Password:
Don't forget to launch getflag !
$ getflag
Check flag.Here is your token : f2av5il02puano7naaf6adaaf
</pre>

https://www.openwall.com/john/
