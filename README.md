# 가장 쉬운 Git 강좌 - (상) 혼자작업편

https://www.youtube.com/watch?v=FXDjmsiv8fI

# 명령어들
## 기본 명령어

    // 처음 Git을 설치했을 때 설정
    git config --global user.name "이름"
    git config --global user.email "메일"

    // 기본 명령어
    git init
    git status
    git add -A
    git commit -m "message"
    git log

## 원격 저장소에서 다운로드 받기

    git clone [url]

## 되돌아가기

    /* 특정 시점으로 되돌아가기 (복원불가)
    돌아갈 시점 git log 에서 보고 해쉬 앞 6자리 (그 커밋한 상태로 바뀜) */
    git reset 000000 --hard 

    /* 특정 시점으로 되돌아가기 (복원가능)
    취소할 내역 중 가장 과거의 것을 선택, 그것의 바로 이전 커밋으로 돌아가는 새 커밋 작성 */
    git revert 000000

## 브랜치 관련

    /* 브랜치 생성
    체크아웃중인 브랜치를 기반으로 생성됨 */
    git branch [branch-name]

    // 브랜치 확인
    git branch

    // 브랜치 체크아웃(현재 브랜치 변경)
    git checkout [branch-name]

    /* 브랜치 합치기(merge)
    메인이 되는 브랜치로 체크아웃 후 사용 */
    git merge [branch-name]

    // 여러 branch 간 병합 분기 기록을 하나로 합칠때 merge 대신 rebase(재배치)
    git rebase [branch-name]

    // 브랜치 삭제
    git branch -D [branch-name]

## 브랜치 관련 추가 명령어들

    // 브랜치 생성과 체크아웃 동시에
    git checkout -b [branch-name]

    // 브랜치 생성, 체크아웃, 원격 브랜치 pull 동시에
    git checkout -b [branch-name] [remote-repo]/[remote-branch]
    // 예시) git checkout -b my-idea origin/my-idea

    /* 원격 저장소에 새로운 브랜치 만들어서 push
    또는 있던 브랜치에 push */
    git push [remote-repo-name] [remote-branch-name]

    /* 로컬, 원격 브랜치 모두 보기
    있는데 안나오면 git fetch 로 변경사항 받아오기 */
    git branch -a

    // 로컬 브랜치와 원격 브랜치가 연동되었으면 파라미터 생략가능
    git pull
    git push

    // 로컬 브랜치 삭제
    git branch -D [branch-name]

    // 원격 브랜치 삭제
    git push -d [remote-repo] [remote-branch]
    // 예시) git push -d origin my-idea

## Conflict (충돌)

같은 파일, 같은 라인에 merge할 브랜치들에서 동시에 수정을 하면 conflict가 발생
- 가급적 여러 사람이 동시에 같은 파일을 작업하는걸 피하는게 좋다.

###  

    /* 먼저 Conflict된 부분을 수정하고 */
    git add [file]
    git commit


## 커밋 내역 그래프로 보기

    git log --graph --all --decorate

# 가장 쉬운 Git 강좌 - (하) Github편

https://www.youtube.com/watch?v=GaKjTjwcKQo

# 저장소를 Github에 업로드 하는 법

1. github 저장소 만들기 (초기화 관련 옵션은 체크 해제)
1. <code>git status</code> 로 상태 확인
1. <code>git add</code>와 <code>git commit</code> 로 수정사항을 전부 커밋
1. <code>git remote</code> 로 원격 저장소가 등록되어 있는지 확인
2. github에 나온 명령어를 복붙
<br><code>remote add [url]</code> -> <code>git push origin master</code>
<br>origin 저장소의 master 브랜치에 현재 브랜치의 커밋 내용들을 push 해주는 명령어.
<br>실행 이후 지정한 원격 브랜치와 로컬 브랜치가 연동된다.

# .gitignore

원격 저장소에 업로드하지 않을 폴더나 파일들을 지정하는 텍스트 파일.
<br>해당 파일에 원하는 파일 이름을 추가하면 <code>git status</code>에 더 이상 나타나지 않는다.

- 코드를 실행하면 다운받아지는 패키지
- 코드를 빌드해서 생성되는 파일들
- 그때 그때 실행해서 만들수 있는 파일들
- IDE 세팅
- 보안에서 중요한 파일들 (DB 비밀번호 등)

## 참고 링크
https://www.atlassian.com/git/tutorials/saving-changes/gitignore

# 초대

다른 사용자를 비공개 저장소를 보거나 push 할수있도록 초대할 수 있다.

    Github 프로젝트 -> Settings -> Manage access -> Invite a collaborator

# 커밋
## 커밋 메세지

협업할때 같이 작업하는 사람들에게 이 커밋에서 어떤 수정이 이루어졌는지 알려준다.

- 커밋 메세지 작성 방법에 대해서 구글링 해보자

## 커밋할때의 절차
### 원격 저장소에 새로운 변경이 있는지 확인

    git fetch
    git status

### 원격 저장소에서 변경사항, 커밋내역 받아오기

협업시에는 작업이나 Push 하기 전에 항상 꼭 해주는게 좋다. 그렇지 않으면 괜한 작업을 추가로 해야 하거나 conflict가 생길 수 있다. 또한 push하기 전에 반드시 pull하도록 강제된다.

    git pull origin master

# Conflict

## 상황 1

브랜치 간 합병시 conflict

## 상황 2

같은 브랜치를 두 컴퓨터가 건드림. 한쪽에서 수정해 push 한걸 다른 사람이 pull 받지 않고 과거 버전에서 수정한 후 push 할때 conflict가 일어나는 상황.

    << HEAD
    // 내 수정내용
    ====
    // 다른 사람 수정내용
    >> 0000

같이 파일이 바뀌게 되는데 이 내용들을 전부 수정해주면 된다.

다른 작업자랑 합의해서 수정하거나, 두 충돌하는 내용 중 하나만 남기고

    git add -A
    git commit (인자 없이)

하면 된다. 텍스트 에디터에서 커밋 메세지 나온대로 그대로 저장해주고

    git push
