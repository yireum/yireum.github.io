---
layout: single
title: "맥북에서 homebrew로 node.js 설치하기"
categories: coding
tags: [macbook, node.js, npm, setting]
---

1. brew 설치하기
    - 아래의 명령어로 brew 설치하기
        
        ```bash
        /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)
        ```
        
    - 설치 이후 터미널에서 다음 명령어를 입력하여 Homebrew를 사용할 수 있도록 환경 변수를 설정
        
        ```bash
        echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
        ```
        
    - Bash를 사용하는 경우 다음과 같이 실행
        
        ```bash
        source ~/.bash_profile
        ```
        
    - 마지막으로, Homebrew가 제대로 설치되었는지 확인하는 명령어. 정상적으로 설치되었다면 Homebrew의 도움말 표시.
        
        ```bash
        brew help
        ```
        

1. node 설치하기
    - 아래 명령어를 입력하여 설치
        
        ```bash
        brew install node
        ```
        
    - 설치가 완료되면 다음 명령어로 Node.js와 npm의 버전을 확인할 수 있음
        
        ```bash
        node -v
        npm -v
        ```