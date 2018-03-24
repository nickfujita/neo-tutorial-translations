# NEO Smart Contracts: Build와 테스트

이것은 Hello World 튜토리얼에 이은 후속 포스트 입니다. 이번 포스트에서는 import해오기에 앞서, Smart contract를 빠르게 build하고 테스트 하는 방법에 대해서 다룰 것 입니다.

만약 Hello World 튜토리얼과 개발환경 설정 튜토리얼을 보지 않으셨다면, 빠르게라도 훑고 다시 돌아와서 이 포스트를 읽어주시기를 권합니다.

Hello World Smart Contract Tutorial

Dev Environment Setup Tutorial

Hello World 튜토리얼에서는 분산적으로 빌드하는 방법과 contract 파일을 가져오는(import) 방법을 알아봤습니다. Hello world 튜토리얼의 경우 contract 코드를 어느정도 적당한 레벨로 빌드할 수 있게 할 것이며 당신의 private net에서 테스트하는 방법들을 다뤘습니다.

그러나 importing할 필요도 없으면 서이것보다 더 빠르게 contract code를 테스트하는 방법이 있습니다.

neo-python cli에는 build 라는 커맨드가 있습니다. 우리는 이것을 아래와 같은 코드로 hello world에서 이미 사용한 적이 있습니다. py file을 avm file로 컴파일하기 위해서 사용했습니다.
```
build path/to/file.py
```

좋은 소식은 build 는 더 많은 parameter를 받을 수 있다는 것입니다. 이것은 import 와testinvoke를 한번에 실행할 수 있게 해줍니다.
```
build {path/to/file.py} test {input_types} {return_type} {needs_storage} {needs_dynamic_invoke} {test_param} ...
```

보이다 시피, 이것은 compact import명령어와 아주 비슷합니다. 그러나 조금 다른 점은 이 빌드 커맨드의 경우 테스트를 위한 모든 parameter, 옵션들을 명령어의 끝까지 한번에 쭉 달 수 있도록 해줍니다.
```
build smartContracts/helloWorld.py test "" 01 False False
```

contract import 와 비교해서 명령어를 살펴보면 .avm파일이 아닌 py파일을 참조하고 있는 것을 발견할 수 있을 것입니다. 이유는 위의 명령어의 경우, 같은 명령어 안에서 새로운 컴파일 뿐만 아니라 컴파일되면서 나온 .avm 을 테스트하는 것 까지 모두 한꺼번에 처리할 수 있기 때문입니다.

좀 더 흥미로운 문자열 연결을 위한 코드를 살펴봅시다.
```
from boa.code.builtins import concat
def Main(initialString, args):
   result = initialString
   for word in args:
       if result == None:
           result = word
       else:
           result = concat(result,' ')
           result = concat(result,word)
       print(result)
   return result
```

이 contract의 경우 2개의 인자를 받습니다. 하나는 최초 문자고 다른 하나는 배열입니다. 이 반복문의 경우 배열안의 요소들을 하나씩 돌면서 문자들을 하나씩 연결해서 결과를 리턴합니다. 이것을 실행하기 위해서는 아래의 커맨드를 실행해야 합니다.

```
build smartContracts/concat.py test 0710 07 False False sunshine ['hello','world','things','otherthings']
```

여기서 패스된 파라미터에서 숫자를 확인할 수 있을 것입니다. 여기서 숫자는 값의 타입(문자열, 배열 etc)를 뜻합니다. 07의 경우 문자열을 뜻하고 10은 배열을 뜻합니다.

0710의 경우, 패스되는 두 개의 인자중 하나인 최초 문자의 타입( 07), 그리고 또 다른 인자인 배열의 타입( 10)을 합친 것입니다. 뒤이어 나오는 07은 리턴값의 타입인 문자를 뜻합니다.

자세한 내용은 아래의 튜토리얼을 확인해주세요.

NEO Smart Contract: Parameter Types

이제 우리는 test invode와 빌드 명령어를 같이 사용하는 방법을 익혔습니다. 이제 contract code를 매번 import하지 않고도 개발하고 테스트를 할 수 있게 되었습니다.

이 튜토리얼이 도움이 되셨다면 아래의 채널에서 후원해주세요:
