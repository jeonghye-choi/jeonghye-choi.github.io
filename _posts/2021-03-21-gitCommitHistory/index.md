---
title: git 커밋 히스토리 삭제
date: 2021-03-21
tags:
  - git
keywords:
  - git
  - 커밋 히스토리 삭제
---

민감한 정보가 푸시(push)되어 GitHub에 업로드 되어버리면, 해당부분만 삭제하거나 수정하기 어렵다.

이럴때 현재 commit을 취소하고 취소한 히스토리까지를 서버에 강제 push하는 방법이 있다.

<br/>

## 최근 commit취소하고 강제 push

현재 올라간 commit 내용을 로컬 작업 패널에서 되돌리고,

다시 서버로 commit. 이 방법을 시행하기 위해 개발자의 작업 내용을 서버상에 강제로 덮어쓰게 되므로 이후 작업했거나 다른 사람의 commit 내용이
지워질 수 있기에 신중해야한다.

먼저 작업 디렉토리로 이동해 다음 명령어를 입력한다.

```bash
$ git reset HEAD^  # 마지막에 실행한 커밋 내용을 되돌림
```

커밋하고

```bash
$ git commit -m "커밋 메시지"
```

푸시

```bash
$ git push origin master -f (또는 git push origin +master)
```

<br/>

## commit history 모두 삭제하고 초기 상태로 되돌리기

히스토리를 모두 지우고 싶은 경우.

- 경고: 이 방법을 사용하면 레포에 있는 모든 파일과 커밋 히스토리가 삭제! 현재 작업 디렉토리에서 initial commit
  상태로 업로드 됨.

먼저 현재 작업 디렉토리(.git 이 존재하는 위치)에서 다음 명령어 입력

```bash
$ rm -rf .git
```

그리고 git init 명령어로 초기화하고 git add 로 파일을 추가(Staging)하기

```bash
$ git init
$ git add . (또는 git add -A)
```

```bash
$ git commit -m "initial commit"
$ git remote add origin <저장소 URL>
```

기존 push할 때와 다르게 --force 명령어를 덧붙여준다. 이미 서버에 존재하는 파일로 인해
발생하는 에러 메세지를 무시하고 강제로 push하겠다는 의미.

```bash
$ git push -u --force origin master
```

<br/>

### 참고

- [JooTC (커밋 히스토리 삭제하여 다시 푸쉬하기)](https://jootc.com/p/201909143109)
