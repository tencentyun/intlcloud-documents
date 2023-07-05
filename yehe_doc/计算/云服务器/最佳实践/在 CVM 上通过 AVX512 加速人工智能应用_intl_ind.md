## Ikhtisar
Instans Tencent Cloud CVM generasi kelima (termasuk S5, M5, C4, IT5, D3, dll.) semuanya dilengkapi dengan prosesor Cascade Lake generasi kedua yang dapat diskalakan dari Intel<sup>®</sup> Xeon<sup>®</sup>. Instans ini menyediakan lebih banyak serangkaian petunjuk dan fitur, yang dapat mempercepat aplikasi kecerdasan buatan (AI). Teknologi peningkatan perangkat keras terintegrasi, seperti Advanced Vector Extensions 512 (AVX-512), dapat meningkatkan performa komputasi paralel untuk inferensi AI dan menghasilkan hasil pembelajaran mendalam yang lebih baik.

Dokumen ini menjelaskan cara menggunakan AVX-512 pada instans CVM S5 dan M5 untuk mempercepat aplikasi AI.

## Model yang Direkomendasikan[](id:RecommendedSelection)
Tencent Cloud menyediakan berbagai jenis CVM untuk pengembangan aplikasi yang berbeda. Jenis instans [Standard S6](https://intl.cloud.tencent.com/document/product/213/11518)、[Standard S5](https://intl.cloud.tencent.com/document/product/213/11518) dan [Memory Optimized M5](https://intl.cloud.tencent.com/document/product/213/11518) dilengkapi dengan prosesor Intel<sup>®</sup> Xeon<sup>®</sup> generasi ke-2 dan mendukung Intel<sup>®</sup> DL Boost, membuatnya cocok untuk pembelajaran mesin atau pembelajaran mendalam. Konfigurasi yang direkomendasikan adalah sebagai berikut:
<table>
<tr>
<th>Skenario</th><th>Spesifikasi Instans</th>
</tr>
<tr>
<td>Platform pelatihan pembelajaran mendalam</td>
<td>84vCPU Standard S5 atau 48vCPU Memory Optimized M5</td>
</tr>
<tr>
<td>Platform inferensi pembelajaran mendalam</td>
<td>8/16/24/32/48vCPU Standard S5 atau Memory Optimized M5</td>
</tr>
<tr>
<td>Pelatihan pembelajaran mendalam atau platform inferensi</td>
<td>48vCPU Standard S5 atau 24vCPU Memory Optimized M5</td>
</tr>
</table>

 ## Keuntungan
Menjalankan beban kerja untuk pembelajaran mesin atau pembelajaran mendalam pada prosesor Intel<sup>®</sup> Xeon<sup>®</sup> yang dapat diskalakan memiliki keuntungan sebagai berikut:
- Cocok untuk memproses topologi 3D-CNN yang digunakan dalam skenario seperti beban kerja memori besar, pencitraan medis, GAN, analisis seismik, pengurutan gen, dll.
- Dukungan inti yang fleksibel hanya dengan menggunakan perintah `numactl`, dan berlaku untuk inferensi online skala kecil.
- Ekosistem yang canggih melakukan pelatihan terdistribusi pada kluster besar secara langsung, tanpa memerlukan arsitektur skala besar yang berisi penyimpanan berkapasitas besar tambahan dan mekanisme caching yang mahal.
- Dukungan untuk banyak beban kerja (seperti HPC, BigData, dan AI) dalam satu kluster untuk memberikan TCO yang lebih baik.
- Dukungan akselerasi SIMD untuk memenuhi persyaratan komputasi berbagai aplikasi pembelajaran mendalam.
- Infrastruktur yang sama untuk pelatihan langsung dan inferensi.

## Petunjuk
### Membuat instans
Buat instans seperti yang diinstruksikan di [Membuat Instans melalui Halaman Pembelian CVM](https://intl.cloud.tencent.com/document/product/213/4855). Pilih [model yang direkomendasikan](#RecommendedSelection) yang sesuai dengan kasus penggunaan aktual Anda.
![](https://main.qcloudimg.com/raw/ceb104790caba9f281f4515f00d32585.png)

>?Untuk informasi selengkapnya tentang spesifikasi instans, lihat [Jenis Instans](https://intl.cloud.tencent.com/document/product/213/11518).

### Login ke instans
1. [Login ke instans Linux menggunakan metode login standar](https://intl.cloud.tencent.com/document/product/213/5436).

### Men-deploy platform
Deploy platform AI seperti yang diinstruksikan di bawah ini untuk melakukan pembelajaran mesin atau tugas pembelajaran mendalam:

### Contoh 1: mengoptimalkan kerangka pembelajaran mendalam TensorFlow* dengan Intel<sup>®</sup>
PyTorch dan IPEX pada prosesor Intel <sup>®</sup> Xeon<sup>®</sup> generasi ke-2 yang dapat diskalakan Cascade Lake akan secara otomatis mengoptimalkan instruksi AVX-512 untuk memaksimalkan performa komputasi.

TensorFlow\* adalah pembelajaran mesin skala besar dan kerangka kerja pembelajaran mendalam yang banyak digunakan. Anda dapat meningkatkan pelatihan instans dan performa inferensi seperti yang diinstruksikan dalam contoh di bawah ini. Informasi selengkapnya tentang kerangka kerja, lihat [Panduan Penginstalan Intel<sup>®</sup> Optimization for TensorFlow\*](https://software.intel.com/content/www/us/en/develop/articles/intel-optimization-for-tensorflow-installation-guide.html). Ikuti langkah-langkah ini:

#### Men-deploy kerangka kerja TensorFlow\*
1. Instal Python di instans CVM. Dokumen ini menggunakan Python 3.7 sebagai contoh.
2. Jalankan perintah berikut untuk menginstal Intel<sup>®</sup> yang dioptimalkan TensorFlow\* intel-tensorflow.
>?**Version 2.4.0 or later** (Versi 2.4.0 atau yang lebih baru) direkomendasikan untuk mendapatkan fitur dan pengoptimalan terbaru.
>
```
pip install intel-tensorflow
```

#### Mengatur parameter runtime
Pilih salah satu dari dua antarmuka runtime berikut untuk mengoptimalkan parameter runtime sesuai kebutuhan. Untuk informasi selengkapnya tentang pengaturan pengoptimalan, lihat [Praktik Terbaik Umum untuk Intel<sup>®</sup> Optimization for TensorFlow](https://github.com/IntelAI/models/blob/master/docs/general/tensorflow/GeneralBestPractices.md).
 - **Batch inference** (Inferensi batch): mengukur berapa banyak tensor input yang dapat diproses per detik dengan batch berukuran lebih besar dari satu. Biasanya, untuk inferensi batch, performa optimal dicapai dengan menjalankan semua inti fisik pada soket CPU.
 - **On-line Inference** (Inferensi Online): (juga disebut inferensi real-time) adalah pengukuran waktu yang diperlukan untuk memproses tensor input tunggal, yaitu batch ukuran satu. Dalam skenario inferensi real-time, throughput optimal dicapai dengan menjalankan beberapa instans secara bersamaan.

Ikuti langkah-langkah di bawah ini:
1. Jalankan perintah berikut untuk mendapatkan jumlah inti fisik dalam sistem.
```
lscpu | grep "Core(s) per socket" | cut -d':' -f2 | xargs
```
2. Atur parameter pengoptimalan menggunakan salah satu metode:
 - Mengatur parameter runtime. Tambahkan konfigurasi berikut di file variabel lingkungan:
``` 
 export OMP_NUM_THREADS= # <physicalcores>
 export KMP_AFFINITY="granularity=fine,verbose,compact,1,0"
 export KMP_BLOCKTIME=1
 export KMP_SETTINGS=1
 export TF_NUM_INTRAOP_THREADS= # <physicalcores>
 export TF_NUM_INTEROP_THREADS=1
 export TF_ENABLE_MKL_NATIVE_FORMAT=0
```
 - Tambahkan variabel lingkungan ke kode. Tambahkan konfigurasi berikut ke kode Python yang sedang berjalan.
```
import os
os.environ["KMP_BLOCKTIME"] = "1"
os.environ["KMP_SETTINGS"] = "1"
os.environ["KMP_AFFINITY"]= "granularity=fine,verbose,compact,1,0"
if FLAGS.num_intra_threads > 0:
    os.environ["OMP_NUM_THREADS"]= # <physical cores>
os.environ["TF_ENABLE_MKL_NATIVE_FORMAT"] = "0"
config = tf.ConfigProto()
config.intra_op_parallelism_threads = # <physical cores>
config.inter_op_parallelism_threads = 1
tf.Session(config=config)
```

#### Menjalankan inferensi pada model pembelajaran mendalam TensorFlow\*
Jalankan inferensi pada pembelajaran mesin lain atau model pembelajaran mendalam seperti yang diinstruksikan dalam [Pengenalan Citra dengan ResNet50, ResNet101 dan InceptionV3](https://github.com/IntelAI/models/blob/master/docs/image_recognition/tensorflow/Tutorial.md). Dokumen ini menjelaskan cara menjalankan pengukuran inferensi dengan ResNet50. Untuk informasi selengkapnya, lihat [ResNet50 (v1.5)](https://github.com/IntelAI/models/blob/master/benchmarks/image_recognition/tensorflow/resnet50v1_5/README.md).

#### Pelatihan model pembelajaran mendalam TensorFlow\*
Dokumen ini menjelaskan cara menjalankan pengukuran pelatihan dengan ResNet50. Untuk informasi selengkapnya, lihat [Petunjuk Pelatihan FP32](https://github.com/IntelAI/models/blob/master/benchmarks/image_recognition/tensorflow/resnet50v1_5/README.md#fp32-training-instructions).

#### Performa TensorFlow

Data performa seperti yang ditunjukkan dalam [Meningkatkan Performa Inferensi TensorFlow* pada Prosesor Intel® Xeon®](https://www.intel.com/content/www/us/en/artificial-intelligence/posts/improving-tensorflow-inference-performance-on-intel-xeon-processors.html), yang mungkin sedikit berbeda menurut model dan konfigurasi aktual.
 - **Latency performance** (Performa latensi):
    Kami menguji model klasifikasi citra dan deteksi objek pada ukuran satu batch, dan menemukan peningkatan performa inferensi Intel Optimization for TensorFlow dengan instruksi AVX-512 terhadap versi yang tidak dioptimalkan. Misalnya, performa latensi ResNet 50 yang dioptimalkan berkurang hingga 45% dari versi aslinya.
 - **Throughput performance** (Performa throughput):
    Kami menguji model klasifikasi citra dan deteksi objek untuk performa throughput pada ukuran batch besar, dan menemukan peningkatan yang signifikan. Performa throughput dari ResNet 50 yang dioptimalkan meningkat menjadi 1,98 kali lipat dari versi aslinya.

### Contoh 2: men-deploy kerangka kerja pembelajaran PyTorch*
#### Petunjuk deployment
1. Instal Python 3.6 atau versi yang lebih baru di instans CVM. Dokumen ini menggunakan Python 3.7 sebagai contoh.
2. Kompilasi dan instal PyTorch dan Intel<sup>®</sup> Extension for PyTorch (IPEX) seperti yang diinstruksikan di [Intel<sup>®</sup> Extension for PyTorch](https://github.com/intel/intel-extension-for-pytorch#installation).

#### Mengatur parameter runtime

PyTorch dan IPEX pada prosesor Intel <sup>®</sup> Xeon<sup>®</sup> generasi ke-2 yang dapat diskalakan Cascade Lake akan secara otomatis mengoptimalkan instruksi AVX-512 untuk memaksimalkan performa komputasi.

Ikuti langkah-langkah ini untuk mengonfigurasi optimasi parameter runtime. Untuk informasi selengkapnya tentang konfigurasi, lihat [Memaksimalkan Performa Intel® Software Optimization for PyTorch* pada CPU](https://software.intel.com/content/www/us/en/develop/articles/how-to-get-better-performance-on-pytorchcaffe2-with-intel-acceleration.html).
 - **Batch inference** (Inferensi batch): mengukur berapa banyak tensor input yang dapat diproses per detik dengan batch berukuran lebih besar dari satu. Biasanya, untuk inferensi batch, performa optimal dicapai dengan menjalankan semua inti fisik pada soket CPU.
 - **On-line Inference** (Inferensi Online): (juga disebut inferensi real-time) adalah pengukuran waktu yang diperlukan untuk memproses tensor input tunggal pada ukuran satu batch, yaitu batch ukuran satu. Dalam skenario inferensi real-time, throughput optimal dicapai dengan menjalankan beberapa instans secara bersamaan.

Ikuti langkah-langkah di bawah ini:

1. Jalankan perintah berikut untuk mendapatkan jumlah inti fisik dalam sistem.
```
lscpu | grep "Core(s) per socket" | cut -d':' -f2 | xargs
```
2. Atur parameter pengoptimalan menggunakan salah satu metode:
 - Gunakan Pustaka GNU OpenMP* untuk mengatur parameter runtime. Tambahkan konfigurasi berikut di file variabel lingkungan:
``` 
export OMP_NUM_THREADS=physicalcores
export GOMP_CPU_AFFINITY="0-<physicalcores-1>"
export OMP_SCHEDULE=STATIC
export OMP_PROC_BIND=CLOSE
```
 - Gunakan Pustaka Intel OpenMP* untuk mengatur parameter runtime. Tambahkan konfigurasi berikut di file variabel lingkungan:
``` 
export OMP_NUM_THREADS=physicalcores
export LD_PRELOAD=<path_to_libiomp5.so>
export KMP_AFFINITY="granularity=fine,verbose,compact,1,0"
export KMP_BLOCKTIME=1
export KMP_SETTINGS=1
```


#### Pengoptimalan inferensi dan pelatihan dalam model pembelajaran mendalam PyTorch*

- Gunakan Ekstensi Intel<sup>®</sup> untuk PyTorch guna meningkatkan performa inferensi model. Contoh kodenya adalah sebagai berikut:
```
import intel_pytorch_extension
...
net = net.to('xpu')       # Pindahkan model ke format IPEX
data = data.to('xpu')     # Pindahkan data ke format IPEX
...
output = net(data)        # Lakukan inferensi dengan IPEX
output = output.to('cpu') # Pindahkan output kembali ke format ATen
```
- Baik inferensi maupun pelatihan dapat menggunakan jemalloc untuk meningkatkan performa. jemalloc adalah implementasi `malloc(3)` tujuan umum yang menekankan penghindaran fragmentasi dan dukungan konkurensi yang dapat diskalakan. Hal ini dimaksudkan untuk digunakan sebagai pengalokasi memori yang disediakan sistem. jemalloc menyediakan banyak fitur introspeksi, manajemen memori, dan penyesuaian di luar fungsi pengalokasi standar. Untuk informasi selengkapnya, lihat [jemalloc](https://github.com/jemalloc/jemalloc/wiki) dan [kode sampel](https://github.com/mingfeima/op_bench-py/blob/master/run.sh).
- Untuk informasi selengkapnya tentang pelatihan terdistribusi untuk beberapa soket, lihat [Skrip Pelatihan CPU Terdistribusi untuk PSSP-Transformer](https://github.com/mingfeima/pssp/blob/master/pssp-transformer/dist_train_cpu.sh).

#### Hasil performa

Diuji pada prosesor Cascade Lake generasi ke-2 Intel <sup>®</sup> Xeon<sup>®</sup> yang dapat diskalakan dengan 2*CPU (28 core per CPU) dan memori 384 GB, model yang berbeda memperoleh data performa seperti yang ditunjukkan pada [Intel dan Facebook* berkolaborasi untuk meningkatkan performa CPU PyTorch*](https://software.intel.com/content/www/us/en/develop/articles/intel-and-facebook-collaborate-to-boost-pytorch-cpu-performance.html). Hasil performa berbeda-beda tergantung pada model dan konfigurasi aktual.


### Contoh 3: menggunakan Alat Pengoptimalan Presisi Rendah Intel<sup>®</sup>AI untuk akselerasi


Alat Pengoptimalan Presisi Rendah Intel<sup>®</sup> (Intel<sup>®</sup> LPOT) adalah pustaka Python sumber terbuka yang menghadirkan antarmuka inferensi presisi rendah yang mudah digunakan di beberapa kerangka kerja jaringan neural. Hal ini membantu pengguna mengukur model, meningkatkan produktivitas, dan mempercepat performa inferensi model presisi rendah pada prosesor Intel<sup>®</sup> Xeon<sup>®</sup> DL Boost generasi ke-3 yang dapat diskalakan. Untuk informasi selengkapnya, lihat [Repositori kode Alat Pengoptimalan Presisi Rendah Intel<sup>®</sup>](https://github.com/Intel/lpot/).

#### Kerangka kerja jaringan neural yang didukung
Intel<sup>®</sup> LPOT mendukung kerangka kerja berikut:
TensorFlow* yang dioptimalkan Intel<sup>®</sup>, termasuk `v1.15.0`, `v1.15.0up1`, `v1.15.0up2`, `v2.0.0`, `v2.1.0`, `v2.2.0` , `v2.3.0`, dan `v2.4.0`.
PyTorch yang dioptimalkan Intel<sup>®</sup>, termasuk `v1.5.0+cpu` dan `v1.6.0+cpu`.
MXNet yang dioptimalkan Intel<sup>®</sup>, termasuk `v1.6.0`, `v1.7.0`; ONNX-Runtime: `v1.6.0`.

#### Kerangka kerja implementasi
Gambar berikut menunjukkan kerangka kerja implementasi Intel<sup>®</sup> LPOT:
![](https://main.qcloudimg.com/raw/6062f647b40e2900354fbc73d8a4248a.jpg)

#### Alur kerja
Gambar berikut menunjukkan alur kerja Intel<sup>®</sup> LPOT:
![](https://main.qcloudimg.com/raw/acbc366d69819b443064ba5df58608fc.png)

#### Performa dan akurasi model terkuantisasi

Tabel di bawah menunjukkan performa dan akurasi yang dicapai oleh model yang dioptimalkan Intel® LPOT pada prosesor Intel<sup>®</sup> Xeon<sup>®</sup> generasi ke-2 yang dapat diskalakan Cascade Lake:

<table class="docutils">
<thead>
  <tr>
    <th rowspan="2">Kerangka kerja</th>
    <th rowspan="2">Versi</th>
    <th rowspan="2">Model</th>
    <th colspan="3">Akurasi</th>
    <th>Percepatan performa</th>
  </tr>
  <tr>
    <td>Akurasi Penyesuaian INT8</td>
    <td>Garis Dasar Akurasi FP32</td>
    <td>Rasio Acc [(INT8-FP32)/FP32]</td>
    <td>Rasio Latensi Realtime [FP32/INT8]</td>
  </tr>
</thead>
<tbody>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>resnet50v1.5</td>
    <td>76,92%</td>
    <td>76,46%</td>
    <td>0,60%</td>
    <td>3,37x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>renet101</td>
    <td>77,18%</td>
    <td>76,45%</td>
    <td>0,95%</td>
    <td>2,53x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>inception_v1</td>
    <td>70,41%</td>
    <td>69,74%</td>
    <td>0,96%</td>
    <td>1,89x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>inception_v2</td>
    <td>74,36%</td>
    <td>73,97%</td>
    <td>0,53%</td>
    <td>1,95x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>inception_v3</td>
    <td>77,28%</td>
    <td>76,75%</td>
    <td>0,69%</td>
    <td>2,37x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>inception_v4</td>
    <td>80,39%</td>
    <td>80,27%</td>
    <td>0,15%</td>
    <td>2,60x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>inception_resnet_v2</td>
    <td>80,38%</td>
    <td>80,40%</td>
    <td>-0,02%</td>
    <td>1,98x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>mobilenetv1</td>
    <td>73,29%</td>
    <td>70,96%</td>
    <td>3,28%</td>
    <td>2,93x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>ssd_resnet50_v1</td>
    <td>37,98%</td>
    <td>38,00%</td>
    <td>-0,05%</td>
    <td>2,99x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>mask_rcnn_inception_v2</td>
    <td>28,62%</td>
    <td>28,73%</td>
    <td>-0,38%</td>
    <td>2,96x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>vgg16</td>
    <td>72,11%</td>
    <td>70,89%</td>
    <td>1,72%</td>
    <td>3,76x</td>
  </tr>
  <tr>
    <td>tensorflow</td>
    <td>2.4.0</td>
    <td>vgg19</td>
    <td>72,36%</td>
    <td>71,01%</td>
    <td>1,90%</td>
    <td>3,85x</td>
  </tr>
</tbody>
</table>

<table class="docutils">
<thead>
  <tr>
    <th rowspan="2">Kerangka kerja</th>
    <th rowspan="2">Versi</th>
    <th rowspan="2">Model</th>
    <th colspan="3">Akurasi</th>
    <th>Percepatan performa</th>
  </tr>
  <tr>
    <td>Akurasi Penyesuaian INT8</td>
    <td>Garis Dasar Akurasi FP32</td>
    <td>Rasio Acc [(INT8-FP32)/FP32]</td>
    <td>Rasio Latensi Realtime [FP32/INT8]</td>
  </tr>
</thead>
<tbody>
  <tr>
    <td>pytorch</td>
    <td>1.5.0+cpu</td>
    <td>renet50</td>
    <td>75,96%</td>
    <td>76,13%</td>
    <td>-0,23%</td>
    <td>2,46x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.5.0+cpu</td>
    <td>resnext101_32x8d</td>
    <td>79,12%</td>
    <td>79,31%</td>
    <td>-0,24%</td>
    <td>2,63x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_base_mrpc</td>
    <td>88,90%</td>
    <td>88,73%</td>
    <td>0,19%</td>
    <td>2,10x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_base_cola</td>
    <td>59,06%</td>
    <td>58,84%</td>
    <td>0,37%</td>
    <td>2,23x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_base_sts-b</td>
    <td>88,40%</td>
    <td>89,27%</td>
    <td>-0,97%</td>
    <td>2,13x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_base_sst-2</td>
    <td>91,51%</td>
    <td>91,86%</td>
    <td>-0,37%</td>
    <td>2,32x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_base_rte</td>
    <td>69,31%</td>
    <td>69,68%</td>
    <td>-0,52%</td>
    <td>2,03x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_large_mrpc</td>
    <td>87,45%</td>
    <td>88,33%</td>
    <td>-0.99%</td>
    <td>2,65x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_large_squad</td>
    <td>92,85</td>
    <td>93,05</td>
    <td>-0,21%</td>
    <td>1,92x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_large_qnli</td>
    <td>91,20%</td>
    <td>91,82%</td>
    <td>-0,68%</td>
    <td>2,59x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_large_rte</td>
    <td>71,84%</td>
    <td>72,56%</td>
    <td>-0.99%</td>
    <td>1,34x</td>
  </tr>
  <tr>
    <td>pytorch</td>
    <td>1.6.0a0+24aac32</td>
    <td>bert_large_cola</td>
    <td>62,74%</td>
    <td>62,57%</td>
    <td>0,27%</td>
    <td>2,67x</td>
  </tr>
</tbody>
</table>

<dx-alert infotype="explain" title="">
Baik PyTorch maupun Tensorflow yang ditampilkan dalam tabel adalah kerangka kerja yang dioptimalkan untuk Intel. Daftar model terkuantisasi lengkap tersedia di [Model Tervalidasi Penuh](https://github.com/intel/lpot/blob/master/docs/full_model_list.md).
</dx-alert>



#### Menginstal dan menggunakan Intel<sup>®</sup> LPOT 

1. Jalankan perintah berikut secara berurutan untuk membuat lingkungan virtual python3.x bernama `lpot` di anaconda. Dokumen ini menggunakan python 3.7 sebagai contoh.
```plaintext
conda create -n lpot python=3.7
conda activate lpot
```
2. Instal LPOT menggunakan salah satu metode:
    - Jalankan perintah berikut untuk menginstal dari file biner.
``` plaintext
pip install lpot
```
    - Jalankan perintah berikut untuk menginstal dari sumber.
```plaintext
 git clone https://github.com/intel/lpot.git
 cd lpot
 pip install -r requirements.txt
 python setup.py install
```
3. Ukur TensorFlow ResNet50 v1.0, misalnya.
    1. Siapkan kumpulan data.
Jalankan perintah berikut untuk mengunduh dan mendekompresi kumpulan data validasi mageNet.
```plaintext
mkdir -p img_raw/val && cd img_raw
wget http://www.image-net.org/challenges/LSVRC/2012/dd31405981
ef5f776aa17412e1f0c112/ILSVRC2012_img_val.tar
tar -xvf ILSVRC2012_img_val.tar -C val
``` 
Jalankan perintah berikut untuk memindahkan file citra ke dalam subdirektori yang diklasifikasikan berdasarkan label.
```plaintext
cd val
wget -qO -https://raw.githubusercontent.com/soumith/
imagenetloader.torch/master/valprep.sh | bash
``` 
Jalankan perintah berikut untuk mengonversi data mentah ke format TFrecord menggunakan skrip [prepare_dataset.sh](https://github.com/intel/lpot/blob/master/examples/tensorflow/image_recognition/prepare_dataset.sh).
```plaintext
cd examples/tensorflow/image_recognition
bash prepare_dataset.sh --output_dir=./data --raw_dir=/PATH/TO/img_raw/val/ 
--subset=validation
``` 
Untuk informasi selengkapnya tentang kumpulan data, lihat [Siapkan Kumpulan Data](https://github.com/intel/lpot/tree/master/examples/tensorflow/image_recognition#2-prepare-dataset).
    2. Jalankan perintah berikut untuk menyiapkan model.
 ```plaintext
wget https://storage.googleapis.com/intel-optimized-tensorflow/
 models/v1_6/resnet50_fp32_pretrained_model.pb
```
    3. Jalankan perintah berikut untuk menyesuaikan inferensi.
Modifikasi file `examples/tensorflow/image_recognition/resnet50_v1.yaml` sehingga jalur kumpulan data `quantization\calibration`, `evaluation\accuracy`, dan `evaluation\performance` mengarah ke jalur aktual lokal Anda, yaitu lokasi Data TFrecord dihasilkan dalam persiapan kumpulan data. Untuk informasi selengkapnya, lihat [ResNet50 V1.0](https://github.com/intel/lpot/tree/master/examples/tensorflow/image_recognition#1-resnet50-v10).
```plaintext
cd examples/tensorflow/image_recognition
bash run_tuning.sh --config=resnet50_v1.yaml \
--input_model=/PATH/TO/resnet50_fp32_pretrained_model.pb \
--output_model=./lpot_resnet50_v1.pb
```
    4. Jalankan perintah berikut untuk menjalankan pengukuran.
```plaintext
bash run_benchmark.sh --input_model=./lpot_resnet50_v1.pb
--config=resnet50_v1.yaml
```
Hasilnya adalah sebagai berikut, dengan data performa hanya untuk referensi:
```shell
 hasil pengukuran mode akurasi:
 Akurasi adalah 0,739
 Ukuran batch = 32
 Latensi: 1,341 mdtk
 Throughput: 745,631 citra/dtk
 hasil benchmark mode performa:
 Akurasi adalah 0,000
 Ukuran batch = 32
 Latensi: 1,300 mdtk
 Throughput: 769,302 citra/dtk
```

### Contoh 4: menggunakan Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit untuk akselerasi inferensi
Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit adalah perangkat lengkap untuk men-deploy visi komputer dan aplikasi pembelajaran mendalam lainnya dengan cepat. Hal ini mendukung berbagai akselerator Intel termasuk VPU untuk CPU, GPU, FPGA dan Movidius, dan juga mendukung eksekusi perangkat keras heterogen langsung.

Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit mengoptimalkan model yang dilatih oleh TensorFlow\* dan PyTorch\*. Hal ini mencakup Model Optimizer, Inference Engine, Open Model Zoo, Post-training Optimization Tool:

- **Model Optimizer** (Pengoptimal Model): mencakup model yang dilatih dalam kerangka kerja seperti Caffe\*, TensorFlow\*, PyTorch\*, dan Mxnet\* hingga representasi perantara (IR).
- **Inference Engine** (Mesin Inferensi): menempatkan IR yang dikonversi pada banyak jenis perangkat keras termasuk CPU, GPU, FPGA, dan VPU untuk mengaktifkan akselerasi inferensi dengan panggilan otomatis ke perangkat akselerator perangkat keras.

Untuk informasi selengkapnya, lihat [Situs web Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit](https://software.intel.com/content/www/us/en/develop/tools/openvino-toolkit.html) atau [Ikhtisar OpenVINO™ Toolkit](https://docs.openvinotoolkit.org/latest/index.html).

#### Alur kerja
Gambar berikut menunjukkan alur kerja Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit:
![](https://main.qcloudimg.com/raw/98afcac361352773801fbe863d21b912.png)

#### Performa inferensi Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit
Intel® Distribution of OpenVINO™ menyediakan implementasi pengoptimalan pada beberapa prosesor Intel dan perangkat keras akselerator. Berdasarkan prosesor Intel <sup>®</sup> Xeon<sup>®</sup> yang dapat diskalakan, prosesor ini mempercepat jaringan inferensi menggunakan instruksi Intel<sup>®</sup> DL Boost dan AVX-512. 

 #### Menggunakan Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit - Deep Learning Development Toolkit (DLDT)
 Lihat dokumen berikut:
- [Pengantar Intel<sup>®</sup> Deep Learning Deployment Toolkit](https://docs.openvinotoolkit.org/downloads/cn/I03030-9-Introduction%20to%20Intel_%20Deep%20Learning%20Deployment%20Toolkit%20-%20OpenVINO_%20Toolkit.pdf)
-  [Image Classification C++ Sample Async](https://docs.openvinotoolkit.org/downloads/cn/I03030-10-Image%20Classification%20Cpp%20Sample%20Async%20-%20OpenVINO_%20Toolkit.pdf)
-  [Object Detection C++ Sample SSD](https://docs.openvinotoolkit.org/downloads/cn/I03030-11-Object%20Detection%20Cpp%20Sample%20SSD%20-%20OpenVINO_%20Toolkit.pdf)
-  [Automatic Speech Recognition C++ Sample](https://docs.openvinotoolkit.org/downloads/cn/I03030-12-Automatic%20Speech%20Recognition%20Cpp%20%20Sample%20-%20OpenVINO_%20Toolkit.pdf)
-  [Action Recognition Python* Demo](https://docs.openvinotoolkit.org/downloads/cn/I03030-13-Action%20Recognition%20Python%20Demo%20-%20OpenVINO_%20Toolkit.pdf)
-  [Crossroad Camera C++ Demo](https://docs.openvinotoolkit.org/downloads/cn/I03030-14-Crossroad%20Camera%20Cpp%20%20Demo%20-%20OpenVINO_%20Toolkit.pdf)
- [Human Pose Estimation C++ Demo](https://docs.openvinotoolkit.org/downloads/cn/I03030-15-Human%20Pose%20Estimation%20Cpp%20Demo%20-%20OpenVINO_%20Toolkit.pdf)

#### Pengujian pengukuran Intel<sup>®</sup> Distribution of OpenVINO™ Toolkit
Untuk informasi selengkapnya, lihat [Menginstal toolkit Intel<sup>®</sup> Distribution of OpenVINO™ untuk Linux*](https://docs.openvinotoolkit.org/downloads/cn/I03030-5-Install%20Intel_%20Distribution%20of%20OpenVINO_%20toolkit%20for%20Linux%20-%20OpenVINO_%20Toolkit.pdf).


