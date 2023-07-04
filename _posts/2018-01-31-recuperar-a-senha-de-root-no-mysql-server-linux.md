---
title: 'Recuperar a senha de root no MySQL Server [Linux]'
date: '2018-01-31T15:27:48-02:00'
status: publish
permalink: /recuperar-a-senha-de-root-no-mysql-server-linux
author: 'Johnny Ferreira'
excerpt: ''
type: post
id: 453
thumbnail: ../uploads/2018/01/recuperar-senha-de-root-no-mysql-server-linux-150x150.png
category:
    - 'Dicas de Linux'
    - Linux
tag:
    - 'mysql senha recuperar'
    - 'recovery mysql password'
    - 'recovery password root mysql'
    - 'recuperar mysql login'
    - 'recuperar senha mysql'
    - 'recuperar senha root mysql'
    - 'redefinir mysql root'
    - 'redefinir senha mysql'
    - 'senha root mysql'
post_format: []
_yoast_wpseo_content_score:
    - '60'
_yoast_wpseo_primary_category:
    - '4'
_yoast_wpseo_focuskw:
    - 'MySQL Server'
_yoast_wpseo_metadesc:
    - 'Veja aqui como redefinir de maneira simples e objetiva a senha do usuário root no MySQL Server, tutorial abordando os sistemas Debian e CentOS.'
_yoast_wpseo_linkdex:
    - '82'
---
Opa, beleza? As vezes temos alguns problemas com a senha do usuário “root” no MySQL Server, ou esquecemos, ou simplesmente precisamos recuperar a senha que foi implementada por outro profissional de TI. Por esse motivo resolvi compartilhar com você esse tutorial.

A primeira coisa a se fazer para recuperar a senha do “root” é parar o serviço do MySQL Server no servidor ou host Linux.

Em ambientes baseados em Debian:

```
<pre class="lang:sh decode:true ">service mysql stop
```

Para CentOS 6:

```
<pre class="lang:sh decode:true">/etc/init.d/mysqld stop
```

Já no CentOS 7 a sintaxe para parar o serviço muda:

```
<pre class="lang:sh decode:true ">systemctl stop mysqld
```

O próximo passo é adicionar um parâmetro ao arquivo de configuração do MySQL, o “my.cnf”:

Em ambientes baseados no Debian, pode ser que o arquivo principal esteja em “/etc/mysql/”

```
<pre class="lang:sh decode:true ">vi /etc/mysql/my.cnf
```

Já no CentOS é direto na estrutura do “/etc”

```
<pre class="lang:sh decode:true">vi /etc/my.cnf
```

Insira a linha abaixo no final do arquivo:

```
<pre class="lang:sh decode:true ">skip-grant-table
```

Em seguida, após salvar o arquivo com o parâmetro acima adicionado, inicie novamente o serviço do MySQL.

Debian:

```
<pre class="lang:sh decode:true">service mysql start
```

CentOS 6:

```
<pre class="lang:sh decode:true">/etc/init.d/mysqld start
```

CentOS 7:

```
<pre class="lang:sh decode:true">systemctl start mysqld
```

Agora vamos logar no console do MySQL, sem o parâmetro “-p” responsável pela autenticação por senha:

```
<pre class="lang:sh decode:true ">mysql -u root
```

Após logar no console do MySQL, execute o processo abaixo para recuperar a senha do “root”.

```
<pre class="lang:mysql decode:true ">mysql> USE mysql;
mysql> UPDATE user set password=PASSWORD('senha') WHERE user='root';
mysql> FLUSH PRIVILEGES;
mysql> quit
```

Agora edite novamente o arquivo “my.cnf” e comente ou exclua a linha com o parâmetro “skip-grant-table”, agora reinicie o serviço do mysql.

Debian:

```
<pre class="lang:sh decode:true">service mysql restart
```

CentOS 6:

```
<pre class="lang:sh decode:true">/etc/init.d/mysqld restart
```

CentOS 7:

```
<pre class="lang:sh decode:true ">systemctl restart mysqld
```

Agora pode logar novamente com o root e a senha que você definiu.

```
<pre class="lang:sh decode:true code bash">mysql -u root -psenha
```

Dúvidas, comentário e sugestões postem nos comentários…  
👋🏼 Valeu! e até a próxima!

- - - - - -

![](http://tidahora.com.br/wp-content/uploads/2017/11/foto-perfil-redondo-johnny.png)

**Johnny Ferreira**  
<johnny.ferreira.santos@gmail.com>  
<http://www.tidahora.com.br>

- - - - - -