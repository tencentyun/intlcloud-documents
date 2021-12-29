## Criação de nome de domínio unificado

1. Faça login no [Console do GAAP](https://console.cloud.tencent.com/gaap), acesse a página **Unified Domain Name (Nome de domínio unificado)** e clique em **Create (Criar)**.
2. Configure as informações do **novo nome de domínio unificado**.
![](https://main.qcloudimg.com/raw/ef657658a3746491785734a4b9436efe.png)
- Project (Projeto): o projeto ao qual pertence o nome de domínio unificado (pode ser alterado posteriormente).
- Domain Name (Nome de domínio): pode conter até 30 caracteres.
- Default Entry (Entrada padrão): o endereço de acesso para regiões não aceleradas, que normalmente é o endereço IP do servidor de origem.

> ! Por padrão, a quantidade de nomes de domínio unificados é cinco. Se precisar de mais, entre em contato com seu representante do Tencent Cloud.

## Configuração da região de acesso

1. Acesse a página **[Unified Domain Name (Nome de domínio unificado)](https://console.cloud.tencent.com/gaap/domain)** e clique no nome de domínio especificado ou em **Set (Definir)** para prosseguir para a próxima página.
    ![](https://qcloudimg.tencent-cloud.cn/raw/2be645caa6cbc7d1c0f6016e7ac70fec.png)
   - Domain Name (Nome de domínio): o nome de domínio usado para acesso do cliente.
   - Default Entry (Entrada padrão): o endereço de acesso para regiões não aceleradas, que normalmente é o endereço IP do servidor de origem.
   - Number of Connections (Quantidade de conexões): a quantidade de conexões sob o nome de domínio unificado.
   - Status: o nome de domínio unificado pode trabalhar corretamente apenas com o status **Enabled (Ativado)**.
2. Clique em **Add Settings (Adicionar configurações)** para abrir a janela de **Add Settings (Adicionar configurações)**, selecione a região de aceleração da lista e o nó de acesso, e clique em **OK** para que entrem em vigor conforme mostrado abaixo:
![](https://qcloudimg.tencent-cloud.cn/raw/1d5e8a5fb087abcd21c2ce17a94c12ef.png)

## Configuração da entrada padrão

Depois que o serviço de acesso ao nome de domínio unificado globalmente for ativado, para evitar latência de rede desnecessária causada por desvios e taxas de tráfego adicionais, é necessário configurar o caminho de acesso para usuários dos seguintes tipos:

1. Usuários dentro ou próximos da região do servidor de origem: eles costumam poder acessar o servidor de origem diretamente pela rede pública em vez de usar uma conexão de aceleração.
2. Usuários distantes da região de entrada da conexão de aceleração: eles costumam acessar o servidor de origem diretamente pela rede pública. O acesso por meio de uma conexão de aceleração não tem um efeito de aceleração ideal.

Na página **[Unified Domain Name (Nome de domínio unificado)](https://console.cloud.tencent.com/gaap/domain)**, clique no nome de domínio especificado ou em **Set (Definir)** para prosseguir para a próxima página. Em seguida, clique no ícone **Edit (Editar)** à direita da **Default Entry (Entrada padrão)** na parte superior para configurá-la.
Após configurar o endereço IP de entrada, com exceção dos usuários nas regiões abrangidas pela conexão de aceleração selecionada, os usuários em outras regiões acessarão seu servidor de origem diretamente neste IP pela rede pública.
![](https://qcloudimg.tencent-cloud.cn/raw/c549724b7ac191aa4b45ca7d97144ce0.png)
![](https://qcloudimg.tencent-cloud.cn/raw/3aa59862dd00d759ee4933d8cf7b2a34.png)

