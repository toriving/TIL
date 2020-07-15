# profile, basrhc, bash_profile

## 실행 순서
1. /etc/profile.d/test.sh  
2. /etc/profile  
3. /etc/bashrc  
4. ~/.bashrc  
5. ~/.bash_profile  

## login shell / non-login shell
`Login Shell`  
Login shell은 ID와 PW를 입력하여 실행한 shell을 의미.  
.profile / .bash_profile의 경우 login shell을 실행 할 때 로드됨.  

`Non-Login Shell`  
Non-Login Shell은 로그인 없이 실행하는 shell을 의미.
GUI 세션에서 터미널을 띄우는 경우, ‘sudo bash’나 ‘su’같은 것도 해당.


## .bash / .bash_profile
`.bashrc`  
이미 로그인 한 상태에서 새 터미널 창을 열 때마다 로드됩니다. (Non-Login Shell에서 실행됩니다.)

`.bash_profile`  
시스템에 로그인할 때마다 로드됩니다. (Login Shell에서 실행됩니다.) 대부분 개별 사용자에 대한 설정에 대한 코드들이 들어갑니다.  


`.profile`  
로그인할 때 로드됩니다. 개별 사용자에 대한 설정 코드들 중 bash와는 관계없는 부분을 기재합니다.




[Refer](https://jongmin92.github.io/2016/12/13/Linux%20&%20Ubuntu/bashrc-bash_profile/)

