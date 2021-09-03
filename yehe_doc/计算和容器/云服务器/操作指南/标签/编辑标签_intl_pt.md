## Cenário de operação
Este documento descreve como editar as tags de recursos.

## Limites de uso

Existem várias limitações para a edição de tags:
- Quantidade: cada recurso pode ter no máximo 50 tags.
- Limitações de chaves de tag:
  - Não é possível criar chaves de tag que comecem com `qcloud`, `tencent` e `project`, pois são reservadas para o sistema.
  - As chaves de tag só podem conter `números`, `caracteres do alfabeto`, `+=.@-` e devem ter menos de 255 caracteres.
- Valor da tag: os valores da tag só podem conter `strings vazias ou números`, `caracteres do alfabeto`, `+=.@-` e devem ter menos de 127 caracteres.


## Pré-requisitos
Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm).

## Instruções
### Edição da tag de uma única instância
1. Na página de gerenciamento de instâncias, selecione a instância da qual as tags precisam ser editadas e clique em **More (Mais)** > **Instance Settings (Configurações da instância)** > **Edit Tags (Editar tags)**, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/29ad45e372fc78e28ab0ed69e73ec997.png)
2. Adicione, modifique ou exclua as tags na janela pop-up “1 cloud resource(s) selected (1 recurso de nuvem selecionado)” com base em suas necessidades.

### Edição das tags de várias instâncias
> É possível editar as tags em lote de até 20 recursos de uma vez.
>
1. Na página de gerenciamento de instâncias, selecione as instâncias da qual as tags precisam ser editadas e clique em **More Actions (Mais ações)** > **Instance Settings (Configurações da instância)** > **Edit Tags (Editar tags)** na parte superior, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/d0e1965a2e256cae7b4dbdb7881ca9de.png)
2. Adicione, modifique e exclua as tags na janela pop-up “n cloud resource(s) selected (n recurso(s) de nuvem selecionado(s))” com base em suas necessidades.

## Exemplos de operações

Para obter informações sobre como usar as tags, consulte o [Guia do usuário sobre tags](https://intl.cloud.tencent.com/document/product/213/19548).
