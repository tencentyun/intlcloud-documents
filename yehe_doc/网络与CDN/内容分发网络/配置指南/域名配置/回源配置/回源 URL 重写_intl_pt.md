## Visão geral das configurações

Se você precisar modificar o URL da solicitação de pull de origem para o URL que corresponde ao servidor de origem, use a configuração da reescrita de URL de origem no CDN do Tencent Cloud.



## Guia de configuração

### Visualização da configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar a sua página de configuração. Mude para a guia ***Origin-pull Configuration (Configuração de pull de origem)** para localizar a seção **Origin URL Rewrite Configuration (Configuração da reescrita de URL de origem)**.
![](https://main.qcloudimg.com/raw/e6721b8c8d3ebcb9b5a27fb36e6c6782.png)



### Adição de regras

Você pode clicar em **Add Rule (Adicionar regra)** para adicionar regras de reescrita, conforme necessário.
<img src="https://main.qcloudimg.com/raw/5f7d6907976fb0696f633af29321c99c.jpg" style="height:300px"/>


**Limitações de configuração**

- Cada nome de domínio pode ter até 100 regras de reescrita.
- É possível ajustar a prioridade para várias regras. As regras do final da lista têm prioridade mais alta.
- URL de origem atual: começando com `/`; a correspondência por prefixo é usada por padrão; compatível com a correspondência por caminho completo (por exemplo, /teste/a.jpg) e a correspondência curinga (*) (por exemplo, /teste/*/*.jpg). Se você deseja especificar um diretório de arquivo, não pode terminar o caminho com `/` (por exemplo, /test).
- Domínio de origem de destino: o nome atual de domínio é usado por padrão (excluindo `http://` e `https://`). Se necessário, você pode modificar.
- Caminho de origem de destino: começando com `/` (por exemplo, /newtest/b.jpg); o curinga `*` pode ser capturado com `$n` (por exemplo, se n=1,2,3… então /newtest/$1/$2.jpg). Se você deseja especificar um diretório de arquivo, não pode terminar o caminho com `/` (por exemplo, /test).
- São aceitos até cinco `*` e dez `$n`.
- O domínio de origem de destino pode conter até 250 caracteres. Os demais conteúdos podem conter até 1.024 caracteres. Os caracteres chineses não são aceitos.



## Exemplos de configuração:

Suponha que a **Origin URL Rewrite Configuration (configuração da reescrita de URL de origem)** do nome de domínio de aceleração `www.test.com` seja a seguinte:
![](https://main.qcloudimg.com/raw/c255f4e4643a15e2e47a29a608a9fd01.png)

O URL de pull de origem será reescrito da seguinte forma:
- Caso seja solicitado `www.test.com/images/1.jpg`, a solicitação atinge a primeira e a terceira regra. Conforme as regras são executadas de baixo para cima, o URL será reescrito para `www.test.com/index.html`.
- Caso seja solicitado `www.test.com/images`, a solicitação atinge a primeira, a segunda e a terceira regra. Conforme as regras são executadas de baixo para cima, o URL será reescrito para `www.test.com/index.html`.
