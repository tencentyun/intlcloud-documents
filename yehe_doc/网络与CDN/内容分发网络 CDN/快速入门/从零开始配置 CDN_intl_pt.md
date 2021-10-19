É possível se conectar ao CDN para fornecer conteúdo em seu servidor de origem para nós de serviço mais próximos dos usuários finais, que respondem diretamente às solicitações dos usuários para reduzir a latência de acesso do usuário com eficácia e melhorar a disponibilidade. 
Para configurar o CDN, é necessário criar uma conta do Tencent Cloud, ativar o CDN, adicionar um nome de domínio e configurar o CNAME. As etapas estão detalhadas neste documento.

## Etapa 1. Criar uma conta do Tencent Cloud
Se você já tem uma conta do Tencent Cloud, ignore esta etapa.
<div style="background-color:#00A4FF; width: 270px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3149.btn1">Criar uma conta do Tencent Cloud</a></div>

## Etapa 2. Ativar o serviço do CDN
#### 1. Concluir a verificação de identidade
Primeiro, os usuários registrados devem concluir a verificação de identidade para ativar o CDN. É possível verificar sua identidade no console do CDN ou no Centro de contas. Para obter mais informações sobre o processo de verificação, consulte [Guia de verificação de identidade](https://intl.cloud.tencent.com/document/product/378/3629).
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;;"><a href="https://console.cloud.tencent.com/cdn" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3149.btn2">Acessar o console do CDN</a></div><br>

![](https://main.qcloudimg.com/raw/e593cf6199d64fbcc5c6f50089778cf9.png)
#### 2. Ativar o serviço do CDN
Após concluir a verificação de identidade, você pode ativar o serviço do CDN.
(1) Selecione o modo de faturamento
O CDN do Tencent Cloud tem duas regiões de faturamento: **China Continental** e **fora da China Continental**. Para os usuários que ativaram o CDN após 7 de dezembro de 2020 às 21h30, o **bill-by-hourly traffic (faturamento por hora de tráfego)** é a única opção de faturamento. Para obter mais informações, consulte a [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/228/2949).
![](https://main.qcloudimg.com/raw/5f75a3047566df1413233c2c0ac2736f.png)
(2) Ative o CDN
Indique seu consentimento com os Termos de serviço, clique em **Activate CDN (Ativar o CDN)** e comece a usar o serviço de aceleração.
![](https://main.qcloudimg.com/raw/4b1997247ae88641d1c2af0289b7ad2a.png)

## Etapa 3. Conectar um nome de domínio
É necessário conectar seu nome de domínio empresarial para o serviço de aceleração. O CDN armazena recursos em cache do seu servidor de origem empresarial para nós de cache do CDN por meio de um nome de domínio de aceleração para obter aceleração de acesso a recursos, assim, os usuários finais podem solicitar recursos dos nós mais próximos. Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/228/5734" hotrep="document.guide.3149.linkdomain">Adição de nomes de domínio</a>.

## Etapa 4. Configurar o CNAME
Depois que seu nome de domínio estiver conectado ao CDN, será necessário concluir a configuração do CNAME em seu provedor de serviços de nomes de domínio. Após a configuração entrar em vigor, o CDN pode ser usado corretamente. Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/228/3121" hotrep="document.guide.3149.linkcname">Configuração do CNAME</a>.
