# cat

파일 또는 어떠한 내용을 받아서 터미널에 뿌려주는 역할



ex)
log_file.txt 파일에서 검색 문구를 찾아 log_file_backup.txt로 떨구는 명령문 
```bash
$ cat ./log_file.txt | grep "문구" > log_file_backup.txt  
```


log_file.txt 파일에서 검색 문구를 찾아 해당 라인을 보여주는 명령문  
```bash
$ cat ./log_file.txt | grep "문구1" | grep "문구2" | grep "문구3" | wc -l  
```

여러 파일 이어 붙이기
```bash
$ cat file file2 file3 > file4
```

덧붙이기

```bash
$ cat file1 >> file2
```

다양한 명령어와 함께 사용 가능 (tail, head, more ...)

```bash
$ cat file | more
```

옵션)  

-b: 줄번호를 화면 왼쪽에 나타낸다. 비어있는 행은 제외한다.  
-e: 제어 문자를 ^ 형태로 출력하면서 각 행의 끝에 $를 추가한다.  
-n: 줄번호를 화면 왼쪽에 나타낸다. 비어있는 행도 포함한다.  
-s: 연속되는 2개이상의 빈 행을 한행으로 출력한다.  
-v: tab과 행 바꿈 문자를 제외한 제어 문자를 ^ 형태로 출력한다.  
-E: 행마다 끝에 $ 문자를 출력한다.  
-T: 탭(tab) 문자를 출력한다.  
-A: -vET 옵션을 사용한 것과 같은 효과를 본다.  


