### Como faço login em uma instância da CVM usando o VNC?

A Tencent Cloud permite que os usuários façam login em uma instância da CVM usando o cliente Web VNC. Se você não tiver um cliente de login remoto instalado ou não puder fazer login usando o cliente, poderá usar um cliente Web VNC para fazer login em uma instância da CVM. Você pode usar o cliente Web para fazer login remotamente, exibir o status da instância da CVM e realizar o gerenciamento básico da instância. Para mais detalhes, consulte os seguintes documentos:
- [Login em instâncias do Linux pelo VNC](https://intl.cloud.tencent.com/document/product/213/32494)
- [Login em instâncias do Windows pelo VNC](https://intl.cloud.tencent.com/document/product/213/32496)

### Como habilitar o login remoto multiusuário em um Windows Server?

O Windows Server permite o login remoto multiusuário. Para mais instruções detalhadas de configuração, consulte [Configuração do login remoto multiusuário para os CVMs do Windows](https://intl.cloud.tencent.com/document/product/213/32497).
Se você não conseguir habilitar o login remoto multiusuário em um Windows Server após seguir as instruções no documento acima, reinicie a instância e tente fazer login novamente.

### Como posso fazer login em uma instância executando o Ubuntu como raiz?

O usuário padrão do Ubuntu é `ubuntu`. Por padrão, o `root` não é habilitado durante o processo de instalação.  Se necessário, habilite o `root` segundo as instruções abaixo:
1. Faça login na instância da CVM usando o `ubuntu`.
2. <span id="Step2"></span>Execute o seguinte comando para definir uma senha de `root`:
```
sudo passwd root
```
3. Digite uma senha para `root` e pressione **Enter**.
4. Digite a senha novamente e pressione **Enter**.
Caso apareça a mensagem abaixo, a senha foi definida:
```
passwd: password updated successfully
```
5. Execute o seguinte comando para abrir `sshd_config`:
```
sudo vi /etc/ssh/sshd_config 
```
6. Pressione **i** para alternar para o modo de edição. Localize `#Authentication` e altere o valor de `PermitRootLogin` para `yes`, conforme mostrado na figura a seguir:
> Se `PermitRootLogin` estiver em forma de comentário, remova as marcas de `#`.
> 
![](https://main.qcloudimg.com/raw/359242f7e5df666d43459fe74abce72a.png)
7. Pressione **Esc** e digite **:wq** para salvar o arquivo e fechar o vi.
8. Execute o comando a seguir para reiniciar o serviço SSH.
```
sudo service ssh restart
```
9. Consulte [Login em instâncias do Linux usando o método de login padrão](https://intl.cloud.tencent.com/document/product/213/5436) para mais detalhes de como fazer o login em uma instância da CVM que executa o Ubuntu.
 - **Username (Nome de usuário)**: root
 - **Password (Senha)**: a senha que você definiu na [Etapa 2](#Step2).
 A figura abaixo ilustra um login bem-sucedido usando o root:
![](https://main.qcloudimg.com/raw/a8a6ec3e2499e08d051c9ee11fdcd85e.png)

### O que fazer se não conseguir me conectar (fazer login) a uma instância da CVM após reiniciá-la?

Esse problema pode ser devido ao alto uso de CPU e memória da instância. Para mais informações, consulte os seguintes documentos:
- [Falha ao fazer login em uma CVM do Linux devido ao alto uso de CPU e memória](https://intl.cloud.tencent.com/document/product/213/32387)
- [Falha ao fazer login em uma CVM do Windows devido ao alto uso de CPU e memória](https://intl.cloud.tencent.com/document/product/213/32405)

### O que fazer quando me conecto à uma instância da CVM remotamente e a conexão expira?
Confirme se:
- A instância está em execução.
- A instância está associada a grupos de segurança com as regras necessárias. Para mais detalhes, consulte [Adição de regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272).
- A instância tem o SSH ou o RDP ativados.
- A instância abriu as portas correspondentes. Por padrão, o SSH usa a porta 22 e o RDP usa a porta 3389.

### Por que minha conexão remota com uma instância do Linux foi recusada?
Confirme se:
- A instância tem o SSH ou o RDP ativados.
- A instância abriu as portas correspondentes. Por padrão, o SSH usa a porta 22 e o RDP usa a porta 3389.

### Por que recebo a mensagem de nome de usuário ou senha inválida quando me conecto remotamente à uma instância do Linux?
Confirme se:
- Você usou o nome de usuário correto. O nome de usuário padrão para a maioria das distribuições Linux é `root`. No entanto, o Ubuntu usa `ubuntu`.
- Você digitou a senha corretamente. Se você esqueceu a senha, redefina-a. Para mais detalhes, consulte [Redefinição da senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).

### Por que recebo a mensagem de nome de usuário ou senha inválida quando me conecto remotamente à uma instância do Windows?
Confirme se:
- Você usou o nome de usuário correto. O nome de usuário padrão do Windows é `Administrator`.
- Você digitou a senha corretamente. Se você esqueceu a senha, redefina-a. Para mais detalhes, consulte [Redefinição da senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).
- Para usar um usuário sem privilégios de administrador para fazer login, esse usuário precisa pertencer ao grupo Usuários da Área de Trabalho Remota.

### O console permite o login multiusuário pelo VNC?
Não. Se um usuário já tiver feito login, os outros usuários não poderão fazer login.

### O que devo fazer se esquecer a senha de login de uma instância da CVM?
Você pode redefinir a senha. Para mais detalhes, consulte [Redefinição da senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).

### Por que não consigo usar o Internet Explorer 8.0 para fazer login nas minhas instâncias?
O cliente Web VNC é compatível com o Internet Explorer 10 ou versões posteriores. Baixe a versão mais recente do Internet Explorer.
Além disso, recomendamos que você use o Google Chrome porque o console da Tencent Cloud oferece uma experiência de usuário melhor no Google Chrome do que no Internet Explorer.

### Como fazer login em uma instância do Linux remotamente?
- A Tencent Cloud recomenda [fazer login em uma instância do Linux usando o método de login padrão](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode:
- [Fazer login em uma instância do Linux usando o software de login remoto](https://intl.cloud.tencent.com/document/product/213/32502).
- [Fazer login em uma instância do Linux usando o SSH](https://intl.cloud.tencent.com/document/product/213/32501).
- [Fazer login em uma instância do Linux usando o VNC](https://intl.cloud.tencent.com/document/product/213/32494).

### O que devo fazer se não conseguir me conectar à uma instância do Linux?
Caso não consiga se conectar à uma instância do Linux, consulte [Falhas de login da instância do Linux](https://intl.cloud.tencent.com/document/product/213/32500) para ter acesso às instruções para solução de problemas.
Se o problema persistir, [envie um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1).

### O que devo fazer se não conseguir me conectar à uma instância do Windows?
Caso não consiga se conectar à uma instância do Windows, consulte [Falha de login da CVM](https://intl.cloud.tencent.com/document/product/213/10339) para ter acesso às instruções para solução de problemas.
Se o problema persistir, [envie um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1).

### O que devo fazer caso detecte que a minha instância da CVM foi conectada a partir de locais incomuns?
Se você descobrir que a sua instância da CVM foi conectada a partir de locais que você não reconhece:
1. Verifique novamente o horário de login do local de login incomum e verifique se você ou outros administradores fizeram login naquele momento.
2. Se não tiverem feito, siga as etapas abaixo:
 1. [Redefina a senha](https://intl.cloud.tencent.com/document/product/213/16566) imediatamente.
 2. Verifique a instância em busca de vírus ou trojans.
 3. Use os grupos de segurança para [limitar logins a endereços IP específicos](https://intl.cloud.tencent.com/document/product/213/32369).



