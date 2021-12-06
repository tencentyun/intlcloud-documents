O CLB permite o redirecionamento da camada 7, para que você possa configurar o redirecionamento nos listeners HTTP/HTTPS da camada 7.
>?
>- Persistência de sessão: se o cliente acessar `example.com/bbs/test/123.html` e a persistência de sessão tiver sido ativada no CVM de back-end, após o redirecionamento ser ativado para encaminhar o tráfego para `example.com/bbs/test/456.html`, o mecanismo de persistência de sessão original não terá efeito.
- Redirecionamento TCP/UDP: atualmente, o redirecionamento no nível de IP e porta não é aceito, mas estará disponível em versões posteriores.
## Visão geral do redirecionamento
1. Redirecionamento automático
  - Visão geral
  Para um listener `HTTPS:443` existente, um listener HTTP (porta 80) será criado automaticamente pelo sistema para encaminhamento. As solicitações enviadas para `HTTP:80` serão redirecionadas automaticamente para `HTTPS:443`.
  - Caso de uso
 Redirecionamento de HTTPS forçado, ou seja, redirecionar solicitações de HTTP para HTTPS. Quando um usuário acessa um serviço da web em um PC ou navegador móvel pelo HTTP, o CLB redireciona todas as solicitações enviadas a `HTTP:80` para `HTTPS:443`, para encaminhamento.
  - Vantagens do esquema
		- Configuração definir e esquecer: o redirecionamento HTTPS forçado pode ser implementado para um nome de domínio com apenas uma operação de configuração necessária.
		- Atualização prática: se a quantidade de URLs do serviço HTTPS mudar, basta usar essa funcionalidade novamente no console para atualizar.
2. Redirecionamento manual
 - Visão geral
Você pode configurar o redirecionamento 1 para 1. Por exemplo, em uma instância do CLB, você pode configurar o redirecionamento de `listener 1 / nome de domínio 1 / URL 1` para `listener 2 / nome de domínio 2 / URL 2`.
 - Caso de uso
Redirecionamento de caminho único. Por exemplo, se você deseja desativar temporariamente seu negócio na web em casos como produtos esgotados, manutenção de página ou atualização e upgrade, a página original precisa ser redirecionada para uma nova página. Se nenhum redirecionamento for executado, o endereço antigo nos favoritos do visitante e no banco de dados do mecanismo de pesquisa retornará uma página de mensagem de erro `404/503`, degradando a experiência do usuário e resultando em desperdício de tráfego.

## Redirecionamento automático
O CLB permite o redirecionamento forçado com um clique de HTTP para HTTPS.
Suponha que você precise configurar o site `https://www.example.com`, para que os usuários finais possam visitá-lo com segurança via HTTPS, não importando se eles enviam solicitações HTTP (`http://www.example.com`) ou HTTPS (`https://www.example.com`) no navegador.
### Pré-requisitos
O listener `HTTPS:443` foi configurado.
### Instruções
1. Configure o listener HTTPS do CLB no [Console do CLB](https://console.cloud.tencent.com/clb) e configure o ambiente web de `https://example.com`. Para obter mais informações, consulte [Configuração de um listener HTTPS
](https://intl.cloud.tencent.com/document/product/214/32516).
2. O resultado da configuração do listener HTTPS é conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/6eaf2d1220d140bc37537f3388d78509.png)
3. Na guia "Redirection Configuration (Configuração de redirecionamento)" nos detalhes da instância do CLB, clique em **Create Redirection Configuration (Criar configuração de redirecionamento)**.
![](https://main.qcloudimg.com/raw/47fa6c0bd8b6f060332333b2685f8efe.png)
4. Selecione **Automatic Redirection Configuration (Configuração de redirecionamento automático)**, selecione o listener HTTPS e o nome de domínio configurados e clique em **Next: Configure Path (Avançar: Configurar caminho)**.
![](https://main.qcloudimg.com/raw/4481d9beac8fa51ee7f6c252c3714a41.png)
5. Clique em **Submit (Enviar)** para concluir a configuração.
![](https://main.qcloudimg.com/raw/435e1389eadacc7bc90966480a29a131.png)
6. O resultado após a configuração do redirecionamento é conforme mostrado abaixo. Como você pode observar, o listener `HTTP:80` foi configurado automaticamente para o listener `HTTPS:443`, e todo o tráfego HTTP será redirecionado de forma automática para HTTPS.
![](https://main.qcloudimg.com/raw/c3249968deb68888fb591e59289194d9.png)

## Redirecionamento manual
O CLB aceita a configuração de redirecionamento 1 para 1.
Por exemplo, sua empresa usa uma página `forsale` para uma campanha promocional e precisa redirecionar a página da campanha `https://www.example.com/forsale` para a nova página inicial `https://www.new.com/index` após o término da campanha.

### Pré-requisitos
- Um listener HTTPS foi configurado.
- O nome de domínio encaminhado `https://www.example.com/forsale` foi configurado.
- O nome de domínio encaminhado e o caminho `https://www.new.com/index` foi configurado.


### Instruções
1. Configure o listener HTTPS do CLB no [Console do CLB](https://console.cloud.tencent.com/clb) e configure o ambiente web de `https://example.com`. Para obter mais informações, consulte [Configuração de listener HTTPS](https://intl.cloud.tencent.com/document/product/214/32516).
2. O resultado da configuração do HTTPS é conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/5c1fc217e1795a2f6a7b31c2a7ba3bfc.png)
3. Na guia "Redirection Configuration (Configuração de redirecionamento)" nos detalhes da instância do CLB, clique em **Create Redirection Configuration (Criar configuração de redirecionamento)**.
![](https://main.qcloudimg.com/raw/47fa6c0bd8b6f060332333b2685f8efe.png)
4. Selecione **Manual Redirection Configuration (Configuração de redirecionamento manual)**, selecione a porta do protocolo de front-end originalmente acessada `HTTPS:443` e o nome do domínio `https://www.example.com/forsale`, selecione a porta do protocolo de front-end `HTTPS:443` e o nome do domínio `https://www.new.com/index` após o redirecionamento e clique em **Next: Configure Path (Avançar: Configurar caminho)**.
![](https://main.qcloudimg.com/raw/51106736b5ee61d6e87767652185d57a.png)
5. Selecione `/forsale` para o caminho de acesso original e `/index` para o caminho de acesso após o redirecionamento, e clique em **Submit (Enviar)** para concluir a configuração.
![](https://main.qcloudimg.com/raw/5f59b88ecc291d912b7faf2cf1d3770e.png)
6. O resultado da configuração de redirecionamento é conforme mostrado abaixo. Como você pode observar, no listener `HTTPS:443`, `https://www.example.com/forsale` foi redirecionado para `https://www.new.com/index`.
![](https://main.qcloudimg.com/raw/34364863bd44202df54e89ec3cb923f9.png)

