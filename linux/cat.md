cat ./log_file.txt | grep "문구" > log_file_backup.txt  


log_file.txt 파일에서 검색 문구를 찾아 log_file_backup.txt로 떨구는 명령문  


cat ./log_file.txt | grep "문구1" | grep "문구2" | grep "문구3" | wc -l  



log_file.txt 파일에서 검색 문구를 찾아 해당 라인을 보여주는 명령문  



옵션)  

-c : 문자수 출력
-m : 캐릭터수 출력
-l : 라인수 출력
-w : 단어수 출력
-L : 가장 긴줄 한줄 출력


