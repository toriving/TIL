# Docker Hub

## **로그인**

docker login   
ID와 패스워드를 입력하면 로그인이 되고 ~/.docker/config.json에 인증정보가 저장  

## **이미지 태그**

도커 이미지 이름은 다음과 같이 구성됨  

[Registry URL]/[사용자 ID]/[이미지명]:[tag]  

tage 명령어를 이용하여 기존에 만든 이미지에 추가로 이름을 지어줄 수 있음  

docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]  

ex)  

docker tag app danny/danny-app:1  

## **도커 허브에 이미지 전송**

docker push danny/danny-app:1  