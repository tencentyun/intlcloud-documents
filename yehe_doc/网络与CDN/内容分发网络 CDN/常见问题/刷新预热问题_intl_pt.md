[](id:q6)
### Quando preciso realizar a limpeza e a pré-busca?
- Limpeza: Para garantir que os usuários acessem os recursos mais recentes quando houver recursos a serem atualizados, recursos restritos a serem removidos ou configurações de nome de domínio a serem alteradas em seu servidor de origem, você pode enviar uma tarefa de limpeza, que pode impedir o acesso de usuários a recursos ou configurações antigas do cache do nó. Para obter mais informações, consulte [Limpeza  do cache](https://intl.cloud.tencent.com/document/product/228/6299).
- Pré-busca: Para atividades operacionais, pacotes de instalação ou pacotes de atualização para lançamento, você pode enviar uma tarefa de pré-busca para pré-buscar recursos estáticos para nós de aceleração de CDN, o que reduzirá a tensão no servidor de origem e melhorará a disponibilidade do serviço e a experiência do usuário. Para obter mais informações, consulte [Pré-busca de cache](https://intl.cloud.tencent.com/document/product/228/39000).

[](id:q1)
### Quais são as diferenças entre limpeza e pré-busca?
- Depois que um recurso é limpo, seu cache será excluído em todos os nós CDN em toda a rede. Quando uma solicitação de usuário chega a um nó, o nó irá extrair o recurso correspondente do servidor de origem, retorná-lo ao usuário e armazená-lo em cache no nó para garantir que o usuário possa obter o recurso mais recente.
- Quando é realizada a pré-busca de um recurso, ele será armazenado em cache antecipadamente para todos os nós do CDN em toda a rede. Quando uma solicitação do usuário chega a um nó, o recurso pode ser obtido diretamente no nó.

[](id:q2)
### Quais são os requisitos para limpeza e pré-busca? Quanto tempo demoram para fazer efeito?
- Limpeza de cache
	- Limpeza de URL: no máximo 10.000 URLs podem ser limpos por dia e no máximo 1.000 URLs podem ser enviados para cada limpeza. Leva cerca de 5 minutos para que a limpeza entre em vigor. Se o período de validade do cache configurado para o arquivo for inferior a 5 minutos, recomendamos que você aguarde o tempo limite e a atualização em vez de usar a ferramenta de limpeza.
	- Limpeza de diretório: no máximo 100 diretórios podem ser limpos por dia e no máximo 20 diretórios de URL podem ser enviados para cada limpeza. Leva cerca de 5 minutos para que a limpeza entre em vigor. Se o período de validade do cache configurado para a pasta for inferior a 5 minutos, recomendamos que você aguarde o tempo limite e a atualização em vez de usar a ferramenta de limpeza.
- Recurso de pré-busca
	- Pré-busca de URL: É possível realizar a pré-busca de no máximo 1.000 URLs por dia e no máximo 20 URLs podem ser enviados para cada tarefa de pré-busca. Leva cerca de 5 a 30 minutos para que a pré-busca entre em vigor, dependendo do tamanho do arquivo.

[](id:q3)
### ### O cache será atualizado nos nós do CDN em tempo real?
Não. O conteúdo armazenado em cache nos nós de cache do CDN é atualizado com base na [validade do cache](https://intl.cloud.tencent.com/document/product/228/38424) que você configurou no console. Se você precisar atualizar o cache de um arquivo em tempo real, use a [limpeza de cache](https://intl.cloud.tencent.com/document/product/228/6299).



[](id:q5)
### Como vejo o histórico de limpeza e pré-busca do cache?
Você pode verificar o histórico de limpeza e pré-busca do cache no console do CDN. Para obter mais informações, consulte [Histórico](https://intl.cloud.tencent.com/document/product/228/42176).

[](id:q6)
### Posso realizar a pré-busca com cabeçalhos de solicitação personalizados?
Não. 

