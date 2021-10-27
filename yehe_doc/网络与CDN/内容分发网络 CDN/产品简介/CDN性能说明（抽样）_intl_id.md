
## Deskripsi Pengujian

### Alat Pengujian

Instance CVM (1-core, memori 1 GB) dan Tencent Cloud CDN

### Metode Pengujian

Kami menggunakan metode pengujian tolok ukur yang lazim digunakan dalam industri ini. Penyedia layanan adalah TingYun.

### Parameter Pengujian

| Periode pengujian | 21 Mei 2019 07.45 - 19.15 |
| ---------- | --------------------------------------------- |
| Kota pengujian | Semua |
| ISP pengujian | China Unicom, China Telecom, China Mobile |
| Tautan server asal | http://*/simptab-wallpaper-20190520181120.png |
| Tautan CDN | http://*/simptab-wallpaper-20190520181120.png |

## Analisis Hasil

### Kurva Performa Latensi

Unit: kedua

![Kurva performa latensi](https://main.qcloudimg.com/raw/af4a2f1a8c977561950de6349f9ee755.jpg)

### Kurva Ketersediaan

Dalam %

![Kurva ketersediaan (baru)](https://main.qcloudimg.com/raw/e868c5fc16cb145e785620091e1a10e5.jpg)

### Analisis Bagan

<table>
   <tr>
      <td rowspan="2">Tugas Pemantauan</td>
      <td>Titik-Titik Pemantauan</td>
      <td colspan="5">Performa (dalam detik)</td>
      <td colspan="5">Ketersediaan (%)</td>
   </tr>
   <tr>
      <td colspan="1">Rata-rata</td>
      <td colspan="2">Terbaik</td>
      <td colspan="2">Terburuk</td>
      <td colspan="1">Rata-rata</td>
      <td colspan="2">Terbaik</td>
      <td colspan="2">Terburuk</td>
   </tr>
   <tr>
      <td>CDN</td>
      <td>2235</td>
      <td>  0,196</td>
      <td>21 Mei 07.45</td>
      <td>  0,117</td>
      <td>21 Mei 12.15</td>
      <td>  0,313</td>
      <td> 99,996</td>
      <td>21 Mei 07.45</td>
      <td>100,00</td>
      <td>21 Mei 08.45</td>
      <td> 99,91</td>
   </tr>
   <tr>
      <td>Server Asal</td>
      <td>2177</td>
      <td>  0,933</td>
      <td>21 Mei 10.45</td>
      <td>  0,635</td>
      <td>21 Mei 08.15</td>
      <td>  1,827</td>
      <td> 99,035</td>
      <td>21 Mei 07.45</td>
      <td>100,00</td>
      <td>21 Mei 11.15</td>
      <td> 97,65</td>
   </tr>
</table>

### Detail Data

<table>
   <tr>
      <td rowspan="2">Waktu</td>
      <td colspan="3">CDN</td>
      <td colspan="3">Server Asal</td>
   </tr>
   <tr>
      <td>Performa (dalam detik)</td>
      <td>Ketersediaan (%)</td>
      <td>Titik-Titik Pemantauan</td>
      <td>Performa (dalam detik)</td>
      <td>Ketersediaan (%)</td>
      <td>Titik-Titik Pemantauan</td>
   </tr>
   <tr>
      <td>21 Mei 07.45</td>
      <td>  0,117</td>
      <td>100,00</td>
      <td> 98</td>
      <td>  0,945</td>
      <td>100,00</td>
      <td> 98</td>
   </tr>
   <tr>
      <td>21 Mei 08.15</td>
      <td>  0,160</td>
      <td>100,00</td>
      <td> 91</td>
      <td>  1,827</td>
      <td> 98,86</td>
      <td> 88</td>
   </tr>
   <tr>
      <td>21 Mei 08.45</td>
      <td>  0,135</td>
      <td> 99,91</td>
      <td> 92</td>
      <td>  0,645</td>
      <td>100,00</td>
      <td> 88</td>
   </tr>
   <tr>
      <td>21 Mei 09.15</td>
      <td>  0,240</td>
      <td>100,00</td>
      <td> 97</td>
      <td>  0,821</td>
      <td> 98,95</td>
      <td> 95</td>
   </tr>
   <tr>
      <td>21 Mei 09.45</td>
      <td>  0,190</td>
      <td>100,00</td>
      <td> 95</td>
      <td>  1,315</td>
      <td> 98,80</td>
      <td> 83</td>
   </tr>
   <tr>
      <td>21 Mei 10.15</td>
      <td>  0,158</td>
      <td>100,00</td>
      <td> 95</td>
      <td>  0,745</td>
      <td> 98,95</td>
      <td> 95</td>
   </tr>
   <tr>
      <td>21 Mei 10.45</td>
      <td>  0,170</td>
      <td>100,00</td>
      <td> 90</td>
      <td>  0,635</td>
      <td>100,00</td>
      <td> 89</td>
   </tr>
   <tr>
      <td>21 Mei 11.15</td>
      <td>  0,123</td>
      <td>100,00</td>
      <td> 90</td>
      <td>  0,692</td>
      <td> 97,65</td>
      <td> 85</td>
   </tr>
   <tr>
      <td>21 Mei 11.45</td>
      <td>  0,246</td>
      <td>100,00</td>
      <td> 96</td>
      <td>  0,653</td>
      <td>100,00</td>
      <td> 98</td>
   </tr>
   <tr>
      <td>21 Mei 12.15</td>
      <td>  0,313</td>
      <td>100,00</td>
      <td> 89</td>
      <td>  0,763</td>
      <td> 97,83</td>
      <td> 92</td>
   </tr>
   <tr>
      <td>21 Mei 12.45</td>
      <td>  0,258</td>
      <td>100,00</td>
      <td> 92</td>
      <td>  1,181</td>
      <td>100,00</td>
      <td> 93</td>
   </tr>
   <tr>
      <td>21 Mei 13.15</td>
      <td>  0,175</td>
      <td>100,00</td>
      <td> 95</td>
      <td>  1,122</td>
      <td> 97,67</td>
      <td> 86</td>
   </tr>
   <tr>
      <td>21 Mei 13.45</td>
      <td>  0,173</td>
      <td>100,00</td>
      <td> 97</td>
      <td>  1,148</td>
      <td> 98,89</td>
      <td> 90</td>
   </tr>
   <tr>
      <td>21 Mei 14.15</td>
      <td>  0,257</td>
      <td>100,00</td>
      <td> 81</td>
      <td>  1,083</td>
      <td>100,00</td>
      <td> 81</td>
   </tr>
   <tr>
      <td>21 Mei 14.45</td>
      <td>  0,214</td>
      <td>100,00</td>
      <td>103</td>
      <td>  1,044</td>
      <td>100,00</td>
      <td> 97</td>
   </tr>
   <tr>
      <td>21 Mei 15.15</td>
      <td>  0,240</td>
      <td>100,00</td>
      <td> 92</td>
      <td>  0,737</td>
      <td> 97,98</td>
      <td> 99</td>
   </tr>
   <tr>
      <td>21 Mei 15.45</td>
      <td>  0,169</td>
      <td>100,00</td>
      <td> 94</td>
      <td>  0,969</td>
      <td> 98,85</td>
      <td> 87</td>
   </tr>
   <tr>
      <td>21 Mei 16.15</td>
      <td>  0,146</td>
      <td>100,00</td>
      <td> 93</td>
      <td>  0,769</td>
      <td> 98,86</td>
      <td> 88</td>
   </tr>
   <tr>
      <td>21 Mei 16.45</td>
      <td>  0,269</td>
      <td>100,00</td>
      <td> 91</td>
      <td>  0,724</td>
      <td>100,00</td>
      <td> 86</td>
   </tr>
   <tr>
      <td>21 Mei 17.15</td>
      <td>  0,181</td>
      <td>100,00</td>
      <td> 91</td>
      <td>  1,072</td>
      <td> 98,02</td>
      <td>101</td>
   </tr>
   <tr>
      <td>21 Mei 17.45</td>
      <td>  0,208</td>
      <td>100,00</td>
      <td> 96</td>
      <td>  1,000</td>
      <td>100,00</td>
      <td> 90</td>
   </tr>
   <tr>
      <td>21 Mei 18.15</td>
      <td>  0,219</td>
      <td>100,00</td>
      <td> 94</td>
      <td>  0,744</td>
      <td> 98,86</td>
      <td> 88</td>
   </tr>
   <tr>
      <td>21 Mei 18.45</td>
      <td>  0,119</td>
      <td>100,00</td>
      <td> 81</td>
      <td>  0,841</td>
      <td> 98,84</td>
      <td> 86</td>
   </tr>
   <tr>
      <td>21 Mei 19.15</td>
      <td>  0,212</td>
      <td>100,00</td>
      <td>102</td>
      <td>  0,981</td>
      <td> 97,87</td>
      <td> 94</td>
   </tr>
   <tr>
      <td>Rata-Rata/Ringkasan</td>
      <td>  0,196</td>
      <td> 99,996</td>
      <td>2235</td>
      <td>  0,933</td>
      <td> 99,04</td>
      <td>2177</td>
   </tr>
   <tr>
      <td>Titik-titik yang dikecualikan</td>
      <td colspan="3">  0</td>
      <td colspan="3">  0</td>
   </tr>
</table>
