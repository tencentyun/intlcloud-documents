## Visão geral
O RabbitMQ é um agente de mensagens de código aberto baseado no Advanced Message Queuing Protocol (AMQP). Ele apresenta usabilidade, escalabilidade e alta disponibilidade com um servidor programado em Erlang e oferece suporte a vários clientes, incluindo Python, Ruby, .NET, Java, JMS, C, PHP, ActionScript, XMPP, STOMP e AJAX. Este documento descreve como implementar o RabbitMQ no Tencent Cloud CVM.

## Software
Este documento usa o seguinte software como exemplo para implementar o RabbitMQ:
- Linux: Sistema operacional Linux. Este documento usa a versão CentOS 7.7 como exemplo.
- RabbitMQ Server: agente de mensagens de código aberto. Este documento usa o RabbitMQ Server 3.6.9 como exemplo.
- Erlang: linguagem de programação. Este documento usa Erlang 19.3 como exemplo.


## Pré-requisitos
- Um CVM Linux é necessário para implementar o RabbitMQ. Se você ainda não comprou um CVM Linux, consulte [Personalização das configurações do CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517).
- As regras do grupo de segurança para a instância do Linux já foram configuradas. Abrir as portas 80, 5672 e 15672. Para obter mais informações, consulte [Adicionar regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272).

## Instruções
### Instalação do Erlang
1. [Fazer login em uma instância do Linux usando o método de login padrão](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode usar outros métodos de login com os quais se sinta mais confortável:
	- [Fazer login em instâncias do Linux por meio de ferramentas de login remoto](https://intl.cloud.tencent.com/document/product/213/32502)
	- [Fazer login nas instâncias do Linux via chave SSH](https://intl.cloud.tencent.com/document/product/213/32501)
1. Execute o seguinte comando para instalar dependências.
```
yum -y install make gcc gcc-c++ m4 ncurses-devel openssl-devel unixODBC-devel
```
2. Execute o seguinte comando para fazer download do pacote de instalação Erlang.
```
wget http://erlang.org/download/otp_src_19.3.tar.gz
```
3. Execute o seguinte comando para descompactar o pacote de instalação Erlang.
```
tar xzf otp_src_19.3.tar.gz
```
4. Execute o seguinte comando para criar a pasta erlang.
```
mkdir /usr/local/erlang
```
5. Execute os seguintes comandos em sequência para compilar e instalar o Erlang.
```
cd otp_src_19.3
```
```
./configure --prefix=/usr/local/erlang --without-javac
```
```
make && make install
```
6. Execute o seguinte comando para abrir o arquivo de configuração do perfil.
```
vi /etc/profile
```
7. Pressione **i** para entrar no modo de edição e anexe o seguinte no final do arquivo.
```
export PATH=$PATH:/usr/local/erlang/bin
```
8. Pressione **Esc** e digite **:wq** para salvar e fechar o arquivo.

### Instalação do RabbitMQ Server
1. Execute o seguinte comando para fazer download do pacote de instalação do RabbitMQ Server.
```
wget https://github.com/rabbitmq/rabbitmq-server/releases/download/rabbitmq_v3_6_9/rabbitmq-server-3.6.9-1.el7.noarch.rpm
```
Neste exemplo, o RabbitMQ 3.6.9 é utilizado. Se o link de download acima expirou, ou se você deseja usar outras versões do RabbitMQ, vá para [rabbitmq-server](https://github.com/rabbitmq/rabbitmq-server/releases).
10. Execute o seguinte comando para importar a chave de assinatura.
```
rpm --import https://www.rabbitmq.com/rabbitmq-release-signing-key.asc
```
11. Execute os seguintes comandos em sequência para instalar o RabbitMQ Server.
```
cd
```
```
yum install rabbitmq-server-3.6.9-1.el7.noarch.rpm
```
12. Execute os comandos a seguir em sequência para ativar a inicialização automática do RabbitMQ e iniciar o RabbitMQ.
```
systemctl enable rabbitmq-server
```
```
systemctl start rabbitmq-server
```
13. Execute o seguinte comando para excluir a conta de convidado padrão do RabbitMQ.
```
rabbitmqctl delete_user guest
```
14. <span id="Step6"></span>Execute o seguinte comando para criar uma conta.
```
rabbitmqctl add_user Username Password
```
15. Execute o seguinte comando para definir a nova conta como a conta de administrador.
```
rabbitmqctl set_user_tags Username administrator
```
16. Execute o seguinte comando para conceder à conta de administrador todas as permissões.
```
rabbitmqctl set_permissions -p / Username ".*" ".*" ".*"
```


### Verificação da instalação
1. Execute o seguinte comando para abrir a página de gerenciamento da web do RabbitMQ.
```
rabbitmq-plugins enable rabbitmq_management
```
2. Abra um navegador e visite:
```
http://Instance public IP:15672
```
Para mais informações sobre como obter o endereço IP público, consulte [Obtenção de endereços IP públicos](https://intl.cloud.tencent.com/document/product/213/17940).
Se você vir a página a seguir, isso indica que o RabbitMQ foi instalado com sucesso.
![](https://main.qcloudimg.com/raw/aacb15db11b5cf80dd6b7ba1dc80d331.png)
3. Faça login no RabbitMQ com a conta de administrador criada na [Etapa 6](#Step6) e acesse a página de gerenciamento do RabbitMQ, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/7f8d24062541be6ba8b271483343b20a.png)
