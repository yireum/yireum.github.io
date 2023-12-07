---
layout: single
title: "자산관리 웹사이트 만들기#front[2] 프로젝트에 bootstrap 기반 라이브러리 MDB(MDBootstrap) 설치하기"
categories: vue
tags: [vite, blog, vue3, bootstrap, library, plugin]
---

프로젝트 생성 후에는 기존 템플릿 (생각해 본 것은 대쉬보드 스타일의 유료 템플릿이었어요!) 을 사용할까 아니면 Bootstraip기반의 라이브러리를 사용해볼까 고민했는데, 기한이 없는 토이프로젝트라는 점과 아주 다양한 기능의 프로젝트가 아니라는 점에서!

원하는 기능의 몇 개의 페이지만 구현을 목적으로는 bootstrap 기반의 라이브러리를 설치하여 화면작업 해보는 게 좋겠다는 생각을 하게 되었습니다!😉

그리하여 생각해 본 여러 라이브러리 중에서 (블로그 게시물로 올린 적이 있어요!)

[bootstrap 기반의 Library 추천](https://yireum.github.io/coding/Bootstrap-기반의-UI-Library-추천/)

몇가지 검색을 통해 MDB 를 사용하기로 했습니다!👍🏻

1. npm으로 MBD를 설치
    
    ```bash
    npm install mdb-vue-ui-kit
    ```
    
2. vite.config.js에서 code 추가
    
    ```jsx
    export default defineConfig({
      css: {devSourcemap: true},
      plugins: [vue()],
      resolve: {
        base: '/vuelog/'
      }
    })
    ```
    
3. src/main.js에서 css 임포트
    
    ```jsx
    import './assets/main.css'
    
    import { createApp } from 'vue'
    import { createPinia } from 'pinia'
    
    import App from './App.vue'
    import router from './router'
    
    /* css import */
    import 'mdb-vue-ui-kit/css/mdb.min.css';
    ```
    
4. index.html 에 script 추가
    
    ```html
    **<link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet" />
    <link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700,900&display=swap" rel="stylesheet" />**
    ```
    

5. App.vue에서 글꼴 추가

```css
#app {
  font-family: Roboto, Helvetica, Arial, sans-serif;
}
```

1. 이후 vue component를 임포트 하여 사용 (버튼 예시)
    
    ```jsx
    import { MDBBtn } from "mdb-vue-ui-kit";
    ```