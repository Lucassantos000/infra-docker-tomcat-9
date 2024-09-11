# Matriz Online

Projeto de infraestrutura para a aplicação [Matriz Online - PROGRAD/UEA](prograd.uea.edu.br/matrizonline)


<details>

<summary>Configurar o Banco de Dados</summary>

## Configuração do Mysql  

### Conceder Privilégios para acesso ao banco  

1. Acessar o arquivo ```my.cnf``` em ```/etc/mysql/my.cnf```  

```bash
nano etc/mysql/my.cnf
```  
2. Adicionar trecho de código no arquivo
No arquivo **my.cnf** adicione esta linha  

```bash
[mysqld]
bind-address = 0.0.0.0
```  


</details>

<details>

<summary>Configurar o Tomcat</summary>


## Configuração tomcat
Estas são as configurações necessárias para acessar a área de adminstrador do tomcat e subir novas aplicações
<br>

### Mover aas interfaces padrão do tomcat  para webapps

Após esta alteração é possível visualizar a página inical do tomcat (onde mostra a versão e outra informações sobre o servidor).

0. Acesse o **container do tomcat**

```bash
    docker exec -it tomcat /bin/bash
```

1. Ir para o diretório do **tomcat**

```bash
cd /usr/local/tomcat
```

2. Copiar as pastas de webapps.dist para webapps

```bash
cp -r -f webapps.dist/* webapps/    
```  
<br>

### Dar permissão para acessar a área de manager (interface web)

1. Entrar no arquivo /webapps/manager/META-INF/context.xml

```bash
nano /usr/local/tomcat/webapps/manager/META-INF/context.xml
```

2. Altere o tracho:
```xml
de:

<Context antiResourceLocking="false" privileged="true" >
    <Valve className="org.apache.catalina.valves.RemoteAddrValve"
         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
</Context>

para:
<Context antiResourceLocking="false" privileged="true" >
    <!--
    <Valve className="org.apache.catalina.valves.RemoteAddrValve"
         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
    -->
</Context>

```
<br>

### Criar usuário para acessar a área de manager

Dentro da pasta ```/usr/local/webapps/```*(diretório mapeado no docker-compose.yml)* tem o arquivo **tomcat-users.xml** . É preciso sobrepor o arquivo default criado pelo tomcat (```bash /usr/locaç/tomcat/conf/tomcat-users.xml```), por este, que já configura um nome e senha para o usuário adminstrador.


1 Vá para o **diretório** do **configuração do tomcat** 
```bash
   cd /usr/local/tomcat/conf/ 
```  
2 Copie o arquivo mapeado ```tomcat-users.xml``` para o diretório ``` /usr/local/tomcat/conf/ ```usando a flag ```-f``` para força a sobreposição   
```bash
   cp  -f /usr/local/webapps/tomcat-users.xml . 
``` 




</details>


## Tópicos Adicionais:

- [Aumentar o tamanho máximo de um arquivo para deploy ](aumentarTamanhoServidorParaDeploy.md)