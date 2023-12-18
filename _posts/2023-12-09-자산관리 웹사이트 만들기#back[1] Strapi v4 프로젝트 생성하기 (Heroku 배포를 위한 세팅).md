---
layout: single
title: "자산관리 웹사이트 만들기#back[1] Strapi v4 프로젝트 생성하기 (Heroku 배포를 위한 세팅 실패기)"
categories: strapi
tags: [strapi, heroku, postgresql]
---

### 실패기 입니다!! postgresql의 무료 플랜이 없어요.. 🤣

웹사이트에서 필요한 데이터베이스와 백엔드 api를 스트라피를 통해서 구현해보려고 합니다!

Heroku 배포를 위한 스트라피 설치 과정이 약간 다른데 그 부분 정리해보겠습니다.

1. Strapi v4 프로젝트 생성
    - cmd나 vscode에서 아래의 명령어를 입력하여 Strapi를 설치합니다.
    - heroku 공식문서에 sqlite가 heroku와 호환이 되지 않아 postgresql을 사용해야 하는데 quickstart로 설치하면 안됩니다.
    
    ```bash
    $ npx create-strapi-app yoojin-back
    ```
    
    - 여기서 한 가지 문제가 발생하는데 quickstart로 설치하지 않고 custom하려면 node 버전이 18에서 20 사이에서만 설치가 됩니다.
    - 저는 node 버전이 21이었기 때문에 nvm(Node Version Manager)을 이용하여 node 버전 관리를 해주기로 했습니다.
    
    ```bash
    # nvm 설치
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
    
    # 설치 후 nvm 명령어가 안 써지는 경우
    # zsh에서도 nvm을 사용할 수 있도록 설정
    echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.zshrc
    echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm' >> ~/.zshrc
    echo '[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion' >> ~/.zshrc
    source ~/.zshrc
    
    # 사용할 버전의 노드 설치
    nvm install 20
    
    # 설치가 완료되면, 다음 명령으로 사용할 버전을 선택
    nvm use 20
    
    # 현재 쉘 세션에서만 적용하고 싶을 때 명령어
    nvm alias default 20
    ```
    
    - 이후 다시 custom으로 스트라피 설치를 진행합니다.
    
    ```bash
    mero@yujin-ui-MacBookPro dbwls % npx create-strapi-app@latest yoojin-back
    ? Choose your installation type Custom (manual settings)
    ? Choose your preferred language JavaScript
    ? Choose your default database client postgres
    ? Database name: yoojin-db
    ? Host: 127.0.0.1
    ? Port: 5432
    ? Username: yoojin
    ? Password: ******
    ? Enable SSL connection: No
    ```
    

- 프로젝트를 생성한 후에는 .gitignore파일에 package-lock.json을 넣어주어야 heroku에서 이슈가 발생하지 않는다고 합니다.
- 그렇게 하고 습관처럼 스트라피를 실행시키지만 실행되지 않는다.. 아직 postgresql와 연결이 안되어 있어서 그런 것입니다.
- 그래서 heroku 배포를 위해 설치한 스트라피 프로젝트를 깃에 올려줍니다.

```bash
git init
git add .
git commit -m "Initial Commit"
```

깃 저장소에 푸시했으면 다음에는 postgresql 데이터베이스 셋업과 heroku 배포까지 해보려고 했는데,

상단에 써 놓을 것처럼 실패기 입니다!! postgresql의 무료 플랜이 없어졌더라고요.. 🤣
그래서 저는 네이버클라우드에서 1년간 무료로 사용할 수 있는 마이크로 서버에 올리기로 결정하였습니다!

https://ramen4598.tistory.com/85

위의 블로그를 참고해서 가입, 세팅을 하였고,
다음 글에서는 원격 서버 접속 방법과 스트라피를 설치하여 테이블을 생성하는 것까지 해보겠습니다!


