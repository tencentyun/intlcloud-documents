### どのようにしてTencent Cloud Elastic Microserviceを購入しますか。
Tencent Cloud Elastic Microserviceは現在ベータ版テスト段階です。この製品の体験を希望する場合はベータ版テスト申請を提出してください。審査の後、ベータ版テスト期間中は無料で使用することができます。


### Tencent Cloud Elastic Microserviceはどの言語をサポートしていますか。
Tencent Cloud Elastic Microserviceは現在Java言語のマイクロサービスアプリケーションをサポートしています。非マイクロサービスアプリケーションの場合は、Dockerイメージを作成してTencent Cloud Elastic Microserviceにアップロードすると、任意の言語のアプリケーションをデプロイするのに役立ちます。


### 業務がすべてCVM上にあり、Tencent Cloud Elastic Microserviceに移行するには、コードの変更が必要ですか。
Tencent Cloud Elastic Microserviceは無侵入アクセスに重点を置いており、業務コードを変更する必要がなく、移行コストを大幅に低減します。Eureka、Consulを登録センターとするSpring Cloudアプリケーションを例にとると、Tencent Cloud Elastic Microserviceに移行する場合、いかなる変更も必要がなく、ユーザーが気づかないうちに移行がスムーズに実行されます。


### Tencent Cloud Elastic Microserviceのメンテナンスフリーはどのように実現しますか。
Tencent Cloud Elastic MicroserviceではリソースのServerless化が提供され、容量の評価、マシンリソースの購入が必要ありません。これ以外に、Tencent Cloud Elastic Microserviceはアプリケーションのワンクリックデプロイ、監視の自動化、サービス管理などの機能を提供しており、マイクロサービスの運用保守のハードルを下げ、メンテナンスフリー機能を実現しています。


### Tencent Cloud Elastic Microserviceはどの程度のリソース自動スケーリングをサポートしていますか。
Tencent Cloud Elastic Microserviceは自動スケーリングの比較的細かいリソース粒度をサポートしており、最小でCPU 0.25コアのスケーリングをサポートし、リソースコストを非常に節約することができます。


### Tencent Cloud Elastic Microserviceはどの監視指標を提供していますか。
Tencent Cloud Elastic Microserviceは現在ベータ版テスト段階で基本監視機能（CPU、メモリレベルの監視）を提供しています。将来、業務レベルに基づき、QPS、レスポンス遅延、スロークエリーなどの監視指標が提供されます。

### Tencent Cloud Elastic Microserviceを使用していますが、Tencent Cloudのその他のサービス（Redis、CKafka）などを使用することはできますか。
Tencent Cloud Elastic MicroserviceはTencent Cloudの他のサービスを完全に含んでおり、Redis、CKafkaなどにアクセスでき、制限はありません。


### Tencent Cloud Elastic MicroserviceとTencent Service Frameworkにはどんな違いがありますか。
-Tencent Service Frameworkは現在CVMおよびContainer Servicesに基づくデプロイをサポートしています。この2種類のデプロイメントモデルは事前にピーク時のビジネスリソースを準備する必要があり、スケーリング操作も非常に面倒です。
- Tencent Cloud Elastic Microserviceは、必要に応じて使用する従量課金であり、メンテナンスフリーで使用することができ、事前にリソースを準備する必要がありません。
