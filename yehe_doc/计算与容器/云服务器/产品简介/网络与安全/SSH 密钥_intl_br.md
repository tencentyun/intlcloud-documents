Para garantir a segurança e a confiabilidade das instâncias, o Tencent Cloud fornece dois métodos de login criptografado aos usuários. Os usuários podem fazer o login com uma [senha de login](/doc/product/213/6093) ou com o par de chaves SSH. Este documento descreve como fazer login com um par de chaves SSH.
Você pode escolher o par de chaves SSH como o método de login criptografado do CVM na [Personalização das configurações do CVM do Linux](/doc/product/213/10517#.E8.AE.BE.E7.BD.AE.E4.BF.A1.E6.81.AF).

## Visão geral das chaves SSH
Recomendamos **usar o par de chaves SSH** para fazer login em uma instância do Linux. Um par de chaves contém uma chave pública e uma chave privada. Ele é gerado com o método de criptografia RSA de 2048 bits.
- **Chave pública**: quando o par de chaves SSH é gerado, o Tencent Cloud armazena apenas a chave pública e a salva no arquivo `~/.ssh/authorized_keys`.
- **Chave privada**: você precisa baixar a chave privada e mantê-la segura. A chave privada só pode ser baixada uma vez. O Tencent Cloud não guardará sua chave privada. Qualquer pessoa com sua chave privada pode acessar a sua instância. Certifique-se de mantê-la segura.

Você pode usar o par de chaves para se conectar ao CVM com segurança. Esse método é mais seguro do que fazer login com uma senha. Você só precisa especificar o par de chaves ao criar uma instância do Linux, ou associá-lo à uma instância existente, e a partir daí usar a chave privada para fazer login na instância sem inserir uma senha.

## Funcionalidades e vantagens
Em comparação com os métodos tradicionais de autenticação por senha, o login com par de chaves SSH traz as seguintes vantagens:
- O login por par de chaves SSH é mais complexo e difícil de burlar.
- O login por par de chaves SSH é mais fácil de usar. Você pode fazer login em instâncias remotamente com algumas etapas simples de configuração no console e no cliente local, e não precisa inserir uma senha ao fazer login novamente.

## Limites de uso
- O login com par de chaves SSH só está disponível para as instâncias do Linux.
- Cada conta do Tencent Cloud comporta até 100 pares de chaves SSH.
- O Tencent Cloud não reterá a sua chave privada. Você precisa baixar a chave privada após criar uma chave SSH, e mantê-la segura.
- Para garantir a segurança dos dados, é necessário encerrar a instância antes de carregar a chave.
- Para melhorar a segurança do CVM, você não pode usar o método de login por senha depois de vincular um par de chaves à instância.


## Casos de uso
- Para saber como criar, vincular, desvincular ou excluir uma chave, consulte o [Gerenciamento de pares de chaves SSH](https://intl.cloud.tencent.com/document/product/213/16691).
- Para saber como fazer login em instâncias do CVM remotamente usando um par de chaves SSH, consulte
 - [Login em instâncias do Linux por meio de ferramentas de login remoto](https://intl.cloud.tencent.com/document/product/213/32502)
 - [Login em instâncias do Linux com chave SSH](https://intl.cloud.tencent.com/document/product/213/32501)



