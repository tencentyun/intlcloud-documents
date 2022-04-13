

O CDN do Tencent Cloud permite configurar o pull de origem refinado com base em regras de pull de origem, como regras baseadas em caminho (ou seja, especificando um tipo de arquivo, pasta, caminho completo do arquivo ou página inicial para pull de origem) e regras baseadas na região do IP do cliente.

>!
>- O pull de origem com base na região de IP do cliente está em beta. Fique atento ao lançamento oficial.
>- Apenas os servidores de origem principais oferecem suporte ao pull de origem avançado. Essa configuração herdará as configurações de tipo de origem e domínio de origem do servidor de origem principal, independentemente dos diferentes tipos de regras.

## Instruções

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia ***Basic Configuration (Configurações básicas)** para localizar a seção **Advanced Origin-pull Configuration (Configuração avançada de pull de origem)**.
![](https://main.qcloudimg.com/raw/17e0385a7cea2cbdd0ae012cae8b2555.png)

### Adição de regras

Adicione regras para pull de origem avançado conforme necessário. Para adicionar um, clique em **Edit (Editar)** na seção ** Primary Origin (Origem principal)** e depois em **Advanced Origin-pull Configuration (Configuração de pull de origem avançado)**.
![](https://main.qcloudimg.com/raw/ef2ae0e51a0cb032d493f89b8029b316.png)

**Limitações de configuração**

- Cada nome de domínio pode ser configurado com até 50 regras.
- O endereço de pull de origem de uma única regra pode ser um IP, nome de domínio e porta (faixa: 0 a 65535; a porta pode ser omitida). Se "HTTPS" ou "Follow Protocol (Seguir o protocolo)" for selecionado como o protocolo de pull de origem, a porta deve ser 443 ou deve ser deixada em branco.
- Mais ações: é possível ajustar a prioridade das regras e editar ou excluir várias regras em lotes.

>?
>- As regras do final da lista têm prioridade mais alta. A prioridade é importante apenas para os mesmos tipos de regras de pull de origem, ou seja, a prioridade de regras baseadas em caminho (ou seja, especificando um tipo de arquivo, pasta, caminho completo do arquivo ou página inicial para pull de origem) e a prioridade das regras baseadas na região de IP do cliente são independentes.
>- Se uma solicitação corresponder a ambos os tipos de regra, elas serão executadas na ordem das regras baseadas no caminho e, em seguida, das regras baseadas na região de IP do cliente.
Por exemplo, existem duas regras de pull de origem: "encaminhar as solicitações iniciadas por qualquer endereço IP de Jiangsu para `1.1.1.1`" e "encaminhar as solicitações acessando `/test` para `2.2.2.2`". Se um IP localizado em Jiangsu acessar o diretório `/test`, a solicitação será encaminhada para `2.2.2.2`.
