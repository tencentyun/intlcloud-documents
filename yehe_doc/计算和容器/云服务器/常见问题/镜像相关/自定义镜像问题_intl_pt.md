### O que devo fazer se o sistema Windows falhar ao criar uma imagem personalizada?

Se o sistema Windows falhar ao criar uma imagem personalizada, você poderá solucionar o problema da seguinte maneira:
1. A criação de uma imagem personalizada depende do Instalador de Módulos do Windows fornecido pela Microsoft. Verifique se esse serviço está funcionando corretamente.
2. Algumas ferramentas antivírus ou o Safedog podem bloquear a execução de scripts personalizados de criação de imagens. Para evitar falhas na criação, recomendamos que você desative essas ferramentas antes de criar uma imagem personalizada.
3. Se a ferramenta de criação de imagem for interrompida por pop-ups do sistema, faça login remotamente na CVM, e verifique e ajuste a configuração da CVM para bloquear pop-ups.

### É possível criar uma imagem personalizada a partir do snapshot do disco de dados?
Não. É possível criar uma imagem personalizada a partir do snapshot do disco do sistema, mas não do snapshot do disco de dados.
Se precisar manter os dados no disco de dados da instância original ao iniciar uma nova instância, é possível primeiro tirar um snapshot do disco de dados e, depois, usar esse snapshot para criar um novo disco de dados do CBS. Para mais informações, consulte a [Criação de discos em nuvem usando snapshots](https://intl.cloud.tencent.com/document/product/362/5757).

### Como confirmo se o disco de dados foi desmontado e se uma imagem personalizada pode ser criada?
1. Confirme se a linha da instrução de partição do disco de dados montado automaticamente já foi excluída no arquivo `/etc/fstab`.
2. Execute o comando `mount` para consultar as informações de montagem de todos os dispositivos. Certifique-se de que o resultado da execução não inclua as informações de partição do disco de dados correspondente.

### A imagem personalizada ainda existirá após a liberação da instância?
Sim.

### Posso alterar o sistema operacional de uma instância criada a partir de uma imagem personalizada? Após alterar o sistema operacional, ainda poderei usar a imagem personalizada original?
Sim. Você pode continuar a usar a imagem personalizada original após alterar o sistema operacional.


### Posso fazer upgrade da CPU, da memória, da largura de banda, do disco e de outras configurações de uma instância da CVM habilitada por uma imagem personalizada?
Sim. Você pode fazer upgrade de todos eles. Para mais informações, consulte [Alteração da configuração da instância](https://intl.cloud.tencent.com/document/product/213/2178) e [Ajuste da configuração da rede](https://intl.cloud.tencent.com/document/product/213/15517).

### É possível usar uma imagem personalizada entre regiões?
Não. Só é possível usar uma imagem personalizada na mesma região. Por exemplo, você não pode iniciar diretamente uma instância da CVM no Leste da China (Nanjing) usando a imagem personalizada criada a partir de uma instância da CVM no Leste da China (Xangai).
Para usar uma imagem personalizada entre regiões, primeiro copie a imagem na região de destino. Para mais informações, consulte [Cópia de imagens](https://intl.cloud.tencent.com/document/product/213/4943).

### Onde posso exibir o progresso de criação da imagem? Quanto tempo leva para criar uma imagem?
Você pode exibir o progresso de criação da imagem na página **Images (Imagens)** do console da CVM. O tempo necessário para criar uma imagem depende do tamanho dos dados da instância.


