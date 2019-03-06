## アプリケーション型と従来型の比較
CLBのインスタンスのタイプはアプリケーション型と従来型に分かれ、そのうち従来型は初期のバージョンで、アプリケーション型は強化されたバージョンです。アプリケーション型は従来型のすべての機能をほぼカバーしています。製品機能、製品性能など多方面の観点から、アプリケーション型CLBを使用することをお勧めします。両者の詳細な比較は以下のとおりです。選択の際に参照してください。

<table>
        <tbody>
                <tr>
            <th style="width: 10%;" rowspan="2">製品タイプ</th>
            <th style="width: 45%;" colspan="2" >アプリケーション型CLB</th>
            <th style="width: 45%;" colspan="2">従来型CLB</th>
        </tr>
        <tr>
            <th>パブリックネットワーク</th>
            <th>プライベートネットワーク</th>
            <th>パブリックネットワーク</th>
            <th>プライベートネットワーク</th>
        </tr>
        <tr>
            <td>7層転送（HTTP/HTTPS）</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✖</td>
        </tr>
        <tr>
            <td>4層転送（TCP/UDP）</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
        </tr>    
                <tr>
            <td>HTTP/2およびwebsocket（secure）をサポート</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✖</td>
        </tr>
        <tr>
            <td>CLBポリシー</td>
                        <td>ip hash（7層）<br>重み付きラウンドロビン<br>重み付き最小接続数</td>
                        <td>ip hash（7層）<br>重み付きラウンドロビン<br>重み付き最小接続数</td>
                        <td>ip hash（7層）<br>重み付きラウンドロビン<br>重み付き最小接続数</td>
                        <td>重み付きラウンドロビン</td>
        </tr>   
         <tr>
            <td>セッション保留</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
        </tr>   
        <tr>
            <td>正常性検査</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✔</td>
        </tr>   
         <tr>
            <td>転送規則のカスタマイズ（ドメイン名/URL）</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✖</td>
                        <td>✖</td>
        </tr>   
            <tr>
            <td>異なるバックエンドポートへの転送</td>
                        <td>✔</td>
                        <td>✔</td>
                        <td>✖</td>
                        <td>✖</td>
        </tr>   
         <tr>
            <td>リダイレクト機能（rewrite）をサポート</td>
                        <td>✔</td>
                        <td>✖</td>
                        <td>✖</td>
                        <td>✖</td>
        </tr>   
             <tr>
            <td>地域間バインディング機能をサポート</td>
                        <td>✔</td>
                        <td>✖</td>
                        <td>✖</td>
                        <td>✖</td>
        </tr>   
        <tr>
            <td>ログをCOSに保存する機能をサポート</td>
                        <td>まもなくサポート予定</td>
                        <td>まもなくサポート予定</td>
                        <td>まもなくサポート予定</td>
                        <td>✖</td>
        </tr>   
</tbody></table>

