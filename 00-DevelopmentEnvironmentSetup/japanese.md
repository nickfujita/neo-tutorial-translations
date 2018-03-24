# NEO開発環境の設定方法

NEO private netを開始するためのチュートリアルです。Dockerとneo-python v0.5.3（python v3.6）を使用して任意のOSでWindows、Mac、Linuxに関係なく、ローカル環境でのPythonをインストールしなくても可能です。

## Docker インストールをします
Mac OSX
Windows PC
Other

## smart contract codeのフォルダを作成します
terminalを開きます：


注意：smart contract codeを保持するためのフォルダを作成するか、保持したいフォルダに移動してください。このフォルダはdocker containerと接続され、このcontainerを介してsmart contract filesへのアクセスが可能になるので重要です。

例えば：


## docker container開始します
neo-privatenetを使用します。これwalletにすでに含まれているneo private net instanceとNEO/ GASが含まれています。

次のコマンドを実行します：
```
docker run -d --name neo-privatenet -p 20333-20336:20333-20336/tcp -p 30333-30336:30333-30336/tcp -v "$(pwd)":/neo-python/smartContracts cityofzion/neo-privatenet
```

containerが動作しているかどうか、以下のcommandを端末で確認します：
```
docker ps
```

次のコマンドを実行してSSHをdockerコンテナに追加します。
```
docker exec -it neo-privatenet /bin/bash
```

この中でsmartContractsフォルダを見ることができるでしょう。これはhost machineからローカルディレクトリに接続されていることを表わしています。


事前に作成されたwalletを確認することができるようになり：

neo-privnet.wallet
neo-python promptで試してみましょう

full commandを使用するか：
```
python3 prompt.py -p
```

bash script短縮コードを使用しても実行されます:
```
neopy
```

今neo自体のcommand lineを使用することができます。ここでprivate neo netとの相互作用が可能です。

事前に作成されたwalletを開いてみましょう
```
open wallet neo-privnet.wallet
```

walletパスワードを入力します
```
coz
```

walletをRebuildします
```
wallet rebuild
```

wallet balanceを確認します
```
wallet
```

walletは100,000,000 NEOと16,000 GASを持っています。

おめでとうございます！すべてがインストールがされ、独自のDappsとsmart contractsをコーディングすることができる最初の設定が完了しました。

もしこのチュートリアルが役に立ちましたらこのチャンネルを是非フォローしてください：
