### Backup
O TencentDB for MySQL permite o backup automático e manual para fornecer a capacidade de restauração de dados que garante a integridade e a confiabilidade dos dados. Por padrão, ele fornece funcionalidades de backup de dados e backup de logs, em que a frequência do backup automático deve ser definida para mais de duas vezes por semana. Se você tiver outras necessidades de backup, poderá iniciar o backup manual por meio do [console](https://console.cloud.tencent.com/cdb) ou das APIs a qualquer momento.

Além disso, você pode configurar com flexibilidade o período de retenção dos arquivos de backup conforme necessário, que é de 7 dias por padrão e pode ser de até 732 dias. Os arquivos de backup que excederem o período de retenção serão excluídos automaticamente.

Para mais informações sobre como usar essa funcionalidade, consulte [Modo de backup](https://intl.cloud.tencent.com/document/product/236/32340).

### Restauração
O TencentDB for MySQL permite a restauração de dados. Você pode usar a funcionalidade de reversão para restaurar os dados para qualquer ponto de tempo dentro do período de retenção, conforme necessário. Como os pontos de tempo disponíveis para restauração de dados estão sujeitos ao período de retenção, você deve configurar uma política de retenção de backup razoável com base em suas necessidades de operação para garantir a capacidade de restauração de dados.

Para mais informações sobre como usar essa funcionalidade, consulte [Reversão de banco de dados](https://intl.cloud.tencent.com/document/product/236/7276).
