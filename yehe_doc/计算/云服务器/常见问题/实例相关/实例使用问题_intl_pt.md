### Como exibir as CVMs que estão atualmente em uso?

Você pode fazer login no [console da CVM](https://console.cloud.tencent.com/cvm/index) para exibir as CVMs que estão em uso no momento.

### Uma máquina virtual pode ser instalada em uma CVM?

Não.

### Como desligar uma instância?

Para mais informações, consulte [Desligamento de instâncias](https://intl.cloud.tencent.com/document/product/213/4929).

### Como reiniciar uma instância?

Para mais informações, consulte [Reinicialização de instâncias](https://intl.cloud.tencent.com/document/product/213/4928).

### Como encerrar uma instância?

Para mais informações, consulte [Encerramento de instâncias](https://intl.cloud.tencent.com/document/product/213/4930).

### Como consultar o nome de usuário e a senha de uma instância do Linux?
Após criar uma instância da CVM, o nome de usuário e a senha serão enviados à sua conta por meio do [Centro de mensagens](https://console.cloud.tencent.com/message). A conta de administrador de uma instância do Linux é `root` por padrão.

### Como consultar, particionar e formatar os discos de uma instância do Linux?

Você pode executar o comando `df -h` para consultar as capacidades totais e usadas do disco, e executar o comando `fdisk -l` para exibir as informações do disco. Para mais informações sobre como particionar e formatar os discos de instâncias do Linux, consulte [Inicialização de discos em nuvem (menores que 2TB)](https://intl.cloud.tencent.com/document/product/362/31597) e [Inicialização de discos em nuvem (maiores que 2TB)](https://intl.cloud.tencent.com/document/product/362/31598).

### Como carregar arquivos em uma instância do Linux?
- Você pode [usar o SCP para carregar arquivos em uma instância do Linux](https://intl.cloud.tencent.com/document/product/213/2133).
- Você pode [usar o FTP para carregar arquivos em uma instância do Linux](https://intl.cloud.tencent.com/document/product/213/35307).

### Como alterar os proprietários e grupos de proprietários de diretórios e arquivos em uma instância do Linux?
Se as permissões de arquivo ou diretório estiverem configuradas incorretamente no servidor Web, ocorrerá um erro 403 quando você acessar um site hospedado na instância. Portanto, antes de ajustar um arquivo ou diretório, você deve confirmar a identidade sob a qual o processo de arquivo ou diretório está sendo executado.
- Você pode executar os comandos `ps` e `grep` para consultar as identidades sob as quais o processo de arquivo ou diretório está sendo executado.
- Você pode executar o comando `ls –l` para consultar os proprietários e os grupos de proprietários de arquivos e diretórios.
- Você pode executar o comando `chown` para modificar as permissões. Por exemplo, você pode executar o comando `chown -R www.www /tencentcloud/www/user/` para alterar os proprietários e grupos de proprietários de todos os arquivos e diretórios no diretório `/tencentcloud/www/user` para a conta “www”.

### Uma instância do Linux é compatível com a área de trabalho visual?
Sim, desde que você tenha criado uma área de trabalho visual na instância do Linux. Para mais informações, consulte [Criação de uma área de trabalho visual do Ubuntu](https://intl.cloud.tencent.com/document/product/213/37500).

### Por que não consigo adicionar placas de som ou vídeo às instâncias da CVM?
Por padrão, as CVMs da Tencent Cloud não fornecem servidores multimídia e componentes de placa de som e vídeo. Portanto, não é possível adicionar placas de som e vídeo a instâncias da CVM.

### Posso transferir o tempo não utilizado de uma instância da CVM para outra?
Não. Se você deseja maior flexibilidade e economia, recomendamos que adquira instâncias com pagamento conforme o uso.

### Como consultar a região onde está localizado o endereço IP de uma instância da CVM?
O endereço IP de uma instância da CVM está localizado na mesma região em que você a adquiriu.

### As instâncias da CVM fornecem bancos de dados por padrão?
Não. Para usar os serviços de banco de dados, você pode:
- Implantar o seu próprio banco de dados. Por exemplo, você pode [instalar e configurar o MySQL](https://intl.cloud.tencent.com/document/product/213/10190).
- Adquirir o [TencentDB for MySQL](https://intl.cloud.tencent.com/product/cdb) separadamente.

### Posso criar um banco de dados em uma instância da CVM?
Sim. Você pode instalar um software de banco de dados e configurar um ambiente de banco de dados em uma instância da CVM conforme necessário. Você também pode adquirir o [TencentDB for MySQL](https://intl.cloud.tencent.com/product/cdb) separadamente.

### As instâncias da CVM são compatíveis com os bancos de dados Oracle?
Sim. Antes de instalar um banco de dados Oracle, recomendamos que você realize um teste de estresse de desempenho na instância da CVM em questão, a fim de garantir que a instância possa atender aos requisitos de leitura/gravação do banco de dados.

### Quando posso forçar a interrupção de uma instância da CVM? Quais são as consequências da interrupção forçada de uma instância da CVM?
Você pode forçar a interrupção de uma instância da CVM quando o desligamento normal falhar. Observe que o desligamento forçado é equivalente a uma queda de energia e pode resultar na perda de dados não salvos.
