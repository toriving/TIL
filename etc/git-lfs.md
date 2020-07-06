# git-lfs
Naver Summary News Corpus (NSMC)를 구축하고, github에 업로드 하는 과정에서 아래와 같은 에러가 발생하였다.

```
remote: Resolving deltas: 100% (3/3), done.
remote: error: GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
remote: error: Trace: 5e2918cbe094c90305f575a16412e721
remote: error: See http://git.io/iEPt8g for more information.
remote: error: File raw_data.tsv is 137.16 MB; this exceeds GitHub's file size limit of 100.00 MB
remote: error: File train_data.tsv is 102.91 MB; this exceeds GitHub's file size limit of 100.00 MB
To https://github.com/toriving/nsnc.git
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'https://github.com/toriving/nsnc.git'
```

웹 환경에서는 25mb, git-bash 환경에서는 100mb 업로드 제한이 존재한다.

그 이상의 데이터를 업로드 하기 위해서는 git-lfs를 사용해야 한다.

**설치** (ubuntu / wsl2)
```
$ sudo apt install git-lfs
```

**사용**  
git이 존재하는 폴더 내에서
```
$ git lfs install
$ git lfs track "*.tsv"
$ git add .gitattributes
```