# tee

**tee 는 표준 입력(standard input)에서 읽어서 표준 출력(standard output) 과 파일에 쓰는 명령어.**

다음 명령을 실행하면 OUTFILE 에 hello 라는 내용이 기록됨
```shell-script
echo "hello" | tee OUTFILE
```

위 명령어를 활용하면 간단한 텍스트 파일 복사를 tee 를 이용해서 구현할 수 있으며 다음 명령어는 OUTFILE 을 NEWFILE 로 복사함
(cp 를 사용하면 더 편할 것 같은데...?)
```shell-script
cat OUTFILE | tee NEWFILE
```

echo사용시 shell 의 append 연산자인 >> 를 사용하려면 -a 나  --append 옵션을 사용하면 됨

```shell-script
echo "hello" | tee -a OUTFILE
```

tee 는 표준 입력에서 읽은 내용을 표준 출력에도 쓰므로 화면에도 표준 입력에서 읽은 내용이 표시됨

즉 다음 명령어를 실행하면 OUTFILE 과 터미널에 모두 "hello world" 가 표시됩니다.
```shell-script
echo "hello world" | tee OUTFILE

hello world
```

이를 방지하면 tee 의 맨 마지막에 /dev/null 을 연결해 주면 표준 출력 장치(예: 터미널)에 표시 되지 않음.

```shell-script
echo "hello world" | tee -a OUTFILE /dev/null
```

## 왜 tee 를 써야 하는가?
**이게 중요**

tee 의 사용 설명을 읽어도 echo 나 cat 등에 IO redirection 연산자를 사용하면 될텐데 왜 tee 가 필요한지 궁금증이 생길 수 있음
(맞아 redirection 쓰면 되지)

즉 다음과 같이 echo 로 써도 되는데 왜 tee 로 다시 한 번 받아야 하는지 궁금할텐대요.
(넵)

file 에 append 하기 #1
```shell-script
echo "hello world" >> OUTFILE
```
file 에 append 하기 #2
```shell-script
echo "hello world" | tee -a OUTFILE
```

shell 에서 출력을 redirection 할 경우 sudo를 사용해도 일반 사용자로 전환 되므로 root 권한으로 파일에 쓰거나 내용 추가가 필요한 경우 제대로 동작하지 않음

그래서 아래와 같이 root 소유인 파일에 sudo echo 를 실행하면 "permission denied" 에러가 나고 내용 추가에 실패함

```shell-script
sudo echo "validate_password.policy=LOW" >> /etc/mysql/mysql.conf.d/mysqld.cnf 
```

이럴 경우 echo 를 받아서 sudo tee 를 하면 정상적으로 동작하며 tee 는 shell script 에서 root 권한으로 특정 파일을 쓰거나 append 할때 주로 활용함.
```shell-script
echo "validate_password.policy=LOW" | sudo tee -a /etc/mysql/mysql.conf.d/mysqld.cnf 
```

### Reference
[Linux/Unix Power Tools](https://www.lesstif.com/lpt/linux-tee-89556049.html)
