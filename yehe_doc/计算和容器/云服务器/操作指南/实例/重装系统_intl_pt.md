## Visão geral

A reinstalação do sistema é um método importante para restaurar as instâncias aos seus status iniciais em caso de falha do sistema.

Os CVM são compatíveis com os seguintes dois tipos de reinstalação:
 - **Reinstalação de sistema único**: os CVMs em todas as regiões podem ser reinstalados no mesmo sistema operacional.
 Por exemplo, o Linux é reinstalado como Linux e o Windows é reinstalado como Windows. 
 - **Reinstalação entre sistemas**: apenas os CVMs na China Continental (exceto em Hong Kong, na China) podem ser reinstalados em um sistema operacional diferente.
 Por exemplo, o Linux é reinstalado como Windows e o Windows é reinstalado como Linux.
>? 
> - Atualmente, todas as novas instâncias do CBS e os discos locais são compatíveis com a reinstalação entre sistemas. No entanto, alguns discos locais de 20 GB existentes não são compatíveis com a reinstalação entre sistemas por meio do console. Se você precisar implementar a reinstalação entre sistemas para instâncias nesses discos locais, [envie um tíquete](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=7&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM) para solicitar a funcionalidade de instalação entre sistemas.
> - As instâncias spot não são compatíveis com a reinstalação de sistema.

## Observações
 - **Preparação para a reinstalação:** faça backup dos dados importantes no disco do sistema antes da reinstalação, pois os dados do disco do sistema serão perdidos após a reinstalação. Para manter os dados do sistema, recomendamos que você [crie uma imagem personalizada](https://intl.cloud.tencent.com/document/product/213/4942) e use essa imagem para reinstalar o sistema.
 - **Seleção de imagem:** recomendamos que você use a imagem fornecida pelo Tencent Cloud ou sua imagem personalizada em vez de aquelas de fontes desconhecidas ou outras. Não execute outras operações enquanto o disco do sistema estiver sendo reinstalado.
 - **Recursos físicos da instância:** o IP público da instância não será alterado.
 - **Faturamento:** ao ajustar o tamanho do disco do sistema (apenas para o CBS), você será cobrado de acordo com os padrões de preços do CBS. Para obter mais informações, consulte a [Lista de preços](https://intl.cloud.tencent.com/document/product/213/2255).
 - **Operações subsequentes:** depois que o disco do sistema for reinstalado, os dados nos discos de dados não serão afetados e estarão disponíveis para uso somente depois que os discos de dados forem remontados.

## Direções

Você pode usar um dos seguintes métodos para reinstalar o sistema operacional:
- [Reinstalar o sistema pelo console](#consoleRestart)
- [Reinstalar o sistema pelas APIs](#apiRestart)

<span id="consoleRestart"></span>
### Reinstalação do sistema pelo console

1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
2. Na linha da instância para a qual deseja reinstalar o sistema, clique em **More (Mais)** > **Reinstall the system (Reinstalar o sistema)**, conforme mostrado na figura a seguir:
![Reinstalar o sistema](https://main.qcloudimg.com/raw/cf9c32f589a0243d84d6db0b92ccad2e.png)
3. Na janela pop-up que é exibida, clique em **OK, reinstall now (OK, reinstalar agora)**.
4. Selecione a imagem usada pela instância atual ou outra imagem, defina o tamanho do disco, defina a senha de login para a instância e clique em **Start reinstall (Iniciar reinstalação)**.
![](https://main.qcloudimg.com/raw/868508ad1ab1e1e2a60ea98d5d936a92.png)

<span id="apiRestart"></span>
### Reinstalação do sistema pelas APIs

Para obter mais informações, consulte a API [ResetInstance](https://intl.cloud.tencent.com/document/product/213/33242).

## Operações subsequentes
Se o seu CVM montou um disco de dados antes da reinstalação entre sistemas, consulte os seguintes documentos sobre como ler os dados dos discos de dados do sistema operacional original:
- [Leitura/gravação de discos de dados EXT depois de reinstalar um CVM do Linux para CVM do Windows](https://intl.cloud.tencent.com/document/product/213/3856)
- [Leitura/gravação de discos de dados NTFS depois de reinstalar um CVM do Windows para CVM do Linux](https://intl.cloud.tencent.com/document/product/213/3857)
