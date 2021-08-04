# 버전관리

## GIt

Git은 분산버전관리시스템



컴퓨터 파일의 변경사항을 추적하고, 여려명의 사용자들간 해당 파일 작업 조율



## 분산버전관리시스템

중앙집중식 :  시스템 중앙 서버에서 관리, 파일을 받아 수정 , 다시 서버에 전송...

분산버전관리시스템: 원격 저장소를 통해 협업, 모든 히스토리를 사용자들이 공유



## 기본 흐름

1)작업

2)add해 Staging area에 모아

3)commit으로 버전 기록



## 기초 CLI명령어



![image-20210804113430409](C:\Users\MyScvit\AppData\Roaming\Typora\typora-user-images\image-20210804113430409.png)



touch - 파일 만들기

```bash
$ touch <파일명>
$ touch REAME.md
```

ls - 목록 (list)

```bash
$ touch <파일명>
1.txt
```

pwd-작업 파일 경로출력 (print working directory)

```bash
$ pwd
/c/users/lec/desktop/실습1
```

mkdir- 폴더 만들기(make directory )

```bash
$ mkdir test 
```



cd  - 폴더 이동 (change directory)

```bash
$ cd test
~/Desktop/실습1/test $ cd
```



`..`- 상위 디렉토리

`.` - 현재 디렉토리







## 기본명령어



### $ git init

특정 폴더를 git 저장소(repository)를 만들어 git으로 관리

- git 폴더 생성되며
- git bash에서는 (master)라는 표기를 확인할 수 있다



### $ git add <file>

working directory 상 변경내용을 staging area에 추가하기 위해 사용

* untracted 상태의 파일을 staged로 변경
* modifed 상태파일 staged로 변경

![image-20210804132630802](C:\Users\MyScvit\AppData\Roaming\Typora\typora-user-images\image-20210804132630802.png)



### git commit -m '<커밋메시지>'

### git status

### git log



```bash
$ git status
$ git commit -m '커밋메세지'

$ git log 

$ git log - oneline // 1줄로

$ git log-2 -- oneline //2쨰줄 로그까지만 1줄로
```



# !!명령어 정리!!



*** touch a.txt 은 git과 상관이 없다. only bash환경에만 씀

### 저장소 만들기

git clone 주소

git init



### 작업하면서

git add ___

git commit -m '메시지'



### 상태보기

git log

git status



### 원격 저장소

git remote add origin <url주소>: 설정

==>깃아, 원격저장소(remote) 추가해줘(add). origin이란 이름으로. url을

git push origin master : 저장소에 올리는





