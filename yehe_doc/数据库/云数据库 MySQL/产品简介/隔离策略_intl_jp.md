
本ドキュメントではTencentDB for MySQLの隔離ポリシーについて、基本型、汎用型、専用型を含めてご紹介いたします。

>?
>- 元の基本バージョンのアーキテクチャを「単一ノード-基本型」にアップグレードすると、元の単一ノードの高IOバージョンが「単一ノード-汎用型」にアップグレードされます。
>- 2ノードおよび3ノードのアーキテクチャでは共通型および独自型分離ポリシーがサポートされます。

| 隔離ポリシー | 説明                                                         |
| -------- | ------------------------------------------------------------ |
| 基本型   | 単一ノードのみが基本型の隔離ポリシーをサポートします（元の基本バージョン）。計算とストレージは分離され、基盤はクラウドストレージを採用しています。 |
| 汎用型   | <li>割り当てられたメモリと磁気ディスクを独占し、同一の物理マシン上の他の汎用仕様のインスタンスとCPUリソースを共有します。 <li>リソースを再利用することでスケールメリットを享受し、コストパフォーマンスが高く、CPUリソースはわずかな再利用で済みます。 <li>磁気ディスクのサイズはCPUやメモリに依存しないため、柔軟に選択することができます。 |
| 専用型   | <li>CPU（コアをバインド）、メモリおよび磁気ディスクのリソースを完全に独占して使用するため、長期にわたり性能が安定し、物理マシンの他のインスタンスによる影響を受けません。  <li>専用型のハイエンド構成は物理マシンを独占し、物理マシンのすべてのリソースを完全に独占します。 | 


##　異なるインスタンスのアーキテクチャ分離ポリシーの説明
- TencentDB for MySQLのシングルノード（クラウドストレージ版）は、クラウドネイティブのTKEに基づいて配置されており、各インスタンスはそれぞれCPU、メモリ、ディスクを使用し、異なるインスタンス間は完全に分離されています。
- TencentDB for MySQLの2ノード（ローカルディスク）と3ノード（ローカルディスク）は、ローカル物理マシンに基づいて配置され、各物理マシンには複数のインスタンスが配置されています。分離ポリシーによって、異なるインスタンス間の完全な分離が保証され、CPU、メモリ、ディスクが単独で使用されます。
このほかTencentDB for MySQLもアカウント、リージョン、アベイラビリティーゾーン、ネットワークなどについても必要なデータ分離ポリシーを作成しています。
  
