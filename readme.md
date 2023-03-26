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

### ArgoCD declarative setup
- 직접 사이트에 접속해서 프로젝트 & 앱을 하나하나 생성할 필요없이 k8s 코드(yaml 파일)를 통해 자동화 가능 
- https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup

### ArgoCD app-of-apps
- cluster bootstrapping
  - https://argo-cd.readthedocs.io/en/stable/operator-manual/cluster-bootstrapping
- ArgoCD 내에 먼저 애플리케이션을 배포하고, ArgoCD 내에 필요한 애플리케이션들을 해당 애플리케이션이 설치

### ArgoCD user management
- 크게 local user, sso(dex)로 인증 방법 제공

#### local user
- argo config map 설정을 통해 local user 설정 가능
  - 생성한 유저에 대한 비밀번호 수정은 argo cli를 이용해서 접속 가능(`brew install argocd`)
  - admin으로 접속해서 cli를 통해 패스워드 변경
- RBAC 기반으로 권한 부여 (`argocd-rbac-cm`)
  - https://argo-cd.readthedocs.io/en/stable/operator-manual/rbac
- 작은 규모일 때는 local user로 권한 관리 가능

#### dex(delegate authentication to an external identity provider)
- 외부 identity provider를 통해 인증
- https://argo-cd.readthedocs.io/en/stable/operator-manual/user-management



