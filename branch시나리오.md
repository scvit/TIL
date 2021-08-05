# Git branch

## 1. branch 관련 명령어

> Git 브랜치를 위해 **root-commit을 발생**시키고 진행하세요.

```bash
$ git init
$ touch README.md
$ git add .
$ git commit -m 'README!'
$ git log # 확인
```

1. 브랜치 생성

    ```bash
    (master) $ git branch {브랜치명}
    ```

2. 브랜치 이동

    ```bash
    (master) $ git checkout {브랜치명}
    ```

3. 브랜치 생성 및 이동

    ```bash
    (master) $ git checkout -b {브랜치명}
    ```

4. 브랜치 삭제

    ```bash
    (master) $ git branch -d {브랜치명}
    ```

5. 브랜치 목록

    ```bash
    (master) $ git branch
    ```

6. 브랜치 병합

    ```bash
    (master) $ git merge {브랜치명}
    ```

	* master 브랜치에서 {브랜치명}을 병합

## 2. branch 병합 시나리오

> branch 관련된 명령어는 간단하다.
>
> 다양한 시나리오 속에서 어떤 상황인지 파악하고 자유롭게 활용할 수 있어야 한다.
>
> 웹 개발을 한다고 생각하세요.

### 상황 1. fast-foward (프리라이딩)

> fast-foward는 feature 브랜치 생성된 이후 master 브랜치에 변경 사항이 없는 상황

**about.html 페이지를 만드는 작업을 합니다.**

1. feature/about branch 생성 및 이동

   ```bash
   (master) $ git checkout -b feature/about
   (feature/about)
   ```

2. 작업 완료(about.html 파일 생성) 후 commit

   ```bash
   $ touch about.html
   $ git status
   
   $ git status
   On branch feature/about
   Changes to be committed:
     (use "git restore --staged <file>..." to unstage)
           new file:   about.html
   
   
   $ git add .
   $ git commit -m 'Complete About page'
   ```

3. log 결과 확인

   ```bash
   $ git log
   //
   $ git log
   commit d4cb0485a121c35e71f9183dad8cee1c6acd6ce4 (HEAD -> master)
   Author: scvit <goscvit@naver.com>
   Date:   Thu Aug 5 13:47:14 2021 +0900
   
       Complete About Page
   
   commit bcd7da17eb243d9d7c458f80d67a7f2bdeb52bfa
   Author: scvit <goscvit@naver.com>
   Date:   Thu Aug 5 13:45:33 2021 +0900
   
       root commit master
   
   
   ```


3. master 이동

   ```bash
   (feature/about) $ git checkout master
   (master)
   ```


4. master에 병합 > fast-foward (단순히 HEAD를 이동)

  ```bash
  (master) $ git merge feature/about
  ```

5. 결과 확인(log) 

   ```bash
   $ git log
   $ git log
   commit d4cb0485a121c35e71f9183dad8cee1c6acd6ce4 (HEAD -> master)
   Author: scvit <goscvit@naver.com>
   Date:   Thu Aug 5 13:47:14 2021 +0900
   
       Complete About Page
   
   commit bcd7da17eb243d9d7c458f80d67a7f2bdeb52bfa
   Author: scvit <goscvit@naver.com>
   Date:   Thu Aug 5 13:45:33 2021 +0900
   
       root commit master
   
   ```

6. branch 삭제

   > 병합이 완료된 브랜치는 삭제합니다.
   
   ```bash
   $ git branch
   $ git branch -d feature/about
   $ git branch
   
   $ git log
   
   commit d4cb0485a121c35e71f9183dad8cee1c6acd6ce4 (HEAD -> master)
   Author: scvit <goscvit@naver.com>
   Date:   Thu Aug 5 13:47:14 2021 +0900
   
       Complete About Page
   
   commit bcd7da17eb243d9d7c458f80d67a7f2bdeb52bfa
   Author: scvit <goscvit@naver.com>
   Date:   Thu Aug 5 13:45:33 2021 +0900
   
       root commit master
   
   
   
   ```

---

### 상황 2. merge commit (보고서 발표자료 각각)

> 서로 다른 이력(commit)을 병합(merge)하는 과정에서 **다른 파일이 수정**되어 있는 상황
>
> git이 auto merging을 진행하고, **commit이 발생된다.**

**메인 페이지를 만드는 작업을 합니다**

1. feature/main branch 생성 및 이동

   ```bash
   MyScvit@DESKTOP-KOT3PVM MINGW64 /e/kdigital2/강의 노트/GitHub특강 Day1/branchmerge/web/case2 (master)
   $ git branch feature/main
   
   MyScvit@DESKTOP-KOT3PVM MINGW64 /e/kdigital2/강의 노트/GitHub특강 Day1/branchmerge/web/case2 (master)
   $ git switch feature/main
   Switched to branch 'feature/main'
   
   ```

2. 작업 완료 후 commit

   ```bash
    (feature/main)
   $ touch main.html
   
    (feature/main)
   $ git add .
   
    (feature/main)
   $ git commit -m 'main page case2'
   [feature/main faa90d7] complete about page 2
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 about2.html
   
   ```

