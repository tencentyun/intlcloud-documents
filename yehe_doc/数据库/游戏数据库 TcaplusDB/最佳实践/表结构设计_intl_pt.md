O design do banco de dados é importante no ciclo de vida de desenvolvimento de software. Este documento traz diretrizes e práticas recomendadas para o design de banco de dados.

## Diretrizes para definição da estrutura da tabela
- O nome de um campo ou tabela não deve conter nenhum caractere especial e o comprimento recomendado não deve ser superior a 32 bytes.
- O nome de um campo ou tabela deve ser significativo e evitar abreviações ambíguas, se possível.
- Você deve escolher os tipos de dados corretos e não perder a precisão necessária dos números.
- As chaves primárias e shardkeys devem ser altamente discretas para facilitar o balanceamento de carga e o escalonamento.
- A quantidade de índices que você cria depende das consultas de que precisa. Os índices não devem ter a mesma definição com as chaves primárias.
- Recomendamos o tipo INT para os endereços IP da sua empresa.
- Recomendamos o tipo LONG para armazenar dados de tempo em segundos.
- Para garantir a atomicidade da operação, recomendamos que os campos relacionados logicamente estejam na mesma tabela.
- Se você requer altos requisitos de desempenho do banco de dados, você pode adotar um design de redundância de dados.
- As chaves primárias e shardkeys devem ser altamente discretas para facilitar o escalonamento.
- As chaves primárias devem ser legíveis para consultas e solução de problemas mais fáceis. Não recomendamos chaves primárias binárias.
- De preferência, use chaves primárias curtas, se possível, o que torna as consultas mais rápidas.
- Você deve definir o tamanho de um campo de acordo com suas necessidades. Evite casos em que um campo definido com tamanho grande seja preenchido com um valor pequeno.
- Você deve adicionar comentários a todas as tabelas e campos.

## Diretrizes para design de banco de dados de jogos
- Se um banco de dados precisar gerar IDs globalmente exclusivos, recomendamos o comando `increase`.
- Você deve evitar sobrecargas de banco de dados ao projetar a arquitetura do banco de dados. Por exemplo, você pode adicionar um mecanismo de enfileiramento.
- Você deve armazenar dados relevantes na mesma tabela para evitar inconsistência de dados.
- Não recomendamos implementar todas as funcionalidades em uma única tabela. Uma funcionalidade independente requer a própria tabela.
- Se uma tabela é usada com frequência e possui uma grande quantidade de registros, você precisa projetar uma tabela de perfil para evitar que o aplicativo acesse os dados da tabela original, diminuindo assim a carga do banco de dados.
- Como o chat no lobby do jogo pode compartilhar a memória e o chat em um único jogo pode ser acessado em tempo real, não recomendamos o uso de bancos de dados em tais cenários. Mas os bancos de dados são adequados para chat privado offline.
- Recomendamos usar o tipo de matriz fornecido por bancos de dados para lidar com dados históricos de jogos, e-mails e relatórios. Este tipo de dados aceita enfileirar/retirar da fila e `TopN` na ordem em que os dados são enfileirados.
- Recomendamos usar o componente de classificação no design da lista de classificação. Se a funcionalidade de classificação for implementada no servidor do jogo, recomendamos armazenar os resultados da classificação em bancos de dados de forma assíncrona.
- Uma operação marginal e demorada no jogo precisa de um processo diferente, e que pode evitar impactos na lógica principal do servidor do jogo.
- O ciclo de desenvolvimento de um jogo é longo e complexo em termos de lógica. Durante o processo de desenvolvimento, a estrutura lógica dos dados provavelmente mudará. Para escalabilidade e facilidade de manutenção, recomendamos que os dados mutáveis sejam definidos como dados BLOB na fase de design da tabela de banco de dados do jogo. Esse tipo de dados é serializado antes de ser armazenado em bancos de dados para evitar mudanças frequentes nas tabelas do banco de dados devido a mudanças na estrutura de dados.

## Definição de tabela do TDR
- As chaves primárias devem ser tão discretas que as solicitações do servidor do jogo possam ser distribuídas para vários nós da camada de acesso.
- Não recomendamos que as chaves primárias sejam idênticas às chaves de índice na definição da tabela, porque chaves idênticas desperdiçam recursos de rede e disco.
- Para definir campos de chave não primária como matrizes, o atributo `refer` deve ser adicionado (`count` é o tamanho definido, e `refer` é o tamanho real), para que o tamanho de `count` possa ser expandido posteriormente, e a pegada de dados na transmissão de rede e em discos possa ser reduzida.
- A profundidade de aninhamento dos campos é limitada a três e os campos de chave não primária devem estar no primeiro nível de aninhamento.
- Os campos de chave primária binários não são recomendados, pois funcionam de maneira ineficiente na solução de problemas.
- Podem ser definidos até oito índices por tabela. Recomendamos dois ou três índices por tabela. Muitos índices reduzirão o desempenho do banco de dados, portanto, defina os índices com base em suas necessidades.

## Definição de tabela do Protocolo Buffers
- As chaves primárias devem ser tão discretas que as solicitações do servidor do jogo possam ser distribuídas para vários nós da camada de acesso.
- Os campos de chave não primária podem ser definidos como estruturas aninhadas. O acesso aos dados será comprometido se o nível de aninhamento for muito profundo.

## Exemplos de design obsoleto
- Designs incapazes de atender às demandas
Esses designs levam a muitas modificações. Para projetos logo antes da fase de entrada em operação, o custo de modificação é ainda maior.
- Baixo desempenho
Existem muitas restrições entre tabelas com grandes quantidades de dados; as instruções de consulta SQL são complexas devido à falta de campos bem projetados para consultas; não existe um método eficaz para lidar com tabelas com grandes quantidades de dados; há muitas visualizações ou as visualizações não são usadas de maneira eficiente.
- Perda de integridade de dados
As chaves primárias ou externas mal projetadas causam erros de programa após as operações de atualização e exclusão; dados que foram excluídos ou descartados são usados.
- Pouca escalabilidade
A tabela tem alta afinidade com o negócio e não tem capacidade de escalar, se adaptar às mudanças ou atender a novas demandas.
- Muitos dados inúteis redundantes
Muitos dados inúteis redundantes consomem recursos e reduzem a eficiência das consultas.
- Campos ineficientes em cálculos ou estatísticas
Não há campos projetados para cálculos ou estatísticas; os campos usados para cálculos e estatísticas estão espalhados por várias tabelas, tornando o processo de cálculo e estatísticas complicado ou mesmo impossível.
- Não há registros de dados detalhados
Não há campos que possam ser usados para rastrear alterações de dados e operações do usuário ou analisar dados.
- Acoplamento estreito entre as tabelas
As tabelas são altamente dependentes umas das outras. As alterações em uma tabela afetarão outras.
- Campos mal projetados
O comprimento de um campo é muito curto ou o tipo de um campo é difícil de alterar posteriormente. Esses campos reduzirão a escalabilidade.



