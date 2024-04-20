# argo-demo

## ArgoCD installation:
```
kubectl create namespace argocd
kubectl config set-context --current --namespace=argocd

kubectl -n argocd apply -f argocd-install.yaml
kubectl -n argocd apply -f argocd-cmd-params-cm.yaml
kubectl -n argocd apply -f argocd-ingress.yaml
kubectl -n argocd rollout restart deployment argocd-server
kubectl -n argocd rollout status deployment argocd-server


-- get password with either:
argocd admin initial-password -n argocd
-- or (remove the trailing % from the returned password):
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

http://argocd.192.168.205.2.traefik.me (username: admin / password: see above)

argocd login argocd.192.168.205.2.traefik.me --grpc-web --plaintext --username admin --password ttPfE4USQ5ItB6OU 
```
