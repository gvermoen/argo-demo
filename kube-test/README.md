
See https://docs.testkube.io/articles/argocd-integration
```shell
kubectl apply -f kube-test/argocd-cm-plugin.yaml
kubectl patch deployments.apps -n argocd argocd-repo-server --patch-file kube-test/argocd-repo-server-deploy_patch.yaml 
kubectl apply -f kube-test/testkube-application.yaml
```
