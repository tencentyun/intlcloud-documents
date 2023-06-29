## Descrição do erro

Mesmo depois que o tempo de expiração do cache do nó é definido e a pré-busca é concluída, a solicitação não atinge o cache do nó.

## Causa

1. Existem várias regras de cache, mas suas prioridades não são claras.
2. "Follow origin server (Seguir servidor de origem)" está configurado, mas o campo `Cache-Control` no servidor de origem está definido como `no-cache/no-store/private`.

## Solução

1. Defina a prioridade da regra de cache corretamente.
   Você pode definir várias regras de cache do CDN. Quanto mais baixa a posição da regra, maior a prioridade da mesma. É preciso garantir que a prioridade da regra atenda às suas expectativas para que as regras entrem em vigor conforme o esperado.
2. Defina a validade do cache corretamente.
Verifique se a validade do cache configurada no console é muito curta.
>! URLs com pouco acesso a arquivos correm o risco de serem removidos do cache do nó, mesmo que atendam a todas as regras de cache.
3. Verifique se as regras de cache atendem às suas expectativas.
	- Verifique se a configuração "Ignore Query String (Ignorar string de consulta)" em uma regra de chave de cache do CDN causa uma falha ao armazenar em cache os recursos no nó.
	- Verifique se "No cache (Sem cache)" está definido em uma regra de validade de cache do nó do CDN.
	- Verifique se o cabeçalho da solicitação do servidor de origem retorna `no-cache/no-store/private` durante o pull de origem quando o tempo de expiração definido para o cache do nó do CDN é o mesmo que no servidor de origem.

## Procedimento de solução de problemas

1. Verifique a prioridade da regra de cache (a que está na parte inferior tem a prioridade mais alta).
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, localize o nome de domínio desejado, clique em **Manage (Gerenciar)** na coluna **Operation (Operação)** para inserir a **Domain Configuration (Configuração de domínio) **, alterne para a guia **Cache Configuration (Configuração de cache)** e você poderá encontrar a **Cache Key Rule Configuration (Configuração de regra de chave de cache)**. Conforme mostrado abaixo, a prioridade da regra em que arquivos .jpg são excluídos para "Ignore Query String" é maior do que a regra em que "Ignore Query String" está configurado para todos os arquivos. Você precisa garantir que as políticas de cache de negócios atendam às configurações de prioridade.

2. Verifique a validade do cache.
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, localize o nome de domínio desejado e clique em **Manage (Gerenciar)** -> **Cache Configuration (Configuração de cache)** -> **Node Cache Validity Configuration (Configuração da validade do cache do nó)**. Conforme mostrado abaixo, se a validade definida para o cache for muito curta, a configuração do cache poderá ser tida como ineficaz. Certifique-se de que a configuração de cache atenda às suas políticas de cache de negócios.

3. Verifique as políticas de cache.
Verifique se as políticas aplicadas à configuração da regra de chave de cache e à configuração de validade do cache do nó atendem à expectativa.
Se "Seguir servidor de origem" estiver configurado, certifique-se de que o campo `Cache-Control` no servidor de origem não esteja definido como `no-cache/no-store/private`.
4. Pré-busque o recurso a ser armazenado em cache novamente. Depois que a pré-busca for concluída, solicite o recurso novamente.

