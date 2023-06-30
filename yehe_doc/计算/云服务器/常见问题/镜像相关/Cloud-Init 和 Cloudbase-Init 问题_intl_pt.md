## Cloud-init

### O que é o cloud-init?
O cloud-init é uma ferramenta de software livre que é executada dentro de uma instância da CVM como um serviço não residente. Ele é executado na inicialização e é fechado imediatamente após a execução. Adicionalmente, não se comunica com nenhuma porta.
Todas as imagens públicas do Linux da Tencent Cloud são pré-instaladas com o serviço cloud-init. É necessário rodar o serviço como usuário raiz porque ele é usado principalmente para a inicialização de instâncias da CVM. Por exemplo, a configuração do DNS, do nome do host e do IP, e a execução de alguns scripts personalizados que os usuários configuram para abrir durante a primeira inicialização durante a criação das instâncias da CVM.

### Como verifico se o serviço cloud-init dentro de uma instância do Linux está funcionando corretamente?

<span id="checkcloud-init"></span>
#### Verificação do funcionamento do cloud-init
Em primeiro lugar, faça login na instância e execute os comandos a seguir para conferir a presença de erros. Caso o sistema sinalize a execução do serviço, significa que o serviço está rodando normalmente. Do contrário, você receberá uma mensagem de erro. Você pode solucionar o problema de acordo com a mensagem de erro.
1. Exclua o diretório de cache do cloud-init.
```
rm -rf /var/lib/cloud
```
2. Execute a inicialização completa do cloud-init.
```
cloud-init init --local
```
3. Efetue o pull dos dados da fonte configurada.
```
cloud-init init
```
4. A inicialização do cloud-init abrange vários estágios. Para garantir o link adequado entre eles, o estágio de configuração (config stage) esté incluído nos módulos do cloud-init.
```
cloud-init modules --mode=config
```
5. Especifique o estágio final para os módulos cloud-init.
```
cloud-init modules --mode=final
```

### Quais operações de inicialização o cloud-init executa nas instâncias?

