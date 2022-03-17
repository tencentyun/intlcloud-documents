## Introdução
Este artigo descreve como configurar um ambiente Java Web em um CVM Linux.

Isso requer que você esteja familiarizado com os comandos comuns do Linux, como [Instalação do software via YUM em um ambiente CentOS](https://intl.cloud.tencent.com/document/product/213/2046), e compreenda as versões do software instalado.

## Software
Estes são os softwares envolvidos:
- O CentOS é uma distribuição do sistema operacional Linux. Usamos o CentOS 7.6 neste artigo.
- O Apache Tomcat fornece um ambiente de servidor da web HTTP "Java puro" no qual o código Java pode ser executado. Usamos Apache Tomcat 8.5.47.
- JDK, ou Java Development Kit, é uma implementação da Java Platform. Usamos JDK 1.8.0_221 neste artigo.


## Pré-requisitos
A configuração de um ambiente Java Web requer um CVM Linux. Se você ainda não comprou um, consulte [Introdução aos CVMs Linux](http://intl.cloud.tencent.com/document/product/213/2936).

## Instruções
### Etapa 1: login em uma instância do Linux
- [Faça login em uma instância do Linux usando WebShell (recomendado)](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode usar outros métodos de login com os quais se sinta confortável:
- [Faça login em uma instância do Linux usando software de login remoto](https://intl.cloud.tencent.com/document/product/213/32502).
- [Faça login em uma instância do Linux usando SSH](https://intl.cloud.tencent.com/document/product/213/32501)


### Etapa 2: Instalação do JDK
1. Faça download do arquivo de instalação do JDK. Acesse a [página de download do Java SE](https://www.oracle.com/technetwork/java/javase/downloads/index.html) para selecionar uma versão e fazer o download.
> Baixe o arquivo JDK, salve-o localmente e envie-o ao seu CVM. Caso contrário, descompactar o arquivo resultará em erros.
> - Se você estiver usando o Windows, use [WinSCP](https://intl.cloud.tencent.com/document/product/213/2131) para fazer upload do arquivo.
> - Se você estiver usando MacOS ou Linux, use [SCP](https://intl.cloud.tencent.com/document/product/213/2133) para fazer upload do arquivo.
>
2. Execute o seguinte comando para criar um diretório para a instalação do JDK.
```
mkdir /usr/java
```
3. Execute o seguinte comando para descompactar o JDK para o diretório.
```
tar xzf jdk-8u221-linux-x64.tar.gz -C /usr/java
```
4. Execute o seguinte comando para abrir o `profile`.
```
vim /etc/profile
```
5. Pressione **i** para entrar no modo de edição. Inicie uma nova linha após `export PATH USER ...` e adicione o seguinte:
```
export JAVA_HOME=/usr/java/jdk1.8.0_221 (substitua 1.8.0_221 pelo número da sua versão JDK)
export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
export PATH=$JAVA_HOME/bin:$PATH
```
O resultado deve ser o seguinte:
![](https://main.qcloudimg.com/raw/a4d0466eca6c4c0ef219f571b7d165de.png)
6. Pressione **Esc** e insira **: wq** para salvar o arquivo e voltar.
7. Execute o seguinte comando para ler as variáveis ​​de ambiente do sistema.
```
source /etc/profile
```
8. Execute o seguinte comando para verificar se o JDK foi instalado corretamente.
```
java -version
```
Se a página a seguir for exibida, a instalação foi bem-sucedida.
![](https://main.qcloudimg.com/raw/f12cfeed5d8aa15cccb9836637e9555f.png)

### Etapa 3: Instalação do Tomcat
1. Execute o comando a seguir para fazer download dos códigos-fonte do Tomcat. Selecione uma versão que lhe atenda.
> Consulte o [site oficial do Apache Tomcat](https://tomcat.apache.org/) para mais informações.
>
```
wget http://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v8.5.47/bin/apache-tomcat-8.5.47.tar.gz
```
2. Execute o seguinte comando para descompactar o arquivo.
```
tar xzf apache-tomcat-8.5.47.tar.gz
```
3. Execute o seguinte comando para mover o diretório que contém o Tomcat para `/usr/local/tomcat/`.
```
mv apache-tomcat-8.5.47 /usr/local/tomcat/
```
4. Execute o seguinte comando para abrir `server.xml`.
```
vim /usr/local/tomcat/conf/server.xml
```
5. Encontre `<Host … appBase="webapps”>` e pressione **i** para entrar no modo de edição. Substitua `appBase="webapps"` pelo seguinte:
```
appBase="/usr/local/tomcat/webapps"
```
6. Pressione **Esc** e insira **: wq** para salvar o arquivo e voltar.
7. Execute o seguinte comando para criar um arquivo com o nome `setenv.sh`.
```
vi /usr/local/tomcat/bin/setenv.sh
```
8. Pressione **Enter** para entrar no modo de edição e insira o que segue para definir as variáveis de memória do JVM.
```
JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8' 
```
9. Pressione **Esc** e insira **: wq** para salvar o arquivo e voltar.
10. Execute o seguinte comando para iniciar o Tomcat.
```
/usr/local/tomcat/bin/startup.sh
```
Se aparecer o que segue, a instalação foi iniciada com sucesso.
![](https://main.qcloudimg.com/raw/64bdd25e734db46464655f15acae4c2f.png)

## Verificação da configuração do ambiente.
1. Execute o seguinte comando para criar um arquivo de teste.
```
echo Hello World! > /usr/local/tomcat/webapps/ROOT/index.jsp
```
2. Abra uma janela do navegador em sua máquina local e visite a seguinte URL para verificar se a configuração do ambiente foi bem-sucedida.
```
http://[endereço IP público da instância CVM]:8080
```
Se os resultados a seguir forem exibidos, a configuração do ambiente foi bem-sucedida.
![](https://main.qcloudimg.com/raw/359b7119e9e7d81e2e2728dabd57456a.png)

## Perguntas frequentes
Se você encontrar um problema ao usar o CVM, consulte os seguintes documentos para solucionar problemas com base em sua situação real.
- Para questões sobre o login do CVM, consulte [Login com senha e login com chave SSH](https://intl.cloud.tencent.com/document/product/213/18120) e [Login e acesso remoto](https://intl.cloud.tencent.com/document/product/213/17278).
- Para questões sobre a rede CVM, consulte [Endereços IP](https://intl.cloud.tencent.com/document/product/213/17285) e [Portas e grupos de segurança](https://intl.cloud.tencent.com/document/product/213/2502).
- Para problemas sobre discos CVM, consulte [Discos de sistema e dados](https://intl.cloud.tencent.com/document/product/213/17351).
