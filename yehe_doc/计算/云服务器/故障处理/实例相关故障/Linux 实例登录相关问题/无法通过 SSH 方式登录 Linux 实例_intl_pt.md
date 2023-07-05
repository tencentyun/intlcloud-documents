Este documento usa o CVM com o CentOS 7.5 como exemplo para mostrar como solucionar o problema em que não é possível fazer login em uma instância do Linux usando SSH.

## Problemas

Durante o [login em uma instância do Linux usando o SSH](https://intl.cloud.tencent.com/document/product/213/32501), é exibida uma mensagem indicando que a conexão não está disponível ou falhou.

## Localização e solução de problemas
### Etapa 1: verificar a regra configuração do grupo de segurança

Use a [ferramenta de verificação de porta para grupos de segurança](https://console.cloud.tencent.com/vpc/helper) para verificar se as regras do grupo de segurança estão corretas.
- Se o problema for causado pela configuração da porta do grupo de segurança, você pode usar a funcionalidade **Open All Ports (Abrir todas as portas)** para abrir todas as portas. Você também pode personalizar as regras do grupo de segurança com base em suas necessidades reais. Para mais informações, consulte [Adição de regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272).
- Se a configuração da porta do grupo de segurança estiver correta, vá para [a próxima etapa](#step07).
 
### Etapa 2: consultar a porta do serviço SSHD
1. <span id="step07">[Faça login em uma instância do Linux usando o VNC](https://intl.cloud.tencent.com/document/product/213/32494).</span>
>?Quando o login remoto e outros métodos de login falham, você pode usar o VNC para conectar a instância, monitorar o status da instância e solucionar problemas.
>
2. Na interface do sistema operacional, execute o comando a seguir para verificar se uma porta é escutada pelo serviço SSH daemon (SSHD):
```
netstat -tnlp | grep sshd
```
 - Se o seguinte resultado for retornado, o processo do SSHD está escutando na porta 22. Nesse caso, [envie um tíquete](https://console.cloud.tencent.com/workorder/category).
```
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1015/sshd  
```
 - Se nenhum resultado for retornado, o serviço SSHD ainda não foi iniciado. Nesse caso, prossiga para [a próxima etapa](#step09).
 
### Etapa 3: verificar se o serviço SSHD foi iniciado
<span id="step09">Execute o comando a seguir para verificar se o serviço SSHD foi iniciado.</span>
```
systemctl status sshd.service
```
 - Se tiver sido, [envie um tíquete](https://console.cloud.tencent.com/workorder/category).
 - Se não tiver sido, execute o comando a seguir para iniciar o serviço SSDH e tente fazer login na instância do Linux novamente usando o SSH.
```
systemctl start sshd
```

Se você ainda não conseguir fazer login na instância após executar essas etapas, recomendamos que relate esse problema [enviando um tíquete](https://console.cloud.tencent.com/workorder/category).

