# tar

**tar로 압축을 하기 위해 사용**

tar cvzf 압축명.tgz --exclude 묶을폴더/제외1 --exclude 묶을폴더/제외2 묶을폴더

ex)   
tar cvzf test.tgz --exclude no --exclude no2 .

c : 파일을 tar로 압축  
p : 권한을 저장  
v : 압축되거나 풀리는 과정을 화면에 출력  
f : 파일 이름을 지정  
C : 경로 지정  
x : tar 압축해제  
z : gzip 사용


refer : https://sqlplus.tistory.com/entry/tar-%EC%95%95%EC%B6%95%EC%8B%9C-%ED%8C%8C%EC%9D%BC%EC%9D%B4%EB%82%98-%EA%B2%BD%EB%A1%9C-%EC%A0%9C%EC%99%B8%EC%8B%9C%ED%82%A4%EA%B8%B0
