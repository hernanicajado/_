#PHP
Alguns recursos

* [PHP - The Right Way](http://www.phptherightway.com/) - leitura indispensável
* [fnlist](http://php.fnlist.com) - permite a execução "on the fly" de algumas das funções que se podem tornar chatas de fazer debug
* [fnlist](http://php.fnlist.com) - permite a execução "on the fly" de algumas das funções que se podem tornar chatas de fazer debug

##Shell interativa PHP
Em windows a shel interativa do php.exe não funciona / ou funciona mal.
A aplicação __psysh__ resolve o problema. Mandatório!

## self vs static
Ver este artigo:
* [stackoverflow](http://stackoverflow.com/questions/5197300/new-self-vs-new-static)

##is_null empty?
verifica null com === null

* [types comparisons](http://php.net/manual/en/types.comparisons.php)
* [http://stackoverflow.com/questions/8236354/php-is-null-or-empty](http://stackoverflow.com/questions/8236354/php-is-null-or-empty)

##anonimous functions
[php.net](http://php.net/manual/en/functions.anonymous.php#114546)

##OOP visibility
* `public` scope to make that variable/function available from anywhere, other classes and instances of the object.
* `private` scope when you want your variable/function to be visible in its own class only.
* `protected` scope when you want to make your variable/function visible in all classes that extend current class including the parent class.


##Phar on windows
* [http://stackoverflow.com/questions/19413669/windows-8-phar-files-how-do-you-want-to-open](http://stackoverflow.com/questions/19413669/windows-8-phar-files-how-do-you-want-to-open)
<br>a ideia é construir um .phar para o codeception e assim poder correr isto

* outra coisa que parece interessante é o [Robo](http://robo.li/)
