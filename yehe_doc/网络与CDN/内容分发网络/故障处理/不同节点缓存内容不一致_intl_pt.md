## Descrição do erro

Os usuários em outras regiões recebem conteúdos diferentes para o mesmo URL de recurso.

## Motivos possíveis

- Motivo 1: a chave de cache foi configurada para **Filter All (Filtrar tudo)** para o nome de domínio, e o servidor de origem foi configurado para retornar recursos diferentes de acordo com os parâmetros.
  Nesse caso, nós diferentes podem armazenar em cache conteúdos diferentes devido aos parâmetros diferentes de suas primeiras solicitações de acesso recebidas. Quando a mesma solicitação acessa um nó diferente, o conteúdo retornado será diferente. 

- Motivo 2: o recurso solicitado não foi limpo depois de ter sido atualizado no servidor de origem.
  O CDN armazena recursos em cache com base no URL. Se o conteúdo no servidor de origem for atualizado, mas o URL não for alterado, quando um usuário enviar uma solicitação ao URL, o conteúdo armazenado em cache no nó anteriormente será retornado. Além disso, a frequência de acesso varia por região, de modo que a validade do cache de recursos pode ser diferente em cada região. Quando uma solicitação do usuário acessa um nó de cache, se o recurso solicitado no nó expirar, a solicitação será encaminhada ao servidor de origem, será efetuado pull do conteúdo mais recente e ele será retornado. Alguns nós têm o conteúdo mais recente, já outros possuem o conteúdo herdado.  

## Soluções

1. Não configure o servidor de origem para retornar recursos diferentes de acordo com os parâmetros de URL se a chave de cache "Filter All (Filtrar tudo)" for usada.
2. Limpe o recurso de URL após ele ser atualizado no servidor de origem.

## Procedimento de solução de problemas

Etapa 1. Verifique se o seu servidor de origem retorna recursos diferentes de acordo com os parâmetros de URL.
   - Se retornar, vá para a [Etapa 2](##step2).
   - Se não retornar, vá para a [Etapa 4](#step4).

[](id:step2)
Etapa 2. Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia **Cache Configuration (Configuração de cache)** para localizar a seção **Cache Key Configuration (Configuração da chave de cache)** e verifique se **Ignore Query String (Ignorar string de consulta)** está configurado como **Not Filter (Não filtrar)**.

   - Se não estiver, vá para a [Etapa 3](##step3).
   - Se estiver, vá para a [Etapa 4](#step4).



[](id:step3)
Etapa 3. Clique em **Modify (Modificar)** à direita da regra, marque **Not Filter (Não filtrar)** e clique em **Save (Salvar)**.

> ?Se essa operação não for adequada para a sua empresa, é possível usar a funcionalidade **Reserve Specified Parameter (Reservar o parâmetro especificado)** conforme necessário. Para obter mais informações, consulte [Configuração da chave de cache](https://intl.cloud.tencent.com/document/product/228/35316).

[](id:step4)
Etapa 4. Clique em **Purge and Prefetch (Limpeza e pré-busca)** na barra lateral esquerda para limpar o recurso que foi atualizado no servidor de origem.

> ?Também é possível vincular a API para a limpeza de recursos, de forma que os recursos possam ser limpos em toda a rede imediatamente após a atualização, garantindo a consistência do conteúdo para acesso. Para obter mais informações, consulte [PurgeUrlsCache](https://intl.cloud.tencent.com/document/product/228/33601) e [PurgePathCache](https://intl.cloud.tencent.com/document/product/228/33602).
