
## Descrição do problema

Meu site continua lento depois de ter sido conectado ao CDN do Tencent Cloud.

## Motivos possíveis

- 1. Você não configurou um registro CNAME para o nome de domínio conectado em um provedor de serviços de DNS; portanto, o serviço de aceleração do CDN para o nome de domínio não está em vigor. [Verifique o DNS](#step1).
- 2. A validade do cache do nó não está configurada corretamente. [Verifique a configuração de validade do cache do nó](#step2).
- 3. O URL do recurso foi acessado pela primeira vez após a ativação do CDN e teve nenhuma operação de pré-busca antes. [Realize a pré-busca do URL](#step3).
- 4. A arquitetura do site apresenta defeitos. [Otimize a arquitetura do site](#step4).



## Soluções

[](id:step1)
### Verifique o DNS
Este exemplo mostra como executar `nslookup` para verificar o registro de DNS de um nome de domínio de aceleração do CDN:
```
Execute `nslookup` para o nome de domínio de aceleração
```
![](https://main.qcloudimg.com/raw/e60f03d058f29134524166c211791568.png)
Se o nome de domínio resultante não tiver o sufixo `dnsv1.com` como mostrado acima, o serviço de aceleração do CDN para seu nome de domínio não está em vigor. Verifique o registro CNAME do nome de domínio no provedor de serviços de DNS conforme instruído em [Configuração do CNAME](https://intl.cloud.tencent.com/document/product/228/3121).

[](id:step2)
### Verifique a configuração de validade do cache do nó
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar a sua página de configuração. Mude para a guia ***Cache Configuration (Configuração de cache)** para localizar a seção **Node Cache Validity Configuration (Configuração da validade do cache do nó)**.
![](https://main.qcloudimg.com/raw/7722e07d356878b4e031984df0328759.png)

- Verifique as regras de cache do nó do recurso: se a validade é "0", muito curta ou se está configurada como "No Cache (Sem Cache)".
  As solicitações de acesso serão encaminhadas ao servidor de origem se os recursos da solicitação não forem armazenados em cache nos nós, caso em que a aceleração não é efetiva. Configure a validade do cache conforme necessário para sua empresa.
- Verifique se o cabeçalho `Cache-Control` está definido como `no-store/no-cache/private` para seu servidor de origem.
  - Se estiver, é necessário habilitar **Force Cache (Forçar cache)** para os nós do CDN, a fim de armazenar os recursos em cache conforme configurado.
  - Se **Force Cache (Forçar cache)** não estiver habilitado e o cabeçalho estiver configurado dessa forma, os nós do CDN não armazenarão os recursos em cache, mesmo que a validade do cache esteja configurada.

Para informações acerca das regras de configuração, consulte [Configuração da validade do cache do nó (nova)](https://intl.cloud.tencent.com/document/product/228/38424).

[](id:step3)
### Realize a pré-busca do URL

É normal que a velocidade seja lenta ao acessar pela primeira vez um recurso o qual não foi realizada a pré-busca antes. Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), clique em **Purge and Prefetch (Limpeza e pré-busca)** na barra lateral esquerda e, em seguida, envie o URL para pré-busca. Para obter mais informações, consulte [Pré-busca de cache](https://intl.cloud.tencent.com/document/product/228/39000).
![](https://main.qcloudimg.com/raw/83e7ceeb26fca38870fe020231542988.png)

[](id:step4)
### Otimize a arquitetura do site

As solicitações de recursos dinâmicos são sempre encaminhadas ao servidor de origem para obter os recursos mais recentes, reduzindo a velocidade de acesso. Se o seu site tiver muitos recursos dinâmicos, recomendamos separá-los dos recursos estáticos e usar o CDN apenas para seus recursos estáticos.
