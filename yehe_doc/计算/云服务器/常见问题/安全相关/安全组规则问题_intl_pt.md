### Em quais cenários preciso adicionar regras de grupo de segurança?
Para garantir a acessibilidade das instâncias da CVM, é necessário adicionar regras de grupo de segurança nos seguintes cenários:
- Não há regra de grupo de segurança (adicionada ou padrão) para as instâncias da CVM. Se as instâncias da CVM precisarem acessar a rede pública ou se comunicar com instâncias da CVM associadas a outros grupos de segurança na mesma região, será necessário adicionar regras de segurança.
- O aplicativo que você criou usa uma porta personalizada ou intervalo de portas, em vez da porta padrão. Nesse caso, é necessário abrir a porta personalizada ou o intervalo de portas antes de testar a conectividade do aplicativo. Por exemplo, se você configurar um serviço Nginx nas instâncias da CVM que escuta na porta de comunicação 1800 do TCP, mas o grupo de segurança abre apenas a porta 80, é necessário adicionar regras de grupo de segurança para garantir a acessibilidade do serviço Nginx.
- Para conferir outros cenários, confira [Casos de uso de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/32369).

### Qual será o impacto da configuração incorreta das regras de grupos de segurança?
Se alguma regra de grupo de segurança for configurada incorretamente, as instâncias da CVM não conseguirão acessar outros dispositivos pela rede privada ou rede pública. Por exemplo:
- Pode falhar ao se conectar remotamente a uma instância do Linux por SSH ou a uma instância do Windows por meio da Área de Trabalho Remota.
- Pode falhar ao executar ping remotamente do IP público de uma instância da CVM.
- Pode falhar ao acessar os serviços da Web fornecidos por instâncias da CVM com o protocolo HTTP ou HTTPS.
- Pode falhar ao acessar outras instâncias da CVM pela rede privada.


### As regras de entrada e de saída de um grupo de segurança são contadas separadamente?
É possível definir um máximo de 100 regras de entrada e 100 de saída para um grupo de segurança.


### Posso ajustar a quantidade máxima de regras de grupo de segurança permitidas?
É possível configurar até 200 regras para cada grupo de segurança, incluindo 100 regras de entrada e 100 regras de saída. Uma instância da CVM pode ser associada a até 5 grupos de segurança e, portanto, pode adotar até 1.000 regras de grupo de segurança, o que é suficiente para atender às necessidades da maioria dos cenários.
Se o seu uso ultrapassar esse limite superior, verifique se existem regras redundantes.
- Se existirem, remova-as.
- Se não existirem, crie mais grupos de segurança.

Além disso, você pode [enviar um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) para aumentar o limite superior de regras de grupos de segurança.
