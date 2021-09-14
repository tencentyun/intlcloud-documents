### Expansão de discos do sistema em nuvem
Se o disco em nuvem funcionar como um disco do sistema, é possível expandi-lo usando os dois métodos a seguir.
- [Expansão pelo console do CVM](https://intl.cloud.tencent.com/document/product/362/5747#useCVMconsole)
- [Reinstalação do sistema](https://intl.cloud.tencent.com/document/product/362/5747#reinstallSystem)



### Expansão de discos de dados em nuvem

Se o disco em nuvem for um disco de dados, é possível expandi-lo usando os três métodos a seguir.
- [Expansão de discos em nuvem pelo console do CVM](https://intl.cloud.tencent.com/document/product/362/5747#useCVMConsole)
- [Expansão de discos em nuvem pelo console do CBS](https://intl.cloud.tencent.com/document/product/362/5747#useCBSConsole)
- [Expansão de discos em nuvem por API](https://intl.cloud.tencent.com/document/product/362/5747#useAPI)




Com base no status de **montagem** dos discos de dados do CBS, é possível expandir sua capacidade por diferentes métodos.
- Se o disco de dados do CBS atual **puder ser desmontado**, é possível expandir sua capacidade no console do CBS ou pela API [`ResizeDisk`](https://intl.cloud.tencent.com/document/product/362/16310).
- Se o disco de dados do CBS atual **não puder ser desmontado**, é possível expandir sua capacidade no console do CVM ou pela API [`ResizeDisk`](https://intl.cloud.tencent.com/document/product/362/16310).

>! Se a capacidade máxima do disco em nuvem não atender às suas necessidades empresariais, tente [criar grupos RAID](https://intl.cloud.tencent.com/document/product/362/2932) ou [criar volumes lógicos LVM com vários discos em nuvem elásticos](https://intl.cloud.tencent.com/document/product/362/2933).

Depois que a capacidade do disco de dados for expandida, você deve realizar as seguintes operações para que a instância reconheça e use o disco de dados:
<table>
     <tr>
         <th nowrap="nowrap">Antes da expansão</th>  
         <th nowrap="nowrap">Depois da expansão</th>  
		 <th>Operações subsequentes</th>  
     </tr>
	 <tr>
         <td   rowspan="2" nowrap="nowrap">Sistema de arquivos não criado</td>
         <td>Capacidade do disco < 2 TB/td>
		 <td><a href="https://intl.cloud.tencent.com/document/product/362/31597">Inicialização de discos em nuvem (< 2 TB)</a></td>
     </tr> 
	 <tr>
         <td nowrap="nowrap">Capacidade do disco ≥ 2 TB</td>
         <td><a href="https://intl.cloud.tencent.com/document/product/362/31598">Inicialização de discos em nuvem (≥ 2 TB)</a></td>
     </tr>
	 <tr>
         <td   rowspan="2">Sistema de arquivos criado</td>
         <td>Capacidade do disco < 2 TB/td>
    		 <td><ul><li>Discos em nuvem montados em um CVM do Windows:<a href="https://intl.cloud.tencent.com/document/product/362/31601">extensão de partições e sistemas de arquivos (Windows)</a></li>
			 <li>Discos em nuvem montados em um CVM do Linux:<a href="https://intl.cloud.tencent.com/document/product/362/31602">extensão de partições e sistemas de arquivos (Linux)</a></li></ul>
				 </td>
     </tr>
	 <tr>
         <td>Capacidade do disco ≥ 2 TB</td>
         <td>
				 <ul><li>Formato de partição GPT:<a href="https://intl.cloud.tencent.com/document/product/362/31601">extensão de partições e sistemas de arquivos (Windows)</a> ou <a href="https://intl.cloud.tencent.com/document/product/362/31602">extensão de partições e sistemas de arquivos (Linux)</a></li>
				 <li>Formato de partição MBR: Não compatível.</li>A partição MBR é compatível com disco com capacidade máxima de 2 TB. Ao particionar o disco com capacidade superior a 2 TB, recomendamos que você crie e monte um novo disco de dados e use o formato de partição GPT para copiar os dados.</ul>
				 </td>
     </tr>
</table>


