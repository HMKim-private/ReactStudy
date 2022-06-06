---
description: 코드 형상 관리에 사용되는 git의 명령어 모음
---

# Git command

![git flow](<.gitbook/assets/git flow.png>)

* git init: git 생성하기
* git clone git\_path: 코드 clone
* git checkout branch\_name: branch 선택
* git checkout -t remote\__path/branch_\_name: remote branch 선택
* git branch branch\_name: branch 생성
* git branch -r: remote branch 목록 보기
* git branch -a: local barnch 목록 보기
* git branch -m branch\__name change\_branch\_name: branch 이름 바꾸기_
* git branch -d branch\_name: branch 삭제하기
* git push remote_name -- delete branch_name: remote branch 삭제하기
* git add file_path: 수정한 코드 선택하기 (git add \*_)
* git commit -m "commit\_description": commit description 기술
* git push remote\__name branch\__name: add하고 commit한 코드 git server에 보내기 (git push origin master)
* git pull: git server에서 최신 코드 받아와 merge 하기
* git fetch: git server에서 최신 코드 받아오기
* git reset -- hard HEAD^: commit한 이전 코드 취소하기
* git reset -- soft HEAD^: 코드는 살리고 commit만 취소하기
* git reset -- merge: merge 취소하기
* git reset -- hard HEAD && git pull: git 코드 강제로 모두 받아오기
* git config -- global user:name "user\_name": git 계정 이름 변경하기
* git config -- global user:email "user\_email": git 계정 이메일 변경하기
* git stash / git stash save "description": 작업 코드 임시 저장하고 branch 바꾸기
* git stash pop: 마지막으로 임시 저장한 작업 코드 가져오기
* git branch — set-upstream-to=remote\_path/branch\_name: git pull no tracking info error 해결
