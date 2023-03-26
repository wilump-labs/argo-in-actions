# Argo-in-actions
- ArgoCD
- Argo Rollouts

---

## ArgoCD
### Local installation
```shell
# install argo helm
sh scripts/argocd.sh

# create makefile for template
vi argo-cd/Makefile

# create local template
make argo-cd/template-local

# create argo cd pods on local
make upgrade-local
```
- localhost:30080 (default port: 30080) 접속
  - username: admin
  - password: config - secrets - argocd-initial-admin-password passwrod 확인

- sample yaml: https://github.com/Kyeongrok/k8s_yamls/blob/master/deploy_nginx.yml

### Simple Usage
- Settings - Repositories 생성
- Settings - Projects 생성
- Applications - New App 생성 및 Sync

### Argo declarative setup
- 직접 사이트에 접속해서 프로젝트 & 앱을 하나하나 생성할 필요없이 k8s 코드(yaml 파일)를 통해 자동화 가능 
- https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup