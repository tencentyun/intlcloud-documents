
## Visão geral
Além da conta raiz padrão criada pelo sistema, você pode criar outras contas adicionais no console do TencentDB for MySQL com base em suas necessidades reais.

## Instruções
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, clique no ID de uma instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a sua página de gerenciamento.
2. Nessa página, selecione **Database Management (Gerenciamento de banco de dados)**> **Account Management (Gerenciamento de conta)** e clique em **Create Account (Criar conta)**.
![](https://main.qcloudimg.com/raw/244439e05841ec094ff337ca56f845c1.png)
3. Na janela pop-up, digite o nome, o host e a senha da conta, confirme a senha e clique em **OK**.
 - **Account name (Nome da conta)**:
    - O nome da conta no MySQL 5.5 e 5.6 pode conter de 1 a 16 letras, dígitos e sublinhados (_) e deve começar com uma letra e terminar com uma letra ou dígito.
    - O nome da conta no MySQL 5.7 e 8.0 pode conter de 1 a 32 letras, dígitos e sublinhados (_) e deve começar com uma letra e terminar com uma letra ou dígito.
 - **Host**: o endereço do host para acesso ao banco de dados pode ser um IP e conter `%` (que indica não limitar o intervalo de IP). Os hosts diferentes devem ser separados por quebras de linha, espaços, ponto e vírgula, vírgulas ou barras verticais.
    - Exemplo 1: digite `%` para indicar não limitar o intervalo de IP, ou seja, os clientes em todos os endereços IP podem usar esta conta para acessar o banco de dados.
    - Exemplo 2: digite `10.5.10.%`, o que significa que os clientes cujo intervalo de IP está dentro de `10.5.10.%` podem usar esta conta para acessar o banco de dados.
 - **Password (Senha)**: a senha deve conter de 8 a 64 caracteres em pelo menos dois dos seguintes tipos de caracteres: letras, dígitos e símbolos especiais `\_+-&amp;=!@#$%^\*()`.
 - **Connection Limit (Limite de conexão)**: a quantidade de conexões para esta conta, que não deve ser superior a 10.240. Se você não inserir um valor, nenhum limite será imposto (sujeito à quantidade máxima de conexões).
4. Após a criação bem-sucedida, a conta do banco de dados pode ser gerenciada na lista de contas do banco de dados da instância atual.

## APIs relacionadas

| Nome da API                                                      | Descrição     |
| ------------------------------------------------------------ | -------- |
| [CreateAccounts](https://intl.cloud.tencent.com/document/product/236/17502) | Cria uma conta do TencentDB |


