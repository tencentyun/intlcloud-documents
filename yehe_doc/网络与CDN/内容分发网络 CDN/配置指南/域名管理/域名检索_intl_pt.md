## Cenários de operação
É possível usar a funcionalidade de pesquisa de nomes de domínio para localizar um nome de domínio específico. Você pode filtrar nomes de domínio por vários critérios tais como nome de domínio, servidor de origem, tag e projeto, assim como várias palavras-chave.
> Uma tag é fornecida pelo Tencent Cloud para identificar os recursos na nuvem. Para obter mais informações sobre as tags e como gerenciá-las, consulte [Tag](https://intl.cloud.tencent.com/document/product/651).

## Instruções
1. Faça login no [console do CDN](https://console.cloud.tencent.com/cdn) e clique em **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda para acessar a página de gerenciamento.
2. Clique na caixa de pesquisa de nomes de domínio para ativar a funcionalidade de pesquisa, selecione um ou mais atributos de recursos, como nome de domínio, servidor de origem, tag ou projeto, e insira um valor para filtrar os nomes de domínio.
![](https://main.qcloudimg.com/raw/5f77724408026bd05f2d1ac14b9f8b86.png)
3. Se você tiver dúvidas sobre o atributo de recurso de entrada ou o formato de entrada, clique no ícone **i** para obter [ajuda com a pesquisa](#help).
![](https://main.qcloudimg.com/raw/b633c3602cc79891cd9ad2e0c11323f9.png)

>
>+ Apenas servidores de origem mestre podem ser pesquisados. Os servidores escravos não podem.
>+ Use ponto e vírgula (;) para separar os endereços IP do servidor de origem ao pesquisar vários servidores de origem.
>+ Apenas a pesquisa de uma única palavra-chave é compatível com nomes de domínio e servidores de origem.

## Descrição da pesquisa
+ Pesquisar por nome de domínio: insira um nome de domínio completo ou parcial para pesquisa. A pesquisa difusa é compatível.
![](https://main.qcloudimg.com/raw/95ff6e4da21cfa031a625146bf912b4b.png)
+ Pesquisar por servidor de origem: insira um servidor de origem completo ou parcial para pesquisa. A pesquisa difusa é compatível.
+ Pesquisar por tag: insira uma tag completa, e uma lista de nomes de domínio que contêm a tag inserida será retornada. A pesquisa difusa não é compatível.
+ Pesquisar por projeto: é possível selecionar vários projetos como filtro.
![Project](https://main.qcloudimg.com/raw/bdcaa7725595005fd1b49c3953559437.png)
- Filtrar por vários critérios: é possível selecionar um ou mais critérios, como tag, nome de domínio, servidor de origem e projeto para filtragem. Use a tecla Enter para separar vários critérios.
- Filtrar por várias palavras-chave: é possível inserir várias palavras-chave para cada critério de filtro. Use a barra vertical (|) para separar várias palavras-chave.

<span id=help></span>
## Ajuda com a pesquisa
<style>
table th:first-of-type {
    width: 110px;
}
table th:nth-of-type(2) {  
width: 240px;
}
</style>

| Tipo               | Formato de entrada                                             | Exemplo                    | Exemplo de caixa de pesquisa                                                  | Descrição                                                         |
| ----------------- | --------------------------------------------------- |----------------------- | ----------------------------------------------------------- | ------------------------------------------------------------ |
|   Palavra-chave única      | **Palavra-chave**                                           | www.test.com             |  ![Single keyword](https://main.qcloudimg.com/raw/af1f1771fd42f0a38df5c7a0bc9bc861.png)| Filtra nomes de domínio contendo `www.test.com`                           |
| Atributo de nome de domínio único        | **Atributo**:**palavra-chave**                                  | Servidor de origem:1.1.1.1            | ![Single domain name attribute](https://main.qcloudimg.com/raw/95eab4659fde0526a6ff7b82b4dae03b.png) | Filtra os nomes de domínio em que o servidor de origem contém 1.1.1.1                                  |
| Atributos de vários nomes de domínio       | **Atributo**:**palavra-chave** **código de fim de linha**<br>**Atributo**:**palavra-chave** | Domain name:test<br>Servidor de origem:1.1.1.1 | ![Multiple domain name attributes](https://main.qcloudimg.com/raw/1e199e5b7a5268ee3e0b458b7db1fa76.png) | Filtra os nomes de domínio em que o nome do domínio contém "test" e o servidor de origem contém "1.1.1.1"              |
| Atributo de nome de domínio único com várias palavras-chave | **Atributo**:**palavra-chave**\|**palavra-chave**                      | Projeto:test1\|test2   | ![Single domain name with multiple keywords](https://main.qcloudimg.com/raw/22a61295630849332aac815db4a6a039.png) | Filtra os nomes de domínio em que o nome de domínio contém "test1" ou "test2" do projeto selecionado. Atualmente, os atributos de nome de domínio e do servidor de origem não aceitam a pesquisa com várias palavras-chave |
| Caractere copiado           | (Caractere colado)                                       | test abc                 | ![Copy](https://main.qcloudimg.com/raw/823aeda4c1e1f43dc2fa3cec34b8c29f.png) | Filtra os nomes de domínio que contém "test" ou "abc"                               |

>O CDN não consegue fazer pesquisas globais se nenhum atributo for inserido. Portanto, o atributo **domain name** é adicionado para pesquisa por padrão. Em outras palavras, ao inserir uma única palavra-chave, o conteúdo da caixa de pesquisa será `domain name:www.test.com`; ao copiar caracteres, o conteúdo da caixa de pesquisa será `domain name:test|abc`.

