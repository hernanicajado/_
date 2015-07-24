#Yii2
Este documento contém uma compilação de diferentes recursos na implementação da framework Yii2.
##Lembretes, links e afins

[Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
[GitHub Guide](https://help.github.com/articles/markdown-basics/)

##Configuração da base de dados
Configuração do componente `Connection` para operar com bases de Dados __SQL SERVER__.

```
return [
    'class'               => 'yii\db\Connection',
    'dsn'                 => 'sqlsrv:Server=130.185.84.150\SQL2012,60055;Database=dbname;MultipleActiveResultSets=false',
    'username'            => 'username',
    'password'            => 'password',
    'charset'             => 'utf8',
    'schemaMap'           => [
        'sqlsrv' => [
            'class'         => 'yii\db\mssql\Schema',
            'defaultSchema' => 'towertex_userdb'
        ], // newer MSSQL driver on MS Windows hosts
    ],
    'enableSchemaCache'   => true,
    'schemaCacheDuration' => 3600,
    'schemaCache'         => 'cache',
];
```
___
[referencia](http://www.techonthenet.com/sql_server/index.php)

###limitações
Não é possível usar batches e iteradores, ou não estou a configurar bem ou não sei...

####defaultSchema
[Yii issues](https://github.com/yiisoft/yii2/issues/5630/)

Em runtime para aceder ao defaultSchema:
`$this->getDb()->getSchema()->defaultSchema;`

####MARS transactions
[Yii issues](https://github.com/yiisoft/yii/issues/112/)

#DI
* http://www.yiiframework.com/doc-2.0/guide-concept-di-container.html#practical-usage

##ActiveRecord
* [http://www.sitepoint.com/yii-2-0-activerecord-explained/](http://www.sitepoint.com/yii-2-0-activerecord-explained/)

###Procura em modelos relacionados
[StackOverflow](http://stackoverflow.com/questions/21992687/php-yii2-gridview-filtering-on-relational-value)
<br>
[Yii wiki](http://www.yiiframework.com/wiki/780/drills-search-by-a-has_many-relation-in-yii-2-0/)

###Múltiplas instâncias de um modelo
* Deu jeito na implementação dos modelos `*Array`
* [http://stackoverflow.com/questions/24837476/yii2-multiple-instances-of-the-same-model](http://stackoverflow.com/questions/24837476/yii2-multiple-instances-of-the-same-model)
* [http://www.yiiframework.com/forum/index.php/topic/53935-solved-subforms/page__p__248184#entry248184](http://www.yiiframework.com/forum/index.php/topic/53935-solved-subforms/page__p__248184#entry248184)


###behaviors, scenarios & rules
* [http://www.bsourcecode.com/yiiframework2/yii2-0-scenarios/](http://www.bsourcecode.com/yiiframework2/yii2-0-scenarios/)
O modelo Store tem a aplicação de rules de um defaultValue:
`[['nvc_codigo_interno'], 'default', 'value' => new \yii\db\Expression('NEWID()')]`


##Application
###Events
[widecodes](http://www.widecodes.com/CmVkUXjqVe/yii2-session-event-before-closedestroy.html)

estes eventos "disparam" a nível global:

```Yii::$app->on(User::EVENT_AFTER_LOGIN, [$this, 'login'], null, false);
Yii::$app->on(User::EVENT_AFTER_LOGOUT, [$this, 'logout'], null, false);```
terão de ser disparados a nível global
`Yii::$app->trigger(EVENT, ...);`


##Views
###GridView
[Yii wiki](http://www.yiiframework.com/wiki/621/filter-sort-by-calculated-related-fields-in-gridview-yii-2-0/)

###FormBuilder
A flag `staticOnly` deve ser configurada no `ActiveForm`.<br>

###Interface
####Flashes
```
SimpleHelper::setFlash('Bem-vindo de volta', 'Bem-vindo', 'fa-circle', 'success');
```

Podem encadear-se Flashes, mas apenas se forem de categorias diferentes. as categorias disponíveis são: `success, warning, info, error, danger`.

##pJax & AJAX

[neatTutorias](http://blog.neattutorials.com/yii2-pjax-tutorial/)

[yii2playground](http://www.yiiplayground.com/yii2/web/index.php?r=ajax/index)

[widecodes](http://www.widecodes.com/CSVVkqkPgg/yii2-active-form-please-wait-message-while-submitting-with-ajax.html)

[zero-exception](http://zero-exception.blogspot.pt/search/label/Yii2)

Dentro de uma zona pJax todos os links são automáticamente capturados pela biblioteca. Para evitar este comportamento a 
propriedade do link ou submissão deve ser acompanhada do atributo HTML5 ` data-pjax=0 `. 


##Mailer (SwiftMailer)
[config at stackoverflow](http://stackoverflow.com/questions/29592790/yii2-swiftmailer-sending-email-via-remote-smtp-server-gmail)


___

##Imagens
Tirado do guide

> Limitations

> Query caching does not work with query results that contain resource handlers. For example, when using the BLOB column type in some DBMS, the query result will return a resource handler for the column data.

> Some caching storage has size limitation. For example, memcache limits the maximum size of each entry to be 1MB. Therefore, if the size of a query result exceeds this limit, the caching will fail.

___


Artigo que dá dicas sobre como converter um campo binario para base64 que pode ser incluído diretamente no HTML
[Techerator](http://www.techerator.com/2011/12/how-to-embed-images-directly-into-your-html/)

As imagens estão guardadas na base de dados em hexadecimal. Para se poderem visualizar deve chamar-se a função `hex2bin`.

####updload
[behaviour](http://yiidreamteam.com/yii2/upload-behavior)
[wiki](http://www.yiiframework.com/wiki/757/how-to-use-imagine-crop-thumb-effects-for-images-on-yii2/)
[MS](https://msdn.microsoft.com/en-us/library/ff628157%28v=sql.90%29.aspx)

            //http://www.phpeveryday.com/articles/PDO-Insert-and-Update-Statement-Use-Prepared-Statement-P553.html
            //https://go4answers.webhost4life.com/Example/bindvalue-problem-scandinavian-105479.aspx


A gravação de um campo binário (imagem) na base de dados é problemática.
    1. o modo de comunicação do PDO tem de ser forçado ao mesmo bitstream.
    2. os campos nvarbin precisam de um cast EXPLÍCITO `INSERT INTO towertex_userdb.imagem_produto (imagem,thumbnail) VALUES(CAST (:pdo2 as varbinary(max)),CAST (:pdo3 as varbinary(max))`
    3. No contexto de ActiveRecord é necessário guardar o id na instância manualmente. [php](http://php.net/manual/en/pdo.lastinsertid.php)


    
####Crop
https://yiigist.com/package/bupy7/yii2-widget-cropbox/?#?tab=readme

http://sjaakpriester.nl/software/illustrated


###FileSystem
https://github.com/creocoder/yii2-flysystem
