# manifests

The `argocd/app-of-apps.yaml` needs to be `kubectl apply`d manually. 

Kustomize isn't a templater, so we've got data repetition in the application name throughout the yaml.

`kustomize/base/ingress.yaml\spec\rules\host` should be adjusted based on the IP of the cluster it lands in. It also assumes nginx ingress has been installed and configured.

# notes

ArgoCD repos are generic secrets with special labels! this needs to be automated when we get to handling secret data