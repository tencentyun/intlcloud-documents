### Qual é a diferença entre o login com chave SSH e o login com senha?
Uma chave SSH permite que você faça login em um servidor Linux remotamente. O gerador de chaves é usado para criar um par de chaves (pública e privada). A chave pública é adicionada ao servidor, e o cliente pode usar a chave privada para concluir a autenticação e o login. Comparado ao login com senha, o login com chave SSH é mais seguro e eficiente.
Atualmente, a instância do Linux aceita tanto o login com senha quanto o com chave SSH, já a instância do Windows aceita apenas o login com senha. Para ter acesso à documentação relacionada, consulte:
- [Login em instâncias do Linux](https://intl.cloud.tencent.com/document/product/213/5436)
- [Login em instâncias do Windows](https://intl.cloud.tencent.com/document/product/213/5435)

### Por que não posso usar a senha para fazer login em uma instância do Linux associada a uma chave SSH?
Depois que a CVM é associado a uma chave SSH, o login com senha é **desativado por padrão**. - Faça [login em uma instância do Linux com a chave SSH](https://intl.cloud.tencent.com/document/product/213/32501). 

### Posso usar a chave SSH junto com a senha de login?
Quando você faz [login na instância do Linux com a chave SSH](https://intl.cloud.tencent.com/document/product/213/32501), o login com senha é desativado por padrão para aumentar a segurança.

### Como crio uma chave SSH, e o que acontece se eu a perder?
Para mais informações sobre a criação de chaves, consulte [Gerenciamento de chaves SSH](https://intl.cloud.tencent.com/document/product/213/16691).
Se você perdeu a chave, solucione o problema usando os seguintes métodos:
 - Crie uma nova chave pela [Chave SSH](https://console.cloud.tencent.com/cvm/sshkey) no console e vincule-a à instância original.
  1. [Crie uma chave SSH](https://intl.cloud.tencent.com/document/product/213/16691).
  2. Após a criação da chave, faça login no [Console da CVM](https://console.cloud.tencent.com/cvm).
  3. Selecione a instância original à qual você deseja vincular a chave, clique em **More (Mais)** -> **Password/key (Senha/chave)** -> **Load a key (Carregar uma chave)**. Você pode então usar a nova chave para fazer login na instância.
 - Redefina a senha no console da CVM e faça login na instância com a nova senha. Para mais informações, consulte [Redefinição da senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).

### Como vinculo/desvinculo uma chave SSH para ou de um servidor?

Para mais informações, consulte a seção **Vinculação/desvinculação de uma chave para ou de uma CVM** em [Gerenciamento de chaves SSH](https://intl.cloud.tencent.com/document/product/213/16691).

### Como modifico o nome/descrição da chave SSH?

Para mais informações, consulte a seção **Modificação do nome e da descrição da chave SSH** em [Gerenciamento de chaves SSH](https://intl.cloud.tencent.com/document/product/213/16691).

### Como excluo uma chave SSH?

Para mais informações, consulte a seção **Exclusão de chaves SSH** em [Gerenciamento de chaves SSH](https://intl.cloud.tencent.com/document/product/213/16691).

### Quais são os limites de uso das chaves SSH?

Para mais informações, consulte a seção **Limites de uso** em [Chaves SSH](https://intl.cloud.tencent.com/document/product/213/6092).

### Como solucionar problemas se eu não conseguir fazer login em uma instância do Linux usando uma chave SSH?

Para mais informações, consulte [Não é possível fazer login em uma instância do Linux via SSH](https://intl.cloud.tencent.com/document/product/213/32486).

### Por que não consigo baixar a chave?
Só é possível baixar a chave uma vez. Se você perdeu a chave, recomendamos que crie uma nova chave, baixe e salve-a.

### Como consulto qual chave é usada pela instância da CVM?
Você pode fazer login no console da CVM e acessar a página de detalhes da instância para exibir as chaves usadas pela CVM.
