## Visão geral da funcionalidade
Depois que um nome de domínio for conectado ao CDN, todas as solicitações serão programadas para um nó do CDN. Se o recurso solicitado for armazenado em cache no nó, o recurso será retornado diretamente; caso contrário, a solicitação será repassada ao servidor de origem para efetuar o pull do recurso solicitado.

Como os nós do CDN respondem à maioria das solicitações, para ajudar a analisar o acesso dos usuários, os pacotes do CDN acessam os logs de toda a rede em uma granularidade horária e, por padrão, os retêm por 30 dias. Esses logs também podem ser baixados.

>? Atualmente, os logs de pull de origem não são fornecidos, apenas os logs de acesso aos nós são fornecidos.

## Visão geral
### Análise de comportamento de acesso
É possível baixar os logs de acesso e analisar os recursos populares e os usuários ativos.

### Monitoramento da qualidade do serviço
Ao baixar os logs de acesso, é possível atualizar-se sobre o status do serviço de todos os nós do CDN e calcular o tempo médio de resposta, a velocidade média de download e outras métricas.

## Guia de operação
### Como usar
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), clique em **Log Service (Serviço de log)** na barra lateral esquerda e selecione um nome de domínio e intervalo de tempo para consultar os logs de acesso. É possível selecionar vários pacotes de log e baixá-los em lotes:
![](https://mc.qcloudimg.com/static/img/043e70b6829ce67d6af125b51736b249/1.png)

>!
- Por padrão, os logs de acesso são empacotados a cada hora. Durante esse período, se não houver solicitação para o nome de domínio para a hora, nenhum pacote de log será gerado.
- Os logs de acesso de um nome de domínio de regiões dentro e fora da China Continental são empacotados separadamente. Os pacotes de log são nomeados no formato de "hora-nome de domínio-região de aceleração".
- Os logs de acesso são coletados de cada nó de cache do CDN, portanto, o atraso pode variar. Normalmente, os pacotes de log podem ser consultados e baixados após 30 minutos aproximadamente. Os pacotes de log serão adicionados continuamente e se estabilizarão após 2 a 3 horas.
- Os pacotes de log de acesso de um nome de domínio são retidos por 30 dias. Você pode usar uma função SCF para transferir os pacotes de log para o COS, conforme as instruções em [Armazenamento regular de logs do CDN](https://intl.cloud.tencent.com/document/product/228/36014) para armazenamento permanente.

### Campos
Os campos (da esquerda para a direita) nos logs são listados conforme abaixo:
<table style="width:660px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">Nº</th>
<th align="left" style="width:560px;font-weight:700">Campos  </th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>Tempo de solicitação</td>
</tr>
</tbody>
<tbody><tr>
<td>2</td>
<td>IP do cliente</td>
</tr>
</tbody>
<tbody><tr>
<td>3</td>
<td>Nome de domínio</td>
</tr>
</tbody>
<tbody><tr>
<td>4</td>
<td>Caminho da solicitação</td>
</tr>
</tbody>
<tbody><tr>
<td>5</td>
<td>Quantidade de bytes acessados desta vez, incluindo o tamanho do próprio arquivo e do cabeçalho da solicitação.</td>
</tr>
</tbody>
<tbody><tr>
<td>6</td>
<td>Números de províncias para os logs da China Continental; números de regiões para os logs fora da China Continental (consulte a tabela de mapeamento abaixo).</td>
</tr>
</tbody>
<tbody><tr>
<td>7</td>
<td>Números de ISPs para os logs da China Continental; O `-1` será usado para os logs fora da China Continental (consulte a tabela de mapeamento abaixo).</td>
</tr>
</tbody>
<tbody><tr>
<td>8</td>
<td>Código de status HTTP</td>
</tr>
</tbody>
<tbody><tr>
<td>9</td>
<td>Informação de referência</td>
</tr>
</tbody>
<tbody><tr>
<td>10</td>
<td>Tempo de resposta (em milissegundos), que se refere ao tempo que um nó leva para retornar todos os pacotes ao cliente depois de receber uma solicitação.</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>11</td>
<td>Informações do agente do usuário</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>12</td>
<td>Parâmetro de intervalo</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>13</td>
<td>Método HTTP</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>14</td>
<td>Identificador de protocolo HTTP</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>15</td>
<td>Acertos/erros do cache. Um acerto em um servidor de borda ou nó pai do CDN será marcado como acerto.</td>
</tr>
</tbody></table>

### Mapeamentos de regiões/ISPs

#### Províncias da China Continental
<table style="width:660px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">ID da região</th>
<th align="left" style="width:120px;font-weight:700">Região</th>
<th align="left" style="width:100px;font-weight:700">ID da região</th>
<th align="left" style="width:120px;font-weight:700">Região</th>
<th align="left" style="width:100px;font-weight:700">ID da região</th>
<th align="left" style="width:120px;font-weight:700">Região</th>
</tr>
</thead>
<tbody><tr>
<td>22</td>
<td>Pequim</td>
<td>86</td>
<td>Mongólia Interior</td>
<td>146</td>
<td>Shanxi</td>
</tr>
<tr>
<td>1069</td>
<td>Hebei</td>
<td>1177</td>
<td>Tianjin</td>
<td>119</td>
<td>Ningxia</td>
</tr>
<tr>
<td>152</td>
<td>Shaanxi</td>
<td>1208</td>
<td>Gansu</td>
<td>1467</td>
<td>Chingai</td>
</tr>
<tr>
<td>1468</td>
<td>Xinjiang</td>
<td>145</td>
<td>Heilongjiang</td>
<td>1445</td>
<td>Jilin</td>
</tr>
<tr>
<td>1464</td>
<td>Liaoning</td>
<td>2</td>
<td>Fujian</td>
<td>120</td>
<td>Jiangsu</td>
</tr>
<tr>
<td>121</td>
<td>Anhui</td>
<td>122</td>
<td>Shandong</td>
<td>1050</td>
<td>Xangai</td>
</tr>
<tr>
<td>1442</td>
<td>Zhejiang</td>
<td>182</td>
<td>Henan</td>
<td>1135</td>
<td>Hubei</td>
</tr>
<tr>
<td>1465</td>
<td>Jiangxi</td>
<td>1466</td>
<td>Hunan</td>
<td>118</td>
<td>Guizhou</td>
</tr>
<tr>
<td>153</td>
<td>Yunnan</td>
<td>1051</td>
<td>Chongqing</td>
<td>1068</td>
<td>Sichuan</td>
</tr>
<tr>
<td>1155</td>
<td>Tibete</td>
<td>4</td>
<td>Cantão</td>
<td>173</td>
<td>Guangxi</td>
</tr>
<tr>
<td>1441</td>
<td>Hainan</td>
<td>0</td>
<td>Outra</td>
<td>1</td>
<td>Hong Kong (China), Macau (China) e Taiwan (China)</td>
</tr>
<tr>
<td>-1</td>
<td>Fora da China Continental</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody></table>


#### ISPs da China Continental
<table style="width:660px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">ID do ISP</th>
<th align="left" style="width:120px;font-weight:700">ISP</th>
<th align="left" style="width:100px;font-weight:700">ID do ISP</th>
<th align="left" style="width:120px;font-weight:700">ISP</th>
<th align="left" style="width:100px;font-weight:700">ID do ISP</th>
<th align="left" style="width:120px;font-weight:700">ISP</th>
</tr>
</thead>
<tbody><tr>
<td>2</td>
<td>China Telecom</td>
<td>26</td>
<td>China Unicom</td>
<td>38</td>
<td>CERNET</td>
</tr>
</tbody>
<tbody><tr>
<td>43</td>
<td>Great Wall Broadband Network</td>
<td>1046</td>
<td>China Mobile</td>
<td>3947</td>
<td>China Mobile Tietong</td>
</tr>
</tbody>
<tbody><tr>
<td>-1</td>
<td>ISPs fora da China Continental</td>
<td>0</td>
<td>Outros ISPs</td>
<td></td>
<td></td>
</tr>
</tbody>
</table>


#### Regiões fora da China Continental
<table style="width:710px">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">ID da região</th>
<th align="left" style="width:170px;font-weight:700">Região</th>
<th align="left" style="width:100px;font-weight:700">ID da região</th>
<th align="left" style="width:120px;font-weight:700">Região</th>
<th align="left" style="width:100px;font-weight:700">ID da região</th>
<th align="left" style="width:120px;font-weight:700">Região</th>
</tr>
</thead>
<tbody><tr>
<td>2000000001</td>
<td>Zona 1 da Ásia-Pacífico (área de serviço)</td>
<td>765</td>
<td>Eslováquia</td>
<td>1613</td>
<td>Angola</td>
</tr>
<tr>
<td>2000000002</td>
<td>Zona 2 da Ásia-Pacífico (área de serviço)</td>
<td>766</td>
<td>Sérvia</td>
<td>1617</td>
<td>Costa do Marfim</td>
</tr>
<tr>
<td>2000000003</td>
<td>Zona 3 da Ásia-Pacífico (área de serviço)</td>
<td>770</td>
<td>Finlândia</td>
<td>1620</td>
<td>Sudão</td>
</tr>
<tr>
<td>2000000004</td>
<td>Oriente Médio (área de serviço)</td>
<td>773</td>
<td>Bélgica</td>
<td>1681</td>
<td>Ilhas Maurício</td>
</tr>
<tr>
<td>2000000005</td>
<td>América do Norte (área de serviço)</td>
<td>809</td>
<td>Bulgária</td>
<td>1693</td>
<td>Marrocos</td>
</tr>
<tr>
<td>2000000006</td>
<td>Europa (área de serviço)</td>
<td>811</td>
<td>Eslovênia</td>
<td>1695</td>
<td>Argélia</td>
</tr>
<tr>
<td>2000000007</td>
<td>América do Sul (área de serviço)</td>
<td>812</td>
<td>Moldávia</td>
<td>1698</td>
<td>Guiné</td>
</tr>
<tr>
<td>2000000008</td>
<td>África (área de serviço)</td>
<td>813</td>
<td>Macedônia</td>
<td>1730</td>
<td>Senegal</td>
</tr>
<tr>
<td>-20</td>
<td>Ásia (área de cliente)</td>
<td>824</td>
<td>Estônia</td>
<td>1864</td>
<td>Tunísia</td>
</tr>
<tr>
<td>-21</td>
<td>América do Sul (área de cliente)</td>
<td>835</td>
<td>Croácia</td>
<td>1909</td>
<td>Uruguai</td>
</tr>
<tr>
<td>-22</td>
<td>América do Norte (área de cliente)</td>
<td>837</td>
<td>Polônia</td>
<td>1916</td>
<td>Groenlândia</td>
</tr>
<tr>
<td>-23</td>
<td>Europa (área de cliente)</td>
<td>852</td>
<td>Letônia</td>
<td>2026</td>
<td>Taiwan (China)</td>
</tr>
<tr>
<td>-24</td>
<td>África (área de cliente)</td>
<td>857</td>
<td>Jordânia</td>
<td>2083</td>
<td>Myanmar</td>
</tr>
<tr>
<td>-25</td>
<td>Oceania (área de cliente)</td>
<td>884</td>
<td>Quirguistão</td>
<td>2087</td>
<td>Brunei</td>
</tr>
<tr>
<td>35</td>
<td>Nepal</td>
<td>896</td>
<td>Irlanda</td>
<td>2094</td>
<td>Sri Lanka</td>
</tr>
<tr>
<td>57</td>
<td>Tailândia</td>
<td>901</td>
<td>Líbia</td>
<td>2150</td>
<td>Panamá</td>
</tr>
<tr>
<td>73</td>
<td>Índia</td>
<td>904</td>
<td>Armênia</td>
<td>2175</td>
<td>Colômbia</td>
</tr>
<tr>
<td>144</td>
<td>Vietnã</td>
<td>921</td>
<td>Iêmen</td>
<td>2273</td>
<td>Mônaco</td>
</tr>
<tr>
<td>192</td>
<td>França</td>
<td>926</td>
<td>Bielorrússia</td>
<td>2343</td>
<td>Andorra</td>
</tr>
<tr>
<td>207</td>
<td>Reino Unido</td>
<td>971</td>
<td>Luxemburgo</td>
<td>2421</td>
<td>Turcomenistão</td>
</tr>
<tr>
<td>208</td>
<td>Suécia</td>
<td>1036</td>
<td>Nova Zelândia</td>
<td>2435</td>
<td>Laos</td>
</tr>
<tr>
<td>209</td>
<td>Alemanha</td>
<td>1044</td>
<td>Japão</td>
<td>2488</td>
<td>Timor-Leste</td>
</tr>
<tr>
<td>213</td>
<td>Itália</td>
<td>1066</td>
<td>Paquistão</td>
<td>2490</td>
<td>Tonga</td>
</tr>
<tr>
<td>214</td>
<td>Espanha</td>
<td>1070</td>
<td>Malta</td>
<td>2588</td>
<td>Filipinas</td>
</tr>
<tr>
<td>386</td>
<td>Emirados Árabes Unidos</td>
<td>1091</td>
<td>Bahamas</td>
<td>2609</td>
<td>Venezuela</td>
</tr>
<tr>
<td>391</td>
<td>Israel</td>
<td>1129</td>
<td>Argentina</td>
<td>2612</td>
<td>Bolívia</td>
</tr>
<tr>
<td>397</td>
<td>Ucrânia</td>
<td>1134</td>
<td>Bangladesh</td>
<td>2613</td>
<td>Brasil</td>
</tr>
<tr>
<td>398</td>
<td>Rússia</td>
<td>1158</td>
<td>Camboja</td>
<td>2623</td>
<td>Costa Rica</td>
</tr>
<tr>
<td>417</td>
<td>Cazaquistão</td>
<td>1159</td>
<td>Macau (China)</td>
<td>2626</td>
<td>México</td>
</tr>
<tr>
<td>428</td>
<td>Portugal</td>
<td>1176</td>
<td>Singapura</td>
<td>2639</td>
<td>Honduras</td>
</tr>
<tr>
<td>443</td>
<td>Grécia</td>
<td>1179</td>
<td>Maldivas</td>
<td>2645</td>
<td>El Salvador</td>
</tr>
<tr>
<td>471</td>
<td>Arábia Saudita</td>
<td>1180</td>
<td>Afeganistão</td>
<td>2647</td>
<td>Paraguai</td>
</tr>
<tr>
<td>529</td>
<td>Dinamarca</td>
<td>1185</td>
<td>Fiji</td>
<td>2661</td>
<td>Peru</td>
</tr>
<tr>
<td>565</td>
<td>Irã</td>
<td>1186</td>
<td>Mongólia</td>
<td>2728</td>
<td>Nicarágua</td>
</tr>
<tr>
<td>578</td>
<td>Noruega</td>
<td>1195</td>
<td>Indonésia</td>
<td>2734</td>
<td>Equador</td>
</tr>
<tr>
<td>669</td>
<td>Estados Unidos</td>
<td>1200</td>
<td>Hong Kong (China)</td>
<td>2768</td>
<td>Guatemala</td>
</tr>
<tr>
<td>692</td>
<td>Síria</td>
<td>1233</td>
<td>Catar</td>
<td>2999</td>
<td>Aruba</td>
</tr>
<tr>
<td>704</td>
<td>Chipre</td>
<td>1255</td>
<td>Islândia</td>
<td>3058</td>
<td>Etiópia</td>
</tr>
<tr>
<td>706</td>
<td>Tchéquia</td>
<td>1289</td>
<td>Albânia</td>
<td>3144</td>
<td>Bósnia e Herzegovina</td>
</tr>
<tr>
<td>707</td>
<td>Suíça</td>
<td>1353</td>
<td>Uzbequistão</td>
<td>3216</td>
<td>República Dominicana</td>
</tr>
<tr>
<td>708</td>
<td>Iraque</td>
<td>1407</td>
<td>San Marino</td>
<td>3379</td>
<td>Coreia do Sul</td>
</tr>
<tr>
<td>714</td>
<td>Países Baixos</td>
<td>1416</td>
<td>Kuwait</td>
<td>3701</td>
<td>Malásia</td>
</tr>
<tr>
<td>717</td>
<td>Romênia</td>
<td>1417</td>
<td>Montenegro</td>
<td>3839</td>
<td>Canadá</td>
</tr>
<tr>
<td>721</td>
<td>Líbano</td>
<td>1493</td>
<td>Tajiquistão</td>
<td>4450</td>
<td>Austrália</td>
</tr>
<tr>
<td>725</td>
<td>Hungria</td>
<td>1501</td>
<td>Bahrein</td>
<td>4460</td>
<td>China Continental - Norte da China</td>
</tr>
<tr>
<td>726</td>
<td>Geórgia</td>
<td>1543</td>
<td>Chile</td>
<td>-15</td>
<td>Ásia – outra</td>
</tr>
<tr>
<td>731</td>
<td>Azerbaijão</td>
<td>1559</td>
<td>África do Sul</td>
<td>-14</td>
<td>América do Sul – outra</td>
</tr>
<tr>
<td>734</td>
<td>Áustria</td>
<td>1567</td>
<td>Egito</td>
<td>-13</td>
<td>América do Norte – outra</td>
</tr>
<tr>
<td>736</td>
<td>Palestina</td>
<td>1590</td>
<td>Quênia</td>
<td>-12</td>
<td>Europa – outra</td>
</tr>
<tr>
<td>737</td>
<td>Turquia</td>
<td>1592</td>
<td>Nigéria</td>
<td>-11</td>
<td>África – outra</td>
</tr>
<tr>
<td>759</td>
<td>Lituânia</td>
<td>1598</td>
<td>Tanzânia</td>
<td>-10</td>
<td>Oceania – outra</td>
</tr>
<tr>
<td>763</td>
<td>Omã</td>
<td>1611</td>
<td>Madagascar</td>
<td>-2</td>
<td>Fora da China Continental – outra</td>
</tr>
</tbody></table>


#### ISPs fora da China Continental
<table style="width:220px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">ID do ISP</th>
<th align="left" style="width:120px;font-weight:700">ISP</th>
</tr>
</thead>
<tbody><tr>
<td>-1</td>
<td>ISPs fora da China Continental</td>
</tr>
</tbody>
</table>

### Observações
Os dados de tráfego/largura de banda calculados com base na quantidade de bytes registrados no quinto campo de um log de acesso são diferentes daqueles faturáveis do CDN pelo seguinte motivo:
- Apenas os dados da camada de aplicativos podem ser registrados nos logs de acesso. O tráfego gerado durante a transferência real de dados pela rede é cerca de 5 a 15% maior do que o tráfego da camada de aplicativos, incluindo as duas partes a seguir:
	- Consumo por cabeçalhos TCP/IP: nas solicitações HTTP baseadas em TCP/IP, cada pacote tem um tamanho máximo de 1.500 bytes. Isso inclui cabeçalhos TCP e IP que representam 40 bytes e geram tráfego durante a transferência, mas não podem ser contabilizados pela camada de aplicativos. O custo dessa parte é de cerca de 3%.
	- Retransmissão TCP: durante a transferência normal de dados pela rede, cerca de 3 a 10% dos pacotes são perdidos na internet e retransmitidos pelo servidor. Esse tipo de tráfego não pode ser contabilizado pela camada de aplicativos, que representa 3 a 7% do tráfego total.
- Como um padrão do setor, o tráfego faturável é a soma do tráfego da camada de aplicativos e as sobrecargas descritas acima. O CDN do Tencent Cloud considera 10% como a proporção de sobrecargas, então, o tráfego monitorado é cerca de 110% do tráfego registrado em log.

## Casos de uso

### Exemplo de log de acesso da China Continental
![](https://mc.qcloudimg.com/static/img/a3ef1ea051dc277872ec10a7135872df/logs.png)

### Exemplo de log de acesso fora da China Continental
![](https://main.qcloudimg.com/raw/b0612a5204abdbdc6a4364ad02972900.png)
