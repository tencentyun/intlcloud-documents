## Visão geral
Além de usar imagens públicas do Tencent Cloud, também é possível criar imagens personalizadas para criar rapidamente instâncias do Tencent Cloud CVM com as mesmas configurações.
>?
>- As imagens usam o serviço de snapshot do CBS para o armazenamento de dados. Quando você cria uma imagem personalizada, um snapshot é criado automaticamente e associado à imagem. Você será cobrado por esse snapshot. Para obter mais informações, consulte a [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/362/32415).
>- Para os CVMs criados com base em imagens públicas após julho de 2018 e que usam discos em nuvem como discos do sistema, é possível criar imagens sem desligar a instância. Para outros CVMs, é necessário desligar a instância antes de criar uma imagem personalizada para garantir que a imagem tenha o mesmo ambiente de implantação que a instância atual.


## Observações

- Cada região suporta apenas um máximo de 10 imagens personalizadas.
- Os seguintes diretórios e arquivos serão removidos.
 - `/var/log/`  
 - `/root/.bash_history` e `/home/ubuntu/.bash_history` (para o sistema operacional Ubuntu)
- Ao criar uma imagem personalizada em uma instância do Linux, certifique-se de que `/etc/fstab` não contém a configuração do disco de dados. Caso contrário, as instâncias criadas com essa imagem não poderão ser iniciadas normalmente. Se a instância do Linux que for usada para criar uma imagem personalizada tiver um disco de dados montado, comente ou exclua as configurações de disco de dados relevantes em `/etc/fstab`.
- O processo de criação leva dez minutos ou mais, dependendo do tamanho dos dados da instância. Prepare-se com antecedência para evitar impactos na empresa.

## Instruções

### Criação de uma imagem personalizada de uma instância pelo console

1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm).
2. Na página de gerenciamento de instâncias, selecione a instância para a qual as imagens serão criadas e clique em **More (Mais)** > **Instance Status (Status da instância)** > **Shut down (Desligar)**, conforme mostrado abaixo:
![Shutdown](https://main.qcloudimg.com/raw/cc0bb1c82b96cca94cb7c1c011b664a7.png)
3. Depois que a instância for desligada, clique em **More (Mais)** > **Create Image (Criar imagem)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/8e3fc28e1a0b1e9e337ff72e34a9fd01.png)
4. Na janela pop-up, digite o **Image Name (Nome da imagem)** e a **Description (Descrição)** e clique em **Create Image (Criar imagem)**.
>? É possível clicar em <img src="https://main.qcloudimg.com/raw/31b31c7b27848f0378932f17273feff3.png" style="margin: 0;"></img> no canto superior direito para ver o progresso da criação da imagem.
>
5. Após a criação da imagem, clique em **[Images (Imagens)](https://console.cloud.tencent.com/cvm/image)** na barra lateral esquerda para entrar na página de gerenciamento de imagens.
6. Na lista de imagens, selecione a imagem que você criou e clique em **Create an Instance (Criar uma instância)** para adquirir um servidor com as mesmas configurações da imagem.
![Custom Image](https://main.qcloudimg.com/raw/2d64df77d16b3c26d275770e03a1caf1.png)

### Criação de uma imagem personalizada por API

É possível usar a API `CreateImage` para criar uma imagem personalizada. Para obter mais informações, consulte [CreateImage](https://intl.cloud.tencent.com/document/product/213/33276).

## Práticas recomendadas

### Migração dos dados em um disco de dados

Se você precisa manter os dados no disco de dados da instância original ao iniciar uma nova instância, é possível primeiro tirar um [snapshot](https://intl.cloud.tencent.com/document/product/362/31638) do disco de dados e, depois, usar esse snapshot para criar um novo disco de dados em nuvem.
Para obter mais informações, consulte a [Criação de discos em nuvem usando snapshots](https://intl.cloud.tencent.com/document/product/362/5757).