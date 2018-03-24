# NEO 개발환경 설정 튜토리얼(최신 버전)

NEO private net를 시작하기 위한 튜토리얼입니다. Docker와 neo-python v0.5.3 (python v3.6)을 사용해서 어떤 OS에서도 윈도우, Mac, Linux에 상관 없이, 로컬 환경에서 파이썬을 설치하지 않고도 가능합니다.

## Docker 설치하기
Mac OSX
Windows PC
Other

## smart contract code를 위한 폴더 만들기
terminal을 엽니다:


주의: smart contract code를 보관하기 위한 폴더를 새로 만들거나 그렇게 하고자 하는 폴더로 이동해주세요. 이 폴더를 docker container와 연결할 것이며, 이 container를 통해 smart contract files에의 접근이 가능해질 것이므로 중요합니다.

예를 들어:


## docker container 시작하기
neo-privatenet를 사용할 것입니다. 이것은 wallet에 이미 들어있는 neo private net instance 와 NEO/GAS 를 포함하고 있습니다.

아래의 명령어를 실행합니다:
```
docker run -d --name neo-privatenet -p 20333-20336:20333-20336/tcp -p 30333-30336:30333-30336/tcp -v "$(pwd)":/neo-python/smartContracts cityofzion/neo-privatenet
```

container가 작동하고 있는지 아래의 command로 터미널에서 확인합니다:
```
docker ps
```

SSH into the docker container by running:
```
docker exec -it neo-privatenet /bin/bash
```

이 안에서 smartContracts 폴더를 볼 수 있을 것입니다. 이것은 host machine에서 로컬 디렉토리와 연결되어 있을 것 입니다.


미리 만들어진 wallet 을 확인할 수 있을 것입니다: neo-privnet.wallet

neo-python prompt로 가봅시다

full command를 사용하거나:
```
python3 prompt.py -p
```

bash script 단축 코드를 사용해도 됩니다:
```
neopy
```

이제 neo 자체의 command line을 사용할 수 있습니다. 여기서 private neo net와 상호작용이 가능합니다.

미리 만들어진 wallet을 열어봅시다
```
open wallet neo-privnet.wallet
```

wallet 비밀번호를 입력합니다
```
coz
```

wallet을 Rebuild합니다
```
wallet rebuild
```

wallet balance를 확인합니다
```
wallet
```

wallet은 100,000,000 NEO 와 16,000 GAS를 갖고 있을 것입니다.

축하합니다! 모든 것이 다 설치가 되었고 자체적으로 Dapps과 smart contracts을 코딩할 수 있는 첫 번째 작업을 완수하셨습니다.

이 튜토리얼이 도움이 되셨다면 아래의 채널에서 후원해주세요:
