# Level09

On observe deux fichiers a la racine: un exécutable <code>level09</code> et un fichier <code>token</code>

<pre>$ cat token
f4kmm6p|=�p�n��DB�Du{��</pre>

On fait quelque teste sur l'executable

<pre>$ ./level09
You need to provied only one arg.

$ ./level09 "Hello World"
Hfnos%]vzun

$ ./level09 0000000000
0123456789</pre>

On suppose donc que <code>token</code> est le resultat du mot de passe du flag apres etre passé dans cette éxécutable.

On va donc creer un programme qui va décrypter le contenu du fichier <code>token</code>

## Depuis la machine hôte

On copie le fichier <code>token</code>

<pre>scp -P 4242 -r level09@192.168.56.101:/home/user/level09/token</pre>

On crée un fichier <code>level09.py</code> qui decrypte dans la meme logique que l'executable <code>level09</code>

<pre>$ cat level09.py
#!/usr/bin/python

import sys

string = sys.argv[1].encode('utf-8', 'surrogateescape').decode('ISO-8859-1')
for i, char in enumerate(string):
	print(chr(ord(char) - i), end="")
print()
</pre>

On lance, ensuite, notre programme de decryptage sur le contenu du fichier <code>token</code>

<pre>$ python level09.py `cat token`
f3iji1ju5yuevaus41q1afiuq</pre>

On essaye verifie notre resultat

<pre>$ su flag09
Password:
Don't forget to launch getflag !

$ getflag
Check flag.Here is your token : s5cAJpM8ev6XHw998pRWG728z
</pre>
