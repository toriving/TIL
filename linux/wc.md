# wc

wc - (word count) 사용자가 지정한 파일의 행, 단어, 문자수를 세는 프로그램

```
$ wc  [-clmw] [file ....]
$ wc -l  file_name
$ ls | wc -w
$ cat filename | wc -l
```

기본형식 : wc 옵션 파일이름. 
파일이름을 입력하지 않으면 표준 입력으로 부터 정보를 받아들여 계산한다.  
-l 행  
-w 단어   
-c 문자  

[Refer](http://www.incodom.kr/Linux/%EA%B8%B0%EB%B3%B8%EB%AA%85%EB%A0%B9%EC%96%B4/wc)
