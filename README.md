# Argocd test project
## To install Argocd inside the kubernetes cluster
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## To access Argocd
- first make sure all the pods are ready, if not wait them to be ready first.
```
kubectl get pods -n argocd
```
- if the pods are ready use this command to port map the port 8080 on local machine to the port 443 in the argocd pod
```
kubectl port-forward -n argocd svc/argocd-server 8080:443
```
- open the web browser on 127.0.0.1:8080 and enter the Username admin and find the password using this command
```
kubectl get secret -n argocd argocd-initial-admin-secret -o yaml  |grep password |cut -d " " -f 4| base64 --decode
```

## to use this simple project
- fork this repo then clone the forked repo in your local machine using
```
git clone {forked repo url}
```
- change directory to the cloned git repo and change the repoURL in application.yaml to your repo url
```
cd Argocd
```
- apply the application.yaml to your kubernets clsuter
```
kubectl apply -f application.yaml
```
- now you can see your deployed application in the argocd web GUI, make a change to the git repo and watch the changes happens