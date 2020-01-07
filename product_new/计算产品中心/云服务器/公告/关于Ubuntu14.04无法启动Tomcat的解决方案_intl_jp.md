
お客様：
こんにちは、
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Tencent Cloudは「Tencent Cloud公式サイトでUbuntu14.04 CVMを購入して、 apt-getでTomcatとHadoopをインストールする時、ポートを正常にリッスンできるが、リクエストに応答できないこと」を検出しました。Tencent Cloudは相応の回避策を提供します。このような状況が発生したら、お勧めの措置で回避することをお勧めします。

**【問題の原因】**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Java Runtime Environment の一つ[既知の問題](http://bugs.java.com/bugdatabase/view_bug.do?bug_id=6202721)によりです。
 **【問題分析】**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Tomcat と HadoopはJavaを利用して開発します。java.security.SecureRandom のAPIにも利用しました。
このAPIはあるJREの中でデフォルトで`/dev/random`を利用して生成します。ただし、`/dev/random `はCPU温度、キーボード等のハードウェアノイズを受信してエントロピーを生成します。CVMは仮想化技術を利用したCVM環境であるため、CPU温度などのシグナルを感知するのは困難でもあるため、エントロピーを生成するのが難しいです。したがって、`cat /dev/random `がほとんどブロックされる原因であるため、Tomcat、Hadoopの起動もブロックされます。
**【回避策】**
**JRE構成を修正する**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;元` /etc/java-7-openjdk/security/java.security`（ 実際のURLに基づく）中の` securerandom.source=file:/dev/urandom `を`securerandom.source=file:/dev/./urandom `に修正して、上記の問題を回避します。


2016-10-14    
Tencent Cloud




