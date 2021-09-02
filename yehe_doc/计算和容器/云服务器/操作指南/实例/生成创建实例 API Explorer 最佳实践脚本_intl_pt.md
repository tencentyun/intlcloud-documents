## Visão geral
Ao comprar CVMs na página de aquisição do CVM, você pode gerar scripts reutilizáveis de práticas recomendadas da OpenAPI com as configurações selecionadas. Depois, você pode usar esses códigos para adquirir instâncias do CVM com as mesmas configurações.

## Pré-requisitos
- Você fez login no console do Tencent Cloud e acessou a página de [**Configuração personalizada**](https://buy.cloud.tencent.com/cvm?tab=custom) do CVM.
- Você concluiu as configurações do CVM e entrou na página **Confirm Configuration (Confirmar configuração)**. Para saber mais sobre como configurar os parâmetros, consulte [Criação de instâncias pela página de aquisição do CVM](https://intl.cloud.tencent.com/document/product/213/4855).

## Direções
1. Na página **Confirm Configuration (Confirmar configuração)**, clique em **Generate API Explorer Reusable Scripts (Gerar scripts reutilizáveis do API Explorer)** conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/7c095b6809c8815b15d4fe2c45b89305.png)
2. Você pode ver as seguintes informações na janela pop-up.
![](https://main.qcloudimg.com/raw/5fba656be4ee0977245a7778f6a4c910.png)
 - **API Workflow (Fluxo de trabalho da API)**: fornece a descrição e os parâmetros reais da API `RunInstances` com base nas configurações selecionadas. Os parâmetros marcados com “*” são obrigatórios para a API. Você pode passar o mouse sobre os dados para exibi-los totalmente.
 - **API Script (Script de API)**: gera códigos nas linguagens de programação Java e Python. Selecione a guia Java ou Python conforme necessário, clique em **Copy Script (Copiar script)** no canto superior direito e salve os códigos para adquirir instâncias do CVM que contêm as mesmas configurações.
>?
>- A senha da instância não será exibida na página ou nos códigos de script por motivos de segurança. Modifique-a você mesmo. 
>- A data de expiração coletiva não pode ser definida no script reutilizável do API Explorer. Você precisa configurá-la depois de criar o CVM.
