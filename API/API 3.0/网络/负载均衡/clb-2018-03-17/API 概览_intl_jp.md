## アプリケーション型CLB関連API

| API名 | API機能 |
|---------|---------|
| [DescribeTaskStatus](/document/api/214/30683) | 非同期タスクのステータスの照合 |
| [CreateLoadBalancer](/document/api/214/30692) | ロードバランサーインスタンスの購入 |
| [DescribeLoadBalancers](/document/api/214/30685) | ロードバランサーインスタンスリストの照合 |
| [ModifyLoadBalancerAttributes](/document/api/214/30680) | ロードバランサーインスタンスの属性の変更 |
| [DeleteLoadBalancer](/document/api/214/30689) | ロードバランサーインスタンスの削除 |
| [CreateListener](/document/api/214/30693) | CLBリスナーの作成 |
| [DescribeListeners](/document/api/214/30686) | アプリケーション型CLBリスナーリストの照合 |
| [ModifyListener](/document/api/214/30681) | CLBリスナーの属性の変更 |
| [DeleteListener](/document/api/214/30690) | CLBリスナーの削除 |
| [CreateRule](/document/api/214/30691) | CLB 7層リスナー転送規則の作成 |
| [ModifyDomain](/document/api/214/30682) | 7層転送規則のドメイン名の変更 |
| [ModifyRule](/document/api/214/30679) | アプリケーション型CLBリスナー転送規則の変更 |
| [DeleteRule](/document/api/214/30688) | アプリケーション型7層CLBリスナー規則の削除 |
| [RegisterTargets](/document/api/214/30676) | RSのリスナーへのバインディング |
| [DescribeTargets](/document/api/214/30684) | アプリケーション型CLBのCVMリストの照合 |
| [ModifyTargetPort](/document/api/214/30678) | リスナーにバインディングされているRSのポートの変更 |
| [ModifyTargetWeight](/document/api/214/30677) | リスナーにバインディングされているRSの転送重みの変更 |
| [DeregisterTargets](/document/api/214/30687) | アプリケーション型CLBリスナーに登録されたRSのバインディング解除 |

## 従来型CLB関連API

| API名 | API機能 |
|---------|---------|
| [DescribeClassicalLBListeners](/document/api/214/31791) | 従来型CLBリスナーリストの取得 |
| [RegisterTargetsWithClassicalLB](/document/api/214/31789) | RSの従来型CLBへのバインディング |
| [DescribeClassicalLBTargets](/document/api/214/31790) | 従来型CLBにバインディングされたRSリストの取得 |
| [DescribeClassicalLBHealthStatus](/document/api/214/31792) | 従来型CLBバックエンドの正常性の取得 |
| [DeregisterTargetsFromClassicalLB](/document/api/214/31794) | 従来型CLBのRSのバインディング解除 |
| [DescribeClassicalLBByInstanceId](/document/api/214/31793) | バックエンドCVMを介したそのバインディングされた従来型CLBの逆引き検索 |


