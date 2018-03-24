# NEO Smart Contracts 튜토리얼: helloWorld

이 튜토리얼은 NEO에서 스마트 계약(smart contract)를 만들고 deploy하고 실행하기 위한 튜토리얼입니다.

만약 아직 개발환경을 docker container와 gas안에 있는 private new net과 함께 설정하지 않았다면 아래의 튜토리얼을 먼저 참고하시길 바랍니다.

Quick Setup: NEO Private Net

한글 버전: NEO Private Net 개발 환경 설정

## docker container 시작하기
만약 터미널에서 이미 docker container를 실행하고 있는 경우 이 단계는 건너뛰면 됩니다.

neo privnet docker container가 실행되고 있는지 확인합니다
```
docker ps
```

만약 docker container가 실행되고 있지는 않으나,


이미 만들어 놓은 경우(아래처럼 이미 neo-privatenet 이름 아래 container id가 있는 경우)
```
docker ps -a
```

container id를 확인하고, container를 시작하십시오. CONTAINER ID를 복사해 넣고 아래의 커맨드를 실행하세요
```
docker start CONTAINER_ID
```

SSH into the docker container
```
docker exec -it neo-privatenet /bin/bash
```

## 첫 번째 smart contract를 만들어 보기
- 좋아하는 text editor를 열어주세요
- 새로운 파일을 생성하고, 이 파일을 개발환경 설정 튜토리얼에서 미리 만들어놨던 디렉토리에 저장합니다.(설정 튜토리얼에서 중요하다고 나온 부분입니다). 이 폴더에서 docker image가 공유될 것이며, docker container안에서 당신의 computer로의 파일 접근이 가능하게 해 줄 것입니다.
- 이 파일에서는 string을 로그하고 boolean을 이언하는 간단한 함수를 작성할 것입니다.
```
def Main():
  print("hello world");
  return True
```

이 코드는 여기에서도 확인할 수 있습니다.

파일을 저장합니다

## python smart contract파일을 컴파일 하기
docker container SSH session이 있는 터미널로 돌아가 봅시다. 현재 위치가 neo-python directory에 있는지 확인해주세요.

그리고 neo cli를 열어주세요. 이를 위해서 아래의 커맨드를 사용하거나
```
python3 prompt.py -p
```

이것을 사용하면 됩니다.
```
neopy
```

compile command를 실행합니다
```
build smartContracts/helloWorld.py
```

주의: 설정 튜토리얼에서 나왔던 것처럼 공유되는 폴더의 이름을 smartContracts 라고 설정했을 것으로 가정하고 이 튜토리얼에서도 계속해서 같은 이름을 사용합니다. 가급적 튜토리얼을 따라하는 경우 폴더의 이름을 똑같이 맞춰주세요.

아래와 같이 성공했다는 확인 메세지와 함께 smartContracts 에 컴파일 된 helloWorld.avm 파일을 확인할 수 있을 것입니다.


## contract 가져오기(importing)
NEO/GAS를 통해 wallet을 열어주세요
```
open wallet neo-privnet.wallet
```

wallet 비밀번호를 입력하세요
```
coz
```

아래의 커맨드와 함께 smart contract를 가져옵니다(import)
```
import contract CONTRACT_FILE INPUT_TYPES OUTPUT_TYPES NEEDS_STORAGE NEEDS_DYNAMIC_INVOKE
```

아래의 코드를 보면 많은 옵션들이 나와있는데 해당 내용은 이후의 튜토리얼에서 좀 더 자세하게 다룰 것입니다. 그 때까지 우선은 아래의 커맨드를 사용한다 정도로 알고 다음으로 넘어가 주세요.
```
import contract ./smartContracts/helloWorld.avm "" 01 False False
```

이 contract에 대한 내용을 채우라고 터미널에 나올 텐데 우선은 다 공백으로 쭉 엔터를 쳐주세요.


wallet 비밀번호 (coz)를 쳐서 이 contract의 deployment를 승인해 주고 기다립니다. 그리고 나면 성공적인 deployment를 알리는 메시지를 확인할 수 있을 것입니다.


## contract를 만들어 보기
contract가 deployed된 것을 확인할 수 있는 커맨드 입니다
```
contract search CONTRACT_NAME
```

우리의 경우 helloWorld가 contract의 이름이었으므로 아래와 같습니다
```
contract search helloWorld
```

contract의 hash값을 복사합니다. 위의 캡쳐의 경우 이와 같습니다. a89e1bc8437cfce24a523829a71a35d73fc18bb2

그러나 해시코드는 각각 다르게 생성되므로 본인의 터미널에서 확인해야 합니다.

contract에서 testinvoke 를 해시값과 함께 실행합니다
```
testinvoke CONTRACT_HASH
```

test invoke가 성공적이었다는 메시지와 함께 우리의 로그인 “hello world”와 결과 “1” (True와 같은 값)을 확인할 수 있을 것입니다.

wallet의 비밀번호를 넣는 대신에 리턴을 누릅니다. 이렇게 함으로써 실제로 contract를 실행할 건이며 neo 블록체인에 거래를 전송할 것입니다.

축하합니다!! 당신은 NEO와 함께 첫번째 smart contract를 코딩하고 실행하고 deploy를 하셨습니다.

이 튜토리얼이 도움이 되셨다면 아래의 채널에서 후원해주세요:
