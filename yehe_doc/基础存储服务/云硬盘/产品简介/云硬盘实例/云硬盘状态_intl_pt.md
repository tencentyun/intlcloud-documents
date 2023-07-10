O disco em nuvem tem o seguinte status:

<table>
     <tr>
         <th>Status</th>  
         <th>Atributo</th>  
         <th>Descrição</th>  
     </tr>
	 <tr>      
         <td nowrap="nowrap">Para ser montado</td>   
	     <td nowrap="nowrap">Status estável</td>
	     <td>O status após o disco em nuvem ter sido criado e antes de ser montado em um CVM.</td>
     </tr> 
	 <tr>      
         <td>Montagem</td>   
	     <td>Status provisório</td>
	     <td>Quando o disco em nuvem está sendo montado, ele entra no status **montagem**.</td>
     </tr> 
	 <tr>      
         <td>Montado</td>   
	     <td>Status estável</td>
	     <td>O status quando o disco em nuvem foi montado em um CVM na mesma zona de disponibilidade.</td>
     </tr> 
	 <tr>      
         <td>Desmontagem</td>   
	     <td>Status provisório</td>
	     <td>Quando o disco em nuvem está sendo desmontado, ele entra no status **desmontagem**.</td>
     </tr> 
	 <tr>      
         <td>Para ser reavido</td>   
	     <td>Status estável</td>
	     <td>O status quando um disco em nuvem que não foi renovado dentro do período especificado após a expiração, ou um disco em nuvem com assinatura mensal que foi encerrada manualmente, é enviado para a lixeira após ser suspenso (o disco não está disponível e só pode armazenar dados) e é forçado a desmontar.</td>
     </tr> 
	 <tr>      
         <td>Encerrado</td>   
	     <td>Status estável</td>
	     <td>O disco em nuvem não é renovado e recuperado antes que seu tempo de armazenamento na lixeira expire ou a operação de encerramento seja concluída. O disco em nuvem original não existe mais e os dados foram completamente apagados.</td>
     </tr> 
</table>

A relação de conversão entre os status dos discos em nuvem é mostrada na figura a seguir:
![](https://main.qcloudimg.com/raw/096ea77e63990160092f22bcc3ff69ad.png)
