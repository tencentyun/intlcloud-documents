## Visão geral das configurações

Se você precisar modificar o URL de acesso real para o URL que corresponde ao servidor de origem, é possível usar a configuração da reescrita de URL de acesso no CDN do Tencent Cloud.

Você pode personalizar a configuração da reescrita de URL de acesso para redirecionar URLs com o código 302 para o URL especificado.

## Guia de configuração

### Visualização da configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia ***Cache Configuration (Configuração de cache)** para localizar a seção **Access URL Rewrite Configuration (Configuração da reescrita de URL de acesso)**.

A **Access URL Rewrite Configuration (Configuração da reescrita de URL de acesso)** fica desabilitada por padrão.
![](https://main.qcloudimg.com/raw/01f93aaa70c523ae0bb1ab5debae8558.png)


### Adição de regras

Você pode clicar em **Add Rewrite Rule (Adicionar regra de reescrita)** para adicionar regras, conforme necessário.
<img src="https://main.qcloudimg.com/raw/97ea8713395f3af8654c39be97f124d3.png"  style="height:300px"></img>

**Limitações de configuração**
+ Cada nome de domínio pode ter até 100 regras de reescrita.
+ É possível ajustar a prioridade para várias regras. As regras do final da lista têm prioridade mais alta.
+ URL atual: começando com `/`; compatível com a correspondência de caminho completo (por exemplo, /teste/a.jpg) e a correspondência curinga (*) (por exemplo, /teste/*/*.jpg). Se você deseja especificar um diretório de arquivo, não pode terminar o caminho com `/` (por exemplo, /test).
+ Host de destino: é o nome de domínio atual (começando com `http://`) por padrão. Ele pode ser modificado para outros nomes de domínio começando com `http://` ou `https://`.
+ Caminho de destino: começando com `/` (por exemplo, /newtest/b.jpg); o curinga `*` pode ser capturado com `$n` (por exemplo, se n=1,2,3… então /newtest/$1/$2.jpg). Se você deseja especificar um diretório de arquivo, não pode terminar o caminho com `/` (por exemplo, /test).
+ São aceitos até cinco `*` e dez `$n`.
+ O conteúdo pode conter até 1.024 caracteres e os caracteres chineses não são aceitos.




## Exemplos de configuração

Se a **Access URL Rewrite Configuration (Configuração da reescrita de URL de acesso)** do nome de domínio de aceleração `www.test.com` for a seguinte:
![](https://main.qcloudimg.com/raw/214b034e578d5eaac0a63cacd49f1e2d.png)

Então, o acesso real será:

+ Um cliente solicita `www.test.com/test/a.jpg` e o nó do CDN retorna `www.test.com/newtest/b.jpg`.
+ Um cliente solicita `www.test.com/test/a.png` e o nó do CDN retorna `www.newtest.com/newtest/a.png`.



