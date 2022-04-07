## Como fazer backup de dados da CVM?

- Se a CVM usa um disco em nuvem, você pode fazer backup dos seus dados criando uma imagem personalizada do disco de sistema e um snapshot do disco de dados. 
  - Para mais informações sobre como criar uma imagem personalizada, consulte [Criação de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4942).
  - Para mais informações sobre como criar um snapshot, consulte [Criação de snapshots](https://intl.cloud.tencent.com/document/product/362/5755)
- Se a CVM usa um disco local, você pode fazer backup dos dados no disco de sistema criando uma imagem personalizada. Para dados de negócios no disco de dados, você ainda precisa personalizar a política de backup. 
  Você pode usar o FTP para fazer backup dos dados no servidor para outros locais. Para acessar os métodos específicos de implantação do FTP, consulte: 
  - Para Windows: [Implantação do serviço FTP (Windows)](https://intl.cloud.tencent.com/document/product/213/10414)
  - Para Linux: [Implantação do serviço FTP (Linux)](https://intl.cloud.tencent.com/document/product/213/10912) 

## Quais são as soluções comuns de backup e recuperação de dados?

As soluções de backup e recuperação de dados variam de acordo com os cenários de programas e atividades. As recomendações a seguir podem ser usadas com base em suas necessidades em si:
- Faça backup da instância regularmente usando a funcionalidade [Snapshot do CBS](https://intl.cloud.tencent.com/document/product/362/5757).
- Utilize os componentes principais de uma aplicativo em várias zonas de disponibilidade e copie os dados conforme necessário.
- Use um [IP público elástico](https://intl.cloud.tencent.com/document/product/213/5733) para o mapeamento de nomes de domínio, a fim de garantir que o IP de serviço possa ser redirecionado rapidamente para outra instância da CVM quando o servidor estiver indisponível.
- Confira os dados de monitoramento regularmente e configure os alarmes correspondentes. Para mais informações, consulte [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248).
- Processe solicitações de emergência com o Auto Scaling. Para mais informações, consulte [Auto Scaling](https://intl.cloud.tencent.com/document/product/377).
