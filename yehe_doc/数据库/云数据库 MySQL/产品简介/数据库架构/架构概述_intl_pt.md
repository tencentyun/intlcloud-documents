O TencentDB for MySQL fornece três tipos de arquiteturas: nó único (anteriormente Edição básica), dois nós (anteriormente Edição de alta disponibilidade) e três nós (anteriormente Edição financeira).As instâncias de nó único geral eram conhecidas como instâncias de edição de alta E/S de nó único (single-node).
>! Nó único (anteriormente Edição básica) está atualmente em processo de reconstrução e modernização, e as vendas serão suspensas durante esse período.

## Exibição das arquiteturas de instâncias
- Para instâncias a serem adquiridas, faça login na [página de aquisição do TencentDB for MySQL](https://buy.cloud.tencent.com/cdb) e selecione a arquitetura na seção **Architecture (Arquitetura)**.
- Para instâncias já adquiridas, faça login no [Console do MySQL](https://console.cloud.tencent.com/cdb), localize a instância desejada na lista de instâncias e exiba sua arquitetura na coluna **Configuration (Configuração)**.

## Comparação de arquiteturas
<table>
<thead>
<tr><th>Arquitetura</th><th >Dois nós</th><th>Três nós</th><th colspan=2>Nó único</th>
</thead>
<tbody><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/39794">Política de isolamento de recursos</a></td>
<td>Geral</td><td>Geral</td><td>Geral</td><td>Básica</td></tr>
<tr>
<td>Versões compatíveis</td>
<td>MySQL 5.5, 5.6, 5.7 e 8.0</td><td>MySQL 5.6, 5.7 e 8.0</td><td>MySQL 5.6, 5.7 e 8.0</td><td>MySQL 5.7</td></tr>
<tr>
<td>Nó</td>
<td>Uma source, uma réplica</td><td>Uma source, duas réplicas</td><td>Nó único</td><td>Nó único</td></tr>
<tr>
<td>Modo de replicação de réplica de source</td>
<td>Assíncrona (padrão), semissincronizada</td><td>Assíncrona (padrão), sincronização forte e semissincronizada</td><td>-</td><td>-</td></tr>
<tr>
<td>Disponibilidade da instância</td>
<td>99,95%</td><td>99,99%</td><td>-</td><td>-</td></tr>
<tr>
<td>Armazenamento subjacente</td>
<td>SSD NVMe local</td><td>SSD NVMe local</td><td>SSD NVMe local</td><td>Disco em nuvem premium</td></tr>
<tr>
<td>Desempenho</td>
<td>Até 240 mil IOPS</td><td>Até 240 mil IOPS</td><td>-</td><td>Fórmula de cálculo de IOPS: <br>{mín 1.500 + 8 x capacidade do disco, máx 4.500}</td></tr>
<tr>
<td>Casos de uso</td>
<td>Jogos, internet, IoT, varejo, comércio eletrônico, logística, seguros, títulos etc.</td>
<td>Jogos, internet, IoT, varejo, comércio eletrônico, logística, seguros, títulos etc.</td>
<td>Aplicações com requisitos de separação de leitura/gravação</td>
<td>Aprendizagem pessoal, sites de pequeno porte, sistemas não essenciais para pequenas empresas, e desenvolvimento e testes de empresas de médio a grande porte</td></tr>
</tbody></table>

## Documentação
- O TencentDB for MySQL é compatível com o MySQL 8.0, 5.7, 5.6 e 5.5. Para mais informações, consulte [Versões de bancos de dados](https://intl.cloud.tencent.com/document/product/236/31896).
- O TencentDB for MySQL fornece os seguintes tipos de instância: instâncias de source e réplicas somente leitura. Para mais informações, consulte os [Tipos de instâncias de banco de dados](https://intl.cloud.tencent.com/document/product/236/7268).
- O TencentDB for MySQL fornece funcionalidades diferentes em arquiteturas diferentes. Para mais informações, consulte [Lista das diferenças nas funcionalidades](https://intl.cloud.tencent.com/document/product/236/36007).
