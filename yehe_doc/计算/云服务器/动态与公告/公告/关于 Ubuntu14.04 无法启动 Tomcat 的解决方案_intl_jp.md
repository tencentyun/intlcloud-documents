
ユーザーの皆様へ
Tencent Cloudは「Tencent Cloud公式サイトから購入したUbuntu14.04 CVMにapt-getを使用してTomcatとHadoopをインストールすると、ポートは正常にリッスンできますが、リクエストに応答できないこと」を検出しました。Tencent Cloudは対応する回避策を提示します。このような状況が発生したら、お勧めの対処方法で回避することをお勧めします。

### 問題の原因
Java Runtime Environment の[既知の問題](http://bugs.java.com/bugdatabase/view_bug.do?bug_id=6202721) に起因する問題です。

### 問題の分析
TomcatとHadoopはJava言語で開発され、java.security.SecureRandomのAPIが使用されています。
このAPIはあるJREの中でデフォルトで`/dev/random`を利用して生成されていますが、`/dev/random `はCPU温度、キーボード等のハードウェアのノイズを受信して、エントロピーを生成します。CVMの仮想マシン環境では、CPU温度などの信号を検知してエントロピーを生成することは困難です。そのため、`cat /dev/random `はほぼブロックされ、TomcatとHadoopが起動できなくなります。

###　ソリューション
#### JRE設定を変更する
元の`/etc/java-7-openjdk/security/java.security`（ 実際のURLに基づく）中の` securerandom.source=file:/dev/urandom `を`securerandom.source=file:/dev/./urandom `に変更して、上記の問題を回避します。




