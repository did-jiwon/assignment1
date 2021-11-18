# 20203187 양지원/assignment1

## 쉘 스크립트
### getopt명령어

*shellscript*로 프로그램을 만들다 보면 실행 인자 및 옵션을 필요로 하는 경우가 있는데, 실행 옵션을 구현할 때 ***getopt***함수를 쓰면 매우 간단해진다.

* Example

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

