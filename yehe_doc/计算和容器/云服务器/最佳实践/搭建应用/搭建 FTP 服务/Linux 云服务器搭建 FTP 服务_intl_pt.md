## Cenário
Very Secure FTP Daemon (Vsftpd) é o servidor FTP padrão para a maioria das distribuições Linux. Este documento usa um CVM CentOS 7.6 de 64 bits como exemplo para descrever como usar o vsftpd para configurar o serviço FTP para um CVM Linux.

## Software
A seguir estão os programas de software para configurar o serviço FTP.
- Linux: Imagem pública CentOS 7.6
- Vsftpd: vsftpd 3.0.2


## Instruções
### Etapa 1: Faça login no CVM
[Faça login em uma instância do Linux usando WebShell (recomendado)](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode usar qualquer um dos métodos de login a seguir com os quais se sinta confortável.
- [Login em uma instância do Linux usando software de login remoto](https://intl.cloud.tencent.com/document/product/213/32502)
- [Faça login em uma instância do Linux usando SSH](https://intl.cloud.tencent.com/document/product/213/32501)

### Etapa 2: Instalar vsftpd
1. Execute o seguinte comando para instalar o vsftpd:
```
yum install -y vsftpd
```
2. Execute o seguinte comando para iniciar automaticamente o vsftpd na inicialização do sistema:
```
systemctl enable vsftpd
```
3. Execute o seguinte comando para iniciar o serviço FTP:
```
systemctl start vsftpd
```
4. Execute o seguinte comando para verificar se o serviço foi iniciado:
```
netstat -antup | grep ftp
```
Se as informações a seguir forem exibidas, o serviço FTP foi iniciado.
![](https://main.qcloudimg.com/raw/2a7abf80253a8469c9340878d89b452a.png)
Por padrão, o vsftpd habilitou o modo de acesso anônimo. É possível fazer login no servidor FTP sem inserir um nome de usuário ou senha. No entanto, você não tem permissão para modificar ou fazer upload de arquivos neste modo de login.

<span id="user"></span>
### Etapa 3: Configurar vsftpd
1. Execute o seguinte comando para criar um usuário para o serviço FTP que, neste caso, é ftpuser:
```
useradd ftpuser
```
2. Execute o seguinte comando para definir uma senha para ftpuser:
```
passwd ftpuser
```
Após inserir a senha, pressione **Enter** para confirmar. Por padrão, a senha não é exibida. Neste caso, a senha usada como exemplo é `tf7295TFY`.
3. Execute o seguinte comando para criar um diretório de arquivo para o serviço FTP que, neste caso, é `/var/ftp/test`:
```
mkdir /var/ftp/test
```
4. Execute o seguinte comando para modificar a permissão do diretório:
```
chown -R ftpuser:ftpuser /var/ftp/test
```
5. Execute o seguinte comando para abrir o arquivo `vsftpd.conf`:
```
vim /etc/vsftpd/vsftpd.conf
```
6. Pressione **i** para alternar para o modo de edição. Selecione um modo FTP com base em suas necessidades reais e modifique o arquivo de configuração `vsftpd.conf`.
<span id="config"></span>
> O servidor FTP pode se conectar ao cliente em modo ativo ou passivo para transmissão de dados. Devido às configurações de firewall da maioria dos clientes e ao fato de que o endereço IP real não pode ser obtido, recomendamos que você use o modo passivo para configurar o serviço FTP. A seguinte modificação usa o modo passivo como exemplo. Para usar o modo ativo, consulte [Configuração do modo FTP ativo](#port).
>
 1. Modifique os parâmetros de configuração a seguir para definir permissões de login para usuários anônimos e locais, defina o caminho para armazenar a lista de usuários excepcionais e habilite a escuta em soquetes IPv4.
```
anonymous_enable=NO
local_enable=YES
chroot_local_user=YES
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd/chroot_list
listen=YES
```
  2. Adicione o sinal de cerquilha (`#`) no início da linha seguinte para anotar `listen_ipv6=YES` e desabilitar a escuta em soquetes IPv6.
```
#listen_ipv6=YES
```
  3. Adicione os seguintes parâmetros de configuração para habilitar o modo passivo, defina o diretório onde os usuários locais residem após o login e defina o intervalo de portas para transmissão de dados pelo CVM.
```
local_root=/var/ftp/test
allow_writeable_chroot=YES
pasv_enable=YES
pasv_address=xxx.xx.xxx.xx # Substituir xxx.xx.xxx.xx pelo endereço IP público do CVM Linux
pasv_min_port=40000
pasv_max_port=45000
```
7. Pressione **Esc** e digite **:wq**. Em seguida, salve as alterações e feche o arquivo.
<span id="create"></span>
8. Execute o seguinte comando para criar e editar o arquivo `chroot_list`:
```
vim /etc/vsftpd/chroot_list
```
9. Pressione **i** para alternar para o modo de edição e digite o nome de usuário. Observe que cada nome de usuário ocupa uma linha. Após terminar a configuração, pressione **Esc** e digite **:wq**. Em seguida, salve a alteração e feche o arquivo.
Se você não precisa definir usuários excepcionais, pule esta etapa digitando **:wq** e fechando o arquivo.
10. Execute o seguinte comando para reiniciar o serviço FTP:
```
systemctl restart vsftpd
```

### Etapa 4: Configurar grupos de segurança
Depois de configurar o serviço FTP, configure **inbound rules (regras de entrada)** para o CVM Linux com base no modo FTP, de fato, utilizado. Para obter detalhes, consulte [Adicionar regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272).
A maioria dos clientes converte endereços IP em LANs. Se você estiver usando o modo FTP ativo, certifique-se de que o cliente obteve o endereço IP real. Caso contrário, o cliente pode falhar ao efetuar login no servidor FTP.
- Para o modo ativo: abra a porta 21.
- Para o modo passivo: abra a porta 21 e todas as portas que variam de `pasv_min_port` a `pasv_max_port` definidas no [arquivo de configuração](#config), como as portas 40000 a 45000 neste documento.

### Etapa 5: Verifique o serviço FTP
Você pode verificar o servidor FTP usando ferramentas como um cliente FTP, um navegador ou através do Windows Explorer. Neste caso, o Windows Explorer é usado como exemplo.
1. Abra o Internet Explorer no cliente, escolha **Tools (Ferramentas)** > **Internet Options (Opções da Internet)** e clique na guia **Advanced (Avançado)**. Faça as seguintes modificações com base no modo FTP selecionado.
 - Para o modo ativo: desmarque **Passive FTP (FTP passivo)**.
 - Para o modo passivo: selecione **Passive FTP (FTP passivo)**.
2. Abra o Windows Explorer no cliente, digite o seguinte endereço na caixa de endereço e pressione **Enter**, conforme mostrado na figura a seguir.
```
ftp://<CVM public IP address:21>
```
![](https://main.qcloudimg.com/raw/40cef1738cb1d2fad07d2ef219822d2f.png)
3. Na página de login que aparece, digite o nome de usuário e senha definidos em [Configuração vsftpd](#user).
Neste caso, o nome de usuário é `ftpuser` e a senha é `tf7295TFY`.
4. Após o login bem-sucedido, você pode fazer upload e download de arquivos.


## Apêndice
<span id="port"></span>
### Configuração do modo FTP ativo
Para usar o modo ativo, modifique os seguintes parâmetros de configuração e deixe outros como padrões:
```
anonymous_enable=NO      # Proibir que usuários anônimos façam login
local_enable=YES         # Permitir que usuários locais façam login
chroot_local_user=YES    # Restringir o acesso de todos os usuários apenas ao diretório raiz
chroot_list_enable=YES # Habilitar a lista de usuários excepcionais
chroot_list_file=/etc/vsftpd/chroot_list  # Especificar a lista de usuários, na qual os usuários listados não estão restritos a acessar apenas o diretório raiz
listen=YES               # Ativar a escuta em soquetes IPv4
# Adicionar o sinal de cerquilha (#) no início da linha seguinte para comentar o seguinte parâmetro.
#listen_ipv6=YES         # Desativar escuta em soquetes IPv6
# Adicionar os seguintes parâmetros
allow_writeable_chroot=YES
local_root=/var/ftp/test # Definir o diretório onde os usuários locais residem após o login
```
Pressione **Esc** e digite **:wq**. Em seguida, salve as alterações e feche o arquivo. Depois disso, vá para a [Etapa 8](#create) para configurar o vsftpd.

### Falha ao fazer upload de arquivos de um cliente FTP
#### Descrição do Problema
No ambiente Linux, os usuários encontram a seguinte mensagem de erro ao enviar arquivos com vsftpd.
```
553 Não foi possível criar o arquivo
```

#### Solução
1. Execute o seguinte comando para verificar a utilização do espaço em disco do servidor:
```
df -h
```
 - Se o espaço em disco for insuficiente, você não pode fazer upload de arquivos. Nesse caso, recomendamos que você exclua alguns arquivos grandes e desnecessários do disco.
 - Se o espaço em disco for suficiente, vá para a próxima etapa.
2. Execute o seguinte comando para verificar se você tem permissão de gravação no diretório FTP:
```
ls -l /home/test      
# Neste caso, /home/test indica o diretório FTP. Substitua-o pelo seu diretório FTP real.
```
 - Se `w` não for retornado no resultado, você não tem permissão de gravação para o diretório. Nesse caso, vá para a próxima etapa.
 - Se `w` for retornado no resultado, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para solução de problemas adicionais.
3. Execute o seguinte comando para conceder permissão de gravação ao diretório FTP:
```
chmod +w /home/test 
# Neste caso, /home/test indica o diretório FTP. Substitua-o pelo seu diretório FTP real.
```
4. Execute o seguinte comando para verificar se a permissão de gravação foi concedida com sucesso:
```
ls -l /home/test   
# Neste caso, /home/test indica o diretório FTP. Substitua-o pelo seu diretório FTP real.
``` 




