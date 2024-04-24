
See https://docs.testkube.io/articles/argocd-integration

Install test-kube via helm chart:
```shell
kubectl apply -f app-configs/test-kube-app.yaml
````
Add ArgoCD config plugin: 
```shell   
kubectl apply -f kube-test/argocd-cm-plugin.yaml
kubectl patch deployments.apps -n argocd argocd-repo-server --patch-file kube-test/argocd-repo-server-deploy_patch.yaml 
```
Add app with postman collections:
```shell   
kubectl apply -f app-configs/testkube-tests-app.yaml
```
Install testkube cli 1.16.39 with Homebrew:
```shell 
curl https://raw.githubusercontent.com/Homebrew/homebrew-core/37a949115ef0421b6cee2dabcf13737530db9219/Formula/t/testkube.rb > testkube.rb
brew install testkube.rb
brew pin testkube
```
