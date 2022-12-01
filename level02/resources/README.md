# Level02

On trouve un fichier <code>level02.pcap</code> qu'il faut extraire de la vm pour l'analyser.

Depuis la machine hôte :

```bash
$ scp -P 4242 -r level02@ip_vm:/home/user/level02/level02.pcap .
chmod 444 level02.pcap
```

On ouvre ensuite le pcap dans <code>WireShark</code>, on selectionne le premier paquets puis : Analyze / Follow / TCP Stream

Ce qui nous permet de trouver :

<code>Password: ft_wandr...NDRel.L0L</code>

En visualisant la donnée en Hex Code on peut voir que les points représentent en fait le caractère non imprimable <code><7F></code> soit <code>DEL</code>

```bash
000000B9  66                                                 f
000000BA  74                                                 t
000000BB  5f                                                 _
000000BC  77                                                 w
000000BD  61                                                 a
000000BE  6e                                                 n
000000BF  64                                                 d
000000C0  72                                                 r
000000C1  7f                                                 .
000000C2  7f                                                 .
000000C3  7f                                                 .
000000C4  4e                                                 N
000000C5  44                                                 D
000000C6  52                                                 R
000000C7  65                                                 e
000000C8  6c                                                 l
000000C9  7f                                                 .
000000CA  4c                                                 L
000000CB  30                                                 0
000000CC  4c                                                 L
000000CD  0d                                                 .
```

Le mot de passe pour flag02 est donc :

<code>ft_waNDReL0L</code>

```shell
$ su flag02
Password: ft_waNDReL0L
Don't forget to launch getflag !
$ getflag
Check flag.Here is your token : kooda2puivaav1idi4f57q8iq
```
