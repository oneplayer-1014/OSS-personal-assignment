Configuration
-------------
1. git config 확인하기
2. git config -l
3. git config --global -l
4. git config 수정하기
5. git config --global --edit

사용자명/이메일 설정하기
-------------
1. git config --global user.name "USER NAME"
2. git config --global user.email "USER EMAIL"
3. file permission 무시하기
4. 리눅스는 chmod 로 퍼미션을 주는 게 git 에서 무시하게 설정한다

git config core.fileMode false
-------------

Login credentials 캐쉬 설정
-------------
14. git config --global credential.helper cache

Repository
-------------
1. repository 생성
2. 개발 folder 에서 init 하면 .git 폴더가 생기면서 git 이 설정됩니다

git init
-------------
1. git init PROJECT_NAME
2. staging area 로 파일 추가
## 변경된 전체 파일 추가
git add .

## 변경된 1개 파일 추가
git add FILE-NAME

## PATH 내의 변경된 파일 추가
git add FILE-PATH
브랜치 상태확인
git status
commit 하기
## editor 로 commit message 작성
git commit
## command line 으로 commit message 작성
git commit -m "COMMIT-MESSAGE"

## tracked files 을 add 하고 commit 을 동시에 한다
git commit -a -m "COMMIT-MESSAGE"

## 자체서명 commit 을 만든다
git commit -as
git commit -as -m "commit message"
Log
commit Log 확인
## commit history 를 본다
git log

## commit의 변경 내용까지 확인
git log -p

## NUMBER 갯수 만큼 log 를 보여줌
git log -NUMBER

## log 를 한줄로 보여줌
git log --oneline

## log 를 커밋해시와 저자만 보여줌
git log --pretty=format:"%H, %an"

## merge 된 브랜치 그래프를 보여줌
git log --oneline --decorate --graph --all

## first hash 부터 last hash 까지 commit log 를 보여줌
git log <first_commit_hash>~..<last_commit_hash>

## commit hash 의 log 만 보여줌
git log <commit_hash>~..<commit_hash>

## commit hash 의 commit 내용을 보여줌
git show <commit_hash>

## log stats 를 조회한다
git log --stat
commit 전에 변경내역을 확인
## unstaged changes 와 비교한다
## add 로 추가되지 않은 변경된 소스코드를 보여준다
## working directory 와 Index 를 비교
git diff

git diff filename

## staged changes 와 비교한다
## add 로 추가된 소스코드를 커밋로그 첫번째(HEAD)와 비교해준다
## index 와 HEAD 를 비교
git diff --staged
git diff --cached

## working directory 와 HEAD 를 비교
git diff HEAD

## working directory 와 HEAD^ 를 비교
git diff HEAD^
tracked files 에서 삭제
git rm filename
file 이름 변경
git mv oldfile newfile
git 에서 파일 무시
.gitignore 파일에 등록한다

변경사항 원복
file 원복
## revert unstaged changes
git checkout filename

## revert staged changes
git reset HEAD filename
git reset HEAD -p
최근 commit 수정
## overhead commit 을 변경한다
## commit hash 가 바뀜
git commit --amend -a
## HEAD 의 commit 메시지만 변경 한다
git commit --amend -m "CHANGE-COMMIT-MESSAGE"
마지막 commit 으로 원복
## 가장 최근 commit 으로 원복
git revert HEAD

## 되돌릴 COMMIT-ID 로 Revert 한다 
git revert COMMIT-ID
## 또는
## HEAD~3 최근 3개 전의 commit 으로 Revert 한다
git revert --no-commit HEAD~3
git commit -m "Revert Comit A,B,C"
Branch
새로운 브랜치 만들기
## NEW-BRANCH-NAME
git branch NEW-BRANCH-NAME

## 브랜치로 전환
git checkout NEW-BRANCH-NAME

#-b 옵션은 현재 branch 를 복사해서 NEW-BRANCH-NAME 으로 만들고 switch
git checkout -b NEW-BRANCH-NAME
브랜치 리스트 조회
git branch
git branch --list
브랜치 삭제
git branch -d BRANCH-NAME
## 강제로 브랜치 지우기
git branch -D BRANCH-NAME
브랜치 병합
#현재 브랜치에 BRANCH-NAME 을 병합한다
git merge BRANCH-NAME
병합된 브랜치 리스트 조회
## 현재 브랜치에 병합된 브랜치 리스트를 보여준다
git branch -a --merged
브랜치 병합을 원복
git merge --abort
브랜치 이름 변경하기
git branch -m OLD-BRANCH-NAME NEW-BRANCH-NAME
원격 Repository
github 의 remote repository 연결하기
## remote repository 를 조회한다
git remote
## remote repository 의 주소도 조회한다
git remote -v

