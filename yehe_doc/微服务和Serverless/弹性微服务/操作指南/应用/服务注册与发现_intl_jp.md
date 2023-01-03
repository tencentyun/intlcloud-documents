## 操作シナリオ

ここでは、主にTEMコンソールでSpringCloudアプリケーションサービスの登録と検出を実装するための具体的な手順を紹介します。

## 操作手順
### コンソール操作

1. [TEMコンソール](https://console.cloud.tencent.com/tem)にログインします。
2. 左側のナビゲーションバーで、**アプリケーション管理**をクリックしてアプリケーション管理ページに進み、アプリケーションをデプロイするリージョンを選択します。
3. **新規作成**をクリックしてアプリケーションの新規作成ページに進み、アプリケーション情報を入力してデプロイします。[アプリケーションの作成とデプロイ](https://intl.cloud.tencent.com/document/product/1094/40362)をご参照ください。
4. Spring Cloudアプリケーションの場合、選択した**環境のパブリッシュ**がレジストリにバインドされている場合、デプロイする際に**レジストリ情報を自動的に挿入**を選択することができます。

### 具体的な構成

レジストリの自動挿入を選択した場合、ユーザーがデプロイを送信すると、TEMは自動的にレジストリのデフォルトパラメータをpropertiesの形式で環境内の`tse-config`という名前のConfigMapに保存します。また、[VolumeMounts](https://kubernetes.io/docs/concepts/storage/volumes/#configmap)の形式で、アプリケーションの`/config/tse-default-spring-cloud-config.properties`ディレクトリにマウントします。

同時にTEMは、このディレクトリをアプリケーションの [SPRING_CONFIG_ADDITIONAL-LOCATION](https://docs.spring.io/spring-boot/docs/2.1.8.RELEASE/reference/html/boot-features-external-config.html#boot-features-external-config-application-property-files)環境変数に追加します。SPRING_CONFIG_ADDITIONAL-LOCATIONがアプリケーションに存在しない場合、この環境変数はアプリケーションに追加されます。

基本構成は次のとおりです。
<dx-codeblock>
:::  bash
apiVersion: v1
kind: Deployment
metadata:
  name: my-service
spec:
  containers:
    - name: my-service
      image: my-image
      env:
        - name: SPRING_CONFIG_ADDITIONAL-LOCATION
          value: file:/config/tse-default-spring-cloud-config.properties
      volumeMounts:
        - name: tse-config
          mountPath: /config/tse-default-spring-cloud-config.properties
          subPath: tse-default-spring-cloud-config.properties
  volumes:
    - name: tse-config
      configMap:  
        name: tse-config
        items:
          - key: tse-default-spring-cloud-config.properties
            path: tse-default-spring-cloud-config.properties
:::
</dx-codeblock>


TEMはそれぞれのレジストリに応じて、異なるパラメータを注入します。
<dx-tabs>
::: zookeeper
申請するzookeeperのアドレスを10.0.1.30:2181と仮定します。
<dx-codeblock>
:::  bash
apiVersion: v1
data:
  tse-default-spring-cloud-config.properties: |
    spring.cloud.zookeeper.connectString=10.0.1.30:2181
    spring.cloud.zookeeper.discovery.preferIpAddress=true
kind: ConfigMap
metadata:
  name: tse-config
:::
</dx-codeblock>
:::

::: nacos
申請するnacosのアドレスを10.0.120.11:8848と仮定します。
<dx-codeblock>
:::  bash
apiVersion: v1
data:
  tse-default-spring-cloud-config.properties: |
    spring.cloud.nacos.discovery.server-addr=10.0.120.11:8848
kind: ConfigMap
metadata:
  name: tse-config
:::
</dx-codeblock>
:::
</dx-tabs>



## 説明と注意事項

### preferIpAddressについて

ここでは、挿入されたすべてのレジストリパラメータにxxx.preferIpAddress=trueが追加されます。これは、Spring CloudがローカルIP（TEMのPod IP）を取得すると、IPに従ってドメイン名を自動的に逆引きするからです。preferIpAddressがfalse（デフォルトはfalse）であると判断した場合は、ドメイン名を使用して登録します。それ以外の場合はIPを介して登録します。

TEMでは、Pod IPはPodNameにマッピングされます。つまり、preferIpAddress=trueが設定されていない場合、レジストリに登録されているアドレスはPodNameとなります。他のサービスがレジストリからプルするサービスインスタンスのアドレスはPodNameであるため、PodNameを介してインスタンスにアクセスすることができなくなります。

### Spring boot additional locationについて

TEMによって自動的に追加される環境変数 [SPRING_CONFIG_ADDITIONAL-LOCATION](https://docs.spring.io/spring-boot/docs/2.1.8.RELEASE/reference/html/boot-features-external-config.html#boot-features-external-config-application-property-files)は、Spring bootアプリケーションにアプリケーションの外部でconfigをカスタマイズする機能を提供しますが、このパラメータはSpring boot 2.0バージョン以降でのみ有効になります。

Spring boot 1.xバージョンを使用している場合は、マウントディレクトリ`/config/tse-default-spring-cloud-config.properties`を[SPRING_CONFIG_LOCATION](https://docs.spring.io/spring-boot/docs/1.5.22.RELEASE/reference/html/boot-features-external-config.html#boot-features-external-config-application-property-files)環境変数にご自身で追加してください。

JVM起動パラメータを直接追加して設定することもできます。具体的な設定は次のとおりです。
<dx-tabs>
::: zookeeper
```bash
# 申請するzookeeperのアドレスを10.0.1.30:2181と仮定します
-Dspring.cloud.zookeeper.connectString=10.0.1.30:2181 
-Dspring.cloud.zookeeper.discovery.preferIpAddress=true
```
:::
::: nacos
```bash
# 申請するnacosのアドレスを10.0.120.11:8848と仮定します
-Dspring.cloud.nacos.discovery.server-addr=10.0.120.11:8848
```
:::
</dx-tabs>

