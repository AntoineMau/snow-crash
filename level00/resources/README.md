# Level00

On cherche les fichier de l'user <code>flag00</code> auquels on a accès :

```bash
$ find / -user flag00 -print 2>/dev/null
/usr/sbin/john
/rofs/usr/sbin/john
```

Ces deux fichiers sont identiques

```bash
$ cat /usr/sbin/john
cdiiddwpgswtgt
```

Ce mot de passe ne fonctionne pas pour <code>flag00</code>, il est sans doute chiffré. Il s'agit d'un <code>rot15</code> qui après déchiffrement donne :

<code>nottoohardhere</code>

```shell
$ su flag00
Password: nottoohardhere
Don't forget to launch getflag !
$ getflag
Check flag.Here is your token : x24ti5gi3x0ol2eh4esiuxias
```

`https://www.dcode.fr/chiffre-rot`
