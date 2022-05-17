## Cenários de operação
Se você esqueceu a senha da sua conta de banco de dados ou precisa alterá-la enquanto usa o TencentDB for MySQL, pode redefini-la no console.
>?
>- Para o TencentDB for MySQL, a função de redefinição de senha foi conectada ao [CAM](https://intl.cloud.tencent.com/document/product/236/14469); portanto, recomendamos que você exerça um controle mais rígido sobre a permissão para a API de redefinição de senha ou os recursos confidenciais das instâncias do TencentDB for MySQL, concedendo tal permissão apenas ao pessoal apropriado.
>- Para segurança dos dados, recomendamos redefinir a senha regularmente pelo menos uma vez a cada três meses.


## Instruções
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Na lista de instâncias, clique no ID de uma instância ou em **Manage (Gerenciar)** na coluna “Operation (Operação)” para acessar a sua página de gerenciamento.
2. Selecione **Database Management (Gerenciamento de banco de dados)** > **Manage Account (Gerenciar conta)**, localize a conta para a qual deseja redefinir a senha e selecione **More (Mais)** > **Reset Password (Redefinir senha)**.
![](https://main.qcloudimg.com/raw/f8ff03d7b57ab9c96231f98920704441.png)
3. Na caixa de diálogo pop-up, digite e confirme a nova senha, e clique em **OK**.
>?A senha do banco de dados deve conter de 8 a 64 caracteres em pelo menos dois dos seguintes tipos de caracteres: letras, dígitos e símbolos especiais (_+-&=!@#$%^*()).
> 
![](https://main.qcloudimg.com/raw/8a2a4d08a1d14cfbcbb683f804bfeb78.png)

## APIs relacionadas

| Nome da API | Descrição |
| ------------------------------------------------------------ | -------- |
| [ModifyAccountPassword](https://intl.cloud.tencent.com/document/product/236/17497) | Modifica a senha da conta do TencentDB |
