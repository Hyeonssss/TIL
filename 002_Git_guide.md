## 01_CLI_intro



### Command 꿀팁

- 과거 명령어 불러오기 - 위, 아래 방향키
- 자동완성 - tab
- `ctrl + a` : 커서가 명령어 맨 앞으로 이동
- `ctrl + e` : 커서가 명령어 맨 뒤로 이동
- `ctrl + w` : 커서 앞에 단어 지워줌
- '>'에 갇혔을 때는 `ctrl + c`를 누르세요.

----



### 경로

- 파일이나 폴더의 고유한 위치를 나타내는 문자열 (주소)

---

#### 루트 디렉토리

- 모든 파일/폴더를 담고 있는 폴더
- windows의 경우 보통 C드라이브를 의미함

#### 상대 경로

- 현재 워킹 디렉토리를 기준으로 계산된 경로
- 현재 워킹 디렉토리가 `c:`라면 `c:\code`의 상대경로는 `code`임
- 간결해서 좋지만 현재 워킹 디렉토리가 변하면 상대 경로도 변경됨

#### `~`틸드(Tilde)

- 현재 사용자의 홈 디렉토리 의미
- 현재 사용자란 컴퓨터를 킬 때 로그인하는 계정

---



### Command

#### cd

- Change Directory
- 현재 워킹 디렉토리를 변경할 때 사용
- `cd ..`하면 부모 디렉토리로 이동

#### date

- 현재 날짜가 출력됨

#### ls

- 현재 워킹 디렉토리의 폴더/파일 확인
- `ls -al`을 활용하면 숨김 폴더와 자세한 정보를 알 수 있음

#### touch

- `touch a.txt` 형식으로 파일을 만들 수 있다

#### mkdir

- `mkdir 디렉토리 이름` 형식으로 폴더 생성
- 만약 폴더 이름 사이에 공백이 있다면 따옴표로 묶어야 한다

#### pwd

- 현재 작업중인 폴더(디렉토리)

#### rm

- 파일 삭제
- `rm -r`폴더 삭제

#### cp, mv

- 복사

  ```python
  $ cp a.txt b.txt
  ```

- 이동(잘라내기)

  ```python
  $ mv b.txt b/b.txt
  ```

- 이름바꾸기

  ```python
  $ mv aa.txt c.txt
  ```

---



## 02_Git_intro



### Git 초기 설정



#### 커밋 작성자(author) 설정

```python
$ git config --global user.email "메일주소"
$ git config --global user.name "유저네임"
```

- 커밋을 작성하는 사람이 누군지 알아야하기 때문

#### 지정된 설정 확인

```python
$ git config --global -l
$ git config --global --list
```

#### 커밋 편집기 변경

```python
$ git config --global core.editor "code --wait"
```

- 해당 명령어는 반드시 vscode가 설치되어 있어야 함
- 기본 텍스트 편집기 vim을 vscode로 대체하는 것

---



### Git Basic

#### 로컬 저장소 설정

```python
$ git init

Initialized empty Git repository in C:/Users/student/Desktop/git_class

student@M172 MINGW64 ~/Desktop/git_class (master)
```

- 폴더에 git 저장소를 초기화하면,
  - `.git` 숨김 폴더가 생기고
  - bash에는 `(master)`라고 표기된다
- 주의사항 git 저장소 내에 또 다른 git 저장소를 만들면 안됨
- git init 명령어를 입력할 때 (master)가 있으면 절대 입력하지 말 것

#### add

> staging area / INDEX

```python
$ git add 파일명
$ git add . # 현재 디렉토리(하위 디렉토리)
$ git add a.txt # 특정 파일
$ git add my_folder/ # 특정 폴더
```

- `working directory`상태의 파일을 `staging area`상태로 변경
- 커밋을 위한 파일 및 폴더들을 추가하는 명령어

```python
$ touch a.txt b.txt

$ git status
On branch master

No commits yet

Untracked files: # 트래킹 되고 있지 않는 파일 목록
  (use "git add <file>..." to include in what will be committed)
        a.txt
        b.txt

nothing added to commit but untracked files present (use "git add" to track)
```

```python
$ git add a.txt
```

```python
$ git status

On branch master

No commits yet

Changes to be committed: # 커밋 예정인 변경사항(staging area)
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt

Untracked files: # 트래킹 되고 있지 않은 파일
  (use "git add <file>..." to include in what will be committed)
        b.txt
```

> 모든 정보는 git status에 있다.

#### commit

```python
$ git commit -m "first commit"
[master (root-commit) c02659f] first commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a.txt
```

```python
$ git log
commit c02659fc917b40f1ab6106a1727703a7884df12e (HEAD -> master)
Author: edujunho <edujunho.hphk@gmail.com>
Date:   Mon Jun 7 15:29:54 2021 +0900

    first commit
```

```python
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        b.txt

nothing added to commit but untracked files present (use "git add" to track)
```

- 커밋을 통해 하나의 버전으로 기록 됨
- 커밋 메시지는 현재 변경사항들을 잘 나타낼 수 있도록 작성
- 커밋은 고유한 아이디인 해시 값을 가짐
  - SHA-1 알고리즘에 의해 생성
