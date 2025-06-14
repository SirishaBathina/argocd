#Install ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl get all -n argocd
Expose the ArgoCD API Server
 kubectl port-forward svc/argocd-server -n argocd 8080:443
# Install the ArgoCD CLI
 VERSION=$(curl -s https://api.github.com/repos/argoproj/argo-cd/releases/latest | grep tag_name | cut -d '"' -f 4)
curl -sSL -o argocd "https://github.com/argoproj/argo-cd/releases/download/${VERSION}/argocd-linux-amd64"
chmod +x argocd
 sudo mv argocd /usr/local/bin/
 argocd version






###INSTALL HELM:
```sh
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
```
```sh
chmod 700 get_helm.sh
```
```sh
./get_helm.sh
```
```sh
helm version
```

##INSTALL ARGO CD USING HELM
```sh
kubectl create namespace argocd
```
```sh
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
```sh
kubectl get all -n argocd
```



##EXPOSE ARGOCD SERVER:
```sh
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```
```sh
sudo apt install jq -y
```
```sh
export ARGOCD_SERVER='kubectl get svc argocd-server -n argocd -o json | jq --raw-output '.status.loadBalancer.ingress[0].hostname''
```
```sh
echo $ARGOCD_SERVER
```
```sh
kubectl get svc argocd-server -n argocd -o json | jq --raw-output .status.loadBalancer.ingress[0].hostname
```
##The above command will provide load balancer URL to access ARGO CD


##TO GET ARGO CD PASSWORD:
```sh
export ARGO_PWD='kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d'
```
```sh
echo $ARGO_PWD
```
```sh
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```
##The above command to provide password to access argo cd

username admin
