### O que é a limpeza de cache?
A limpeza de cache inclui a limpeza de URL, a limpeza de diretório e a pré-busca de URL. Para obter mais informações, consulte [Limpeza de cache](https://intl.cloud.tencent.com/document/product/228/6299).
- A limpeza de URL significa limpar o cache, arquivo por arquivo.
- A limpeza de diretório significa limpar todos os arquivos em um diretório, arquivo por arquivo.
- A pré-busca de URL significa realizar a pré-busca de recursos, arquivo por arquivo.

Limpeza vs. pré-busca:
- Depois que um recurso é limpo, seu cache em todos os nós do CDN, em toda a rede, será excluído. Quando uma solicitação do usuário chega a um nó, o nó efetua o pull do recurso correspondente do servidor de origem, o retorna ao usuário e o armazena em cache no nó para garantir que o usuário possa obter o recurso mais recente.
- Quando é realizada a pré-busca de um recurso, ele será armazenado em cache antecipadamente para todos os nós do CDN em toda a rede. Quando uma solicitação do usuário chega a um nó, o recurso pode ser obtido diretamente no nó.


### Quais são os requisitos para a limpeza do cache? Quanto tempo leva para ela entrar em vigor?
A limpeza de cache inclui a limpeza de URL, a limpeza de diretório e a pré-busca de URL.
- Limpeza de URL: no máximo 10.000 URLs podem ser limpos por dia e no máximo 1.000 URLs podem ser enviados para cada limpeza. Leva cerca de 5 minutos para que a limpeza entre em vigor. Se o período de validade do cache configurado para o arquivo for inferior a 5 minutos, recomendamos que você aguarde o tempo limite e a atualização em vez de usar a ferramenta de limpeza.
- Limpeza de diretório: no máximo 100 diretórios podem ser limpos por dia e no máximo 20 diretórios de URL podem ser enviados para cada limpeza. Leva cerca de 5 minutos para que a limpeza entre em vigor. Se o período de validade do cache configurado para a pasta for inferior a 5 minutos, recomendamos que você aguarde o tempo limite e a atualização em vez de usar a ferramenta de limpeza.
- Pré-busca de URL: se o recurso já foi armazenado em cache no nó e não expirou, ele não será atualizado para a versão mais recente. Se você precisar atualizar os recursos em todos os nós do CDN para as versões mais recentes, poderá limpá-los antes da pré-busca. É possível realizar a pré-busca de no máximo 1.000 URLs por dia e no máximo 20 URLs podem ser enviados para cada pré-busca. Leva cerca de 5 a 30 minutos para que a pré-busca entre em vigor, dependendo do tamanho do arquivo.

### O conteúdo armazenado em cache nos nós de cache do CDN será atualizado em tempo real?
Não. O conteúdo em cache nos nós de cache do CDN é atualizado com base na [Configuração de expiração do cache](https://intl.cloud.tencent.com/document/product/228/35317) que você configurou no console. Se você precisar atualizar o cache de um arquivo em tempo real, use a [Limpeza de cache](https://intl.cloud.tencent.com/document/product/228/6299).

### O CDN aceita a limpeza de diretório?
Sim. O CDN aceita a limpeza de URL, a limpeza de diretório e a pré-busca de URL.
Método 1: Você pode realizar a limpeza do diretório no [console do CDN](https://console.cloud.tencent.com/cdn/refresh). Para obter mais informações, consulte [Limpeza de cache](https://intl.cloud.tencent.com/document/product/228/6299).
Método 2: Faça a limpeza de URL chamando a API [PurgePathCache](https://intl.cloud.tencent.com/document/product/228/33602).

### Como vejo o histórico de limpeza do cache?
Você pode verificar o histórico de limpeza do cache no console do CDN. Para obter mais informações, consulte o **Guia de operação** em [Limpeza de cache](https://intl.cloud.tencent.com/document/product/228/6299#notes).

