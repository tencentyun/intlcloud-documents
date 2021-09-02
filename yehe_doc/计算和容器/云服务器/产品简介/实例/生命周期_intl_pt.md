O ciclo de vida de uma instância do Tencent Cloud CVM se refere a todos os status, desde a inicialização até a liberação da instância. O gerenciamento adequado da instância do Tencent Cloud em diferentes status pode garantir que os aplicativos em execução na instância forneçam serviços de maneira econômica e eficiente.

Status da instância

- **Uma instância tem os seguintes status:**
	<table>
	<tr><th>Nome do status</th><th>Atributos do status</th><th>Descrição</th></tr>
	<tr><td>Criando</td><td>Status intermediário</td><td>A instância foi criada, mas ainda não está em execução.</td></tr>
	<tr><td>Em execução</td><td>Status estável</td><td>A instância está sendo executada normalmente e você pode executar seus serviços nessa instância.</td></tr>
	<tr><td>Reiniciando</td><td>Status intermediário</td><td>Uma operação de reinicialização foi executada para a instância por meio do console ou de APIs, mas a instância ainda não está em execução. Se esse status dura muito tempo, talvez haja uma exceção.</td></tr>
	<tr><td>Reinstalando</td><td>Status intermediário</td><td>O sistema da instância foi reinstalado ou seu disco foi reconfigurado por meio do console ou de APIs, mas a instância ainda não está em execução.</td></tr>
	<tr><td>Desligando</td><td>Status intermediário</td><td>Uma operação de desligamento foi realizada para a instância por meio do console ou de APIs, mas a instância ainda não foi desligada. Se esse status dura muito tempo, talvez haja uma exceção. Não recomendamos o desligamento forçado.</td></tr>
	<tr><td>Desligada</td><td>Status estável</td><td>A instância foi desligada normalmente e não pode fornecer serviços externos. Alguns atributos da instância só podem ser modificados quando a instância está com o status "Desligada".</td></tr>
	<tr><td>Encerrando</td><td>Status intermediário</td><td>A instância expirou há 7 dias ou o usuário realizou a operação de encerramento, mas ela ainda não foi concluída.</td></tr>
	<tr><td>Recuperada</td><td>Status estável</td><td>Uma instância com pagamento conforme o uso foi encerrada manualmente por menos de 2 horas e enviada para a lixeira. Nesse status, a instância não fornece serviços externos.</td></tr>
	<tr><td>Liberada</td><td>Status estável</td><td>A operação de liberação foi concluída. A instância original não existe mais, não pode fornecer serviços e todos os seus dados foram completamente apagados.</td></tr>
</table>
- **Transição de status da instância:**
![](https://main.qcloudimg.com/raw/2de51f523cc5592c5daeecf179945cfe.jpg)

## Inicialização de uma instância
 - Depois que uma instância é iniciada, ela entra no status "Criando". Para as instâncias com esse status, as especificações de hardware serão configuradas de acordo com o [tipo de instância](https://intl.cloud.tencent.com/document/product/213/11518) especificado, e o sistema iniciará a instância usando a imagem especificada na inicialização.
 - A instância entrará no status "Executando" depois de ser criada. É possível conectar e acessar normalmente uma instância com o status "Executando".

Para obter mais informações sobre a inicialização da instância, consulte [Criação de uma instância](https://intl.cloud.tencent.com/document/product/213/4855), [Login em uma instância do Windows](https://intl.cloud.tencent.com/document/product/213/5435) e [Login em uma instância do Linux](https://intl.cloud.tencent.com/document/product/213/5436).

## Reinicialização de uma instância
Recomendamos que você reinicie uma instância por meio do console do Tencent Cloud ou das APIs do Tencent Cloud, em vez de executar o comando de reinicialização do sistema operacional na instância.
 - Depois que a operação de reinicialização for executada, a instância entrará no status "Reiniciando".
 - Reiniciar uma instância é como reiniciar um computador. Depois de reiniciada, a instância manterá o endereço IP público, o endereço IP privado e todos os dados em disco.
 - Dependendo da sua configuração, reiniciar a instância normalmente leva de dezenas de segundos a vários minutos.

Para obter mais informações sobre como reiniciar uma instância, consulte [Como reiniciar instâncias](https://intl.cloud.tencent.com/document/product/213/4928).

## Desligamento de uma instância
Você pode desligar a instância por meio do console ou das APIs.
 - Desligar uma instância é como desligar um computador.
 - Uma instância desligada não fornece mais serviços externos, mas a cobrança da instância continua.
 - Uma instância desligada ainda será exibida no console.
 - O desligamento é necessário para algumas operações de configuração, como o ajuste das configurações de hardware e a redefinição de senhas.
 - A operação de desligamento não altera o IP público, o IP privado nem os dados no disco do CVM.
 
Para obter mais informações sobre como desligar uma instância, consulte [Como desligar instâncias](https://intl.cloud.tencent.com/document/product/213/4929).

## Encerramento e liberação de uma instância
Se você não precisa mais de uma instância, pode encerrá-la e liberá-la por meio do console ou das APIs do Tencent Cloud.

- Encerramento manual: as instâncias com pagamento conforme o uso serão liberadas após serem mantidas na lixeira por no máximo 2 horas.
- Encerramento automático por expiração ou pagamento em atraso: a instância com pagamento conforme o uso será encerrada automaticamente quando seu saldo ficar negativo por 2 horas e 15 dias. A cobrança continuará pelas primeiras 2 horas. Depois, a instância será encerrada e não haverá mais cobranças. A instância com pagamento conforme o uso em atraso não será enviada para a lixeira e poderá ser visualizada na lista de instâncias. Você pode continuar a usar a instância se renová-la dentro do tempo especificado.

Quando uma instância é encerrada, os discos do sistema e discos de dados especificados na aquisição são liberados. No entanto, os discos em nuvem montados na instância não serão afetados.
Para obter mais informações sobre como encerrar uma instância, consulte [Como encerrar instâncias](https://intl.cloud.tencent.com/document/product/213/4930).
