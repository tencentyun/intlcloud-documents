## Visão geral

As **Tags** são pares de chave-valor fornecidos pelo Tencent Cloud para fácil identificação de recursos. É possível usar as tags para categorizar e gerenciar os recursos do seu CVM.
O Tencent Cloud não usará suas tags, elas são usadas exclusivamente por você para gerenciar os recursos do seu CVM.

## Limites de uso
Observe os seguintes limites ao usar as tags:
- Limites de quantidade: cada recurso do Tencent Cloud permite até 50 tags.
- Limites de chaves de tag:
 - As chaves de tags não podem começar com `qcloud`, `tencent` ou `project`.
 - Uma chave de tag pode conter até 255 caracteres, incluindo números, letras e `+=.@-`.
- Limites de valores da tag: um valor de tag pode conter até 127 caracteres, incluindo números, letras e `+=.@-`. Pode ser deixado vazio, se necessário.

## Instruções e casos

### Caso de uso

Uma empresa adquiriu seis instâncias do CVM, das quais o grupo empresarial, o escopo e os proprietários são os seguintes:

| ID da instância | Grupo empresarial | Escopo empresarial | Proprietário |
|---------|---------|---------|--------|
| ins-abcdef1 | Comércio eletrônico | Campanhas de marketing | John Smith |
| ins-abcdef2 | Comércio eletrônico | Campanhas de marketing | Chris |
| ins-abcdef3 | Jogos | Jogo A | Jane Smith |
| ins-abcdef4 | Jogos | Jogo B | Chris |
| ins-abcdef5 | Entretenimento | Pós-produção | Chris |
| ins-abcdef6 | Entretenimento | Pós-produção | John Smith  |

Considerando ins-abcdef1 como exemplo, podemos adicionar os três conjuntos de tags a seguir à instância:
<table id="table02">
	<tr><th>Chave da tag</th><th>Valor da tag</th></tr>
	<tr><td>dept</td><td>ecommerce</td></tr>
	<tr><td>business</td><td>mkt</td></tr>
	<tr><td>owner</td><td>John Smith</td></tr>
</table>

Da mesma forma, é possível adicionar pares de chave-valor de tags a outras instâncias com base no grupo empresarial, no escopo e nos proprietários.

### Definição de tags no console do CVM
Considere o caso anterior como exemplo. Depois de projetar os pares de chave-valor de tags, é possível fazer login no console do CVM para especificar as tags.

1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm).
2. Na página **Instance (Instância)**, selecione a instância de destino e clique em **More (Mais)** > **Instance Settings (Configurações da instância)** > **Edit Tags (Editar tags)** na coluna **Operation (Operação)**.
2. Defina as tags na seção "1 resource selected (1 recurso selecionado)" da janela pop-up.
Por exemplo, é possível adicionar [três pares de chave-valor de tags](#table02) à instância ins-abcdef1.
3. Clique em **OK**. O sistema exibe uma mensagem indicando que a modificação obteve êxito.


### Filtro de instâncias por tags

Para filtrar instâncias por tag, siga as etapas abaixo:

1. Clique na caixa de pesquisa e selecione **Tag** na lista suspensa.
2. Insira a tag e clique em <img src="https://main.qcloudimg.com/raw/3cca38f08eaa87087cdd1b81eaf08a0a.png" style="margin: 0;"> para pesquisar.
É possível filtrar as instâncias usando as tags. Por exemplo, é possível pesquisar as instâncias vinculadas às tags `key1` ou `key2` digitando `Tag: key1|key2` na caixa de pesquisa.
