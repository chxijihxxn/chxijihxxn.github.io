---
title: "MACOS Github 블로그 설치"
date: "2021-06-23"
---

맥OS로 깃허브 블로그 만드는 것이 윈도우에 비해 아주 조금 복잡해서 기록해둔다. 
템플릿은 [minimal-misakes](https://github.com/mmistakes/minimal-mistakes)를 사용한다.

<br>

## 1. Github repository 생성
{gitID}.github.io 로 Repository name을 작성 후 생성한다.

<img src="/post-images/Gitblog-01.png" width="40%" height="30%" title="Gitblog-01" alt="Gitblog-01"></img>
<br><br>


## 2. minimal-mistakes Download 또는 Fork
https://github.com/mmistakes/minimal-mistakes


minimal-mistakes를 다운로드 했을 경우 앞서 생성한 Github repository를 클론한 후 폴더에 압축을 풀어준다.

minimal-mistakes를 포크 했을 경우 **Repository name**을 자신의 **GitHub Pages url**로 변경해주어야한다.
<br><br><br>


## 3. Homebrew 설치
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
<br><br>

## 4. Ruby 설치
아래 코드를 순서대로 입력하면 된다.
```
brew install rbenv ruby-build

rbenv install 2.6.5

rbenv global 2.6.5
```

<br>

MACOS의 사용자 이름 폴더에서
`Command + Shift + .` 명령어를 입력해 숨겨진 파일을 보이게 하고 `.zshrc` 파일을 텍스트 편집기로 열고 아래 코드를 붙여 넣고 저장.

```
export PATH={$Home}/.rbenv/bin:$PATH && \
eval "$(rbenv init -)"
```

<img src="/post-images/Gitblog-02.png" width="40%" height="30%" title="Gitblog-02" alt="Gitblog-02"></img>

<br>

터미널 재실행 또는 아래 코드 입력.
```
source ~/.zshrc
```
<br><br>


## 5. Bundler 설치 
```
gem install bundler
```
<br><br>


## 6. jekyll 설치 & 실행 
```
bundle install
```
아래 코드는 반드시 **minimal-mistakes를 설치한 Gemfile이 있는 폴더** 위치로 터미널에서 이동하거나 열어 실행한다.
```
bundle exec jekyll serve
```
<br><br>

## 7. localhost에서 접속

여기까지가 MACOS 환경에서 Github 블로그를 설치하는 방법이다.
<br>
이후 `_config.yml` 파일을 수정해 커스텀 하면 된다. 