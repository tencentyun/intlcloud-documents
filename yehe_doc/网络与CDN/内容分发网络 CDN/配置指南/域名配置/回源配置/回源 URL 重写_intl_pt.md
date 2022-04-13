## Visão geral

Se você precisar modificar o URL da solicitação de pull de origem para o URL que corresponde ao servidor de origem, é possível usar a configuração da reescrita do URL de origem no CDN do Tencent Cloud.

>! Esta funcionalidade não está disponível para nome de domínio do ECDN.


## Instruções

### Visualização da configuração

Faça login no [Console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar a sua página de configuração. Mude para a guia ***Origin-pull Configuration (Configuração de pull de origem)** para localizar a seção **Origin URL Rewrite Configuration (Configuração de reescrita do URL de origem)**.
![](https://main.qcloudimg.com/raw/e6721b8c8d3ebcb9b5a27fb36e6c6782.png)



### Adição de regras

Você pode clicar em **Add Rule (Adicionar regra)** para adicionar regras de reescrita, conforme necessário.
<img src="https://main.qcloudimg.com/raw/5f7d6907976fb0696f633af29321c99c.jpg" style="height:300px"/>


**Limitações de configuração**

- Cada nome de domínio pode ter até 100 regras de reescrita.
- É possível ajustar a prioridade para várias regras. As regras do final da lista têm prioridade mais alta.
- URL de origem atual: começando com “/”; a correspondência por prefixo é usada por padrão; compatível com a correspondência de caminho completo (por exemplo, /teste/a.jpg) e a correspondência curinga (*) (por exemplo, /teste/*/*.jpg). Se você deseja especificar um diretório de arquivo, não pode terminar o caminho com “/” (por exemplo, /test).
- Domínio de origem de destino: o nome atual de domínio é usado por padrão (excluindo “http://” e “https://”). Se necessário, você pode modificar.
- Caminho de origem de destino: começando com “/” (por exemplo, /newtest/b.jpg); o curinga “*” pode ser capturado com “$n” (por exemplo, se n=1,2,3… então /newtest/$1/$2.jpg). Se você deseja especificar um diretório de arquivo, não pode terminar o caminho com “/” (por exemplo, /test).
- São aceitos até 5 “*” e 10 “$n”.
- O domínio de origem de destino pode conter até 250 caracteres. Os demais conteúdos podem conter até 1.024 caracteres. 



## Exemplos de configuração:

Suponha que a **Origin URL Rewrite Configuration (Configuração da reescrita do URL de origem)** do nome de domínio de aceleração www.test.com seja a seguinte:


O pull de origem será reescrito da seguinte forma:
- Caso seja solicitado www.test.com/images/1.jpg, a solicitação acerta a primeira, segunda e terceira regras. Como as regras são executadas de baixo para cima, a URL será reescrita para www.test.com/index.html.
-- Caso seja solicitado www.test.com/images e a solicitação acerte a segunda regra, a URL será reescrita para www.test.com/goodboy.html.