A Tencent Cloud implementa todas as operações de inicialização de instâncias por meio do cloud-init, garantindo a transparência das operações dentro de uma instância. Verifique abaixo uma breve descrição de algumas operações de inicialização. Para mais detalhes, consulte a [documentação do cloud-init](http://cloudinit.readthedocs.io/en/latest/).

<table>
<tr><th style="width: 25%;">Operação de inicialização</th><th style="width: 25%;">Comportamento padrão</th><th style="width: 25%;">Personalização</th><th style="width: 25%;">Observações</th></tr>
<tr>
<td>Inicialização do nome do host</td>
<td>Durante <b>a primeira inicialização</b> de uma instância, o cloud-init definirá o nome do host de acordo com as informações do nome do host em <code>vendor_data.json</code>.</td>
<td>Se você criar ou reinstalar uma instância com uma imagem personalizada e quiser manter o nome do host personalizado da imagem, poderá excluir a configuração, <code>- scripts-user</code>, do <code>/etc/cloud/cloud.cfg</code> antes de criar a imagem personalizada.</td>
<td>Após desativar o <code>- scripts-user</code>, o script de inicialização, <code>/var/lib/cloud/instance/scripts/runcmd</code>, da instância não será executado. A desativação da configuração também afetará a inicialização de outros subitens, como a instalação do Cloud Monitor e as configurações de segurança de nuvem e fonte de software. Além disso, o script personalizado não será executado quando você criar a CVM.</td>
</tr>

<tr>
<td>Inicialização de /etc/hosts</td>
<td>Durante <b>a primeira inicialização</b> de uma instância, o cloud-init inicializará <code>/etc/hosts</code> como <code>127.0.0.1 $hostname</code> por padrão.</td>
<td>Se você criar ou reinstalar uma instância com uma imagem personalizada e quiser manter a configuração personalizada de /etc/hosts da imagem, poderá excluir as configurações de <code>- scripts-user</code> e <code>- ['update_etc_hosts', 'once-per-instance']</code> de <code>/etc/cloud/cloud.cfg</code> antes de criar uma imagem personalizada.</td>
<td>
<ul style="margin: 0px;">
<li>Após desativar o <code>- scripts-user</code>, o script de inicialização, <code>/var/lib/cloud/instance/scripts/runcmd</code>, da instância não será executado.. A desativação da configuração também afetará a inicialização de outros subitens, como a instalação do Cloud Monitor e as configurações de segurança de nuvem e fonte de software. Além disso, o script personalizado não será executado quando você criar a CVM.</li>
<li>Cada vez que a CVM for reiniciado, as configurações de <code>/etc/hosts</code> de algumas CVMs existentes serão substituídas. Para resolver esse problema, consulte <a href="https://intl.cloud.tencent.com/document/product/213/32504">Modificação das configurações de etc/hosts de uma instância do Linux</a>.</li>
</ul>
</td>
</tr>

<tr>
<td>Inicialização do DNS (cenário não DHCP)</td>
<td>Durante <b>a primeira inicialização</b> de uma instância, o cloud-init definirá o DNS da instância de acordo com as informações dos nameservers em <code>vendor_data.json</code>.</td>
<td>Se você criar ou reinstalar uma instância com uma imagem personalizada e quiser manter a configuração personalizada do DNS da imagem, poderá excluir a configuração, <code>- resolv_conf</code> e <code>unverified_modules: ['resolv_conf']</code>, de <code>/etc/cloud/cloud.cfg</code> antes de criar a imagem personalizada.</td>
<td>Nenhuma.</td>
</tr>

<tr>
<td>Inicialização da fonte de software</td>
<td>Durante <b>a primeira inicialização</b> de uma instância, o cloud-init definirá a fonte de software da instância de acordo com as informações de write_files em <code>vendor_data.json</code>.</td><td>Se você criar ou reinstalar uma instância com uma imagem personalizada e quiser manter a configuração personalizada da fonte de software da imagem, poderá excluir a configuração, <code>- write-files</code>, de <code>/etc/cloud/cloud.cfg</code> antes de criar a imagem personalizada.</td>
<td>Nenhuma.</td>
</tr>

<tr>
<td>Inicialização do NTP</td>
<td>Durante <b>a primeira inicialização</b> de uma instância, o cloud-init definirá a configuração do servidor NTP da instância de acordo com as informações do servidor NTP em <code>vendor_data.json</code> e iniciará o serviço NTP.</td>
<td>Se você criar ou reinstalar uma instância com uma imagem personalizada e quiser manter a configuração personalizada do NTP da imagem, poderá excluir a configuração, <code>- ntp<code/>, de <code>/etc/cloud/cloud.cfg</code> antes de criar a imagem personalizada.</td>
<td>Nenhuma.</td>
</tr>

<tr>
<td>Inicialização de senha</td>
<td>Durante <b>a primeira inicialização</b> de uma instância, o cloud-init definirá a senha padrão da conta da instância de acordo com as informações de chpasswd em <code>vendor_data.json</code>.</td>
<td>Se você criar ou reinstalar uma instância com uma imagem personalizada e quiser manter a senha padrão personalizada da imagem, poderá excluir a configuração, <code>- set-passwords</code>, de <code>/etc/cloud/cloud.cfg</code> antes de criar a imagem personalizada.</td>
<td>Nenhuma.</td>
</tr>

<tr>
<td>Vinculação de chaves</td>
<td>Durante <b>a primeira inicialização</b> de uma instância, o cloud-init definirá a chave padrão da conta da instância de acordo com as informações de ssh_authorized_keys em <code>vendor_data.json</code>.</td>
<td>Se você criar ou reinstalar uma instância com uma imagem personalizada e quiser manter a chave padrão personalizada da imagem, poderá excluir a configuração, <code>- users-groups</code>, de <code>/etc/cloud/cloud.cfg</code> antes de criar a imagem personalizada.</td>
<td>Se você vincular manualmente a instância a uma chave dentro da instância, a chave anterior será substituída quando a operação de vinculação de chave for executada por meio do console. </td>
</tr>

<tr>
<td>Inicialização da rede (cenário não DHCP)</td>
<td>Durante <b>a primeira inicialização</b> de uma instância, o cloud-init definirá o IP, o gateway e a máscara de acordo com as informações em <code>network_data.json</code>.</td>
<td>Se você criar ou reinstalar uma instância com uma imagem personalizada e quiser manter as informações de rede personalizadas da imagem, poderá adicionar <code>network: {config: disabled}</code> a <code>/etc/cloud/cloud.cfg</code> antes de criar a imagem personalizada.</td>
<td>Nenhuma.</td>
</tr>
</table>

### Como corrigir problemas relacionados ao cloud-init?

#### 1. Erro devido à desmontagem de repartições do cloud-init
- Descrição do problema:
Erro ao usar os comandos para verificar se o serviço cloud-init está funcionando corretamente:
```
Traceback (most recent call last):
  File "/usr/bin/cloud-init", line 5, in
    ********
    raise DistributionNotFound(req)
pkg_resources.DistributionNotFound: pyyaml
```
- Análise do problema:
“pkg_resources.DistributionNotFound: xxxxx” indica que as repartições do cloud-init foram desinstaladas.
- Solução:
 1. Reinstale as repartições.
 2. Siga as instruções em [Verificação do funcionamento do cloud-init](#checkcloud-init) para confirmar se o erro permance.

#### 2. Erro devido à modificação do compilador padrão do Python
- Descrição do problema:
Um erro é gerado quando o cloud-init é executado na inicialização.
- Análise do problema:
Quando o cloud-init está instalado, o Python 2 é usado como compilador padrão do Python, o que significa que os atalhos, `/usr/bin/python` e `/bin/python`, são vinculados ao Python 2. Os usuários podem alterar o compilador padrão do Python para o Python 3 dentro da instância, direcionando os atalhos, `/usr/bin/python` e `/bin/python`, para o Python 3. Devido a problemas de compatibilidade, um erro será gerado quando o cloud-init for executado na inicialização.
- Solução:
 1. Modifique o compilador do Python especificado no arquivo `/usr/bin/cloud-init` alterando `#/usr/bin/python` ou `#/bin/python` para `#! user/bin/python`.
> Não use atalhos. Aponte para um compilador em específico sem utilizar atalhos.
>
 2. Siga as instruções em [Verificação do funcionamento do cloud-init](#checkcloud-init) para confirmar se o erro permance.

## Cloudbase-Init

### O que é o Cloudbase-Init?
Similar ao cloud-init, o Cloudbase-Init é uma ponte pela qual você pode se comunicar com instâncias da CVM do Windows. O serviço Cloudbase-Init é executado quando uma instância é iniciada pela primeira vez. O serviço processará e inicializará as informações de configuração de inicialização. As operações posteriores, como redefinir a senha e modificar os endereços IP, também são feitas por meio do Cloudbase-Init.

### Como verifico se o serviço Cloudbase-Init dentro de uma instância do Windows está funcionando corretamente?

<span id="checkcloudbase-init"></span>
#### Verificação do funcionamento do serviço Cloudbase-Init
1. Faça login na instância.
> Se você esquecer a senha ou não conseguir redefini-la devido a erros do serviço Cloudbase-Init, é possível redefinir a senha seguindo a [Etapa 2](#step02).
>
2. <span id="step02">Abra o **Control Panel (Painel de Controle)** > **Administrative Tools (Ferramentas Administrativas)** > **Services (Serviços)**.
3. Localize o serviço Cloudbase-Init, clique com o botão direito do mouse e acesse **Properties (Propriedades)**. </span>
 - Verifique se o “Startup type (Tipo de inicialização)” está definido como “Automatic (Automática)”, conforme mostrado na figura abaixo.
![](https://main.qcloudimg.com/raw/310a278dd2eaf2124d0d52055e0b5b6f.png)
 - Exiba a “Logon identity (Identidade de login)” e certifique-se de que a “Local System account (Conta Sistema local)” esteja selecionada, conforme mostrado na figura abaixo.
![](https://main.qcloudimg.com/raw/5a3f623aaf44d55cfe2eaa6aeadb4c12.png)
 - Inicie manualmente o serviço Cloudbase-Init e veja se algum erro é gerado.
Se um erro for gerado, primeiramente você precisará corrigir o problema e verificar se instalou algum software de segurança que possa impedir o Cloudbase-Init realizar as operações pré-definidas.
![](https://main.qcloudimg.com/raw/dbbe8f9fc05b07d8011705d9d217b76c.png)
 - Abra o registro, localize todas as chaves “LocalScriptsPlugin” e certifique-se de que seus valores sejam 2, conforme mostrado na figura abaixo.
![](https://main.qcloudimg.com/raw/16106e540d8cf4ef39e5dccb44251350.png)
 - Verifique se o carregamento do CD-ROM está desativado. Se houver um drive de disco óptico como mostrado na figura abaixo, significa que o carregamento não foi desativado; caso contrário, significa que foi desativado e precisa ser ativado.
![](https://main.qcloudimg.com/raw/7707e694b475ba4d70b4d1d52a6c98bb.png)

### Como corrigir problemas comuns relacionados ao Cloudbase-Init?
#### Falha ao redefinir a senha durante a inicialização
- Possíveis causas:
 - A senha da conta do Cloudbase-Init foi alterada manualmente, o que gera o erro ao iniciar o serviço Cloudbase-Init, mais à falha de operações como a redefinição de senha durante a inicialização.
 - O serviço Cloudbase-Init está desativado, o que levou à falha de operações como a redefinição de senha durante a inicialização.
 - O software de segurança instalado bloqueia o serviço Cloudbase-Init de redefinir a senha, portanto, a operação retorna um resultado OK, mas na verdade falhou.
- Solução:
Siga o procedimento correspondente para cada motivo possível para corrigir o problema.
 1. Altere o serviço Cloudbase-Init para o serviço LocalSystem. Para mais detalhes, consulte a [Etapa 2](#step02) em [Verificação do funcionamento do serviço Cloudbase-Init](#checkcloudbase-init).
 2. Altere o tipo de inicialização do serviço Cloudbase-Init para automática. Para mais detalhes, consulte a [Etapa 2](#step02) em [Verificação do funcionamento do serviço Cloudbase-Init](#checkcloudbase-init).
 3. Desative o software de segurança afetado ou adicione as operações relevantes do serviço Cloudbase-Init à lista de permissões do software de segurança.
