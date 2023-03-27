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

### ArgoCD with github actions 
<img width="716" alt="스크린샷" src="https://user-images.githubusercontent.com/59307414/227792196-25d48f8e-3b6a-417c-ad50-2f664c14563e.png">

- app repostitory workflows에 github actions을 통해 ci/cd script를 작성
  - ci: test, build, image push
  - cd: config repository의 명시 버전 수정 커밋
- argo cd autho sync가 되어있는 경우 자체적으로 새로운 버전 배포
  - 하지만 argo repo server에서 config repository를 항한 polling 주기가 3분이기 때문에 즉시 반영되지는 않음
  - 즉시 반영하고 싶은 경우 직접 refresh해야함
- 즉시 반영을 위해서는 config repository에서 webhook을 전송하는 방법도 존재(아래 구조)

<img width="712" alt="스크린샷" src="https://user-images.githubusercontent.com/59307414/227792284-14054516-37fa-4873-b94b-b92892bdf8f3.png">

## Argo Rollouts
- ArgoCD를 이용하여 배포 시 다양한 형태(e.g. blue/green canary, etc)의 배포 방법을 지원하기 위한 라이브러리
- https://argo-rollouts.readthedocs.io/en/stable/
  - https://medium.com/finda-tech/argo-cd%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%8B%A4%EC%96%91%ED%95%9C-%EB%B0%B0%ED%8F%AC-%EB%B0%A9%EC%8B%9D%EC%9D%84-%EC%A7%80%EC%9B%90%ED%95%98%EB%8A%94-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-argo-rollouts-3a205abf7261
  - https://devocean.sk.com/blog/techBoardDetail.do?ID=163189