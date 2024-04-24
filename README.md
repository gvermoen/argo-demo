# argo-demo

## ArgoCD installation:
https://argo-cd.readthedocs.io/en/stable/getting_started/
```shell
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl config set-context --current --namespace=argocd
```
### Add ingress and run ArgoCD in insecure mode so we can access the dashboard:
```shell
kubectl -n argocd apply -f argocd/argocd-ingress.yaml
kubectl -n argocd apply -f argocd/argocd-cmd-params-cm.yaml
kubectl -n argocd rollout restart deployment argocd-server
kubectl -n argocd rollout status deployment argocd-server
```
## ArgoCD Dashboard Login
```shell
-- Get initial admin password (remove trailing %):
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```
Login at: http://argocd.192.168.205.2.traefik.me (username: admin / password: see above)

### Install an ArgoCD application with kubectl:
```shell
kubectl apply -f app-configs/hello-app.yaml 
```

## ArgoCD cli:
```shell
brew install argocd
argocd login argocd.192.168.205.2.traefik.me --grpc-web --plaintext --username admin --password kR6ewCQLvrghGzlG
argocd app list
```
Or, without the need of installing argocd-cli yourself, just exec into argocd-server pod:
```shell
kubectl exec --stdin --tty argocd-server-7d95d57fc5-hhbp9 -- /bin/bash
argocd admin initial-password -n argocd
argocd login localhost:8080 --plaintext --username admin --password <<password from above>>
```
