## Cenário

A partir de 1º de março de 2018, a imagem pública do Linux fornecida pelo Tencent Cloud traz a ferramenta de software livre Cloud-Init pré-instalada, e todas as operações de inicialização em uma instância serão feitas via Cloud-Init, tornando as operações internas da instância mais transparentes. Para obter mais informações, consulte Cloud-Init.
Em **cada inicialização**, o Cloud-Init gera um novo arquivo `/etc/hosts` de acordo com o modelo `/etc/cloud/templates/hosts.${os_type}.tmpl` e substitui o arquivo original `/etc/hosts` de uma instância. Portanto, após o usuário modificar manualmente a configuração interna `/etc/hosts` da instância e reiniciá-la, a configuração `/etc/hosts` volta para a configuração padrão original.

## Pré-requisitos
O Tencent Cloud corrigiu esse problema para instâncias criadas **depois de setembro de 2018**, e a configuração `/etc/hosts` não será substituída.
Para instâncias criadas **antes de setembro de 2018**, siga as etapas abaixo para modificação.

## Etapas

### Solução 1 
1. Faça login no CVM do Linux.
2. Execute o comando a seguir para alterar o `- update_etc_hosts` no arquivo de configuração `/etc/cloud/cloud.cfg` para `- ['update-etc-hosts', 'once-per-instance']`.
```
sed -i "/update_etc_hosts/c \ - ['update_etc_hosts', 'once-per-instance']" /etc/cloud/cloud.cfg
```
3. Execute o comando a seguir para criar um arquivo `config_update_etc_hosts` no caminho `/var/lib/cloud/instance/sem/`.
```
touch /var/lib/cloud/instance/sem/config_update_etc_hosts
```

### Solução 2
>Esta solução usa o sistema operacional CentOS 7.2 como exemplo.
>
#### Obtenção do caminho do arquivo de modelo `hosts`
1. Faça login no CVM do Linux.
2. Execute o comando a seguir para exibir o arquivo de modelo `hosts` do sistema.
```
cat /etc/hosts
```
O arquivo de modelo `hosts` é conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/f51f9c53004574f72d32f5ed790c8563.png)


#### Modificação do arquivo de modelo `hosts`
>Considerando adicionar `127.0.0.1 test test` como exemplo, você pode modificar o modelo `hosts` e o arquivo `/etc/hosts` conforme necessário.
>
1. Execute o comando a seguir para modificar o arquivo de modelo `hosts`.
```
vim /etc/cloud/templates/hosts.redhat.tmpl
```
2. Pressione **i** ou **Insert** para mudar para o modo de edição.
3. Adicione o conteúdo a seguir ao final do arquivo.
```
127.0.0.1 test test
```
4. Pressione **Esc**, digite **:wq**, salve o arquivo e retorne.

#### Modificação do arquivo /etc/hosts
1. Execute o comando a seguir para modificar o arquivo `/etc/hosts`.
```
vim /etc/hosts
```
2. Pressione **i** ou **Insert** para mudar para o modo de edição.
3. Adicione o conteúdo a seguir ao final do arquivo.
```
127.0.0.1 test test
```
4. Pressione **Esc**, digite **:wq**, salve o arquivo e retorne.
