# Helm repository setup using Helm github pages
- ref: https://github.com/stefanprodan/helm-gh-pages

```
Github pages 를 이용하여 구축


pages.github.com

github에서 helm-charts-repo 이름으로 생성

cd myrepo

git clone git@github.com:swgu931/helm-charts-repo.git

cd helm-charts-repo
git checkout --orpahn gh-pages
git reset --hard
git status

vi index.html

---
<html>
  <head>
    <title> Chart Repo </title>
  </head>
  <body>
    <h1> Welcom to my Helm chart repo? </h1>
    <p> This is Helm repository published by github pages. </p>
  </body>
</html>
---

git add index.html
git commit -m "Add index.html"
git push origin gh-pages
    
# 사이트에서 확인
---
# https://github.com/stefanprodan/helm-gh-pages#

git checkout main

mkdir -p .github/workflows
vi .github/workflows/publish.yaml
---
name: Publish Helm charts

on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  publish-chart:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Publsh Helm charts
        uses: stefanprodan/helm-gh-pages@master
        with:
          token: ${{ secrets.GITHUB_TOKEN }}

---

git status
git add .github/
git commit -m "Add workflows"

git push origin main

mkdir charts
ls charts
ls ../common
ls ../my-first-release

cp -r ../common charts
cp -r ../hello charts
cp -r ../my-first-release charts
cp -r ../wordpress charts

git status

ls charts
git add charts
git checkout -b test  # 이후 pull request 로 만들기 위해

git commit 
git log
git push origin test

# github site 에서 test branch 를 main branch 를 머지하는 요청을 처리
# create pull request
# merging pull request

---

helm repo add jaesang https://jaesang.github.io/helm-charts-repo
helm repo update
helm search repo jaesang

helm pull jaesang/wordpress
rm wordpress-13.2.2.tgz

helm install myapp3 jaesang/hello
helm ls
kubectl get po
```
