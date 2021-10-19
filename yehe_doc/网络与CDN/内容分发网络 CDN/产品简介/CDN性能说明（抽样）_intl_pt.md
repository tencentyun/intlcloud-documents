
## Descrições do teste

### Ferramentas de teste

Instância do CVM (1 núcleo, 1 GB de memória) e CDN do Tencent Cloud

### Método do teste

Usamos o método de teste de avaliação de desempenho comumente usado no setor. O provedor de serviços é a TingYun.

### Parâmetros do teste

| Período testado | 21 de maio de 2019 das 7h45 às 19h15 |
| ---------- | --------------------------------------------- |
| Cidade testada | Todas |
| ISP testado | China Unicom, China Telecom, China Mobile |
| Link do servidor de origem | http://*/simptab-wallpaper-20190520181120.png |
| Link do CDN | http://*/simptab-wallpaper-20190520181120.png |

## Análise dos resultados

### Curva de desempenho de latência

Unidade: segundo

![Curva de desempenho de latência](https://main.qcloudimg.com/raw/af4a2f1a8c977561950de6349f9ee755.jpg)

### Curva de disponibilidade

Em %

![Curva de disponibilidade (nova)](https://main.qcloudimg.com/raw/e868c5fc16cb145e785620091e1a10e5.jpg)

### Análise de gráfico

<table>
   <tr>
      <td rowspan="2">Tarefa de monitoramento</td>
      <td rowspan="2">Pontos de monitoramento</td>
      <td colspan="5">Desempenho (em segundos)</td>
      <td colspan="5">Disponibilidade (%)</td>
   </tr>
   <tr>
      <td colspan="1">Médio</td>
      <td colspan="2">Melhor</td>
      <td colspan="2">Pior</td>
      <td colspan="1">Média</td>
      <td colspan="2">Melhor</td>
      <td colspan="2">Pior</td>
   </tr>
   <tr>
      <td>CDN</td>
      <td>2235</td>
      <td>  0,196</td>
      <td>21 de maio às 7h45</td>
      <td>  0,117</td>
      <td>21 de maio às 12h15</td>
      <td>  0,313</td>
      <td> 99,996</td>
      <td>21 de maio às 7h45</td>
      <td>100,00</td>
      <td>21 de maio às 8h45</td>
      <td> 99,91</td>
   </tr>
   <tr>
      <td>Servidor de origem</td>
      <td>2177</td>
      <td>  0,933</td>
      <td>21 de maio às 10h45</td>
      <td>  0,635</td>
      <td>21 de maio às 8h15</td>
      <td>  1,827</td>
      <td> 99,035</td>
      <td>21 de maio às 7h45</td>
      <td>100,00</td>
      <td>21 de maio às 11h15</td>
      <td> 97,65</td>
   </tr>
</table>

### Detalhes dos dados

<table>
   <tr>
      <td rowspan="2">Hora</td>
      <td colspan="3">CDN</td>
      <td colspan="3">Servidor de origem</td>
   </tr>
   <tr>
      <td>Desempenho (em segundos)</td>
      <td>Disponibilidade (%)</td>
      <td>Pontos de monitoramento</td>
      <td>Desempenho (em segundos)</td>
      <td>Disponibilidade (%)</td>
      <td>Pontos de monitoramento</td>
   </tr>
   <tr>
      <td>21 de maio às 7h45</td>
      <td>  0,117</td>
      <td>100,00</td>
      <td> 98</td>
      <td>  0,945</td>
      <td>100,00</td>
      <td> 98</td>
   </tr>
   <tr>
      <td>21 de maio às 8h15</td>
      <td>  0,160</td>
      <td>100,00</td>
      <td> 91</td>
      <td>  1,827</td>
      <td> 98,86</td>
      <td> 88</td>
   </tr>
   <tr>
      <td>21 de maio às 8h45</td>
      <td>  0,135</td>
      <td> 99,91</td>
      <td> 92</td>
      <td>  0,645</td>
      <td>100,00</td>
      <td> 88</td>
   </tr>
   <tr>
      <td>21 de maio às 9h15</td>
      <td>  0,240</td>
      <td>100,00</td>
      <td> 97</td>
      <td>  0,821</td>
      <td> 98,95</td>
      <td> 95</td>
   </tr>
   <tr>
      <td>21 de maio às 9h45</td>
      <td>  0,190</td>
      <td>100,00</td>
      <td> 95</td>
      <td>  1,315</td>
      <td> 98,80</td>
      <td> 83</td>
   </tr>
   <tr>
      <td>21 de maio às 10h15</td>
      <td>  0,158</td>
      <td>100,00</td>
      <td> 95</td>
      <td>  0,745</td>
      <td> 98,95</td>
      <td> 95</td>
   </tr>
   <tr>
      <td>21 de maio às 10h45</td>
      <td>  0,170</td>
      <td>100,00</td>
      <td> 90</td>
      <td>  0,635</td>
      <td>100,00</td>
      <td> 89</td>
   </tr>
   <tr>
      <td>21 de maio às 11h15</td>
      <td>  0,123</td>
      <td>100,00</td>
      <td> 90</td>
      <td>  0,692</td>
      <td> 97,65</td>
      <td> 85</td>
   </tr>
   <tr>
      <td>21 de maio às 11h45</td>
      <td>  0,246</td>
      <td>100,00</td>
      <td> 96</td>
      <td>  0,653</td>
      <td>100,00</td>
      <td> 98</td>
   </tr>
   <tr>
      <td>21 de maio às 12h15</td>
      <td>  0,313</td>
      <td>100,00</td>
      <td> 89</td>
      <td>  0,763</td>
      <td> 97,83</td>
      <td> 92</td>
   </tr>
   <tr>
      <td>21 de maio às 12h45</td>
      <td>  0,258</td>
      <td>100,00</td>
      <td> 92</td>
      <td>  1,181</td>
      <td>100,00</td>
      <td> 93</td>
   </tr>
   <tr>
      <td>21 de maio às 13h15</td>
      <td>  0,175</td>
      <td>100,00</td>
      <td> 95</td>
      <td>  1,122</td>
      <td> 97,67</td>
      <td> 86</td>
   </tr>
   <tr>
      <td>21 de maio às 13h45</td>
      <td>  0,173</td>
      <td>100,00</td>
      <td> 97</td>
      <td>  1,148</td>
      <td> 98,89</td>
      <td> 90</td>
   </tr>
   <tr>
      <td>21 de maio às 14h15</td>
      <td>  0,257</td>
      <td>100,00</td>
      <td> 81</td>
      <td>  1,083</td>
      <td>100,00</td>
      <td> 81</td>
   </tr>
   <tr>
      <td>21 de maio às 14h45</td>
      <td>  0,214</td>
      <td>100,00</td>
      <td>103</td>
      <td>  1,044</td>
      <td>100,00</td>
      <td> 97</td>
   </tr>
   <tr>
      <td>21 de maio às 15h15</td>
      <td>  0,240</td>
      <td>100,00</td>
      <td> 92</td>
      <td>  0,737</td>
      <td> 97,98</td>
      <td> 99</td>
   </tr>
   <tr>
      <td>21 de maio às 15h45</td>
      <td>  0,169</td>
      <td>100,00</td>
      <td> 94</td>
      <td>  0,969</td>
      <td> 98,85</td>
      <td> 87</td>
   </tr>
   <tr>
      <td>21 de maio às 16h15</td>
      <td>  0,146</td>
      <td>100,00</td>
      <td> 93</td>
      <td>  0,769</td>
      <td> 98,86</td>
      <td> 88</td>
   </tr>
   <tr>
      <td>21 de maio às 16h45</td>
      <td>  0,269</td>
      <td>100,00</td>
      <td> 91</td>
      <td>  0,724</td>
      <td>100,00</td>
      <td> 86</td>
   </tr>
   <tr>
      <td>21 de maio às 17h15</td>
      <td>  0,181</td>
      <td>100,00</td>
      <td> 91</td>
      <td>  1,072</td>
      <td> 98,02</td>
      <td>101</td>
   </tr>
   <tr>
      <td>21 de maio às 17h45</td>
      <td>  0,208</td>
      <td>100,00</td>
      <td> 96</td>
      <td>  1,000</td>
      <td>100,00</td>
      <td> 90</td>
   </tr>
   <tr>
      <td>21 de maio às 18h15</td>
      <td>  0,219</td>
      <td>100,00</td>
      <td> 94</td>
      <td>  0,744</td>
      <td> 98,86</td>
      <td> 88</td>
   </tr>
   <tr>
      <td>21 de maio às 18h45</td>
      <td>  0,119</td>
      <td>100,00</td>
      <td> 81</td>
      <td>  0,841</td>
      <td> 98,84</td>
      <td> 86</td>
   </tr>
   <tr>
      <td>21 de maio às 19h15</td>
      <td>  0,212</td>
      <td>100,00</td>
      <td>102</td>
      <td>  0,981</td>
      <td> 97,87</td>
      <td> 94</td>
   </tr>
   <tr>
      <td>Média/Resumo</td>
      <td>  0,196</td>
      <td> 99,996</td>
      <td>2235</td>
      <td>  0,933</td>
      <td> 99,04</td>
      <td>2177</td>
   </tr>
   <tr>
      <td>Pontos excluídos</td>
      <td colspan="3">  0</td>
      <td colspan="3">  0</td>
   </tr>
</table>
