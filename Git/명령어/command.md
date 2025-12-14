#### git init
> 현재 디렉토리 기준 git 저장소 생성, 초기화
> 해당 폴더에 .git 폴더 생성됨

#### git remote add origin <원격저장소URL>
> 원격 저장소 (Remote Repository) 등록  
> git remote add origin https://github.com/username/myproject.git

#### git remote -v
> 현재 로컬저장소에 연결된 원격 저장소 확인

#### git remote set-url origin https://github.com/username/new-repo.git
> 원격 저장소 URL 수정하기

#### git remote remove origin
> 기존 연결된 원격 저장소 삭제하기

#### get add .
> 수정된 파일 추가

#### git status
> 추가된 파일 확인

#### git commit -m 
> 커밋 메시지 작성

#### git push -u origin main
> 원격 저장소로 반영(push)

#### git pull origin main --rebase
> 원격저장소의 코드 pull로 가져와서 병합 (충돌이 없으면 바로 push 가능)

#### git push -u origin main --force
> 로컬 소스를 원격저장소에 강제로 덮어쓰기

#### git clone https://github.com/username/repo.git
> 원격저장소의 내용을 로컬로 가져오기

#### git config --list
> 저장소 설정 확인

#### git branch
> 현재 브랜치명 확인

#### git branch -vv
> 로컬이 어디에 연결되어 있는지 확인

#### rmdir /s /q .git
> 윈도우 .git 디렉토리 삭제
