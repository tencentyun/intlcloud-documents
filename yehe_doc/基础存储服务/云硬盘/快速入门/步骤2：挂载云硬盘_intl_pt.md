## Visão geral
Este documento usa o disco em nuvem `cbs-test`, que será montado na Zona 2 de Pequim como exemplo para descrever como montá-lo em um CVM pelo console.
>?
>- Os discos em nuvem só podem ser montados em CVMs que estejam na mesma zona de disponibilidade.
>- Para obter mais informações sobre a montagem de discos em nuvem, consulte [Montagem de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/32401).
>

## Pré-requisitos
- Já ter [criado o disco em nuvem `cbs-test`](https://intl.cloud.tencent.com/document/product/362/31647).
- Ter CVMs sendo executados na mesma zona de disponibilidade (Zona 2 de Pequim neste exemplo) que o disco em nuvem. Para obter mais informações sobre como adquirir e iniciar um CVM, consulte [Personalização das configurações de um CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517) e [Personalização das configurações de um CVM Windows](https://intl.cloud.tencent.com/document/product/213/10516).

## Orientações
1. Faça login no console do CVM e clique em [**Cloud Block Storage**](https://console.cloud.tencent.com/cvm/cbs) na barra lateral à esquerda.
2. Selecione **Beijing (Pequim)** na parte superior da página, localize o disco em nuvem `cbs-test` e selecione **More (Mais)** > **Mount (Montar)** na coluna **Operation (Operação)**.

3. Na janela pop-up, selecione uma instância do CVM na qual o disco em nuvem será montado e clique em **Next (Avançar)** > **Mount Now (Montar agora)**.
>?Você pode marcar a opção **Release upon instance termination (Liberar mediante encerramento da instância)** de acordo com as circunstâncias reais.
>
Volte à página de lista do disco em nuvem. O status do disco em nuvem será **Mounting (Montando)**, o que indica que ele está sendo montado no CVM. Quando o status mudar para **Mounted (Montado)**, significará que a montagem foi concluída com êxito.


## Operações subsequentes
Após o disco em nuvem ser montado em um CVM, ele funciona como um disco de dados, o qual fica offline por padrão. Você precisa inicializar os discos em nuvem formatando, particionando e criando um sistema de arquivos. Para obter mais informações, consulte [Inicialização de discos em nuvem](https://intl.cloud.tencent.com/zh/document/product/362/31645).






