---
layout: single
title: "자산관리 웹사이트 만들기#front[1] Vite를 이용하여 Vue.js 프로젝트 생성하기"
categories: vue
tags: [vite, blog, vue3, pinia]
toc: true
---

1. 프로젝트 생성

   - cmd나 vscode에서 아래의 명령어를 입력하여 Vite 기반의 Vue 프로젝트 생성하고 종속성을 설치합니다.
   - 설치 후 프로젝트 폴더로 이동하여 npm을 설치합니다.

   ```bash
   npm create vue@latest

   // 혹은

   npm init vue@latest
   ```

   ```bash
   Vue.js - The Progressive JavaScript Framework

   √ Project name: ... vuelog
   √ Add TypeScript? ... No / Yes
   √ Add JSX Support? ... No / Yes
   √ Add Vue Router for Single Page Application development? ... No / Yes
   √ Add Pinia for state management? ... No / Yes
   √ Add Vitest for Unit Testing? ... No / Yes
   √ Add an End-to-End Testing Solution? » No
   √ Add ESLint for code quality? ... No / Yes
   √ Add Prettier for code formatting? ... No / Yes

   Scaffolding project in D:\dbwls\vuelog...

   Done. Now run:

     cd vuelog
     npm install
     npm run format
     npm run dev
   ```

   ```bash
   1@DESKTOP-BILOJD9 MINGW64 /d/dbwls
   $ cd vuelog

   1@DESKTOP-BILOJD9 MINGW64 /d/dbwls/vuelog
   $ npm i

   added 191 packages, and audited 192 packages in 7s

   57 packages are looking for funding
     run `npm fund` for details

   found 0 vulnerabilities
   ```

2. 프로젝트 실행

   - 프로젝트 실행을 위해 터미널 창에 `npm run dev` 입력
   - 프로젝트 빌드 시에는 터미널 창에 `npm run build` 입력

   ```json
   {
     "name": "vuelog",
     "version": "0.0.0",
     "private": true,
     "scripts": {
       "dev": "vite",
       "build": "vite build",
       "preview": "vite preview",
       "lint": "eslint . --ext .vue,.js,.jsx,.cjs,.mjs --fix --ignore-path .gitignore",
       "format": "prettier --write src/"
     },
     "dependencies": {
       "pinia": "^2.1.7",
       "vue": "^3.3.4",
       "vue-router": "^4.2.5"
     },
     "devDependencies": {
       "@rushstack/eslint-patch": "^1.3.3",
       "@vitejs/plugin-vue": "^4.4.0",
       "@vue/eslint-config-prettier": "^8.0.0",
       "eslint": "^8.49.0",
       "eslint-plugin-vue": "^9.17.0",
       "prettier": "^3.0.3",
       "vite": "^4.4.11"
     }
   }
   ```
