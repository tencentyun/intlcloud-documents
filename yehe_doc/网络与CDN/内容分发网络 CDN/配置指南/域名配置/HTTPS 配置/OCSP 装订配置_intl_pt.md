## Configuração
Após a ativação do grampeamento OCSP (uma extensão de consulta do status do certificado TLS), o servidor enviará uma resposta em Protocolo de status de certificado on-line (Online Certificate Status Protocol) pré-armazenada durante o handshake do TLS para a verificação do usuário; assim, o usuário não precisará enviar uma solicitação de consulta para a autoridade de certificação (AC). O grampeamento OCSP melhora muito a eficiência do handshake do TLS e reduz o tempo de verificação do usuário.

O CDN do Tencent Cloud permite ativar/desativar o grampeamento OCSP.

## Guia de configuração
### Visualização da configuração
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita do nome de domínio para acessar a página de configuração. Na guia **Advanced Configuration (Configuração avançada)**, localize **OCSP Stapling Configuration (Configuração do grampeamento OCSP)**, que fica desativado por padrão:
![](https://main.qcloudimg.com/raw/a0f84d254848ea7c28a0642b3ab1866a.png)

### Modificação da configuração
Se um nome de domínio foi configurado com a aceleração HTTPS, é possível alternar o botão do grampeamento OCSP diretamente, para ativar/desativar essa funcionalidade. Depois que a configuração do certificado for excluída, o grampeamento OCSP será automaticamente invalidado:
![](https://main.qcloudimg.com/raw/af090e9a10a99f552c2a57378d0b46ff.png)

>Se o seu nome de domínio estiver configurado para a aceleração global, a configuração do grampeamento OCSP terá efeito global. Essa configuração não distingue entre solicitações da China Continental e de fora da China Continental.
