## Visão geral da funcionalidade

Por padrão, o CDN do Tencent Cloud ativa as versões 1.0/1.1/1.2 do TLS e desativa a versão 1.3 do TLS. É possível ativar e desativar as versões do TLS conforme necessário.

>!
>- Certifique-se de que o certificado HTTPS esteja configurado corretamente.
>- No momento, a configuração da versão do TLS está disponível apenas nas regiões da China Continental. Se a região de aceleração de um nome de domínio for "Global", as alterações na configuração entrarão em vigor apenas na China Continental.
>- Essa funcionalidade pode não estar disponível em algumas plataformas. Concluiremos a atualização do servidor o mais breve possível.



## Guia de configuração

### Visualização da configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia ***HTTPS Configuration (Configuração do HTTPS)** para localizar a seção **TLS Version Configuration (Configuração da versão do TLS)**.

Por padrão, as versões 1.0/1.1/1.2 do TLS ficam ativadas e a versão 1.3 do TLS fica desativada.

![](https://main.qcloudimg.com/raw/7445026074dc473c366db6e65b807a17.png)


### Modificação da configuração

Abra **Modify Configuration (Modificar configuração)** para ativar e desativar as versões do TLS conforme necessário.
![](https://main.qcloudimg.com/raw/0cd09ce66a94d6886d68c60f22844310.png)


**Limitações de configuração**

- Você pode ativar uma única versão ou várias versões consecutivas. Por exemplo, você pode ativar a versão 1.0, 1.1 e 1.2, mas não a versão 1.0 e 1.2.
- Pelo menos uma versão deve ser ativada.