3. log 확인

   ```bash
   
   $ git log
   commit faa90d7a102aa557fe3d757e68f58eea1b1f5ce7 (HEAD -> feature/main)
   Author: scvit <goscvit@naver.com>
   Date:   Thu Aug 5 14:11:46 2021 +0900
   
      main page case 2
   
   commit 6913abe0cb5f2cdbd520e02031834d2e318f04d0 (master)
   Author: scvit <goscvit@naver.com>
   Date:   Thu Aug 5 14:08:42 2021 +0900
   
       root commit master
   
   ```

4. master 이동

   ```bash
   $ git switch master
   ```

5. *master에 추가 commit 이 발생시키기!!*

   * **다른 파일을 수정 혹은 생성하세요!**

   ```bash
   $ touch additional.txt
   $ git add 'additional.txt'
   $ git commit -m 'master commit add case 2'
   [master 7573bef] master commit add case 2
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 addtional.txt
   
   
   ```

6. master에 병합 -> 자동으로 *merge commit 발생*

   ```bash
   $ git merge feature/main
   ```

7. 결과 (log 확인)

   * vim 편집기 혹은 vs code 화면이 나타납니다.
   * 창을 종료해주시고, 커밋을 확인해보세요.

   ```bash
   $ git merge feature/main
   Merge made by the 'recursive' strategy.
    main.html | 0
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 main.html
   
   
   ```

8. 그래프 확인하기

   ```bash
   
   $ git log --oneline --graph
   *   8548ab6 (HEAD -> master) Merge branch 'feature/main'
   |\
   | * 0ec6a9f (feature/main) main page case2
   * | 7573bef master commit add case 2
   |/
   * d4cb048 Complete About Page
   * bcd7da1 root commit master
   
   
   ```

9. branch 삭제

   ```bash
   $git branch -d feature/main
   ```

---

### 상황 3. merge commit 충돌 (같이 보고서)

> 서로 다른 이력(commit)을 병합(merge)하는 과정에서 **같은 파일의 동일한 부분이 수정**되어 있는 상황
>
> git이 auto merging을 하지 못하고, 충돌 메시지가 뜬다.
>
> 해당 파일의 위치에 표준형식에 따라 표시 해준다.
>
> 원하는 형태의 코드로 직접 수정을 하고 직접 commit을 발생 시켜야 한다.

1. feature/board branch 생성 및 이동

   ```bash
   (master)
   $ git branch feature/board
   
   (master)
   $ git switch feature/board
   Switched to branch 'feature/board'
   
   ```

   

2. 작업 완료(board.html) 후 commit (log 확인)

   * **README.md 파일을 수정하고 같이 커밋하세요.**

   ```bash
   $ touch README.md
   $ git add 'README.md'
   
    (feature/board)
   $ git commit -m 'README커밋'
   [feature/board a5e69fa] README커밋
    1 file changed, 1 insertion(+)
    create mode 100644 README.md
   
   
   ```
   
   


3. master 이동

   ```bash
   $ git switch master
   Switched to branch 'master'
   ```
   
   


4. *master에 추가 commit 이 발생시키기!!*

   * **README.md 파일을 수정 하세요!**
   
   ```bash
   $ touch README.md
   $ git add 'README.md'
   $ git commit -m 'master README'
   [master de6fae6] master README
    1 file changed, 1 insertion(+)
    create mode 100644 README.md
   
   ```
   
   
   
5. master에 병합

   ```bash
   $ git merge feature/board
   CONFLICT (add/add): Merge conflict in README.md
   Auto-merging README.md
   Automatic merge failed; fix conflicts and then commit the result.
   
   
   ```
   
   


6. 결과 -> *merge conflict발생*

   > git status 명령어로 충돌 파일을 확인할 수 있음.
   
   ```bash
   $ git status
   On branch master
   You have unmerged paths.
     (fix conflicts and run "git commit")
     (use "git merge --abort" to abort the merge)
   
   Changes to be committed:
           new file:   board.html
   
   Unmerged paths:
     (use "git add <file>..." to mark resolution)
           both added:      README.md
   
   ```
   
   


7. 충돌 확인 및 해결

   ```bash
   $ git status
   On branch master
   All conflicts fixed but you are still merging.
     (use "git commit" to conclude merge)
   
   Changes to be committed:
           modified:   README.md
           new file:   board.html
   
   ```
   
   


8. merge commit 진행

   ```bash
   $ git add
   $ git commit -m '수정README merge'
   [master e29d99c] 수정README merge
   
   ```

   * vs code 창 닫아주세요!

9. 그래프 확인하기

    ```bash
    $ git log --oneline --graph
    *   e29d99c (HEAD -> master) 수정README merge
    |\
    | * 8fc6af8 (feature/board) readme커밋board
    | * 5e7411f README commit
    | * a5e69fa README커밋
    * | de6fae6 master README
    |/
    *   8548ab6 Merge branch 'feature/main'
    |\
    | * 0ec6a9f main page case2
    * | 7573bef master commit add case 2
    |/
    * d4cb048 Complete About Page
    * bcd7da1 root commit master
    
    ```

   


10. branch 삭제

    ```bash
    $ git branch -d feature/board
    Deleted branch feature/board (was 8fc6af8).
    ```
    
    