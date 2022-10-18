CLBインスタンスタイプ：CLB（これまで「アプリケーション型CLB」とも呼ばれていたものです）。
- CLB：TCP/UDP/HTTP/HTTPSプロトコルをサポートし、ドメイン名およびURLパスベースのバランシング機能を提供することで、フレキシブルな転送を可能にします。

製品機能、製品のパフォーマンスなどの多方面を考慮し、お客様にはインスタンスタイプのCLBのご利用をお勧めします。メリットは次のとおりです。

<table>
        <tbody>
               <tr>
            <th style="width: 10%;" rowspan="2">製品タイプ</th>
            <th style="width: 45%;" colspan="2" >CLB</th>
            </tr>
        <tr>
            <th>パブリックネットワーク</th>
            <th>プライベートネットワーク</th>
           </tr>
        <tr>
            <td>レイヤー7転送（HTTP/HTTPS）</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                       </tr>
        <tr>
            <td>レイヤー4転送（TCP / UDP）</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        </tr>  
        <tr>
            <td>レイヤー4暗号化転送（TCP SSL）</td>
                        <td>&#10003;</td>
                       <td>&#10003;</td>
                       </tr>    
                <tr>
            <td>HTTP/2およびwebsocket（secure）をサポート</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        </tr>
        <tr>
            <td>ロードバランシングポリシー</td>
                        <td>IP hash（レイヤー7）<br>重み付けラウンドロビン<br>重み付け最小接続 </td>
                        <td>IP hash（レイヤー7）<br>重み付けラウンドロビン<br>重み付け最小接続</td>
                        </tr>   
         <tr>
            <td>セッション維持</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                       </tr>   
        <tr>
            <td>ヘルスチェック</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        </tr>   
         <tr>
            <td>カスタム転送ルール（ドメイン名/URL）</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                       </tr>   
        <tr>
           <td>SNIマルチ証明書機能のサポート</td>
                       <td>&#10003;</td>
                       <td>&#10003;</td>
                      </tr>
            <tr>
            <td>異なるバックエンドポートへの転送</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                     </tr>   
        <tr>
           <td>レイヤー7カスタム設定</td>
                       <td>&#10003;</td>
                       <td>&#10003;</td>
                     </tr>  
         <tr>
            <td>レイヤー7リダイレクト機能（rewrite）</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                      </tr>
             <tr>
            <td>クロスリージョンバインディング機能のサポート</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                      </tr>   
                <tr>
            <td>レイヤー7アクセスログのCLSへの保存設定</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                      </tr>    
</tbody></table>

>?  
>
>- CLBインスタンス：CLBのHTTP/2に対するサポートを有効にするか無効にするかを選択できます。詳細については、[HTTPSリスナーの設定](https://intl.cloud.tencent.com/document/product/214/32516#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E9.85.8D.E7.BD.AE.E7.9B.91.E5.90.AC.E5.99.A8)をご参照ください。


