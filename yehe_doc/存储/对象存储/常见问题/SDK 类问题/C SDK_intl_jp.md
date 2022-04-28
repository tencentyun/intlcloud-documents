### C SDKを使用して中断からの再開を実現するにはどうすればよいですか。

[C SDKの高度なアップロード](https://intl.cloud.tencent.com/document/product/436/31518)インターフェースを使用して、中断からの再開を実現できます。中断からの再開を使用する場合は、アップロード制御パラメータを**COS_TRUE**に設定する必要があります。例えば、`clt_params = cos_create_resumable_clt_params_content(p, 0, 1, COS_TRUE, NULL)`のようになります。

