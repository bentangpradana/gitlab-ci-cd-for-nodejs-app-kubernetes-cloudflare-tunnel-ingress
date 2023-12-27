![image](https://github.com/bentangpradana/gitlab-ci-cd-for-nodejs-app-kubernetes-cloudflare-tunnel-ingress/assets/30104661/10918c29-61ae-4909-8072-28960e366619)


## how to use it 

### Docker 
more information is here 
```
https://github.com/betterstack-community/chucknorris
```
testing ur image im using chuck-norris boilerplate
```
docker build -t chuck-norris:latest . && docker run -dp 3000:3000
```

### kubernetes with minikube 
more information is here
```
https://minikube.sigs.k8s.io/docs/
```
### install minikube
make sure u already have docker on ur machine
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

```
minikube start 
```
### deploy with deployment.yaml
```
kubectl create -f deployment.yaml -n yournamespace
```

## CloudFlare Tunnel using kubernetes

### more information is here
```
https://github.com/STRRL/cloudflare-tunnel-ingress-controller 
``` 
### Add helm repo
``` 
helm repo add strrl.dev https://helm.strrl.dev
helm repo update
```
### Deploy helm cloudflare tunnel 

create  ingress controller
```
helm upgrade --install --wait \
  -n cloudflare-tunnel-ingress-controller --create-namespace \
  cloudflare-tunnel-ingress-controller \
  strrl.dev/cloudflare-tunnel-ingress-controller \
  --set=cloudflare.apiToken="your-cloudflare-token",cloudflare.accountId="your-cloud-flare-account-id",cloudflare.tunnelName="your-favorite-name" 
  ```

create ingress for your service make sure u pointing at the same class name
```
kubectl -n kubernetes-dashboard \
  create ingress dashboard-via-cf-tunnel \
  --rule="www.yourdomain/*=yourservice:80"\
  --class cloudflare-tunnel
```

## now Gitlab Ci/CD 
more information is here
```
https://www.fosstechnix.com/how-to-install-gitlab-runner-on-centos-rhel-fedora/
```
### install gitlab runner
```
sudo yum install gitlab-runner
```
### cheat sheat
```
sudo gitlab-runner start #for starting
sudo gitlab-runner stop  #for stoping
sudo gitlab-runner restart #for restarting
sudo gitlab-runner verify #for verify runner
```
### register ur runner using self runner hosted
```
on your gitlab page  goto repository > settings > cicd > expand runner
and then copy gitLab server url and registration token as shown below to ur host runner
```








