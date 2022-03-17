## Visão geral
Para associar uma instância a um domínio e fazer login no CVM do Windows com a conta do domínio, é necessário executar o Sysprep antes de criar uma imagem personalizada para garantir que o SID seja exclusivo. Caso contrário, a instância não pode ser associada ao domínio porque o CVM criado com a imagem personalizada e a instância original contém informações idênticas, como SIDs duplicados. Ignore essa operação se você não precisar associar seu CVM do Windows a um domínio.

Este documento descreve como executar o Sysprep no sistema operacional Windows Server 2012 R2 de 64 bits para garantir que os CVMs do Windows no domínio tenham SIDs exclusivos.

Para obter mais informações sobre o Sysprep, consulte `https://technet.microsoft.com/zh-cn/library/cc721940(v=ws.10).aspx`


## Observações

- O CVM do Windows deve ser um sistema operacional Windows genuíno ativo.
- Se o seu CVM do Windows for criado com uma imagem não pública, você deve sempre executar a versão do Sysprep fornecida na imagem original no diretório `%WINDIR%\system32\sysprep`.
- As contagens de redefinição restantes do Windows devem ser maiores que 1, caso contrário, o Sysprep não pode ser encapsulado.
Para verificar as contagens de reinicialização restantes do Windows, execute o comando `slmgr.vbs /dlv`.
- A conta do Cloudbase-Init cuida das ações de inicialização quando uma instância do CVM é iniciada. Se você alterar/excluir essa conta ou desinstalar o Couldbase-Init, poderá perder informações personalizadas ao fornecer um novo CVM a partir de uma imagem personalizada. Portanto, não recomendamos modificar ou excluir a conta do Cloudbase-init.   

## Pré-requisitos

1. [Faça login no CVM do Windows](https://intl.cloud.tencent.com/document/product/213/5435) como Administrador.
- [Instale o Cloudbase-Init no CVM do Windows](https://intl.cloud.tencent.com/document/product/213/32364).

## Instruções

1. Na área de trabalho, clique em<img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png"></img> para abrir a janela Windows PowerShell.
2. Execute o comando a seguir na janela do Windows PowerShell para acessar o diretório de instalação da ferramenta Cloudbase-init.
> Suponha que o Cloudbase-init esteja instalado em `C:\Program Files\Cloudbase Solutions\`.
>
```
cd 'C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf'
```
3. Execute o comando a seguir para encapsular o sistema Windows.
> 
> - Inclua `/unattend:Unattend.xml` no comando a seguir, caso contrário, seu nome de usuário atual, senha e outras configurações do CVM serão redefinidos. Se você escolher **Follow image (Seguir imagem)** para o login, precisará redefinir manualmente o nome de usuário e a conta após a inicialização.
> - Depois que o comando a seguir for executado, o CVM será encerrado automaticamente. Para garantir que os CVMs criados a partir desta imagem tenham SIDs exclusivos, não inicie a instância do CVM antes de criar uma imagem personalizada, ou esta ação só terá efeito para o CVM atual.  
> - Depois de executar o comando a seguir no sistema operacional Windows Server 2012 ou Windows Server 2012 R2, o Administrador da conta e sua senha do CVM serão excluídos. Redefina sua conta e senha depois de reiniciar o CVM conforme detalhado em [Redefinir senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).
> 
```
C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /unattend:Unattend.xml
```
4. Crie uma imagem personalizada a partir da instância do CVM na qual o Sysprep foi executado e inicie novas instâncias do CVM com a imagem. - Consulte [Criação de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4942).
E agora, cada nova instância do CVM terá um SID exclusivo ao ser associada a um domínio.
> Para verificar o SID do CVM, execute o comando `whoami /user`.
>


