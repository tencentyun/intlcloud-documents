

## Visão geral das configurações

O HTTP Strict Transport Security (HSTS) é um protocolo de segurança da web promovido pelo Institution of Electronics and Telecommunication Engineers (IETE). Ele força o cliente (por exemplo, um navegador) a usar o HTTPS para criar uma conexão com o servidor, com o objetivo de ajudar a criptografar o site globalmente.

## Limitações de configuração

- `expireTime` pode variar de 0 a 365 dias e é configurado em segundos.
- Marque `includeSubDomain` se precisar incluir nomes de subdomínio.
- Para ativar a configuração do HSTS, a configuração de aceleração do HTTPS deve ser concluída primeiro.
- Após a ativação da configuração do HSTS, recomendamos ativar a [Configuração de redirecionamento forçado](https://intl.cloud.tencent.com/document/product/228/35214) para redirecionar as solicitações do HTTP para o HTTPS. Caso contrário, o navegador não criará cache do HSTS para as solicitações do HTTP.

## Guia de configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia **HTTPS Configuration (Configuração do HTTPS)** para localizar a seção **HSTS Configuration (Configuração do HSTS)**. Por padrão, ela fica desativada.
![](https://main.qcloudimg.com/raw/4e44076b3485c9de15776134af7d5e96.png)
Ative o botão de alternância e configure adequadamente:
![](https://main.qcloudimg.com/raw/5a98a2ede54d4eceb8b5f4f0a8bbaa3b.png)
Clique em **Confirm (Confirmar)** para aplicar a configuração ao cabeçalho da resposta. Você pode clicar em **Edit (Editar)** para modificá-lo mais tarde.
![](https://main.qcloudimg.com/raw/e22e2cf4ad493379db7f1bcf49cfa03a.png)

## Exemplo de configuração

Se a configuração do HSTS do nome de domínio `cloud.tencent.com` for:
![](https://main.qcloudimg.com/raw/58e49b2b5a0b94f21fa3547dda08daed.png)
O cabeçalho da resposta será:
![](https://main.qcloudimg.com/raw/910e57e5abdedba4a33b4e4748a81318.png)

