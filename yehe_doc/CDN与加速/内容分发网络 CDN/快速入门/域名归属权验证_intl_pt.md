

Se o nome de domínio de aceleração que você está conectando atender a uma das seguintes condições, você precisará verificar a propriedade do nome de domínio:

- O nome de domínio está sendo conectado pela primeira vez.
- O nome de domínio foi conectado por outro usuário.
- O nome de domínio é um nome de domínio curinga.

## Instruções

1. Clique em **Verification Method (Método de verificação)** para obter as informações do registro de DNS para verificação de DNS. Não feche esta página antes da verificação ser concluída.

2. Se o seu provedor de serviços DNS for a Tencent Cloud, vá para o [console DNSPod](https://console.cloud.tencent.com/cns), encontre o nome de domínio correspondente, clique em **Record (Registrar)**, adicione um registro TXT e digite `_cdnauth` como o respectivo registro de host.

3. Aguarde o registro TXT entrar em vigor e clique em **Verify (Verificar)**.

