# 포크한 깃허브 저장소를 원본 저장소와 동기화 하기

```
// 포크 저장소를 로컬로 클론
$ git clone https://github.com/toriving/transformers.git

// 로컬 저장소로 이동
$ cd transformers

// 현재 설정된 리모트 저장소 조회
$ git remote -v
origin  https://github.com/toriving/transformers.git (fetch)
origin  https://github.com/toriving/transformers.git (push)

// 리모트 저장소 추가
$ git remote add upstream https://github.com/huggingface/transformers.git

// 리모트 저장소 확인
$ git remote -v
origin  https://github.com/toriving/transformers.git (fetch)
origin  https://github.com/toriving/transformers.git (push)
upstream        https://github.com/huggingface/transformers.git (fetch)
upstream        https://github.com/huggingface/transformers.git (push)

// 리모트 저장소 fetch
$ git fetch upstream
remote: Enumerating objects: 3449, done.
remote: Counting objects: 100% (3449/3449), done.
remote: Compressing objects: 100% (54/54), done.
remote: Total 26794 (delta 3399), reused 3431 (delta 3392), pack-reused 23345
Receiving objects: 100% (26794/26794), 21.86 MiB | 5.78 MiB/s, done.
Resolving deltas: 100% (18144/18144), completed with 303 local objects.
From https://github.com/huggingface/transformers
...

// 리모트 저장소 merge
$ git merge upstream/master
Updating f382a8de..2f2aa0c8
Updating files: 100% (1091/1091), done.
Fast-forward
...

// 포크 저장소로 push
$ git push
```

Refer : https://hyunjun19.github.io/2018/03/09/github-fork-syncing/
