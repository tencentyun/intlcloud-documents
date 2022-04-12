Depois que uma instância do TencentDB for MySQL é criada, ela fica com o status **Uninitialized (Não inicializada)** e precisa ser inicializada antes do uso.

## Instruções
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), selecione a região em questão, selecione uma instância com o status **Uninitialized (Não inicializada)** na lista de instâncias e clique em **Initialize (Inicializar)** na coluna **Operation (Operação)**.
2. Na janela pop-up de inicialização, configure os parâmetros de inicialização e clique em **OK**.
 - **Conjunto de caracteres**: São aceitos os conjuntos de caracteres LATIN1, GBK, UTF8 e UTF8MB4. O valor padrão é UTF8. Após inicializar a instância, você pode alterar o conjunto de caracteres na página de detalhes da instância no console. Para mais informações, consulte [Limites de uso > Observações sobre conjunto de caracteres](https://intl.cloud.tencent.com/document/product/236/7259).
 - **Table Name Case Sensitivity (Diferenciação de maiúsculas e minúsculas no nome da tabela)**: se o nome da tabela faz distinção entre maiúsculas e minúsculas. O valor padrão é sim.
 - **Custom Port (Porta personalizada)**: a porta de acesso ao banco de dados, que é 3306 por padrão.
 - **Root Account Password (Senha da conta raiz)**: defina a senha da conta raiz (o nome de usuário padrão para um novo banco de dados do MySQL é “root”).
 - **Confirm Password (Confirmar senha)**: digite a senha novamente.
3. Na janela pop-up de inicialização, clique em **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/cd8d4f83c43cc23b23c50c2e85773473.png)
4. Retorne à lista de instâncias. Depois que o status da instância for alterado para **Running (Em execução)**, ela poderá ser usada normalmente.

## Operações subsequentes
Você pode acessar a instância do TencentDB for MySQL pelas redes privada e pública a partir de uma instância da CVM do Windows ou do Linux. Para mais informações, consulte [Conexão à instância do MySQL](https://intl.cloud.tencent.com/document/product/236/37788).
