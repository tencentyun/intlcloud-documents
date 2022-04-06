## Descrição do erro
Digitei a senha correta, mas ainda não consegui fazer login no CVM usando o VNC. A mensagem “Module is unknown (O módulo é desconhecido)” é exibida.
![](https://main.qcloudimg.com/raw/117961622ff73a5859a56bd890011302.png)

## Possíveis causas
A origem deste problema pode ser a configuração de `/etc/pam.d/system-auth` no arquivo `/etc/pam.d/login`. 
![](https://main.qcloudimg.com/raw/334e393e16d8a03eec44009be9265ea9.png)
Se o caminho do módulo `pam_limits.so` não estiver configurado corretamente no arquivo de configuração `system-auth`, o login falhará.
![](https://main.qcloudimg.com/raw/36f36e0f2f5d0954f6fcebd39095d3b6.png)
<dx-alert infotype="explain" title="">
O módulo `pam_limits.so` limita o uso de recursos do sistema de um usuário durante a sessão. Se o caminho do módulo não estiver configurado corretamente de acordo com o sistema operacional correto, a autenticação de login falhará.

</dx-alert>



## Soluções
1. Realize o [procedimento de solução de problemas](#ProcessingSteps) para localizar a configuração do caminho `pam_limits.so` no arquivo `system-auth`.
2. Corrija o caminho do módulo `pam_limits.so`. 

[](id:ProcessingSteps)

## Procedimento de solução de problemas

1. Tente [fazer login no CVM do Linux usando uma chave SSH](https://intl.cloud.tencent.com/document/product/213/32501).
 - Se o login for bem-sucedido, siga para a próxima etapa.
 - Se o login falhar, use o modo de usuário único. Para mais informações, consulte a seção [Inicialização no modo de usuário único do Linux](https://intl.cloud.tencent.com/document/product/213/34819).
2. Execute o comando a seguir para exibir os logs.
```
vim /var/log/secure
```
Este arquivo registra as informações de segurança, principalmente os logs de login do CVM. Você pode verificar os logs de erros de `/lib/security/pam_limits.so` de acordo com o exemplo abaixo.
![](https://main.qcloudimg.com/raw/8f9f992d1835a9058020b435f1ef3c99.png)
3. Execute o passo a passo a seguir para entrar no diretório `/etc/pam.d` e procurar `/lib/security/pam_limits.so`.
```
cd /etc/pam.d
```
```
find . | xargs grep -ri "/lib/security/pam_limits.so" -l
```
Se um resultado semelhante à imagem abaixo for retornado, /lib/security/pam_limits.so está configurado no arquivo `system-auth`.
![](https://main.qcloudimg.com/raw/eab27cf686eccfeb8a8b796360010bb5.png)
4. Acesse o arquivo `system-auth` para corrigir o caminho do módulo `pam_limits.so`.
Por exemplo, você pode usar o caminho absoluto `/lib64/security/pam_limits.so` ou um caminho relativo `pam_limits.so` em um sistema operacional de 64 bits.