- 커밋 목록은 `git log`를 통해서 확인 가능

```pyy
$ git log --oneline # 커밋 목록 한 줄로 보기
c02659f (HEAD -> master) first commit

---

#### status

- working directory, staging area 공간의 파일 상태를 확인할 수 있다.

```python
$ git status
```

#### git log

- 커밋이 완료 되면, 잘 기록되었는지 확인

```python
$ git log
$ git log -1 # 최근 몇개까지 보여주는 옵션
$ git log --oneline # 한줄로 보여주는 옵션
```

---

#### 추가 커밋 쌓기

- a.txt 내용 수정

```python
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   a.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        b.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

```python
$ git add a.txt

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   a.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        b.txt
```

```python
$ git commit -m "second commit"

[master 4cac5c6] second commit
 1 file changed, 1 insertion(+)
```

```python
$ git log --oneline
4cac5c6 (HEAD -> master) second commit
c02659f first commit
```



- b.txt 커밋 만들기

```python
$ git add b.txt

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   b.txt

$ git commit -m "add b.txt"
[master 6fe9152] add b.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 b.txt
```

```python
$ git log --oneline
6fe9152 (HEAD -> master) add b.txt
4cac5c6 second commit
c02659f first commit
```

---



#### git show

- 현재 커밋의 변경기록 확인하기

#### git diff 커밋아이디1 커밋아이디2

- 커밋들 사이에 변경 사항을 확인 가능

```python
git diff 9b15 539d
```

---



## 03_Github



### 기본  설정

#### 원격 저장소

> remote repository

1. 로컬 git 저장소 준비
2. Github repository 생성
3. Repository default branch 변경 (settings -> repositories)
   - main -> master로 변경



---

### 명령어

#### 원격 저장소 주소 추가

```python
$ git remote add origin 저장소URL
```

> git아, 원격 저장소(remote) 추가해줘(add) origin 이라는 이름으로 저장소 URL을!

- origin은 원격 저장소 이름

#### 원격 저장소 목록 보기

```python
$ git remote -v
origin  https://github.com/woongedu/TIL.git (fetch)
origin  https://github.com/woongedu/TIL.git (push)
```

- 잘못 add 한 경우 삭제하기 `$ git remote rm origin`

#### 원격 저장소에 업로드

```python
$ git push -u origin master

Enumerating objects: 8, done.
Counting objects: 100% (8/8), done.
Delta compression using up to 12 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (8/8), 645 bytes | 645.00 KiB/s, done.
Total 8 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/woongedu/TIL.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

> git아, push해줘 origin이라는 이름의 원격저장소에 master 브랜치로!

- 원격 저장소에는 commit이 올라간다.
- commit 이력이 없다면 push할 수 없다.
- 두번째 push 부터는 u 생략 가능

#### pull

- 원격 저장소의 변경사항을 받아옴(update)

```python
$ git pull origin master
```

#### clone

- 원격 저장소 전체를 복제

```python
$ git clone 저장소URL
```

> [주의] clone 받은 프로젝트는 이미 git init이 되어있음
>
> remote도 추가되어 있음

---



## 04_push_pull



### 집 강의장 시나리오

집 ↔ 강의장 (clone & pull ↔ push) 시나리오

- 준비

  - 폴더로 공간 분리

    ```
    # 강의장 컴퓨터라고 가정하는 임의의 폴더
    강의장/
    
    # 집 컴퓨터라고 가정하는 임의의 폴더
    집/
    ```

  - GitHub에서 연습용 레포지토리를 생성한다.

    ```
    TIL-test
    ```

- 강의장 (init, commit, push)

  - `TIL-test`

  - 강의장에서 수업 내용을 정리하고 원격 저장소에 푸쉬!

    - TIL-test 폴더 생성하기

      ```
      강의장/
          TIL-test/
      ```

    - `git init` + 개발 진행

      ```
      # 강의장/TIL-Test/
      
      $ git init
      $ touch a.txt
      ```

      ```
      강의장/
          TIL-test/
              a.txt
      ```

    - `git add + git commit + git push`

      ```
      # 강의장/TIL-Test/
      
      $ git add .
      $ git commit -m "a.txt 파일 추가"
      $ git remote add origin {url}
      $ git push origin main
      ```

    - Github 접속해서 원격 저장소에 업로드 되었는지 확인

- 집 (clone, commit, push)

  - 집으로 가서 강의장에서 올려둔 내용 clone!

    - 처음이기에 clone!

    - 다음부터는 pull!

    - `git clone`

      Github 레포지토리로 가서 `Clone or Download` 메뉴를 눌러서 URL 주소 복사-붙여넣기

      .을 붙여서 한다.

      ```
      # 집/
      
      $ git clone {url} .
      ```

      ```
      집/
      TIL-test/
      a.txt
      ```

  - 집에서 새로운 내용을 추가하고 원격 저장소에 업로드하기

    - `git push`

      ```
      # 집/TIL-Test
      
      $ touch b.txt
      ```

      ```
      집/
      TIL-test/
      a.txt
      b.txt
      ```

      ```
      # 집/TIL-Test
      
      $ git add .
      $ git commit -m "b.txt 파일 추가"
      $ git push origin master
      ```

  - 다음날 강의장으로 가서 집에서 작업한 내용을 가져오기

    - `git pull`

      ```
      강의장/
          TIL-test/
              a.txt
      ```

      ```
      # 강의장/TIL-Test
      
      $ git pull origin main
      ```

      ```
      강의장/
          TIL-test/
              a.txt
              b.txt
      ```

- 강의장 (pull, commit, push)

- 집 (pull, commit, push)

- (반복!)



### push가 안돼요!

1. GitHub 사이트에서 직접 작성한 커밋이 있는 경우

   → GitHub 사이트 통해서 파일을 수정하는 것도 commit으로 기록된다!

2. 집에서 push한 commit이 있는데, 강의장 와서 pull 안하고 commit한 경우

   → 두 상황 모두, 하나의 브랜치에 부모가 같은 서로 다른 commit이 존재해서

   → `A - B` & `A - C`

   → (상황 만들어서 보여주기)

   → pull을 하면 된다!

   2-1. B와 C에서 서로 다른 파일을 수정한 경우

   → pull 해서 `A - B - C - A'(Merge)` 이런 식으로 만들어주면 된다.

   2-2. 같은 파일을 수정한 경우

   → 일이 복잡해짐 → Merge Conflict를 수정해야 한다.