## origin 이라는 명칭으로 github 의 repository 가 정의됩니다
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY

git remote show origin
remote repository 를 복사해오기
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY
github repository 로 소스 올리기
git push -u REMOTE-NAME BRANCH-NAME

git push -u origin master
## origin 은 git remote add origin 에서 설정한 명칭 입니다

## 혼자 쓰는 거면 이렇게 git push 만 처도 됨
git push
## git push -u origin master 와 동일하게 처리됨
원격 브랜치 확인
git branch -r
원격 repository 와 local repository 병합하기
## github repository 를 가져와서
git fetch REMOTE-NAME
## 로컬 repository 와 병합한다
git merge REMOTE-NAME/BRANCH-NAME
병합 없이 remote branch 를 가져오기
git remote update
원격 브랜치 삭제
git push --delete REMOTE-NAME :BRANCH-NAME
원격 브랜치 이름 변경하기
git push origin :OLD-BRANCH-NAME NEW-BRANCH-NAME
MISC
commit history 변경
git rebase BRANCH-NAME
git rebase -i BRANCH-NAME
원격 브랜치의 최신정보 가져오기
## pull = fetch + merge
## git pull origin master
git pull REMOTE-NAME BRANCH-NAME

## 원격 저장소에서 다운만 한다 (merge 는 따로 해야 한다)
git fetch REMOTE-NAME
## 가져온 정보를 로컬브랜치와 비교 하고 직접 병합 해준다
## git diff HEAD origin/master
## git log --decorate --all --oneline
## git merge origin/master

## 모든 리모트 정보를 업데이트 한다
## fetch 수행됨
git remote update
prune
리모트 저장소에 삭제된 브랜치도 로컬 저장소에서 삭제한다
local 에서 remote 를 ref 하는 것 중 유효하지 않은 것을 제거

## 새로 추가되었거나 삭제된 리모트 브랜치의 정보를 최신화 한다
git remote prune REMOTE-NAME

## 리모트 저장소에서 삭제된 브랜치를 로컬 저장소에도 적용
git pull --prune
git fetch --prune

git prune

## 옵션으로 적용도 가능하다
git config --global fetch.prune true

Stash/un-stash files
변경저장
체크아웃 에러 발생시에 commit 전 상태를 저장해 둔다

git stash

## stash list 를 본다
git stash list
변경저장 해제
저장해둔 상태를 불러온다

git stash pop
브랜치 변경을 동기화
변경사항 확인
git diff --cached

## unstage 로 원복
git reset <file_path>

## 변경사항에 문제 없으면 commit 한다
git commit
untracked 파일 또는 폴더 제거하기
## To remove untracked files
git clean -f
## TO remove untracked directories
git clean -fd
마지막 commit 으로 reset 하기
git reset -hard origin/BRANCH-NAME
모든 변경사항 취소하기
git reset --hard
다른 브랜치에 commit 이동
다른 브랜치의 commit 을 가져올 수 있는데 충돌날 가능성이 많아서 잘 사용하지 않는다

git cherry-pick COMMIT-HASH
원격 저장소의 커밋 되돌리기 (Reset : 히스토리가 망가짐)
## overhead commit 으로 Reset 한다
git reset --hard
git reset --hard HEAD

## 되돌릴 COMMIT-ID 로 Reset 한다
git reset --hard COMMIT-ID
## 또는
## 바로 이전 commit 으로 Reset 한다
git reset --hard HEAD^
## 또는
## HEAD~3 최근 3개 전의 commit 으로 Reset 한다
git reset --hard HEAD~3

## 바로 전으로 reset 한다
git reset --hard HEAD~

## 원격저장소에 안전하게 넣는다
git push --force-with-lease
## 또는
## 강제로 원격저장소에 넣는다
git push --force
커밋 해쉬 정보
git show-ref HEAD
git show-ref HEAD -s
git show-ref master
Patch
## patch 를 적용한다
git am <patch1> <patch2>
## patch 를 취소한다
git am --abort

## conflicts 발생시 하나 이상의 patch 를 적용한다
git am -3 <patch1> <patch2> ...

## conflicts 해결 후에 patch 를 계속 한다
git am --continue

## overhead commit 으로 부터 patch 를 생성한다
git format-patch HEAD~

## n 개 전의 commit 으로 부터 patch 를 생성한다
git format-patch HEAD~n
git config
.gitignore 수정 적용하기
.gitignore 로 git 에서 제외 시킬 수 있는데 .gitignore 수정시에 다시 적용을 해줘야 한다

git rm -r --cached .
git add .
git commit -m "gitignore fixed untracked files"
commit 다시하기
git reset HEAD~

git add <filename1>

git commit

