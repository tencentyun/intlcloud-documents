Linux マシンは下記のコマンドを通して、Linux CVMにファイルをアップロードできます。

```
scp ローカルファイルパス CVMログイン名@CVMパブリックIP /ドメイン名 CVMファイルパス
```

例えば、ローカルファイル「/home/lnmp0.4.tar.gz」をIPアドレスが「129.20.0.2」のCentOS CVMの対応するディレクトリにアップロードします。

```
scp /home/Inmp0.4.tar.gz root@129.20.0.2 /home/Inmp0.4.tar.gz
```

Enterキーを押してログインパスワードを入力し、アップロードを完了します。