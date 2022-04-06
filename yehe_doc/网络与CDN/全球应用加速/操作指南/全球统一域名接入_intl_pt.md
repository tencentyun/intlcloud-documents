## Criação de nome de domínio unificado
1. Faça login no [Console do GAAP](https://console.cloud.tencent.com/gaap), acesse a página **Unified Domain Name (Nome de domínio unificado)** e clique em **Create (Criar)**.
2. Configure o nome de domínio unificado criado.
 ![](https://main.qcloudimg.com/raw/ef657658a3746491785734a4b9436efe.png)
- **Project (Projeto)**: o projeto ao qual o nome de domínio unificado pertence, que pode ser alterado.
- **Domain Name (Nome de domínio)**: pode conter até 30 caracteres.
- **Default Entry (Entrada padrão)**: o endereço de acesso para regiões não aceleradas, que normalmente é o endereço IP do servidor de origem.

> ! Por padrão, a quantidade de nomes de domínio unificado é cinco. Se precisar de mais, entre em contato com seu representante da Tencent Cloud.

## Configuração da região do acelerador
1. Acesse a página **[Unified Domain Name (Nome de domínio unificado)](https://console.cloud.tencent.com/gaap/domain)** e clique no nome de domínio ou em **Set (Definir)** no nome de domínio.
 ![](https://qcloudimg.tencent-cloud.cn/raw/2be645caa6cbc7d1c0f6016e7ac70fec.png)
	- **Domain Name (Nome de domínio)**: o nome de domínio acessado pelo cliente.
	- **Default Entry (Entrada padrão)**: o endereço de acesso para regiões não aceleradas, que normalmente é o endereço IP do servidor de origem.
	- **Number of Connections (Quantidade de conexões)**: a quantidade de conexões sob o nome de domínio unificado.
	- **Status**: o nome de domínio unificado pode trabalhar corretamente apenas com o status **Enabled (Ativado)**.
2. Clique em **Add Setting Item (Adicionar item de configuração)**. Na janela pop-up, selecione a região e a conexão do acelerador mais próximas e clique em **OK**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/1d5e8a5fb087abcd21c2ce17a94c12ef.png)

## Configuração da entrada padrão
Depois que o serviço de acesso ao nome de domínio unificado globalmente for ativado, para evitar latência de rede desnecessária causada por desvios e taxas de tráfego adicionais, é necessário configurar o caminho de acesso para usuários dos seguintes tipos:
1. Usuários dentro ou próximos da região do servidor de origem: eles costumam poder acessar o servidor de origem diretamente pela rede pública em vez de usar uma conexão de aceleração.
2. Usuários distantes da região de entrada da conexão de aceleração: eles costumam acessar o servidor de origem diretamente pela rede pública. O acesso por meio de uma conexão de aceleração não tem um efeito de aceleração ideal.

Na página **Unified Domain Name (Nome de domínio unificado)**, clique no nome de domínio ou em **Definir** no nome de domínio. Na página exibida, clique no ícone de edição à direita de **Default Entry (Entrada padrão)** para configurar a entrada padrão.
Após a configuração do endereço IP da entrada, os usuários das regiões abrangidas pela conexão de aceleração e de outras regiões podem acessar diretamente o seu servidor de origem usando esse endereço IP pela rede pública.
![](https://qcloudimg.tencent-cloud.cn/raw/c549724b7ac191aa4b45ca7d97144ce0.png)
![](https://qcloudimg.tencent-cloud.cn/raw/3aa59862dd00d759ee4933d8cf7b2a34.png)

