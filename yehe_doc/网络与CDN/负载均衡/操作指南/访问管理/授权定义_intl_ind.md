## Tipe Sumber Daya CLB yang Dapat Diotorisasi di CAM
| Tipe Sumber Daya | Deskripsi Sumber Daya dalam Kebijakan Otorisasi |
| :-------- | -------------- |
| Instance CLB |  ` qcs::clb:$region::clb/$loadbalancerid`  |
| Server asli CLB | `qcs::cvm:$region:$account:instance/$cvminstanceid` |

Berikut:
- `$region` harus selalu berisi ID wilayah dan boleh dikosongi.
- `$account` harus selalu berisi `AccountId` pemilik sumber daya atau `*`.
- `$loadbalancerid` harus selalu berisi ID instance CLB atau `*`.

Dan seterusnya...

## API yang Dapat Diotorisasi untuk CLB di CAM
Anda dapat mengotorisasi tindakan berikut untuk sumber daya CLB di CAM.
### Instance

| Operasi API | Deskripsi Sumber Daya | Deskripsi API |
| :-------- | :--------| :------ |
| DescribeLoadBalancers |  Membuat kueri daftar instance CLB | `*` menunjukkan agar hanya mengautentikasi API |
| CreateLoadBalancer |  Membeli instance CLB | `qcs:$projectid:clb:$region:$account:clb/*` |
| DeleteLoadBalancers |  Menghapus instance CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyLoadBalancerAttributes |  Memodifikasi atribut instance CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyForwardLBName |  Mengganti nama instance CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |

### Pendengar

| Operasi API | Deskripsi Sumber Daya | Deskripsi API |
| :-------- | :---------| :------ |
| DeleteLoadBalancerListeners | Menghapus pendengar CLB| `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| DescribeLoadBalancerListeners | Menampilkan daftar pendengar CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyLoadBalancerListener | Memodifikasi atribut pendengar CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| CreateLoadBalancerListeners | Membuat pendengar CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| DeleteForwardLBListener | Menghapus pendengar CLB (lapisan 4 dan lapisan 7) | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| ModifyForwardLBSeventhListener | Memodifikasi atribut pendengar lapisan 7 CLB | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| ModifyForwardLBFourthListener | Memodifikasi atribut pendengar lapisan 4 CLB | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| DescribeForwardLBListeners | Membuat kueri daftar pendengar CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| CreateForwardLBSeventhLayerListeners | Membuat pendengar lapisan 7 CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| CreateForwardLBFourthLayerListeners | Membuat pendengar lapisan 4 CLB| `qcs::clb:$region:$account:clb/$loadbalancerid` |

### URL dan nama domain CLB

| Operasi API | Deskripsi Sumber Daya | Deskripsi API |
| :-------- | --------| :------ |
| ModifyForwardLBRulesDomain | Memodifikasi nama domain aturan penerusan pendengar CLB | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| CreateForwardLBListenerRules |Membuat aturan penerusan pendengar CLB | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| DeleteForwardLBListenerRules | Menghapus aturan pendengar CLB lapisan 7 | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| DeleteRewrite | Menghapus hubungan pengalihan aturan penerusan instance CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ManualRewrite | Secara manual menambahkan hubungan pengalihan aturan penerusan instance CLB | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| AutoRewrite | Secara otomatis membuat hubungan pengalihan aturan penerusan instance CLB | `qcs::clb:$region:$account:clb/$loadbalancerid`  |

### Server asli

| Operasi API | Deskripsi Sumber Daya | Deskripsi API |
| :-------- | :--------| :------ |
| ModifyLoadBalancerBackends | Memodifikasi berat server asli instance CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| DescribeLoadBalancerBackends | Menampilkan daftar server asli yang terikat dengan instance CLB | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| DeregisterInstancesFromLoadBalancer | Melepaskan server asli | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| RegisterInstancesWithLoadBalancer | Mengikat server asli ke instance CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| DescribeLBHealthStatus | Membuat kueri status kondisi CLB | `qcs::clb:$region:$account:clb/$loadbalancerid`  |
| ModifyForwardFourthBackendsPort | Memodifikasi port instance CVM dalam aturan penerusan pendengar lapisan 4 | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| ModifyForwardFourthBackendsWeight | Memodifikasi berat instance CVM dalam aturan penerusan pendengar lapisan 4 | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| RegisterInstancesWithForwardLBSeventhListener | Mengikat instance CVM ke aturan penerusan pendengar lapisan 7 CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| RegisterInstancesWithForwardLBFourthListener | Mengikat instance CVM ke aturan penerusan pendengar lapisan 4 CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| DeregisterInstancesFromForwardLBFourthListener | Melepaskan instance CVM dari aturan penerusan pendengar lapisan 4 CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| DeregisterInstancesFromForwardLB | Melepaskan instance CVM dari aturan penerusan pendengar lapisan 7 CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| ModifyForwardSeventhBackends | Memodifikasi berat instance CVM dalam aturan penerusan pendengar lapisan 7 | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| ModifyForwardSeventhBackendsPort | Memodifikasi port instance CVM dalam aturan penerusan pendengar lapisan 7 | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| DescribeForwardLBBackends | Membuat kueri daftar instance CVM dari instance CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/*` |
| DescribeForwardLBHealthStatus | Membuat kueri status pemeriksaan kondisi CLB | `qcs::clb:$region:$account:clb/*`  |
| ModifyLoadBalancerRulesProbe | Memodifikasi jalur penerusan dan pemeriksaan kondisi aturan penerusan pendengar CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |


