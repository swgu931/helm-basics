# Helm Local setup
## Method 1. Using local storage
## Method 2. By installing chartmuseum

```
helm repo update : index.yaml 갱신

helm repo index : index.yaml 생성



helm package .

cp mya---0.1.0.tgz ../myrepo
cd ../myrepo
ls -alh


helm repo index .

helm repo index . --url http://my-helm-repo.com/

===============
local Helm repo 구축

Using Chartmuseum
Binary & Helm chart

mkdir chartmuseum
cd chrtmuseum

curl https://raw.githubusercontent.com/helm/chartmuseum/main/scripts/get-chartmuseum | bash

chartmuseum --debug --port=8080 \
  --storage="local" \
  --storage-local-rootdir="./chartstorage"


ls myrepo

helm repo list
helm repo add local http://localhost:8080
helm repo list
# github.com/chartmuseum/helm-push

helm plugin install https://github.com/chartmuseum/helm-push
helm cm-push

cd myrepo
helm cm-push commonxx.tgz local
helm cm-push my-first-release.tgz local

helm repo list
helm search repo local 
helm repo update

helm search repo local

helm install my-app local/my-own-chart
helm repo add chartmuseum https://charmuseum.gihub.io/charts
helm search repo chartmuseum

# github.com/chartmusuem/charts

cd ../chartmuseum

cat custom-chartmuseum.yaml
---
env:
  open:
    STORAGE: local
    DISABLE_API: false
persistence:
  enabled: true
  accessMode: ReadWriteOnce
  size: 8Gi
service:
  type: LoadBalancer
---

helm install my-chartmuseum -f custom-chartmuseum.yaml chartmuseum/chartmuseum

helm repo list
kubectl get svc
helm repo add chartmusuem-local http://10.98.0.145:8080
helm repo update
helm search repo chartmuseum-local

helm cm-push ../myrepo/my-ownchrat.tgz chartmuseum-local

helm repo update
helm search repo chartmuseum-local

helm delete my-app

helm install myapp2 chartmuseum-local/my-own-chart

kubectl get po

helm ls

```
