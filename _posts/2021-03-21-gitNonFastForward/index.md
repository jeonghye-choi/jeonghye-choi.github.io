---
title: \! [rejected] master -> master (non-fast-forward)
date: 2021-03-21
tags:
  - git
  - error
keywords:
  - git
  - master -> master (non-fast-forward)
---

```bash
$ git push --set-upstream origin master

! [rejected] master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/SOMJANG-42MARU/MaruKeyword.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

업로드하려는 디렉토리에서

```bash
$ git init   # 초기화
```

```bash
$ git remote add origin <url>   # 원격저장소 설정
```

```bash
$ git push origin master   # ERROR!!!!
```

<br/>

## 원인

.gitignore 파일 또는 README.md 파일로 인해 발생

<br/>

## 해결방법

push하려고 하는 브랜치 앞에 +를 붙여 push

```bash
$ git push origin +master
```

push 성공!

<br/>

## 참고

- [솜씨좋은장씨 유용한정보 참고](https://somjang.tistory.com/entry/Git-rejected-master-master-non-fast-forward-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95)
