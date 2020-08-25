# awk

awk 명령어를 입력한 다음, 작은따옴표로 둘러싸인 패턴이나 액션을 입력하고 마지막엔 입력 파일 이름. 파일 이름을 지정하지 않으면 키보드 입력에 의한 표준 입력을 받음.  
그리고 awk는 입력된 라인들의 데이터들을 공백 또는 탭을 기준으로 분리해 $1부터 시작하는 각각의 필드 변수로 분리해 인식. [1]




Q : Using awk to print all columns from the nth to the last  
A : [2]
```shell-script
awk '{$1=""; print $0}' somefile
awk '{$1=$2=""; print $0}' somefile

# clean
awk '{$1=""; print substr($0,2)}' 
```


Reference  
[[1]](https://zzsza.github.io/development/2017/12/20/linux-6/)  
[[2]](https://stackoverflow.com/questions/2961635/using-awk-to-print-all-columns-from-the-nth-to-the-last)  
