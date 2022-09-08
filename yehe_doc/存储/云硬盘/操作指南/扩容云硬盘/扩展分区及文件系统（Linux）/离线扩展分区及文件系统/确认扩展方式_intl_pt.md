## Visão geral
Um disco em nuvem é um dispositivo de armazenamento expansível na nuvem. Depois que um disco em nuvem é criado, é possível expandir sua capacidade a qualquer momento para aumentar sua capacidade de armazenamento sem perder nenhum dado nele.
Depois de [expandir a capacidade do disco em nuvem](https://intl.cloud.tencent.com/document/product/362/5747) no console, é preciso fazer login na instância do CVM para atribuir sua capacidade expandida a uma partição existente usando um método apropriado, conforme necessário. Este documento descreve como determinar o método de expansão em um CVM do Linux.
<dx-alert infotype="notice" title="">
Estender o sistema de arquivos pode afetar os dados existentes. É altamente recomendável que você [crie um snapshot](https://intl.cloud.tencent.com/document/product/362/5755) manualmente para fazer backup de seus dados antes da operação.
</dx-alert>


## Pré-requisitos
- Você [expandiu o disco em nuvem pelo console](https://intl.cloud.tencent.com/document/product/362/5747).
- Você [montou o disco em nuvem](https://intl.cloud.tencent.com/document/product/362/32401) em um CVM do Linux e criou um sistema de arquivos.
- Você [fez login na instância do Linux](https://intl.cloud.tencent.com/document/product/213/5436) que requer a extensão de partições e sistemas de arquivos.

## Instruções
1. Execute o seguinte comando como usuário raiz para visualizar o formato da partição do disco em nuvem.[](id:fdisk)
```shellsession
fdisk -l
```
 - Se o resultado mostrar apenas `/dev/vdb` sem uma partição, é preciso estender o sistema de arquivos.
 ![](https://main.qcloudimg.com/raw/661ad0745c10a44035697cf4d03759f5.png)
 - Se o resultado for o mostrado nas duas figuras a seguir (que podem variar de acordo com o sistema operacional), o formato de partição GPT deve ser usado.
![](https://main.qcloudimg.com/raw/5ff70adb58a223d32d334470c5b29e0e.png)
![](https://main.qcloudimg.com/raw/ce19715fc8494a9735b714d86f0cccfa.png)
 - Se o resultado for o mostrado na figura a seguir (que pode variar de acordo com o sistema operacional), o formato de partição MBR deve ser usado.
![](https://main.qcloudimg.com/raw/0e336cd3354c098cf5e70d0672e6f625.png)
2. Escolha o método de expansão correspondente ao formato de partição obtido na [etapa 1](#fdisk).
<dx-alert infotype="notice" title="">
- A partição MBR é compatível com disco com capacidade máxima de 2 TB.
- Ao particionar o disco com capacidade superior a 2 TB, recomendamos que você crie e monte um novo disco de dados e use o formato de partição GPT para copiar os dados. 
</dx-alert>
<table>
     <tr>
         <th nowrap="nowrap">Formato da partição</th>  
				 <th>Método de expansão</th>  
         <th>Descrição</th>  
     </tr>
		 	 <tr>      
         <td>-</td>   
	     <td nowrap="nowrap">Extensão de sistemas de arquivos</a></td>
			 <td>Aplicável a cenários onde um sistema de arquivos foi criado diretamente em um dispositivo vazio e <b>nenhuma partição foi criada</b>.</td>
     </tr>
	 <tr>      
         <td rowspan="2">GPT</td>   
	     <td nowrap="nowrap"><a href="https://intl.cloud.tencent.com/document/product/362/39997#Add">Atribuição da capacidade expandida a uma partição GPT existente</a></td>
	     <td>Aplicável a cenários de formatação direta quando nenhuma partição foi criada.</td>
     </tr> 
	 <tr>
         <td><a href="https://intl.cloud.tencent.com/document/product/362/39997#New">Formatação da capacidade expandida em uma nova partição GPT independente</a></td> 
	     <td>Aplicável a cenários onde as partições originais permanecem inalteradas e uma nova partição GPT é criada para expansão.</td>
     </tr> 
	 <tr>
         <td rowspan="2">MBR</td>   
	     <td><a href="https://intl.cloud.tencent.com/document/product/362/39998#Add">Atribuição da capacidade expandida a uma partição MBR existente</a></td> 
	     <td>Aplicável a cenários de formatação direta quando nenhuma partição foi criada.</td>
     </tr> 
	 <tr>
         <td><a href="https://intl.cloud.tencent.com/document/product/362/39998#New">Formatação da capacidade expandida em uma nova partição MBR independente</a></td> 
	     <td>Aplicável a cenários onde as partições originais permanecem inalteradas e uma nova partição MBR é criada para expansão.</td>
     </tr> 
</table>






