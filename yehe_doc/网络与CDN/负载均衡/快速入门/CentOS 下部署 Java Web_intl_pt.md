Este documento descreve como implementar projetos Java Web no CentOS e é adequado para novos usuários individuais do Tencent Cloud.
## Versão de software
As versões das ferramentas de software usadas neste documento seguem indicadas abaixo e podem ser diferentes das versões que você utilizará ao executar as operações.
- Sistema operacional: CentOS 7.5
- Tomcat: apache-tomcat-8.5.39
- JDK: JDK 1.8.0_201

## Instalação do JDK
Depois de comprar o CVM, você pode clicar em **Login** na página de detalhes do CVM para fazer login na instância do CVM e inserir seu nome de usuário e senha para configurar o ambiente Java web. Para obter mais informações sobre como criar uma instância do CVM, consulte [CVM - Criação de instância](https://intl.cloud.tencent.com/document/product/213/4855).

### Fazer download do JDK
Insira o seguinte comando:
```
mkdir /usr/java  # Criar uma pasta `java`
cd /usr/java     # Acessar a pasta `java`
```
<pre>
<code># Fazer upload do pacote de instalação do JDK (recomendado)
Recomenda-se usar ferramentas como <a href="https://winscp.net/eng/docs/lang:chs" target="_blank">WinSCP</a> para fazer upload do pacote de instalação do JDK para a pasta `java` acima e então descompactá-lo.
Ou
# Usar um comando (recomenda-se fazer upload do pacote de instalação): execute `wget` para fazer o download do pacote, que não pode ser descompactado porque um pacote baixado rejeita a licença Oracle BSD por padrão. Acesse https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html para aceitar o contrato de licença e obter o link de download com seus cookies.
wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-linux-x64.tar.gz</code>
</pre>
```
# Descompactar
chmod +x jdk-8u201-linux-x64.tar.gz
tar -xzvf jdk-8u201-linux-x64.tar.gz
```

### Configuração da variável ambiental
1. Abra o arquivo `/etc/profile`.
```
vi /etc/profile
```
2. Pressione I para entrar no modo de edição e adicionar as seguintes informações ao arquivo.
```
# definir ambiente java
export JAVA_HOME=/usr/java/jdk1.8.0_201
export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
export PATH=$JAVA_HOME/bin:$PATH
```
3. Pressione Esc para sair do modo de edição e digite `:wq` para salvar e fechar o arquivo.
4. Carregue a variável ambiental.
```
source /etc/profile
```

### Visualização do resultado da instalação do JDK
Execute o comando `java -version`. Se as informações da versão do JDK forem exibidas, o JDK foi instalado com êxito.
![](https://main.qcloudimg.com/raw/6d3531f4d466e5428885ec38a3542c2e.png)

## Instalação do Tomcat
### Fazer download do Tomcat
Insira os seguintes comandos:
```
# O endereço do espelho pode mudar e a versão do Tomcat pode ser continuamente atualizada. Caso o link de download tenha expirado, vá para [site oficial do Tomcat](https://tomcat.apache.org/download-80.cgi) e selecione um endereço de pacote de instalação apropriado.
wget http://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v8.5.39/bin/apache-tomcat-8.5.39.tar.gz
tar -xzvf apache-tomcat-8.5.39.tar.gz
mv apache-tomcat-8.5.39 /usr/local/tomcat/
```
Os arquivos a seguir estão no diretório `/usr/local/tomcat/`:
- bin: arquivo de script, que contém scripts para iniciar e interromper o serviço Tomcat.
- conf: arquivos de configuração global, dos quais os mais importantes são `server.xml` e `web.xml`.
- webapps: o principal diretório de lançamento da web no Tomcat, que é o diretório padrão para armazenar arquivos de aplicativos da web.
- logs: arquivos de log do Tomcat.

>!Se o link de download tiver expirado, substitua-o pelo link mais recente no [site oficial do Tomcat](https://tomcat.apache.org/download-80.cgi).

### Adicionar usuário
```
# Adicione um usuário geral `www` para executar o Tomcat
useradd www
# Crie um diretório raiz do site
mkdir -p /data/wwwroot/default
# Carregue o arquivo de projeto Java web (pacote WAR) para o diretório raiz do site e modifique a permissão do arquivo no diretório para `www`. Este exemplo mostra como criar uma página de teste do Tomcat no diretório raiz do site:
echo Hello Tomcat! > /data/wwwroot/default/index.jsp
chown -R www.www /data/wwwroot
```

### Configuração do parâmetro de memória JVM
1. Crie um arquivo de script `/usr/local/tomcat/bin/setenv.sh`.
```
vi /usr/local/tomcat/bin/setenv.sh
```
2. Pressione I para entrar no modo de edição e inclua o seguinte:
```
JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8'
```
3. Pressione Esc para sair do modo de edição e digite `:wq` para salvar e sair.

### Configuração do server.xml
1. Mude para o diretório `/usr/local/tomcat/conf/`.
```
cd /usr/local/tomcat/conf/
```
2. Faça backup do arquivo `server.xml`.
```
mv server.xml server_default.xml
```
3. Crie um novo arquivo `server.xml`.
```
vi server.xml
```
4. Pressione I para entrar no modo de edição e inclua o seguinte:
```
<?xml version="1.0" encoding="UTF-8"?>
<Server port="8006" shutdown="SHUTDOWN">
<Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener"/>
<Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener"/>
<Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener"/>
<Listener className="org.apache.catalina.core.AprLifecycleListener"/>
<GlobalNamingResources>
<Resource name="UserDatabase" auth="Container"
 type="org.apache.catalina.UserDatabase"
 description="User database that can be updated and saved"
 factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
 pathname="conf/tomcat-users.xml"/>
</GlobalNamingResources>
<Service name="Catalina">
<Connector port="8080"
 protocol="HTTP/1.1"
 connectionTimeout="20000"
 redirectPort="8443"
 maxThreads="1000"
 minSpareThreads="20"
 acceptCount="1000"
 maxHttpHeaderSize="65536"
 debug="0"
 disableUploadTimeout="true"
 useBodyEncodingForURI="true"
 enableLookups="false"
 URIEncoding="UTF-8"/>
<Engine name="Catalina" defaultHost="localhost">
<Realm className="org.apache.catalina.realm.LockOutRealm">
<Realm className="org.apache.catalina.realm.UserDatabaseRealm"
  resourceName="UserDatabase"/>
</Realm>
<Host name="localhost" appBase="/data/wwwroot/default" unpackWARs="true" autoDeploy="true">
<Context path="" docBase="/data/wwwroot/default" debug="0" reloadable="false" crossContext="true"/>
<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
prefix="localhost_access_log." suffix=".txt" pattern="%h %l %u %t &quot;%r&quot; %s %b" />
</Host>
</Engine>
</Service>
</Server>
```
5. Pressione Esc para sair do modo de edição e digite `:wq` para salvar e sair.

## Iniciar o Tomcat
### Método 1
Entre no diretório `bin` do servidor Tomcat e execute o comando `./startup.sh` para iniciar o servidor Tomcat.
```
cd /usr/local/tomcat/bin
./startup.sh
```
O resultado da execução é o seguinte:
![](https://main.qcloudimg.com/raw/c118899986968ecd5982eb8cdb2beff9.png)
### Método 2
1. Configure o início rápido, para que o servidor Tomcat possa ser iniciado em qualquer lugar usando `service tomcat start`.
```
wget https://github.com/lj2007331/oneinstack/raw/master/init.d/Tomcat-init
mv Tomcat-init /etc/init.d/tomcat
chmod +x /etc/init.d/tomcat
```
2. Execute o seguinte comando e defina o script de inicialização `JAVA_HOME`.
```
sed -i 's@^export JAVA_HOME=.*@export JAVA_HOME=/usr/java/jdk1.8.0_201@' /etc/init.d/tomcat
```
3. Definir a execução automática.
```
chkconfig --add tomcat
chkconfig tomcat on
```
4. Iniciar o Tomcat.
```
# Iniciar o Tomcat
service tomcat start
# Visualizar o status do servidor Tomcat
service tomcat status
# Interromper o Tomcat
service tomcat stop
```
O resultado da execução é o seguinte:
![](https://main.qcloudimg.com/raw/78800e85c09820d98a0a15dc2792aaa8.png)
5. Se o sistema avisar que você não tem permissões, mude para o usuário raiz e modifique as permissões.
```
cd /usr/local
chmod -R 777 tomcat
```
6. Digite `http://public IP:port` (caso a porta seja a porta do conector definida em `server.xml`) na barra de endereço do navegador. Se a página a seguir for exibida, a instalação foi bem-sucedida.
![](https://main.qcloudimg.com/raw/a8d7c77aafc94c9bba262c06125b6c18.png)

### Configuração de grupo de segurança
Em caso de falha de acesso, verifique o grupo de segurança. Conforme mostrado no exemplo acima, a porta do conector é 8080 em `server.xml`, então, é preciso abrir TCP:8080 para a internet no grupo de segurança vinculado à instância do CVM correspondente.
![](https://main.qcloudimg.com/raw/6ffabfd2ef027e4fc69e4fc1a85dde9f.png)
