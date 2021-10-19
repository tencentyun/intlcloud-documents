## Visão geral das configurações

O CDN do Tencent Cloud aceita a configuração de regras de lista de bloqueio/permissões do agente do usuário (UA) para controle de acesso.
O CDN verifica o campo `User-Agent` nos cabeçalhos de solicitação HTTP com base nas regras, para permitir ou rejeitar as solicitações de acesso do usuário.

## Guia de configuração

### Limitações de configuração

- A lista de bloqueio e a lista de permissões não podem ser definidas ao mesmo tempo. Defina as regras da lista de bloqueio ou as regras da lista de permissões.
- Quantidade máxima de regras de lista de bloqueio/permissões: 10
- As regras aceitam o curinga `*`. Separe os valores com `|`.
- Tipos de efeito aceitos: todo o conteúdo, extensão de arquivo, diretório de arquivo e arquivo especificado. Atualmente, a correspondência regular não é aceita.

### Instruções de configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Selecione a guia **Access Control (Controle de acesso)** para localizar a configuração de lista de bloqueio/permissões de agente do usuário (UA), que fica desativada por padrão:
![](https://main.qcloudimg.com/raw/07914bd30b3d422fb4bddf3a323d92f2.png)
Quando o botão de alternância estiver desativado, clique em **Add Rule (Adicionar regra)** para adicionar as regras de lista de bloqueio/permissões, uma a uma:
![](https://main.qcloudimg.com/raw/66d3fc72f575efaa4ae42382d8fde179.png)

>!
>1. Apenas o curinga `*` é aceito; outras expressões regulares não são aceitas.
>2. Se não houver `*`, todos os caracteres serão usados para correspondência exata.

A configuração geral será desativada após a adição de uma regra, para que os serviços em andamento não sejam afetados:
![](https://main.qcloudimg.com/raw/679129885ec36329178e87af671d6743.png)
Você pode ativar o botão de alternância para implantar oficialmente a lista de bloqueio/permissões de UA configurada.
![](https://main.qcloudimg.com/raw/fd85de8e702b24e7d2eaaf8b34667c95.png)

## Exemplos de configuração

A configuração da lista de bloqueio/permissões de UA de `cloud.tencent.com` é a seguinte:
![](https://main.qcloudimg.com/raw/c7e06060bc627aab2e4939b53460951d.png)
Se `User-Agent` no cabeçalho da solicitação HTTP for:

```
user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.61 Safari/537.36
```

A lista de bloqueio será atingida e um erro 403 será retornado diretamente.

