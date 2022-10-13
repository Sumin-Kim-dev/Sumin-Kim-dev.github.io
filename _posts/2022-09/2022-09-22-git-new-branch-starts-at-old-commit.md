---
title:  "[Git] 예전 commit 지점부터 시작되는 새 브랜치 만들기"
categories: Git
tags: switch checkout push
date: 2022-09-22 01:30
last_modified_at: 2022-09-22
toc: true
toc_sticky: true
---

최근 과제를 하던 도중 문제가 생겼다.  
과제 repo에서 내 repo로 fork해서 과제를 하고 pull request로 제출하는 방식의 과제이다.  
첫 과제는 아무 생각 없이 내 repo의 main branch에서 진행했는데, 두번째 과제를 할 때 문제가 생겼다.  
두번째 과제를 내 repo로 업데이트를 할 때 충돌 문제가 발생한 것이다.  

첫 과제를 하기 전 commit으로 돌아가서 새 branch를 만들어주고 거기에 과제 repo를 가져오면 이 문제를 해결할 수 있다.
아래 과정을 순서대로 수행하자.

## 충돌이 일어나기 전 시점의 commit id를 찾기

먼저 내 저장소에서 충돌이 일어나기 전 시점, 즉 과제를 하기 전 시점의 commit id를 찾아야 한다.  
github 사이트에서 commit 목록을 들어가자.
![충돌이 일어나기 전 commit 찾기 - 1](/assets/img/0922git-find-commit-1.PNG "충돌이 일어나기 전 commit 찾기 - 1"){: .center}
*파란 부분을 클릭하면 commit 목록이 나온다.*

원하는 시점의 commit을 찾았다면, commit id를 복사하자.
![충돌이 일어나기 전 commit 찾기 - 2](/assets/img/0922git-find-commit-2.PNG "충돌이 일어나기 전 commit 찾기 - 2"){: .center}
*파란 부분을 클릭하면 commit id가 복사된다.*

## 앞에서 찾은 commit id로 돌아가기

```vim
git checkout [commit id]
```

![찾은 commit id로 이동하기](/assets/img/0922git-checkout.PNG "찾은 commit id로 이동하기"){: .center}
*찾은 commit id로 이동한다.*

## 돌아간 지점에서 새 branch를 만들고, 원격 저장소에 push 하기

```vim
git switch -c [새 branch 이름]
```

![이동한 지점에서 새 branch 만들기](/assets/img/0922git-switch.PNG "이동한 지점에서 새 branch 만들기"){: .center}
*2에서 이동한 지점에서 branch가 만들어진다.*

아래는 제대로 되었는지 확인하기 위해 git log를 찍어본 사진이다.
![새 branch가 제대로 만들어졌는지 확인](/assets/img/0922git-after-switch.PNG "새 branch가 제대로 만들어졌는지 확인"){: .center}
*1에서 찾은 commit id가 최근 로그로 찍힘을 확인할 수 있다.*

이제 방금 만든 새 branch를 원격 저장소에 push 하자.

```vim
git push --set-upstream origin [위에서 만든 새 branch 이름]
```

![원격 저장소로 branch push](/assets/img/0922git-push-branch.PNG "원격 저장소로 branch push"){: .center}
*방금 만든 새 branch를 원격 저장소에 push한다.*

이제 만들어진 새 branch에 과제 repo를 가져오면 충돌없이 깔끔하게 가져올 수 있다!

## 참고 자료

- git commit 돌아가기 & 새 branch 만들기 : [GIT - 과거 commit으로 돌아가서 branch 만들어 사용하기](https://myhappyman.tistory.com/99)
- push branch : [\[Git\] Branch 생성, Branch 원격 저장소 푸쉬](https://codiving.kr/16)
