# 20203187 양지원/assignment1

## 쉘 스크립트
### getopt 명령어

*shellscript*로 프로그램을 만들다 보면 실행 인자 및 옵션을 필요로 하는 경우가 있는데, 실행 옵션을 구현할 때 ***getopt***함수를 쓰면 매우 간단해진다.

**>Example**

```python
while getopts "a:b:h" opt
do
case $opt in
a) arg_a=$OPTARG
echo "Arg A: $arg_a"
;;
b) arg_b=$OPTARG
echo "Arg B: $arg_b"
echo "$arg_b"
;;
h) help ;;
?) help ;;
esac
done
```

* getopt를 사용하는 이유
  1)  다양한 입력 값이 존재할 경우 사용자와 개발자의 편의를 보장하기 위함이고
  2)  스크립트를 보다 체계적으로 관리할 수 있기 때문이다.

> 주의
```python
while getopts "a:b:h" opt
```
보통 이런 형식으로 주로 사용하고 *getopt*는 첫번째 파라미터로 옵션으로 사용될 문자열을 입력 받고 다음에는 옵션으로 활용되는 변수를 사용한다.

getopt를 사용할 때 주의해야 할 점은 ":"이다. 기본적으로 getopt는 한 개의 문자만을 구분자로 사용하며 사용할 문자열 뒤에 ":"을 붙이게 되면 뒤에 *Value*가 붙게 된다는 것을 의미한다.

### getopts 명령어
* getopts가 생긴 이유
  * getopt에 몇 가지 문제가 있었다.
    * 빈 문자열 인 인수를 처리 할 수 없다.
    * 공백이 포함 된 인수를 처리 할 수 없다.

    ***(최신 getopt 버전에는 이러한 제한이 없다.)***

*이러한 문제를 보안하기 위해서 getopts를 제공하게 되었다.*

* getopts의 장점
  1) 이식성이 뛰어나 dash과 같은 다른 쉘에서도 작동한다.
  2) 일반적인 유니스 방식에서 -vf filename와 같은 여러 단일 옵션을 자동으로 처리 할 수 있다.

### sed 명령어
1) sed란?

> sed는 Stream Editor의 약자로 매우 컴팩트한 명령 체계를 이용하여
텍스트를 파싱하고 변형하는 텍스트 편집 도구이다.
sed는 그 전신이 되는 ed의 스크립팅 체계를 기반으로 하고있다.
vim과 같이 편집될 텍스트를 화면상에 보면서 내용을 작성/수정하는 개념의 텍스트 편집기가 개발되기 이전의 텍스트 편집기이다.

SED로 진행하기 위해서는 다음이 필요합니다.
* 텍스트 내용을 완벽히 알고 있어야한다.
* 어느 라인 혹은 어떤 내용을 수정할지 알고있어야 한다.
* 스크립트를 활용해서 해당 라인을 수정한다.

2) sed 명령어 사용법

* 기본

```
$sed[옵션] 스크립트 입력파일1 [입력파일2 ...]
```

* 옵션

![image](https://user-images.githubusercontent.com/66530743/142616294-a5f64eaa-d46c-4ed8-abfe-fdc8e3ac60ad.png)

```
주로 사용하는 옵션 -n, -e, -f
```

### awk 명령어
