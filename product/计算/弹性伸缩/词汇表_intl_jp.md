### AS 
ASは、ユーザーのビジネスニーズとポリシーに基づいて柔軟な計算リソースを自動的に調整する管理サービスです。
### スケーリンググループ 
スケーリンググループ（Scaling Group）は、同じ規則に従い、同じシナリオに向けるCVMインスタンスのセットです。スケーリンググループは、グループ内のCVMインスタンス数の最大値と最小値、およびそれらに関連付けられたCLBインスタンスなどの属性を定義します。
### 起動構成 
起動構成（Scaling Configuration）は、イメージID、CVMインスタンスの種類、システムディスクとデータディスクの種類と容量、暗号鍵ペア、セキュリティグループなどを含む、CVMを自動的に作成するためのテンプレートです。

スケーリンググループを作成するときに起動構成を指定する必要があります。起動構成が作成されると、そのプロパティは編集できません。
### アラームスケーリング 
CMグメトリック（CPU、メモリ、ネットワークトラフィックなど）に基づいてCVMインスタンスを自動的に増減します。
### 時限タスク 
時限タスク（Scheduled Scaling Task）は、ASのタイプの一種です。ある固定時点に達すると、CVMインスタンスは自動的に増減し、定期的な繰り返しがサポートされます。
### スケーリングポリシー 
スケーリングポリシー（Scaling Policy）は、スケーリング動作を実行するための条件です。トリガー条件は時間またはCMのためのアラームである場合もあり、動作はCVMから除去するかCVMに参加することである場合もあります。
### 時限スケーリングポリシー 
一定の時点に達すると、CVMインスタンスは自動的に増減され、定期的な繰り返しがサポートされます。

### 冷却時間 
冷却時間（Cooldown Period）は、同じスケーリンググループ内でスケーリングアクティビティーの実行が完了した後の一定のロック時間です。