---



## 05_gitignore

> git으로 관리하고 싶지 않은 파일들의 리스트를 작성하여, 특정 파일들을 git이 버전 관리를 하지 않도록 하는 것

- 일반적으로 개인정보 및 특정 사람에게만 적용되는 환경들(개인 개발환경 관련)이 이 파일에 작성 됨 mac - .DS_Store
- 개발환경 관련 파일들(.idea 등)은 버전관리가 될 필요도 없을 뿐더러, 개인정보 같은건 애초에 GitHub에 올라가서는 안됨
- `.gitignore` 파일을 만들어서 관리 (위치는 `.git` 파일과 동일한 곳)
- https://gitignore.io/
  - 본인 개발 환경에 대한 내용을 넣고 생성하면, 일반적으로 개발자들이 많이 쓰는 gitignore 문서를 제공

> 일반적으로 git init 후 첫 add 전 작성할 것

---



## 06_Git_자주하는 실수 모음



### submodule => git 속 git

가끔 Github에 폴더에 화살표가 있을 때

- => Git 저장소 내부에 Git 저장소가 있는 경우

- 솔루션 : submodule 형식으로 활용할 수는 있지만, 처음에는 복잡하게 가지말자!

### 경로 공백 처리

- `마크다운_문법.md`  공백을 _로 변환해서 사용하는걸 권장!

### 약속

- git 명령어는 항상 .git 폴더가 있는 곳에서 하자!
- git 저장소로 활용되는 폴더에 다른 git 저장소를 옮기지 말자!

### 커밋 없는 경우

- 커밋이 없어서 push할 수가 없음. 혹은 브랜치가 없다.
- remote 설정은 되어 있는 것을 확인할 수 있음.

### Commit을 하나도 안하면 branch를 만들 때 에러가 발생해요!

컴퓨터로 git clone 명령어를 통해 clone해와서 branch를 생성하려고 하니 다음과 같은 오류를 얻었습니다.

```
$ git branch develop
fatal: Not a valid object name: 'master'.
```

**원인**

아직 commit을 한번도 하지 않은 repository이기 때문입니다.

**해결방법**

최소 1번이상 commit을 진행하면 됩니다.



### 가능? 불가능?

#### 1. TIL 폴더명 바꿔도 되나요? .git 의 상위폴더!

>  => O 바꿔도됨! 전혀 상관 없음

- 폴더 이동도 자유롭게 해도 되지만, 항상 이동할 때 해당 폴더가 다른 git 저장소인지 체크는 할 필요가 있다!
- 프로젝트 폴더 이름이 바뀌는 것은 커밋과 상관이 없다.

#### 2. 원격저장소 이름이랑 로컬 폴더 이름은 같아야 할까요? 

> => X

원격 저장소 이름이랑 로컬 폴더 이름은 전혀 상관이 없습니다.

그러면 상관이 있는 것은 무엇일까요?

```
$ git remote -v # 원격 저장소 정보 조회
```

그리고 정보만 기록되어 있어서 `clone` `pull` `push` 등의 명령어를 입력할 때 활용되는 것이지, sync가 되어 있는 것은 아니다!

#### git push가 안되는 경우

error: failed to push some refs...

원격 레포지토리를 처음 등록하고(`git remote add origin 깃허브주소` )

git push를 하면 에러가 납니다. github에 master 브랜치와 내 로컬의 master 브랜치가 연결되어 있지 않기 떄문입니다.

`git push --set-upstream origin master`해서 내 로컬의 master 브랜치와 github의 master 브랜치를 연결 시켜줘야 합니다.

하지만 만약에 해당 명령어가 에러가 난다면, 아마도 github에 기본 브랜치가 master 브랜치가 아니라 main 브랜치이기 때문입니다.