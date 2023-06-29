## Descrição do erro

A taxa de acertos de tráfego em tempo real está bem abaixo da sua expectativa.

## Motivos possíveis

- O cache está limpo.
  A limpeza do cache limpa o conteúdo especificado no nó, levando a uma taxa de acertos de tráfego temporariamente baixa.
- Há novos conteúdos no servidor de origem.
  Um grande número de novos conteúdos resultará em pulls de origem por nós CDN, ocasionando uma baixa taxa de acertos de tráfego.
- Existem exceções no servidor de origem.
  Caso haja mau funcionamento, com vários erros 4XX ou 5XX, a taxa de acertos de tráfego será afetada.
- A política do cache não está configurada corretamente.
  Você deve configurá-la com base em suas necessidades de negócios.
- Range GETs está desabilitado.
  Neste caso, será efetuado pull dos arquivos em sua totalidade, em vez de várias partes, conforme solicitado durante o pull de origem, o que aumenta o tráfego de pull de origem e reduz a taxa de acertos.
- As solicitações acertam a regra da chave de cache **Ignore all (Ignorar tudo)** configurada para o nome de domínio enquanto o servidor de origem está configurado para retornar conteúdos diferentes de acordo com os parâmetros.
  Nesse caso, todos os conteúdos serão armazenados em cache e um conteúdo específico solicitado pelo parâmetro correspondente não poderá ser correspondido, diminuindo assim a taxa de acertos de tráfego.

## Soluções

1. Verifique para se certificar que o seu servidor de origem funciona corretamente.
2. É normal ver uma diminuição na taxa de acertos de tráfego quando você limpa o cache ou tem novos conteúdos no servidor de origem.
3. Não configure o servidor de origem para retornar recursos diferentes de acordo com os parâmetros de URL se a regra da chave de cache**Ignore All (Ignorar tudo)** for usada.
4. Configure a regra de cache com base em suas necessidades de negócios.

## Procedimento de solução de problemas
[](id:step1)
Etapa 1. Verifique se o seu servidor de origem é excepcional ou se o cache está limpo.
   - Se for o caso, a taxa de acertos será baixa.
   - Se não for, vá para a [Etapa 2](#step2).
[](id:step2)
Etapa 2. Verifique se o seu servidor de origem retorna conteúdos diferentes de acordo com os parâmetros de URL.
   - Se for o caso, vá para a [Etapa 3](# step3).
   - Se não for o caso, vá para a [Etapa 5](# step5).
[](id:step3)
Etapa 3. Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia ***Cache Configuration (Configuração de cache)** para localizar a seção **Cache Key Rule Configuration (Configuração da regra da chave de cache)**. Em seguida, verifique se o **Ignore parameter (Ignorar parâmetro)** está configurado como **Not ignore (Não ignorar)**.

   - Se não for o caso, vá para a [Etapa 4](# step4).
   - Se for o caso, vá para a [Etapa 5](# step5).
[](id:step4)
Etapa 4. Clique em **Modify (Modificar)** à direita da regra, marque **Not ignore (Não ignorar)** e clique em **Save (Salvar)**.

>? Se essa operação não for adequada para a sua empresa, é possível usar a funcionalidade **Reserve Specified Parameter (Reservar o parâmetro especificado)** conforme necessário. Para obter mais informações, consulte [Configuração da regra da chave de cache](https://intl.cloud.tencent.com/document/product/228/35316).
>
[](id:step5)
Etapa 5. Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar a sua página de configuração. Abra a aba **Cache Configuration (Configuração de cache)** para localizar a seção **Node Cache Validity Configuration (Configuração da validade do cache do nó)** e verifique se as regras de cache configuradas atendem às suas necessidades de negócios.
   - Se for o caso, execute a [etapa 5](#step5).
   Se não for o caso, consulte [Configuração de regra de cache do nó] (https://intl.cloud.tencent.com/document/product/228/38424) e defina as regras conforme necessário.
