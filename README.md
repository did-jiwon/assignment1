# 20203187 컴퓨터공학과 양지원/assignment1

## Shell script
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

## Linux
### sed 명령어
1) sed란?

  > sed는 Stream Editor의 약자로 매우 컴팩트한 명령 체계를 이용하여
텍스트를 파싱하고 변형하는 텍스트 편집 도구이다.
sed는 그 전신이 되는 ed의 스크립팅 체계를 기반으로 하고있다.
vim과 같이 편집될 텍스트를 화면상에 보면서 내용을 작성/수정하는 개념의 텍스트 편집기가 개발되기 이전의 텍스트 편집기이다.

* SED로 진행하기 위해서는 다음이 필요합니다.
  * 텍스트 내용을 완벽히 알고 있어야한다.
  * 어느 라인 혹은 어떤 내용을 수정할지 알고있어야 한다.
  * 스크립트를 활용해서 해당 라인을 수정한다.


2) sed 명령어 사용법

  * 기본

  ```
  $sed[옵션] 스크립트 입력파일1 [입력파일2 ...]
  ```

  * 옵션

![image](https://user-images.githubusercontent.com/66530743/142617706-1fa31b1e-5bf4-47d8-8908-239c44fbba82.png)

   ```
  주로 사용하는 옵션 -n, -e, -f
  ```


### awk 명령어
1) awk이란?
  * ``` awk ``` : 데이터를 조작하고 리포트를 생성하기 위해 사용하는 언어이다. 리눅스에서 사용하는 awk는 GNU버전의 ```gawk```로 심볼릭 링크되어 있다.
  * 간단한 연산자를 명령하인에서 사용할 수 있으며, 큰 프로그램을 위해 사용될 수 있다. ```awk```는 데이터를 조작할 수 있기 때문에 쉘 스크립트에서 사용되는 필수 툴이며, 작은 데이터베이스를 관리하기 위해서도 필수이다.
  * Alfred Aho, Peter Weinberger, Brian Kernighan 3명이 만들었는데 이들의 이름 이니셜을 가져와서 awk라고 부른다.

2) awk사용법
* ```awk```명령어를 입력한 다음, 작은따옴표로 둘러싸인 패턴이나 액션을 입력하고 마지막엔 입력 파일 이름. 파일 이름을 지정하지 않으면 키보드 입력에 의한 표준 입력을 받는다. 그리고 awk는 입력된 라인들의 데이터들을 공백 또는 탭을 기준으로 분리해 ```$2```부터 시작하는 각각의 필드 변수로 분리해 인식한다.
* awk 형식
```
awk 'pattern' filename
awk '{action}' filename
awk 'pattern {action}' filename
```

* 예시
```
$ vi awkfile  
홍 길동 3324    5/11/96 50354  
임 꺽정 5246    15/9/66 287650  
이 성계 7654    6/20/58 60000  
정 약용 8683    9/40/48 365000 
```
```
$ awk '{print $0}' awkfile
>
홍 길동 3324    5/11/96 50354  
임 꺽정 5246    15/9/66 287650  
이 성계 7654    6/20/58 60000  
정 약용 8683    9/40/48 365000
```
* ```awk -f``` 옵션
  * ```awk```액션과 명령이 파일에 작성되어 있다면 ```-f```옵션을 사용
```
awk -f [awk 명령파일] [awk 명령을 적용할 텍스트 파일]
```
```
$ vi awkcommand 
  {print "안녕하세요 " $1, $2"님"}
  {print $1, $2, $3, $4, $5}
```
```
$ awk -f awkcommand awkfile
  > 
  안녕하세요 홍 길동님
  홍 길동 3324 5/11/96 50354
  안녕하세요 임 꺽정님
  임 꺽정 5246 15/9/66 287650
  안녕하세요 이 성계님
  이 성계 7654 6/20/58 60000
  안녕하세요 정 약용님
  정 약용 8683 9/40/48 365000
```
