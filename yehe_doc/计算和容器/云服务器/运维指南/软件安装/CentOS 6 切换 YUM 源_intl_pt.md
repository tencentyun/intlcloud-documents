## Informações gerais
O CentOS 6 atingiu o fim da vida útil em 30 de novembro de 2020 e não é mais mantido pela comunidade do Linux. Portanto, a fonte do CentOS 6 não está disponível no `http://mirror.centos.org/centos-6/` e em sites de imagens de terceiros. Os sites do Tencent Cloud, `http://mirrors.cloud.tencent.com/` e `http://mirrors.tencentyun.com/`, não podem obter a fonte do CentOS 6. Se você continuar a usar a fonte padrão do CentOS 6 configurada no Tencent Cloud, pode ocorrer um erro.



>? É recomendável atualizar o sistema operacional para o CentOS 7 ou uma versão posterior. Se você ainda precisar usar as dependências do CentOS 6, troque a fonte do CentOS 6 conforme as instruções abaixo.



## Instruções
1. Faça login em uma instância do Linux usando o Web Shell (consulte a [documentação](https://intl.cloud.tencent.com/document/product/213/5436)). Você também pode usar outros métodos de login com os quais esteja mais familiarizado:
	- [Login em instâncias do Linux por meio de ferramentas de login remoto](https://intl.cloud.tencent.com/document/product/213/32502)
	- [Login em instâncias do Linux usando uma chave SSH](https://intl.cloud.tencent.com/document/product/213/32501)
2. Execute o comando a seguir para verificar a versão do CentOS do sistema operacional atual.
```
cat /etc/centos-release
```
Conforme mostrado na figura a seguir, a versão do sistema operacional é o CentOS 6.9.
![](https://main.qcloudimg.com/raw/de65529a43dc5bfee695c08d5f7bff80.png)
3. Execute o comando a seguir para editar o arquivo `CentOS-Base.repo`.
```
vim /etc/yum.repos.d/CentOS-Base.repo 
```
4. Pressione **i** para entrar no modo de edição e modifique `baseurl` de acordo com a versão do CentOS e o ambiente de rede.
>?
>Determine a fonte necessária para a instância conforme instruído em [Acesso à rede privada](https://intl.cloud.tencent.com/document/product/213/5225) e [Acesso à Internet](https://intl.cloud.tencent.com/document/product/213/5224) 
>
>- Fonte para acesso à rede privada: `http://mirrors.tencentyun.com/centos-vault/6.x/`
>- Fonte para acesso à rede pública: `https://mirrors.cloud.tencent.com/centos-vault/6.x/`

Este documento usa uma instância baseada no CentOS 6.9 que requer acesso à rede privada como exemplo. O arquivo modificado <code>CentOS-Base.repo</code> é conforme abaixo:
<img src="https://main.qcloudimg.com/raw/1d2485a9be0df6d5f7c46151fc50d73b.png"/>
5. Pressione **ESC**, insira **:wq** e pressione **Enter** para salvar a modificação.
6. Execute o comando a seguir para modificar o arquivo `CentOS-Epel.repo`.
```
vim /etc/yum.repos.d/CentOS-Epel.repo 
```
7. Pressione **i** para entrar no modo de edição e modifique `baseurl` de acordo com o ambiente de rede.
Nesse exemplo, altere `baseurl=http://mirrors.tencentyun.com/epel/$releasever/$basearch/` para `baseurl=http://mirrors.tencentyun.com/epel-archive/6/$basearch/`. O resultado deve ser o seguinte:
![](https://main.qcloudimg.com/raw/9c4b3eaf65d005b3d6819f013037443d.png)
8. Pressione **ESC**, insira **:wq** e pressione **Enter** para salvar a modificação.
9. Agora você pode usar o comando `yum install` para instalar o software necessário.
