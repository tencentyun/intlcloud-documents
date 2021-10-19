

O Content Delivery Network do Tencent Cloud proporciona configurações refinadas de pull de origem para encaminhar solicitações de pull de origem com base no caminho (ou seja, especificando um tipo de arquivo, pasta, arquivo de caminho completo ou página inicial para pull de origem) e região de IP do cliente.

>! O pull de origem com base na região de IP do cliente está em beta. Fique atento ao lançamento oficial.

## Guia de configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia ***Basic Configuration (Configurações básicas)** para localizar a seção **Advanced Origin-pull Configuration (Configuração avançada de pull de origem)**.

![](https://main.qcloudimg.com/raw/17e0385a7cea2cbdd0ae012cae8b2555.png)

### Adição de regras

Você pode clicar em **Add Rule (Adicionar regra)** para adicionar regras, conforme necessário.
![](https://main.qcloudimg.com/raw/ef2ae0e51a0cb032d493f89b8029b316.png)

**Limites**

- Cada nome de domínio pode ser configurado com até 50 regras.
- O endereço de pull de origem de uma única regra pode ser um IP, nome de domínio e porta (faixa: 0 a 65535; a porta pode ser omitida). Se "HTTPS" ou "Seguir o protocolo" for selecionado como o protocolo de pull de origem, a porta deve ser 443 ou deixada em branco.
- Mais ações: é possível ajustar a prioridade das regras e editar ou excluir várias regras em lotes.

>?
>- Na lista de regras, uma regra na parte inferior tem a prioridade mais alta. Observe que se você reorganizar uma regra na lista, apenas a prioridade das regras do mesmo tipo será afetada.
>- Se uma solicitação corresponder a ambos os tipos de regra, as regras serão executadas na ordem das regras baseadas no caminho e, em seguida, das regras baseadas na região de IP do cliente.
Por exemplo, quando há duas regras de pull de origem: "forwarding all requests from Jiangsu province to `1.1.1.1` (encaminhar todas as solicitações da província de Jiangsu para `1.1.1.1`)" e "forwarding the requests accessing `/test` to `2.2.2.2` (encaminhar as solicitações de acesso a `/test` para `2.2.2.2`)", se uma solicitação de Jiangsu deseja acessar o diretório `/test`, a solicitação será encaminhada para `2.2.2.2`.
