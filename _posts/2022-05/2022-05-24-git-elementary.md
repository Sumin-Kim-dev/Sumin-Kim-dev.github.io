---
title:  "[Git] 기초적인 사용법"
categories: Git
tags: config clone add commit push
date: 2022-05-24 04:00
last_modified_at: 2022-05-24
toc: true
toc_sticky: true
---

버전 관리 도구 Git의 기초적인 사용법을 콘솔을 기준으로 정리했다.

## 사용자 등록

말 그대로 사용자 등록이다. github에 가입한 상태라면, github에서 사용하는 이름과 이메일을 넣으면 된다.

```vim
git config --global user.name "사용자"
git config --global user.email "사용자 이메일"
```

## git clone

원격 저장소를 로컬로 복사한다.

```vim
git clone [복사한 명령어]
```

## git add

로컬 저장소에 파일을 업로드 한다.

```vim
git add [파일명]
```

모든 파일을 한꺼번에 업로드하고 싶다면

```vim
git add --all
```

## git commit

저장소에 파일 및 폴더 변경 이력을 기록한다.

```vim
git commit
```

commit message를 작성하는 vim 창이 열리게 된다.  
Insert를 눌러 message를 작성한 후 :wq!을 눌러서 vim을 빠져나온다.

작성할 commit message가 간단하다면

```vim
git commit -m "message"
```

로도 사용 가능하다.

## git push

로컬 저장소에 업로드 된 파일을 원격 저장소로 넘겨준다.

```vim?line_numbers=false
git push -u origin master
```

## commit message 수정

가장 최근의 commit message를 수정하고 싶다면

```vim
git commit --amend
```

이미 push한 commit message를 수정하고 싶다면(가급적이면 사용하지 말 것)

```vim
git push --force [브랜치명]
```
