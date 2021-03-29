---
title: \[Error] The current branch master has no upstream branch
date: 2021-03-21
tags:
  - git
  - Error
keywords:
  - git
  - The current branch master has no upstream branch
---

```bash
$ git push

# error
fatal: The current branch master has no upstream branch.

To push the current branch and set the remote as upstream, use

git push --set-upstream origin master
```

<br/>

## 원인

원격저장소 이름을 정확히 언급해주지 않아서.

## 해결방법

git remote -v 를 통해 현재 저장된 원격 저장소 이름을 찾고,

원격 저장소를 명시하여 적어주기! ("origin")

```bash
$ git remote -v

$ git push origin master
```
