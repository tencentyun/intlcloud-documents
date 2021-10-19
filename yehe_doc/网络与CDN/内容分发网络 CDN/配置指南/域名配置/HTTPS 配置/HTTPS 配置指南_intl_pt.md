## Visão geral das configurações
O CDN do Tencent Cloud aceita o serviço de aceleração de HTTPS. Você pode fazer upload de certificados para implantá-los ou implantar diretamente certificados hospedados no SSL Certificate Service do Tencent Cloud para a plataforma do CDN. Dessa forma, você pode habilitar o serviço de aceleração de HTTPS para implementar a transferência de dados criptografados em toda a rede.

## Guia de configuração
### Visualização da configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração e abra a guia **HTTPS Configuration (Configuração de HTTPS)**.
![](https://main.qcloudimg.com/raw/df6c4966cfee58661251f88550214576.png)
Você pode selecionar **Certificate Management (Gerenciamento de certificados)** na barra lateral esquerda para visualizar todos os nomes de domínio configurados com aceleração de HTTPS em sua conta.
![](https://main.qcloudimg.com/raw/91335ed0a426118b76ad6b27a53d5197.png)

### Configuração de um certificado
#### 1. Selecionar um nome de domínio
Na página **Certificate Management (Gerenciamento de certificado)**, clique em **Configure Certificate (Configurar certificado)** e selecione o nome do domínio de aceleração a ser configurado com um certificado:
+ O status do nome de domínio de aceleração deve ser "Deploying (Em implementação)" ou "Enabled (Ativado)". Os nomes de domínio desativados não podem ser configurados com a aceleração de HTTPS.
+ Os nomes de domínio com o sufixo `.file.myqcloud.com` são os nomes de domínio de aceleração padrão do COS do Tencent Cloud e podem usar a aceleração de HTTPS sem configurar nenhum certificado.
+ Os nomes de domínio com o sufixo `.image.myqcloud.com` são os nomes de domínio de aceleração padrão do CI do Tencent Cloud e podem usar a aceleração de HTTPS sem configurar nenhum certificado.

![](https://main.qcloudimg.com/raw/13c71dc1fc13576620768f7ae61d6c9e.png)

#### 2. Selecionar um certificado
Se houver um certificado existente no formato PEM, você pode colar diretamente o conteúdo do certificado e a chave privada nos campos correspondentes:
+ O CDN aceita a implantação de certificado ECC.
+ O conteúdo do certificado deve estar no formato PEM. Se não estiver, consulte [Conversão de outros formatos para PEM](https://intl.cloud.tencent.com/document/product/228/35212).
+ Você pode selecionar um certificado hospedado pelo Tencent Cloud para implantação rápida.

![](https://main.qcloudimg.com/raw/d847eb87f076b972808b8e680705f706.png)



### Configuração em lotes
Clique em **Batch Configuration (Configuração em lote)** na parte superior. Você pode fazer upload de certificados para corresponder automaticamente aos nomes de domínio para configuração em lote:
#### 1. Selecionar um certificado
Se houver um certificado existente no formato PEM, você pode colar diretamente o conteúdo do certificado e a chave privada nos campos correspondentes:
+ O CDN aceita a implantação de certificado ECC.
+ O conteúdo do certificado deve estar no formato PEM. Se não estiver, consulte [Conversão de outros formatos para PEM](https://intl.cloud.tencent.com/document/product/228/35212).
+ Você pode selecionar um certificado hospedado pelo Tencent Cloud para implantação rápida.

![](https://main.qcloudimg.com/raw/fcadb92849ebd780acbbc5b35f343478.png)

#### 2. Selecionar um nome de domínio
Com base no certificado carregado ou selecionado, o CDN corresponderá automaticamente aos nomes de domínio que permitem a configuração. Você pode selecionar os nomes de domínio para configuração conforme necessário:
![](https://main.qcloudimg.com/raw/04a8ad1088655f24282201da7b5ebd74.png)



### Alteração de um certificado
#### Modificação de um certificado
Clique em **Edit (Editar)** à direita de um certificado para atualizá-lo para o nome de domínio especificado. Também é possível reconfigurar certificados em lotes para substituir as configurações de certificado originais.
![](https://main.qcloudimg.com/raw/bb2ed5ec740aa67abf2750dc58baae0d.png)
As atualizações de certificado entrarão em vigor nos nós, um a um, em toda a rede, sem afetar o serviço de HTTPS no ambiente de produção. Você também pode clicar em **Delete (Excluir)** para cancelar o serviço de aceleração de HTTPS.

#### Expiração de certificado
O Tencent Cloud enviará lembretes de expiração por SMS, e-mail e pelo Centro de Mensagens 30, 15 e 7 dias antes da expiração de seu certificado e no dia da expiração. Atualmente, os destinatários de lembretes sobre certificados SSL podem ser personalizados. Acesse a página [Assinatura de mensagens](https://console.cloud.tencent.com/message/subscription) para a configuração.

### Configuração específica da região
Se o seu nome de domínio estiver configurado para a aceleração global, o certificado HTTPS configurado terá efeito global. Atualmente, os certificados configurados para as regiões dentro e fora da China Continental devem ser os mesmos.

Se um nome de domínio tiver certificados diferentes dentro/fora da China Continental, você verá as tags da China Continental e de fora da China Continental na página **Certificate Management (Gerenciamento de certificado)**, o que indica que os nomes de domínio com tags têm configurações herdadas diferentes.

Na guia **Advanced Configuration (Configuração avançada)** do nome de domínio, você também pode ver duas configurações:


