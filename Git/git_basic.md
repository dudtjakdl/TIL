> 해당 문서는 [Do it! 지옥에서 온 문서 관리자 깃&깃허브 입문 (이고잉, 고경희 저)](http://www.yes24.com/Product/Goods/84803146)을 보고 정리한 내용입니다.

## 기본 리눅스 명령어
```shell
cd ~
# 홈 디렉터리로 이동
cd .. 
# 부모 디렉터리로 이동
cd <디렉터리 이름> 
# 디렉터리로 이동

pwd
# 현재 경로 확인

ls 
# 현재 위치의 디렉터리와 파일 표시
ls -a 
# 숨겨진 디렉터리와 파일까지 모두 표시
ls -l 
# 디렉터리의 상세 정보까지 표시

mkdir <디렉터리 이름>
# 디렉터리 생성

rm -r <디렉터리 이름>
# 디렉터리 및 하위 디렉터리, 파일까지 강제로 삭제
```
## 기본 Git 명령어
```shell
git init 
# 저장소 초기화
git init <디렉터리 이름> 
# 새로운 디렉터리를 만들고 저장소 초기화

git config user.name "사용자 이름" 
# 사용자 이름 설정 (--global 옵션 추가시 전역으로 설정)
git config user.email "메일 주소" 
# 메일 주소 설정 (--global 옵션 추가시 전역으로 설정)

git status 
# 현재 깃 상태 확인

git add <파일 이름> 
# 파일 스테이지에 올리기
git add . 
# 수정된 파일 한꺼번에 스테이지에 올리기

git commit -m "메시지" 
# 메시지와 함께 커밋
git commit -am "메시지" 
# 스테이지에 올림과 동시에 커밋 (최초로 커밋한 파일만 가능)

git log
# 커밋 로그 표시
git log --stat  
# 커밋마다 자세한 설명, 변화 보여줌
git log --oneline 
# 한 줄에 한 커밋씩 보여줌
git log --branches 
# 각 브랜치의 커밋을 함께 보여줌
git log --graph 
# 커밋과 커밋의 관계를 그래프 형태로 표시
git log --branches --graph 
# 브랜치와 커밋의 관계를 그래프 형태로 표시
git log <브랜치1>..<브랜치2> 
# 브랜치1을 기준으로 브랜치2와 비교

git diff 
# 최근 버전과 작업 트리의 수정 파일 사이의 차이 표시

git reset HEAD <파일 이름> 
# 지정한 파일의 스테이징 되돌리기
git reset HEAD 
# 스테이지에 있는 모든 파일 되돌림
git reset HEAD^ 
# 가장 최근 커밋 취소
git reset HEAD~3 
# 최근 3개의 커밋 취소
git reset --soft HEAD^ 
# 언스테이징 하지 않고 최근 커밋 취소
git reset --mixed HEAD^ 
# 스테이징 및 최근 커밋 취소 (기본 옵션)
git reset --hard HEAD^ 
# 스테이징, 최근 커밋, 파일 수정한 것도 모두 취소
git reset <커밋 해시> 
# 지정한 커밋 해시로 이동하고 이후 커밋 취소

git revert <커밋 해시> 
# 지정한 커밋 해시의 변경 이력을 취소

git checkout -- <파일 이름> 
# 작업 트리에서 수정한 파일 가장 최신 버전 상태로 되돌리기
git checkout <브랜치 이름> 
# 다른 브랜치로 이동 (체크아웃)
git checkout -b <브랜치 이름> 
# 브랜치를 만들고 바로 체크아웃

git branch 
# 현재 존재하는 브랜치 확인
git branch <브랜치 이름> 
# 브랜치 생성
git branch -d <브랜치 이름> 
# 브랜치 삭제
git branch -D <브랜치 이름> 
# 병합하지 않은 브랜치 강제로 삭제

git merge <브랜치 이름> 
# 현재 브랜치에 <브랜치 이름>을 가져와 병합
git merge <브랜치 이름> --edit 
# 편집기 실행 후 커밋 메시지 추가 및 수정
git merge <브랜치 이름> --no-edit 
# 기본 커밋 메시지 그대로 사용

git stash 
# 수정한 파일 감추기
git stash list 
# 감춘 파일 목록 표시 (스택 방식으로)
git stash pop 
# 감춘 파일 꺼내기 (FILO 방식으로)
git stash apply 
# 감춘 파일 되돌리지만 목록에 그대로 두기
git stash drop 
# 감춘 파일 꺼내지 않고 목록에서 삭제
```

## 깃허브 관련 명령어

```shell
git remote add origin <리포지토리 주소> 
# 깃허브 원격 저장소에 지역 저장소 연결
git remote -v 
# 원격 저장소 연결 확인
git branch -M main 
# 지역 저장소 master 브랜치 이름을 main으로 변경
git push -u origin main 
# 지역 저장소의 브랜치를 원격 저장소의 main 브랜치에 연결

git push origin <브랜치 이름> 
# 지역 저장소의 브랜치를 원격 저장소에 푸시
git push 
# 지역 저장소 -> 원격 저장소로 커밋 푸시
git pull 
# 원격 저장소 -> 지역 저장소로 커밋 풀

git clone <리포지토리 주소> <디렉터리 이름> 
# 해당 디렉터리에 원격 저장소 복제
git clone <리포지토리 주소> . 
# 현재 디렉터리에 원격 저장소 복제

git fetch 
# 원격 저장소 브랜치 정보 가져오기
git checkout FETCH_HEAD 
# 페치해서 가져온 FETCH_HEAD 브랜치로 체크아웃
git diff HEAD origin/main 
# 지역 저장소의 최신 커밋과 페치한 커밋의 차이 비교
git merge FETCH_HEAD 
# 페치로 가져온 브랜치 병합

ssh-keygen 
# SSH 키 만들기
```