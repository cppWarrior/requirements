[개발 환경 세팅](#개발-환경-세팅)
- [윈도우](#윈도우)
- [우분투](#우분투)
- [mac](#mac)

[git 튜토리얼](#git-튜토리얼)
- [git이란?](#git이란)
- [git 설치](#git-설치)
- [git 기본명령어](#git-기본명령어)
- [git 가지치기](#git-가지치기)
- [git flow](#git-flow)
- [GitKraken](#gitkraken)
- [실습](#실습)

# 개발 환경 세팅
GCC(GNU Compiler Collection)를 지원하는 오픈소스 IDE인 `Code :: Blocks`를 사용하여 C/C++ 코드를 작성할 겁니다.

본인의 OS에 따라 아래 안내를 따라주십시오.

> Code :: Blocks 를 사용하는 이유??  
> 1. 무료이다.
> 2. 크로스 플랫폼이다.
> 3. Visual Studio의 컴파일러는 알고리즘 대회 등의 컴파일러와 달라서 학습시 혼동될수있다.
## 윈도우
- ### mingw 설치 

[참고](http://kkikkodev.tistory.com/41)  

    1. [mingw 64 bit 다운 링크](http://sourceforge.net/projects/mingw-w64/files/latest/download)에서 mingw 설치파일을 다운받고 실행한다.  
    2. **Settings**에서 **`Architecture`을 `x86_64`로 바꾸고** 나머지 옵션은 그대로 둔다.  
    3. Next 버튼을 광클하여 설치를 완료한다.  
    4. 환경변수에 `C:\Program Files\mingw-w64\x86_64-7.1.0-win32-seh-rt_v5-rev0\mingw64\bin` (주소는 다를수 있으니 각자의 경로를 정확히 넣을것)을 추가해준다.  
    5. 명령프롬프트에서 `gcc --version`을 쳐보고 설치가 잘되었는지 확인한다.
    
- ### Code :: Blocks 설치

[참고](http://kkikkodev.tistory.com/42)


## 우분투

[참고](http://kkikkodev.tistory.com/40)


## mac
~~깔아보니 맥에서 코드블럭은 쓰레기였다..~~ **깔지 않는걸 추천한다.**

재학중인 학생이라면 코드블럭 대신 [CLion](https://www.jetbrains.com/clion/)을 깔자. 원래는 유료 IDE이지만 학생 인증을 받으면 무료다.

# git 튜토리얼

## git이란?
깃은 버전 관리 시스템 중 하나 입니다. 버전 관리 시스템이란 쉽게 말해서 언제, 누가, 어느 파일의 어떤 부분을 작업했는지 쉽게 관리해주는 시스템입니다.  파일들의 히스토리가 전부 기록이 되어 원하는 위치로 간편하게 이동할 수 있습니다. 지금 읽고 계신 이 페이지도 깃을 사용하고 있습니다.

![4commits](/git.PNG)

스크롤을 위로 올려 저 부분을 클릭하고 내용을 살펴보세요! 보신것이 바로 깃입니다. 만약 많은 사람들과 규모가 큰 프로젝트를 진행중이라면 버전관리는 필수입니다. 

## git 설치
### 윈도우
[윈도우용 깃 설치 링크](https://git-for-windows.github.io/) 에서 설치하세요! 설치가 완료된 후 명령프롬프트창에서
```
git
```
을 입력 했을때 다음과 같은 화면이 나온다면 성공적으로 설치가 된겁니다.

![git success](/git2.PNG)

### 우분투
```
apt-get install git
```
이 한줄이면 됩니다! 윈도우와 마찬가지로 터미널에서 `git`을 입력하고 설치가 잘 되었는지 확인해보세요.

### mac
[mac용 깃 설치 링크](http://sourceforge.net/projects/git-osx-installer/) 에서 설치하시고 마찬가지로 테스트 해보세요.

## git 기본명령어

```
git init
```
이 명령어는 현재 디렉토리를 git 저장소로 관리하겠다고 선언하는 명령어입니다.

```
git clone
```
이미 서버에 올라와져 있는 저장소를 다운받을수도 있습니다. 이걸 git에서는 멋있게 `clone` 이라고 합니다.

명령 프롬프트나 터미널을 열어 실제로 이 저장소를 clone 받아봅시다.

우선 `cd Documents` 라는 명령어로 적절한 폴더로 이동하고, `git clone https://github.com/cppWarrior/requirements.git`을 입력해보세요. clone 뒤의 주소는 이 저장소의 주소입니다.

![clone](/clone.PNG)

![cloneresult](/cloneresult.PNG)

그다음 `문서` 폴더에서 잘 클론되었는지 확인하세요! `requirements` 라는 폴더가 새로 생겼다면 성공한겁니다! :clap::clap:

```
git add 파일/경로 이름
```

git은 파일을 크게 두가지로 나눕니다. 바로 `trackted`파일과 `untrackted`파일입니다. `trackted`파일은 git으로 관리되고 있는 파일이고, `untrackted`파일은 깃이 **무시**하는 파일입니다. 보안상 노출되면 안되는 정보나 이런저런 설정 파일들을 `untrackted`파일로 해놓고 서버에 올라가는걸 방지하죠. 

`tracked` 파일은 다시 세가지로 나뉩니다. `unmodified`, `modified`, 그리고 `staged` 입니다. `unmodified`는 말그대로 수정되지 않은 파일입니다. 그리고 `modified`는 수정된 파일입니다. 그럼 `staged` 파일은 뭘까요?

`staged` 파일은 수정된 파일 중에서 "이건 수정사항을 기록 해놔야**겠**어!" 라고 생각되는 파일들입니다. 수정한 파일들 중 기록에 남기고 싶은 파일은 `git add 파일이름`이라는 명령어로 staged 상태로 만듭니다. "**겠**어"에 강조를 한 이유는 staged 상태라고 바로 기록이 되는건 아니기 때문입니다. 기록은 나중에 staged 파일들을 모아놓고 `commit`이라는 명령어로 한꺼번에 합니다.

아까 clone한 폴더에서 실제로 사용해봅시다.

clone한 그 상태의 파일들은 모두 `tracked`이며 `unmodified` 상태입니다. 이제 README 파일을 메모장으로 열어서 수정을 해봅시다. ``##실습``이라고 적힌 곳 아래에 한글로 본인 이름을 적고 저장하세요.

이제 README 파일은 `modified`상태가 되었습니다. 명령프롬프트나 터미널에서 `git status`를 입력해보세요.

![](/gitstatus.PNG)

수정된사항이 아직 staged 되지 않았다고 하네요.

수정된 이 파일을 `staged` 상태로 만들어 봅시다. `git add README.md`를 입력하세요. 그 다음 다시 `git status`로 상태를 보면,

![](/gitstatus2.PNG)

파일이 잘 `staged` 되었고 커밋만을 기다리고 있군요.

```
git commit -m "커밋 메시지"
```

```
git push
```

```
git pull
```

## git 가지치기



## git flow



## GitKraken

깃 크라켄은 아주 멋진 깃GUI 입니다. 명령어가 아직 익숙하지 않다면 다운받아보세요!

[GitKraken](https://www.gitkraken.com/)

![gitkraken](/gitkraken.png)

## 실습

이 저장소를 로컬에 clone하고 이 파일 마지막 줄에 본인 이름을 적고 푸쉬해보세요!
(이미 깃에 익숙하신 분들은 안하셔도 됩니다.)
