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