## Visão geral
O YUM (Yellowdog Updater, Modified) permite que você baixe e instale software facilmente e simplifica suas instalações em uma instância do CVM, economizando tempo e esforços. Com ele, basta executar o comando `yum` para instalar o software no ambiente CentOS. O Tencent Cloud fornece um repositório YUM para que você possa instalar diretamente os pacotes de software sem adicionar fontes.

## Instruções

### Instalação de software
Faça login na instância do CVM com a conta raiz e execute os comandos a seguir para instalar o software de acordo com o sistema operacional do CVM.

#### CentOS 8 ou versões posteriores
1. Execute o comando a seguir para instalar o software.
```
dnf install [nome de software]
```
O sistema procurará automaticamente o pacote de software relevante e as dependências e pedirá sua confirmação.
Por exemplo, após executar o comando `dnf install php` para instalar o PHP, o seguinte prompt será exibido:
![](https://main.qcloudimg.com/raw/ab6cdf18a685debff13c8f978b38d43f.png)
2. Confirme se o pacote de software está correto. Digite `y` e pressione **Enter** para iniciar a instalação.
O prompt `Complete` indica que a instalação foi concluída.

#### CentOS 7 ou versões anteriores
1. Execute o comando a seguir para instalar o software.
>! A partir do CentOS 7, o MariaDB se tornou o banco de dados padrão no repositório YUM. Se você estiver usando o CentOS 7 ou versões posteriores, o MySQL instalado usando `yum` ficará inutilizável. Você pode usar o MariaDB com compatibilidade total ou [clicar aqui](https://www.linode.com/docs/databases/mysql/how-to-install-mysql-on-centos-7) para verificar como instalar uma versão anterior do MySQL.
>
```
yum install [nome de software]
``` 
O sistema procurará automaticamente o pacote de software relevante e as dependências e pedirá sua confirmação.
Por exemplo, depois de executar o comando `yum install PHP` para instalar o PHP, o seguinte prompt será exibido:
![](https://main.qcloudimg.com/raw/18c4a59a3e0e92b0dcafff662d1e3673.png)
2. Confirme se o pacote de software está correto. Digite `y` e pressione **Enter** para iniciar a instalação.
O prompt `Complete` indica que a instalação foi concluída.

### Exibição de informações do software instalado

Após a conclusão da instalação do software, você pode executar diferentes comandos para exibir as informações relacionadas.
- Exibir o diretório de instalação de um pacote de software
```
rpm -ql [nome de software]
```
Por exemplo, execute `rpm -ql php` para exibir o diretório de instalação do PHP, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/fda98060c9f6ba359d7e705de8d336bb.png)
- Exibir a versão do pacote de software
```
rpm -q
```
Por exemplo, execute `rpm -q php` para exibir a versão do PHP, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/35e1ecee46bc55a5d2510dce59360ecc.png)

