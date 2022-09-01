Java 9のリリース以来、Javaは多くの面で大幅な改善と強化を行っています。またそれに伴ってAPIに対するいくつかの修正が行われ、その多くの機能によって、アプリケーションの起動速度、パフォーマンスおよびメモリ占有を改善することが可能になりました。

## Java 8とJava 11の間の大きな変更

### モジュールシステム

モジュールシステム[JSR 376](http://openjdk.java.net/projects/jigsaw/spec/)はJava 9からJavaに導入されました。これにより、大型アプリケーションにおけるクラスパスの混乱、複雑な設定、有効にパッケージ化できないという問題が解決しました。

モジュールとはJavaのクラスとインターフェース、ならびに関連リソースの集合です。モジュールはカスタムアプリケーションの実行時に設定できます。使用容量がより小さく、また[jlink](https://docs.oracle.com/en/java/javase/11/tools/jlink.html)を使用して、アプリケーションをカスタムランタイムにリンクさせてデプロイすることができます。使用容量が小さいため、マイクロサービスアーキテクチャにおいて非常に実用的です。JVMがロードモジュール内のクラスにある場合も、クラスパスから直接ロードするより速くロードできます。

モジュールは、どのパッケージをエクスポートするか、ならびにどのコンポーネントを必要とするかを明確に述べるとともに、プライベートネットワークモジュールのリフレクションアクセスを制限することで、堅牢なパッケージを実現する必要があります。このようなパッケージレベルによって、アプリケーションはより安全で、よりメンテナンスしやすくなります。

Java 8から移行する開発者にとっては、モジュールは必ずしも必要なものではありません。アプリケーションは引き続きクラスパスを使用してJava 11上で実行できます。

モジュールシステムの使い方についてより詳しく知るには、[The State of the Module System](http://openjdk.java.net/projects/jigsaw/spec/sotms)をご参照ください。

### JVMの分析診断ツール

#### Java Flight RecorderとJava Mission Control

Java Flight Recorder (JFR) [JEP 328](http://openjdk.java.net/jeps/328)は実行中のJavaアプリケーションから診断および分析データを収集します。JFRは実行中のJavaアプリケーションにほとんど影響を与えません。開発者はJava Mission Control (JMC)およびその他のツールを使用して、収集したデータを分析することができます。 JFRとJMCはJava 8では商用機能ですが、Java 11ではどちらもオープンソースです。

#### JVMログシステム

Java 11はJVMのすべてのコンポーネントに共通のログレコードシステムを提供しています[JEP 158](http://openjdk.java.net/jeps/158)。この統一ログシステムでは、ユーザーが記録したいコンポーネント、ならびにどのレベルに記録するかを定義できるようになっています。このような細粒度のログは、開発者がJVMのクラッシュ時に原因を分析したり、本番環境でのパフォーマンスの問題を診断したりする際に役立ちます。

#### 低オーバーヘッドヒーププロファイリング

Java Virtual Machine Tool Interface(JVMTI)に新たなAPIが追加されました。これはJavaのヒープ割り当てに対するサンプリングに用いられます[JEP 331](http://openjdk.java.net/jeps/331)。サンプリングには低オーバーヘッドの特性があります。

### ガベージコレクション

Java 11では、シリアル（Serial）、パラレル（Parallel）、G1（Garbage-First）、Epsilonのガベージコレクターを提供しています。Java 11のデフォルトのガベージコレクターはG1です。

- G1は遅延とスループットの間でバランスを取ることを目標としています。G1の目的はFull GCの回避ですが、コレクションの同時実行によって十分な速度でメモリを回収できない場合は、Full GCが発生してしまいます。
- パラレルGCはJava 8のデフォルトのコレクターです。これはスループット優先のコレクターであり、複数のスレッドを使用してガベージコレクションのスピードをアップします。
- Epsilon GCはメモリの割り当てを行いますが、回収は一切行いません。ヒープメモリの空き容量がなくなると、JVMはシャットダウンします。Epsilonは短時間のサービスやガベージがないアプリケーションにとっては非常に有用です。

この他に、Java 11は3種類のガベージコレクターを提供しています。

- ZGCは同時実行を行う低遅延のコレクターです。ZGCは一時停止時間を10ミリ秒以下に抑えることを目標としています。ZGCはJava 11の実験的な機能として提供されています。
- Shenandoahは一種の低一時停止時間コレクターです。実行中のJavaプログラムとの同時実行が可能であり、これによってGCの一時停止時間を短縮します。ShenandoahはJava 12の実験的な機能ですが、すでにJava 11に移植されています。
- CMSはJava 11で引き続き使用できますが、Java 9以降は廃止と表示されています。

### コンテナ環境の改善

Java 10より前のバージョンでは、JVMはコンテナに設定されているメモリとCPUの制限を認識できませんでした。例えばJava 8では、JVMのデフォルトの最大ヒープサイズは、基盤のホストの物理メモリの1/4です。Java 10以降では、JVMはcgroupsを使用してメモリとCPUの制限を設定します。 例えば、デフォルトの最大ヒープサイズはコンテナのメモリの1/4となります。

また、Java 10では新しいJVMパラメータも提供し、これによってDockerコンテナユーザーは、Javaヒープに使用されるシステムメモリ量を細かく制御できるようになりました。

>?jdk8u191より、cgroupのサポート作業の大部分はJava 8に移植されました。

## Java 8からJava 11への移行

アプリケーションをJava 8からJava 11に移行するプロセスには、万能のソリューションは存在しません。開発者にとって潜在的な問題となり得るものには、削除されたAPI、廃止されたパッケージ、内部APIの使用、クラスローダーの変更、ガベージコレクションの変更などがあります。

### コンパイルを直接実行してみる

一般的に、最も簡単な方法は、再コンパイルを行わず、Java 8でコンパイルしたアプリケーションをJava 11上で直接実行してみるか、または先にJava 11でコンパイルしてから実行することです。アプリケーションをできる限り速やかに起動および実行することが目的の場合、通常はこのような簡単な試みが最適な方法となります。

### その他のツール

Java 11はjdeprscanとjdepsという2つのツールを提供しており、潜在的な問題の発見に用いることができます。これらのツールは既存のクラスファイルまたはjarパッケージに対して実行でき、再コンパイルせずに使用することができます。

#### jdeprscan

[jdeprscan](https://docs.oracle.com/en/java/javase/11/tools/jdeprscan.html)は、プログラム内ですでに廃止または削除されたAPIを使用していないかの検索に用いられます。廃止されたAPIを使用しても移行の障害とはなりませんが、今後のバージョンで削除される可能性があるため、注意が必要です。

[jdeprscan](https://docs.oracle.com/en/java/javase/11/tools/jdeprscan.html)を使用したい場合、最も簡単な方法は既製のjarパッケージを提供し、これにディレクトリまたはクラス名を指定することです。`--release 11`パラメータを使用すると、廃止されたAPIの最も完全な使用リストを取得できます（例：`jdeprscan --release 11 my-application.jar`）。

`error: cannot find class XXX`というエラーが表示された場合は、依存するクラスファイルがjarパッケージのクラスパス内にないかどうかを優先して確認する必要があります。 この依存クラスがサードパーティの依存でなければ、Java 11ですでに削除されたAPIを使用している可能性があります。

`jdeprscan --release 11 --list`を実行するとJava 8より後で廃止されたAPIの詳細を把握できます。 削除されたAPIのリストを取得したい場合は、`jdeprscan --release 11 --list --for-removal`を実行してください。

#### jdeps

[jdeps](https://docs.oracle.com/en/java/javase/11/tools/jdeps.html)は、Javaクラスの依存関係アナライザーです。このツールを`--jdk-internals`パラメータと併せて使用すると、どのクラスが内部APIに依存しているかをjdepsが教えてくれます。また、`--multi-release 11`パラメータを追加して、マルチリリースjarパッケージをサポートすることもお勧めします（例：`jdeps --jdk-internals --multi-release 11 --class-path log4j-core-2.13.0.jar my-application.jar`）。

Java 11で内部APIを引き続き使用することもできますが、この方法は非推奨となっています。OpenJDK wiki [Java Dependency Analysis Tool](https://wiki.openjdk.java.net/display/JDK8/Java+Dependency+Analysis+Tool)では、よく用いられるJDKの内部APIの代替品をいくつか推奨しています。

jdk.unsupportedにある何らかのAPIを使用することはできる限り避けなければなりません。代替のAPIが利用可能となるまでの間、内部APIの使用はサポートされますが、それらは今後、完全に廃止または削除される可能性があります。[JEP 260](http://openjdk.java.net/jeps/260)で代替の方法が提供されています。

GradleとMavenにはどちらもjdepsおよびjdeprscanプラグインがあります。これらのツールをビルドスクリプトに追加することをお勧めします。

| ツール      | Gradleプラグイン                                                  | Mavenプラグイン                                                   |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| jdeps     | [jdeps-gradle-プラグイン](https://github.com/kordamp/jdeps-gradle-plugin) | [Apache Maven JDepsプラグイン](https://maven.apache.org/plugins/maven-jdeps-plugin/index.html) |
| jdeprscan | [jdeprscan-gradle-プラグイン](https://github.com/kordamp/jdeprscan-gradle-plugin) | [Apache Maven JDeprScanプラグイン](https://maven.apache.org/plugins/maven-jdeprscan-plugin/index.html) |

jdeprscanとjdepsはリフレクションアクセスを使用するAPIを確認することはできません。このため、コード内のリフレクションアクセスは実行時に確認する必要があります。

### 実行時の確認

#### JVMパラメータの確認

Java 11で実行する前に、JVMパラメータを確認してください。すでに削除されているJVMパラメータを使用すると、JVMがクラッシュして終了します（`Error: Could not create the Java Virtual Machine`）。GCログを有効にしている場合は、これを確認することが極めて重要です。GCログはJava 8から大幅に変更されているためです。JVMパラメータはJaCoLineツールを使用して確認できます。

#### サードパーティ依存クラスライブラリの確認

すべてのサードパーティ依存クラスライブラリを、Java 11をサポートするバージョンに更新する必要があります。これについて、OpenJDK Quality Groupは[Quality Outreach](https://wiki.openjdk.java.net/display/quality/Quality+Outreach)というwikiページを保守しており、多くの無料オープンソースソフトウェア(FOSS)プロジェクトの、OpenJDKバージョンに対するテストの状態を列記しています。

#### ガベージコレクションパラメータの確認

パラレルガベージコレクター（Parallel GC）はJava 8のデフォルトのGCです。Java 9からは、デフォルトのガベージコレクターはG1GCに変更されました。ガベージコレクターのパラメータが正しく設定されているかどうかを確認する必要があります。

#### クラスローダーの注意事項

- Java 11では、クラスローダーの階層構造が変更されました。`SystemClassloader`（`AppClassloader`とも呼ばれる）は、現在は内部クラスです。`URLClassLoader`に強制的に切り替えると`ClassCastException`のエラーがスローされます。Java 11には、実行時にclasspathを動的に追加するAPIはありませんが、以前と同様にリフレクションによって取得することができます。
- Java 11では、`BootstrapClassloader`はコアモジュールのみをロードします。親クラスローダーを持たないclassloaderを作成した場合、すべてのプラットフォームクラスが見つからない可能性があります。Java 11では、`ClassLoader.getPlatformClassLoader()`を親クラスローダーとして渡す必要があります。

#### ロケールデータの変更

Java 11のロケールデータのデフォルトソースは、[JEP 252](http://openjdk.java.net/jeps/252)に伴ってUnicodeの共通ロケールデータリポジトリに変更されました。これによりローカライズに影響する可能性があります。必要に応じ、システムプロパティ`java.locale.providers=COMPAT,SPI`を設定して、Java 8のロケール動作に戻します。

### よくあるご質問

#### Unrecognized options

JVMパラメータが削除済みの場合、アプリケーションは`Unrecognized option:`または`Unrecognized VM option`を出力します。認識できないパラメータはJVMをクラッシュ、終了させます（`Error: Could not create the Java Virtual Machine`）。廃止されているが削除されていないオプションにはJVMからアラート（`VM Warning: Option <option> was deprecated`）が発出されます。

通常は、これらの認識できないJVMパラメータを削除する必要があります。GCログのパラメータは除きます。GCログは[jep 271](http://openjdk.java.net/jeps/271)で再実装されました。[oracle公式ドキュメント](https://docs.oracle.com/en/java/javase/11/tools/java.html#GUID-BE93ABDC-999C-4CB5-A88B-1994AAAC74D5)を参照して再設定を行ってください。

#### WARNING: An illegal reflective access operation has occurred

Javaコードがリフレクションを使用してJDKの内部APIにアクセスすると、実行時に不正なリフレクションアクセスに対するアラートが発出されます。

#### java.lang.reflect.InaccessibleObjectException

このエラーは、`setAccessible(true)`によるリフレクションによってあるパッケージ/モジュール内のプライベートクラスのフィールドまたはメソッドを取得しようとしたことを表しています。`--add-opens`パラメータを使用することで、コードがパッケージ/モジュールの非パブリックメンバーにアクセスすることが可能になります。

#### java.lang.NoClassDefFoundError

アプリケーションがJava 8で正常に実行されているのに、Java 11から`java.lang.NoClassDefFoundError`または`java.lang.ClassNotFoundException`がスローされる場合、アプリケーションがJava EEまたはCORBAモジュールのパッケージを使用している可能性が高いです。これらのモジュールはJava 9で廃止され、Java 11では削除されています[jep 320](https://openjdk.java.net/jeps/320)。

この問題を解決したい場合は、プロジェクトにランタイム依存を追加してください。

| 削除されたモジュール | 影響を受けるパッケージ             | 推奨される依存                                                   |
| -------- | ---------------------- | ------------------------------------------------------------ |
| JAX-WS   | java.xml.ws            | [JAX WS RIランタイム](https://mvnrepository.com/artifact/com.sun.xml.ws/jaxws-rt) |
| JAXB     | java.xml.bind          | [JAXBランタイム](https://mvnrepository.com/artifact/org.glassfish.jaxb/jaxb-runtime) |
| JAV      | java.activation        | [JavaBeans (TM)アクティベーションフレームワーク](https://mvnrepository.com/artifact/javax.activation/activation) |
| アノテーション     | java.xml.ws.annotation | [JavaxアノテーションAPI](https://mvnrepository.com/artifact/javax.annotation/javax.annotation-api) |
| CORBA    | java.corba             | [GlassFish CORBA ORB](https://mvnrepository.com/artifact/org.glassfish.corba/glassfish-corba-orb) |
| JTA      | java.transaction       | [JavaトランザクションAPI](https://mvnrepository.com/artifact/javax.transaction/jta) |

#### UnsupportedClassVersionError

このエラーは、以前のJavaバージョン上で、それより上のJavaバージョンを使用してコンパイルしたコードを実行しようとしていることを意味します。例えば、JDK 13を使用してコンパイルしたjarをJava 11上で実行する場合などです。

| Javaバージョン | クラスファイルバージョン |
| -------- | ---------- |
| 8        | 52         |
| 9        | 53         |
| 10       | 54         |
| 11       | 55         |
| 12       | 56         |
| 13       | 57         |
