＃NEO smart contract：helloWorld

あなたは、smart contractを展開して実行して、目的を達成することができます。

開発者の環境をドッカーのコンテナとガスで守ることができます。

クイックセットアップ：NEOプライベートネット

日本語版：NEO Private Net開発環境設定

## docker container開始する
そこでは、ドッカーのコンテナを実行していて、その段階では、

neo privnet docker containerガジェットを実行してください
```
docker ps
```

コンテナは、


既に箱入りができている
```
docker ps -a
```

コンテナIDを確認し、コンテナを起動します。コンテナIDをコピーしてください。
```
docker start CONTAINER_ID
```

SSHをドッカーコンテナに入れる
```
docker exec -it neo-privatenet /bin/bash
```

##初めsmart contractを聞くのを見る
- 好きなテキストエディタを使って
- 新しいファイルを作成し、このファイルを開発する環境を調整するには、事前に大宇宙の部分を保存する必要があります。このフォルダからドッカー画像を共有すること、ドッカーコンテナあなたのコンピュータのファイルにアクセスできる可能性があります。
- このファイルは文字列であり、ブール値であれば簡単な関数である。
```
def Main():
  print("hello world");
  return True
```

それはここにある。

ファイルを保存する

## python smart contractファイルをコンパイルする
ドッカーのコンテナSSHセッション現在の位置はneo-pythonのディレクトリです。

そしてneo cliを熱してください。崇拝下の戒厳令を使う
```
python3 prompt.py -p
```

使用しないでください。
```
neopy
```

コンパイルコマンドを実行する
```
build smartContracts/helloWorld.py
```

注意：徹底的に共有することをお勧めします。加水的な方法では、フォルダの名前を取得する。

あなたのためにスマートコンドルをコンパイルしましたhelloWorld.avmファイルを手に入れる必要があります。


##契約取得오기（インポート）
NEO / GASはウォレットを熱くします
```
open wallet neo-privnet.wallet
```

ウォレットのパスワードを入力してください
```
coz
```

下の賢者とsmart contractを取ることに取り込む（インポート）
```
import contract CONTRACT_FILE INPUT_TYPES OUTPUT_TYPES NEEDS_STORAGE NEEDS_DYNAMIC_INVOKE
```

あなたの選択肢は、より多くの選択肢を提供します。それでは、優先順位を下げることができます。
```
import contract ./smartContracts/helloWorld.avm "" 01 False False
```

あなたと契約していれば、それはあなたのためのものです。


wallet password（coz）を契約した時の展開を許可する。そして、その上に配置すると、すぐに展開することができます。


##契約を聞く
契約が展開された
```
contract search CONTRACT_NAME
```

私たちのことhelloWorld契約の様子
```
contract search helloWorld
```

契約のハッシュ値をコピーしてください。上のキャップのためのもの。 a89e1bc8437cfce24a523829a71a35d73fc18bb2

しかし、ハッシュ・シーズンは、覚えておいてください。

testinvokeを使って契約を解読する
```
testinvoke CONTRACT_HASH
```

test invokeは私たちのログイン "hello world"と結果 "1"（真と同じ値）を入力してください。

財布の暗証番号を押してください。 ブロック・アンド・ネゴ・ブロック・チェーンで取引を行うことができます。

おしゃべり！ あなたはNEOであり、スマートな契約を結んで実行し、展開します。

それでは、この手引きでは、
