# Auth Form - Sliding Sign In and Sign up

![build and deploy workflow](https://github.com/kavin25/auth-form/workflows/.github/workflows/build.yml/badge.svg)
Preview at https://kavin.me/auth-form

## Things I learnt

- Creating sliding form
- Using gh-pages npm package for deployment
- Using parcel with Github actions

  - Add the following script to package.json

  ```json
  "build": "parcel build src/index.html -d dist --public-url /auth-form/",
  ```

  - Replace auth-form with repo name
  - Use the following gh workflow

  ```yml
  name: "Build & Deploy"

  on:
    push:
      branches:
        - master

  jobs:
    build:
      runs-on: ubuntu-20.04

      steps:
        - name: Checkout 🛎️
          uses: actions/checkout@v2
          with:
            persist-credentials: false
        - name: Use Node.js
          uses: actions/setup-node@v1
          with:
            node-version: "14.x"
        - name: Install Dependencies 💻
          run: npm install
        - name: Build using Parcel 🎁 🔧
          run: npm run build
        - name: Deploy using gh-pages 🚀
          uses: JamesIves/github-pages-deploy-action@3.7.1
          with:
            GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
            BRANCH: gh-pages
            FOLDER: dist
            CLEAN: true
  ```
