## Visão geral
É possível usar uma imagem personalizada para criar instâncias do CVM do mesmo sistema operacional, aplicativos e dados para melhorar a eficiência. Este documento o orienta em como criar uma instância usando uma imagem personalizada.


## Pré-requisitos
É necessário ter uma imagem personalizada em sua conta e na região onde deseja criar uma instância.
Se não houver imagem personalizada, consulte as seguintes soluções:
<table>
	<tr><th>Status da imagem</th><th>Solução</th></tr>
	<tr><td>Imagens em computadores locais ou outras plataformas</td><td>Importe a imagem do disco do sistema localizada em computadores locais ou outras plataformas para a imagem personalizada no CVM. Para obter mais informações, consulte a <a href="https://intl.cloud.tencent.com/document/product/213/4945">Visão geral</a>.</td></tr>
	<tr><td>Existem instâncias de modelo, mas nenhuma imagem personalizada</td><td>Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/213/4942">Criação de imagens personalizadas</a>.</td></tr>
	<tr><td>Imagens personalizadas em outras regiões</td><td>Copie a imagem personalizada para a região de destino onde você deseja criar uma instância. Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/213/4943">Cópia de imagens</a>.</td></tr>
	<tr><td>Imagens personalizadas em outra conta</td><td>Compartilhe a imagem personalizada com a conta com a qual deseja criar uma instância. Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/213/4944">Compartilhamento de imagens personalizadas</a>.</td></tr>
</table>

## Direções

1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
2. Clique em **Images (Imagens)** na barra lateral esquerda para acessar a página **Image (Imagem)**.
3. Selecione uma região na parte superior da página **Image (Imagem)**.
4. Selecione uma guia com base na origem da imagem para visualizar sua lista de imagens.
 - **Public Image (Imagem pública)**: ir para a página da imagem pública.
 - **Custom Image (Imagem personalizada)**: ir para a página da imagem personalizada.
 - **Shared Image (Imagem compartilhada)**: ir para a página da imagem compartilhada.
5. Na coluna **Operation (Operação)** da imagem que deseja usar, clique em **Create Instance (Criar instância)**.
![](https://main.qcloudimg.com/raw/4c5806f49da53595d31ad07662bf363a.png)
6. Na janela pop-up, clique em **OK**.
7. Configure e crie a instância conforme solicitado pela página.
Os campos **Region (Região)** e **Image (Imagem)** são preenchidos automaticamente. Conclua as outras configurações da instância conforme necessário. Para obter mais informações, consulte [Criação de instâncias pela página de aquisição do CVM](https://intl.cloud.tencent.com/document/product/213/4855).
> Se você usar uma imagem personalizada que contém um ou mais snapshots de disco de dados, o sistema operacional criará automaticamente a mesma quantidade de Cloud Block Storage (CBS) como snapshots e a mesma capacidade de cada snapshot. É possível expandir, mas não reduzir, a capacidade do CBS.
>

## Documentação relacionada

Também é possível criar uma imagem personalizada usando a API RunInstances. Para obter mais informações, consulte [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237)
