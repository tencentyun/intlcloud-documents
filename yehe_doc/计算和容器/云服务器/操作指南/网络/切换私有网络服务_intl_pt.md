## Visão geral

O Tencent Cloud fornece a rede clássica e o VPC para diferentes cenários. Várias funcionalidades são oferecidas para ajudar você a gerenciar de forma flexível as suas redes.
- Alternar entre redes:
 - **Alternar da rede clássica para o VPC**: o Tencent Cloud permite que você migre uma ou mais instâncias do CVM da rede clássica para o VPC por vez.
 - **Alternar entre VPCs**: o Tencent Cloud permite que você migre uma ou mais instâncias do CVM do VPC A para o VPC B por vez.
- Especificar um endereço IP personalizado.
- Optar por manter o HostName.

## Pré-requisitos
- Antes da migração, desvincule a instância do CVM do CLB e do ENI nas redes privada e pública e libere o endereço IP secundário do ENI principal. Vincule-os novamente após a migração.


## Instruções
### Determinação do atributo de rede da instância do CVM
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página **Instances (Instâncias)**, localize a instância de destino que deseja migrar.
A instância está na rede clássica se “Network: Classic Network (Rede: rede clássica)” for exibido na coluna **Instance Configuration (Configuração da instância)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/bb54a50bd8a42e5aeac6ce02bc3c6a4d.png)
>!
>- A migração da rede clássica para o VPC NÃO PODE ser revertida. Após a migração, a instância do CVM não conseguirá se comunicar com os serviços do Tencent Cloud na rede clássica.
>- Depois de determinar o atributo de rede da instância do CVM, é possível [migrar as instâncias para o VPC](#changeVPC) conforme necessário.




### Migração para o VPC<span id="changeVPC"></span>
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página **Instances (Instâncias)**, migre a instância de destino para o VPC.
	- **Método 1**: para migrar uma instância para o VPC, localize-a e selecione **More (Mais)** -> **Resource Adjustment (Ajuste de recursos)** -> **Switch VPC (Alternar para o VPC)** na coluna **Operation (Operação)**.
	![](https://main.qcloudimg.com/raw/e688912e2ad9ea46ce7027f17e1a8045.png)
	- **Método 2**: para migrar em lote as instâncias para o VPC, selecione as instâncias de destino e clique em **More Actions (Mais ações)** -> **Resource Adjustment (Ajuste de recursos)** -> **Switch VPC (Alternar para o VPC)** no topo da lista de instâncias.
	>! A migração em lote só é compatível com as instâncias do CVM na mesma zona de disponibilidade.
	>
	![](https://main.qcloudimg.com/raw/b15f3e4e6c212ff496d38c3753c9a4da.png)
3. Na janela **Switch VPC (Alternar para o VPC)** exibida, leia as observações e clique em **Next (Avançar)**.
4. Selecione o VPC de destino e a sub-rede correspondente e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/acaca8c4343d8e5357bd33b75f1f5f68.png)
5. Especifique o endereço IP pré-atribuído e as opções de HostName para **Set IP (Definir IP)** conforme necessário e clique em **Next (Avançar)**.
>? 
> - Se nenhum endereço IP pré-atribuído for especificado, o sistema atribuirá automaticamente um endereço IP.
> - Ao especificar as opções de HostName, é possível selecionar **Reset HostName (Redefinir o HostName)** ou **Retain the original HostName of the instance (Manter o HostName original da instância)**.
> 
![](https://main.qcloudimg.com/raw/c3908fef18c46a5f88aebfca2204f5c0.png)
6. Realize as operações de acordo com as instruções na página **Shutdown CVM (Desligar o CVM)** e clique em **Start Migration (Iniciar migração)**. Após a conclusão da migração, você pode fazer login no console do CVM. Na página **Instances (Instâncias)**, você verá que **Modifying instance VPC attributes (Modificar os atributos do VPC da instância)** é exibido na coluna **Status** das instâncias migradas.
>!
>- Durante a migração, a instância do CVM precisa ser reiniciada. Portanto, não execute outras operações durante esse período.
>- Verifique o status da instância após a migração e se o acesso à rede privada e o login remoto funcionam corretamente.
>
![](https://main.qcloudimg.com/raw/759d34a61cc6b0d1e430525e3283d43b.png)




