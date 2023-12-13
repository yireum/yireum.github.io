---
layout: single
title: "자산관리 웹사이트 만들기#back[2] Postgresql 셋업과 Heroku배포"
categories: strapi
tags: [strapi, heroku, postgresql]
---

1. 스트라피 프로젝트를 저장한 깃 레파지토리에 heroku 앱을 리모트합니다.
    - 먼저 heroku 로그인을 해야 하는데 보통 나와 있는 `heroku login -i` 를 사용하면 이상하게 이메일에 이메일을 넣어도.. 토큰값을 넣어도 에러가 나더라고요.🤣
    - 어이없게도 이메일에도 패스워드에도 토큰값을 넣어야 하는 것이었습니다.
    - 토큰값은 heroku 로그인 후 프로필 이미지를 클릭 하면 account settings 페이지 안에 API Key가 있는데 바로 그것입니다.
    
    - 이후 로그인이 성공하면 heroku 앱을 생성하거나 리모트해줍니다.
    
    ```bash
    heroku create
    
    # 만약 heroku 앱을 이미 만들었다면
    heroku git:remote -a your-heroku-app-이름
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

깃 저장소에 푸시했으면 다음에는 postgresql 데이터베이스 셋업과 heroku 배포까지 해보겠습니다!😙