### O que é um nome de dispositivo (ponto de montagem)?
Um nome de dispositivo (ponto de montagem) é o local de um disco em nuvem montado na instância da CVM no barramento do controlador de disco. O nome de dispositivo selecionado corresponde ao número do dispositivo de disco no Linux e corresponde ao número de sequência do disco do gerenciador de disco no Windows.

### Posso montar um disco em nuvem em várias instâncias da CVM?
Não. Você pode montar até 20 discos em nuvem na mesma CVM, mas não pode montar o mesmo disco em nuvem em várias CVMs. Só é possível compartilhar dados [desmontando o disco em nuvem](https://intl.cloud.tencent.com/document/product/362/32400) da CVM A e depois [montando-o](https://intl.cloud.tencent.com/document/product/362/32401) na CVM B.

### Preciso particionar o disco em nuvem após adquiri-lo e montá-lo em uma instância da CVM?
Sim. Após adquirir um disco em nuvem, você deve montá-lo em uma instância da CVM na mesma zona de disponibilidade e inicializá-lo formatando, particionando e criando o sistema de arquivos antes de usá-lo como disco de dados. Para mais informações, consulte [Montagem de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/31645) e [Inicialização de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/31645).

### Por que não consigo localizar o disco de dados que adquiri para uma instância do Linux?
Se você adquirir um disco de dados separadamente, deverá particioná-lo, formatá-lo e montá-lo em uma instância para exibir e usar o seu espaço de armazenamento. Para mais informações, consulte [Montagem de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/31645) e [Inicialização de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/31645).

### Quantos discos em nuvem podem ser montados em uma instância da CVM?
Um máximo de 20 discos de dados podem ser montados em uma instância da CVM.

### Por que eu não consigo localizar a CVM no qual quero montar um disco em nuvem?
Verifique se a instância da CVM não foi liberada e se ela está na mesma região e zona de disponibilidade do disco em nuvem.

### Posso montar um disco em nuvem em uma instância da CVM em outra zona de disponibilidade?
Não. Um disco em nuvem só pode ser montado ou desmontado de uma instância da CVM na mesma zona de disponibilidade do disco em nuvem.

### Ao desmontar um disco em nuvem (disco de dados), os dados serão perdidos?
Os dados em discos em nuvem não serão modificados durante a montagem e a desmontagem. Para garantir a consistência dos dados, recomendamos que você siga as etapas abaixo:
- No Windows, recomendamos que você interrompa todas as operações de leitura e gravação em todos os sistemas de arquivos do disco em nuvem para garantir a integridade dos dados. Caso contrário, os dados cuja leitura ou gravação não foi finalizada serão perdidos.
- No Linux, faça login na instância da CVM e execute o comando `umount` no disco em nuvem. Após o comando ser executado, faça login no console da CVM para desmontar o disco em nuvem.

### Como desmontar um disco em nuvem?
Para mais informações, consulte [Desmontagem de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/32400).

### Os discos em nuvem podem ser montados e desmontados?
- Os discos em nuvem podem ser montados e desmontados.
- Os discos do sistema não podem ser montados nem desmontados.

### Os discos em nuvem podem ser montados e desmontados em lotes?
- Os discos em nuvem podem ser montados e desmontados em lotes.
- Os discos do sistema não podem ser montados nem desmontados.

### Os discos do sistema podem ser desmontados?
Não.


